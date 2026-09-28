---
title: "🚀 Tự Động Hóa Báo Cáo Sprint từ Jira sang Email Stakeholders - Giảm 100% Công Việc Lặp Lại"
description: "Workflow tự động hóa hoàn toàn từ Jira đến email báo cáo sprint hàng tuần, giúp các sếp tiết kiệm 10 giờ/ngày và cung cấp dữ liệu chính xác cho stakeholder. Kết hợp AI, Jira và Gmail để báo cáo tự động hóa 24/7."
slug: "tieu-dong-hoa-bao-cao-sprint-jira-sang-email"
tags: [n8n, automation, jira, gmail, agile, sprint-reporting, no-code]
keywords: [n8n workflow jira, tự động hóa báo cáo sprint, báo cáo agile tự động, gửi email từ jira, giảm công việc lặp lại]
---

# 🚀 **Tự Động Hóa Báo Cáo Sprint từ Jira sang Email Stakeholders**

### **Giải quyết vấn đề gì?**
Các sếp và quản lý Agile thường phải mất **10-15 giờ/tuần** để:
- Tìm kiếm và tổng hợp dữ liệu sprint từ Jira.
- Tính toán KPIs như số issue hoàn thành, story points, blockers.
- Chỉnh sửa và gửi báo cáo qua email cho stakeholder.
- Đối phó với lỗi dữ liệu thiếu hoặc không nhất quán.

**Workflow này tự động hóa toàn bộ quy trình đó chỉ trong 10 phút cài đặt!** Báo cáo sprint được tạo và gửi tự động hàng tuần, với dữ liệu chính xác và định dạng chuyên nghiệp.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-15 giờ/tuần** cho việc báo cáo thủ công.
- **Dữ liệu chính xác 100%** (không sai sót do con người).
- **Báo cáo định dạng chuyên nghiệp** với HTML + biểu đồ.
- **Gửi tự động hàng tuần** (không quên hoặc trễ hạn).
- **KPIs tự động tính toán** (số issue hoàn thành, story points, blockers).
- **Kết nối với stakeholder** một cách cá nhân hóa (theo email cụ thể).
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Jira Cloud** (cần **API Token** và **Email API** để fetch dữ liệu).
   - Hướng dẫn tạo API Token: [Jira Cloud API Docs](https://support.atlassian.com/cloud/jira/software/cloud/docs/manage-api-tokens/)
2. **Tài khoản Gmail** (cần **OAuth2** để gửi email tự động).
   - Hướng dẫn cấu hình OAuth2: [n8n Gmail Docs](https://docs.n8n.io/integrations/builtins/nodes/Gmail/)
3. **Dữ liệu JQL** (Jira Query Language) để lọc sprint:
   - Ví dụ: `project = <PROJECT_KEY> AND sprint in openSprints()`
   - Thay `<PROJECT_KEY>` bằng mã dự án của bạn (ví dụ: `PROJ`).
4. **Email của stakeholder** (để nhận báo cáo hàng tuần).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n Workflow](https://n8n.io/workflows/8932) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/8932) và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **7 node** chính, các sếp cần chú ý cấu hình sau:

##### **A. Node "Weekly trigger" (scheduleTrigger)**
- **Cấu hình:**
  - **Schedule:** Chọn `Weekly` và ngày giờ muốn chạy (ví dụ: **Thứ 6, 17:00**).
  - **Time Zone:** Đặt theo múi giờ của bạn (ví dụ: `Asia/Ho_Chi_Minh`).
  - **Test Run:** Kích hoạt để kiểm tra trigger hoạt động.

##### **B. Node "Get many issues" (jira)**
- **Cấu hình:**
  - **Credentials:** Chọn `jiraSoftwareCloudApi` (đã cấu hình trước).
  - **JQL Query:** Điền `project = <PROJECT_KEY> AND sprint in openSprints()` (thay `<PROJECT_KEY>`).
  - **Fields:** Chọn các trường cần lấy:
    ```
    summary, status, assignee, priority, storypoints, sprint, created, updated
    ```
  - **Test Run:** Kiểm tra dữ liệu trả về có đầy đủ không.

##### **C. Node "Jira & email configuration" (set)**
- **Cấu hình:**
  - **Email To:** Điền email của stakeholder nhận báo cáo.
  - **Sprint Name:** Nếu muốn tự động lấy tên sprint từ Jira, giữ nguyên hoặc chỉnh sửa.
  - **Test Run:** Kiểm tra dữ liệu được truyền xuống node tiếp theo.

##### **D. Node "Validation & error handling" (code)**
- **Lưu ý:**
  - Node này **không cần chỉnh sửa** (đã viết sẵn logic kiểm tra dữ liệu).
  - Nếu dữ liệu thiếu (ví dụ: `storypoints` hoặc `sprint`), nó sẽ tự động bỏ qua và báo lỗi.
  - **Test Run:** Chạy để xem có lỗi nào không.

##### **E. Node "Metrics calculation" (code)**
- **Lưu ý:**
  - Node này **tự động tính toán KPIs** như:
    - Số issue ở trạng thái `To Do`, `In Progress`, `Done`.
    - Story points hoàn thành vs tổng.
    - Số blockers (priorit = High hoặc label = blocker).
  - **Không cần chỉnh sửa** (nếu muốn thay đổi logic, cần biết code JavaScript).

##### **F. Node "HTML report generation" (code)**
- **Lưu ý:**
  - Node này **tạo báo cáo HTML** với:
    - Tên sprint + ngày bắt đầu/ket thúc.
    - Bảng tổng hợp KPIs.
    - Bảng chi tiết tất cả issue (key, summary, status, assignee, priority, story points).
    - Link trực tiếp đến Jira.
  - **Test Run:** Kiểm tra báo cáo có hiển thị đúng không.

##### **G. Node "Email notification" (gmail)**
- **Cấu hình:**
  - **Credentials:** Chọn `gmailOAuth2` (đã cấu hình trước).
  - **Subject:** Đặt tiêu đề email (ví dụ: `Báo cáo Sprint #<NUMBER> - <DATE>`).
  - **HTML Body:** Chọn `HTML` và paste nội dung từ node `HTML report generation`.
  - **Test Run:** Gửi email mẫu để kiểm tra.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run:** Chạy workflow với dữ liệu mẫu để kiểm tra tất cả node.
2. **Active Workflow:** Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động hàng tuần.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Slack/Telegram Notification**
   - Kết nối với **Slack** hoặc **Telegram Bot** để thông báo khi báo cáo được gửi.
   - Sử dụng node `webhook` để nhận thông báo và gửi qua Slack/Telegram.

2. **Lưu Log Báo Cáo**
   - Thêm node `stickyNote` để lưu lịch sử báo cáo (giúp theo dõi và phân tích dài hạn).

3. **Báo cáo Định Kỳ Khác**
   - Thay đổi `scheduleTrigger` để gửi báo cáo **ngày đầu tháng** hoặc **khi sprint kết thúc**.

4. **Tùy Chỉnh Dữ liệu JQL**
   - Nếu muốn lọc sprint cụ thể, chỉnh sửa JQL trong node `Get many issues`:
     ```plaintext
     project = PROJ AND sprint = "Sprint 12" AND status != "Done"
     ```

5. **Sử Dụng AI Tự Động Tóm Tắt**
   - Thêm node **LLM** (ví dụ: `n8n-nodes-base.llm`) để tự động tóm tắt báo cáo bằng AI.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào chiến lược và quản lý đội nhóm, thay vì mất công với báo cáo thủ công. **Chỉ cần cài đặt 1 lần**, workflow sẽ tự động chạy hàng tuần, cung cấp dữ liệu chính xác và chuyên nghiệp cho stakeholder.

**Hành động ngay:**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test Run** để đảm bảo mọi thứ hoạt động.
3. **Active workflow** và **quên việc báo cáo thủ công!**

👉 **Bắt đầu tự động hóa ngay hôm nay!** [Tải workflow từ n8n](https://n8n.io/workflows/8932)