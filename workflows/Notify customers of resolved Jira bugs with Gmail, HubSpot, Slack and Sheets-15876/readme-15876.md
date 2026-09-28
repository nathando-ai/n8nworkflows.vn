---
title: "🚀 Tự Động Hóa Thông Báo Khách Hàng Khi Bug Jira Được Giải Quyết (Gmail + HubSpot + Slack + Sheets)"
description: "Workflow n8n tự động gửi thông báo email cho khách hàng khi bug trong Jira được giải quyết, đồng thời cập nhật HubSpot, ghi log vào Google Sheets và thông báo cho team qua Slack. Giúp tiết kiệm thời gian, tránh trùng lặp và đảm bảo khách hàng được thông báo kịp thời."
slug: "tieu-dong-hoa-thong-bao-khach-hang-khi-bug-jira-duoc-giai-quyet"
tags: [n8n, automation, ticket-management, jira, gmail, hubspot, slack, google-sheets, no-code]
keywords: [tự động hóa jira, thông báo bug giải quyết, n8n workflow jira, tự động hóa email khách hàng, tự động hóa hubspot, tự động hóa slack, tự động hóa google sheets]
---

# 🚀 **Tự Động Hóa Thông Báo Khách Hàng Khi Bug Jira Được Giải Quyết (Gmail + HubSpot + Slack + Sheets)**

### **Giải pháp cho vấn đề:**
Hàng ngày, các team DevOps/Tech Support phải thủ công kiểm tra và thông báo cho khách hàng khi bug được giải quyết. Điều này tốn thời gian, dễ bị bỏ quên, và không đảm bảo tính nhất quán. **Workflow này tự động hóa toàn bộ quy trình:**
- **Khi một bug trong Jira được đánh dấu là "Resolved"**, hệ thống sẽ tự động:
  - Kiểm tra xem bug thực sự đã được giải quyết.
  - Lấy thông tin chi tiết về bug từ Jira.
  - Kiểm tra xem khách hàng có email liên hệ không.
  - **Nếu có email:** Gửi email thông báo cho khách hàng, cập nhật thông tin vào HubSpot, ghi log vào Google Sheets và thông báo cho team qua Slack.
  - **Nếu thiếu email:** Gửi cảnh báo cho team để xử lý thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Không cần phải thủ công kiểm tra và gửi email cho từng khách hàng.
- **Tránh trùng lặp:** Kiểm tra và ngăn chặn việc gửi thông báo cho cùng một bug nhiều lần.
- **Cập nhật tự động:** Thông tin khách hàng được đồng bộ vào HubSpot và ghi log vào Google Sheets.
- **Thông báo team:** Slack tự động cảnh báo khi có bug mới được giải quyết hoặc thiếu thông tin khách hàng.
- **Chất lượng dịch vụ cao:** Khách hàng được thông báo kịp thời, tăng độ tin cậy của sản phẩm.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Jira Cloud** (API Key: `jiraSoftwareCloudApi`).
2. **Tài khoản Gmail** (OAuth2: `gmailOAuth2`).
3. **Tài khoản HubSpot** (App Token: `hubspotAppToken`).
4. **Tài khoản Slack** (OAuth2 API: `slackOAuth2Api`).
5. **Google Sheets** (OAuth2 API: `googleSheetsOAuth2Api`).
6. **Thông tin Sheet Jira Logs** (Sheet Name và ID Sheet để ghi log).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/15876](https://n8n.io/workflows/15876) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/15876) và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **18 node**, các bước quan trọng cần chú ý:

##### **A. Cấu hình Jira Trigger**
- **Node:** `Jira Trigger`
- **Tham số cần thiết:**
  - Chọn **Event:** `issue_updated` (để bắt sự kiện khi bug được cập nhật).
  - **Filter:** Chỉ lọc bug với status là **"Done"** hoặc **"Resolved"**.
  - **Credentials:** Điền `jiraSoftwareCloudApi` (API Key từ Jira).

##### **B. Kiểm tra bug đã được giải quyết (`Filter: Bug Resolved?`)**
- **Node:** `Filter: Bug Resolved?` (Node `if`)
- **Cấu hình:**
  - **Condition:** Kiểm tra `jsonpath($.fields.status.name) == "Done"` hoặc `"Resolved"`.
  - Nếu không thỏa mãn, workflow sẽ **dừng lại**.

##### **C. Lấy thông tin chi tiết bug (`Get Jira Issue Details`)**
- **Node:** `Get Jira Issue Details`
- **Tham số cần thiết:**
  - **Credentials:** `jiraSoftwareCloudApi`.
  - **Issue Key:** `$node["Jira Trigger"].jsonpath("$.issue.key")`.

##### **D. Kiểm tra trùng lặp (`Deduplication Check`)**
- **Node:** `Deduplication Check` (Code Node)
- **Mã code mặc định:**
  ```javascript
  const existingLogs = $input.all();
  const isDuplicate = existingLogs.some(log => log.jsonpath("$.fields.issueKey") === $input.current().jsonpath("$.fields.issueKey"));
  return { duplicate: isDuplicate };
  ```
  - **Lưu ý:** Nếu muốn cải tiến, các sếp có thể thêm logic kiểm tra trong **Google Sheets** thay vì trong code.

##### **E. Kiểm tra email khách hàng (`Has Customer Email?`)**
- **Node:** `Has Customer Email?` (Node `if`)
- **Cấu hình:**
  - Kiểm tra trường `customersEmail` trong payload (nếu có, workflow tiếp tục; nếu không, chuyển sang branch cảnh báo).

##### **F. Gửi email cho khách hàng (`Send Gmail to Customer`)**
- **Node:** `Send Gmail to Customer`
- **Tham số cần thiết:**
  - **Credentials:** `gmailOAuth2`.
  - **Email To:** `$node["Has Customer Email?"].jsonpath("$.customersEmail")`.
  - **Subject:** `"Bug #$node["Jira Trigger"].jsonpath("$.issue.key") đã được giải quyết!"`.
  - **Body:** Sử dụng **Code Node** (`Merge Data & Build Templates`) để xây dựng nội dung email động (ví dụ: link Jira, mô tả bug, thời gian giải quyết).

##### **G. Cập nhật HubSpot (`Create/Update HubSpot Contact`)**
- **Node:** `Create/Update HubSpot Contact`
- **Tham số cần thiết:**
  - **Credentials:** `hubspotAppToken`.
  - **Properties:** Điền thông tin khách hàng từ Jira (ví dụ: `email`, `name`, `company`).
  - **Lưu ý:** Nếu khách hàng chưa có trong HubSpot, hệ thống sẽ tạo mới; nếu đã có, sẽ cập nhật.

##### **H. Thông báo team qua Slack (`Slack Team Notification`)**
- **Node:** `Slack Team Notification`
- **Tham số cần thiết:**
  - **Credentials:** `slackOAuth2Api`.
  - **Channel:** `#support-bugs` (hoặc channel phù hợp).
  - **Message:** `"Bug #$node["Jira Trigger"].jsonpath("$.issue.key") đã được giải quyết và thông báo cho khách hàng: $node["Has Customer Email?"].jsonpath("$.customersEmail")"`.

##### **I. Ghi log vào Google Sheets (`Log to Google Sheets`)**
- **Node:** `Log to Google Sheets`
- **Tham số cần thiết:**
  - **Credentials:** `googleSheetsOAuth2Api`.
  - **Sheet Name:** Điền tên Sheet (ví dụ: `Jira_Bug_Logs`).
  - **Range:** `A1` (để ghi dữ liệu vào ô đầu tiên).
  - **Data:** `$input.current()` (tất cả thông tin bug).

##### **J. Xử lý khi thiếu email (`Alert: Manual Follow-Up`)**
- **Node:** `Alert: Manual Follow-Up` (Slack)
- **Tham số cần thiết:**
  - **Credentials:** `slackOAuth2Api`.
  - **Message:** `"Không tìm thấy email khách hàng cho bug #$node["Jira Trigger"].jsonpath("$.issue.key"). Vui lòng liên hệ thủ công!"`.

---

#### **3. Kích hoạt ⚡️**
- **Test Run:** Chạy workflow với **1 bug mẫu** để kiểm tra:
  - Email có được gửi không?
  - HubSpot có được cập nhật không?
  - Slack có thông báo không?
  - Log có ghi vào Google Sheets không?
- **Bật Active:** Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động khi có sự kiện mới.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tăng tính cá nhân hóa email:**
   - Sử dụng **OpenAI API** (n8n-node-openai) để tự động viết nội dung email động dựa trên mô tả bug.
   - Ví dụ: `"Chúng tôi đã sửa lỗi #$issueKey trong ứng dụng. Đây là những thay đổi chính: $description"` (sử dụng LLM để tổng kết).

2. **Ghi log chi tiết hơn:**
   - Thêm **Google Sheets** để lưu lịch sử phản hồi của khách hàng (ví dụ: `customerResponse`, `responseDate`).

3. **Kết hợp với Zapier/Integromat:**
   - Nếu cần thêm tính năng như **gửi SMS** khi bug được giải quyết, có thể kết nối với **Twilio** qua HTTP Request.

4. **Tự động tạo ticket trong Zendesk:**
   - Nếu khách hàng phản hồi không hài lòng, hệ thống có thể tự động tạo ticket mới trong Zendesk.

5. **Báo cáo định kỳ:**
   - Sử dụng **n8n-node-schedule** để gửi báo cáo hàng tuần về số bug được giải quyết và phản hồi của khách hàng.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho team DevOps/Tech Support bằng cách tự động hóa toàn bộ quy trình thông báo bug cho khách hàng. **Không cần viết code**, chỉ cần cấu hình các node và kết nối API là xong!

**Hành động ngay:**
1. **Import workflow** và cấu hình các credentials.
2. **Test Run** với 1-2 bug mẫu.
3. **Bật Active** và để hệ thống làm việc 24/7!

---
**💡 Cần hỗ trợ thêm?**
- **Khóa học tự động hóa n8n:** [iTechNotion](https://itechnotion.com/) (do tác giả Avkash Kakdiya giảng dạy).
- **Hỗ trợ kỹ thuật:** Trên [Community n8n](https://community.n8n.io/).

**Chia sẻ workflow này với đồng nghiệp để cùng tự động hóa công việc!** 🚀