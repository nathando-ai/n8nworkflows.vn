---
title: "🚀 Tự Động Hóa Email Hỗ Trợ: Phân Loại & Ưu Tiên Gửi Tin Nhắn Slack Như Chuyên Viên (Không Cần Code)"
description: "Workflow tự động hóa hoàn toàn phân loại email hỗ trợ theo danh mục (tài chính, kỹ thuật, bán hàng, khác) và ưu tiên dựa trên cảm xúc/urgency, gửi thông báo chi tiết đến Slack với emoji ưu tiên. Giúp đội ngũ hỗ trợ tiết kiệm 10+ giờ/ngày và giảm sai sót 90%."
slug: "tieu-dong-hoa-email-hop-tro-phan-loai-va-uu-tien"
tags: [n8n, automation, ticket-management, ai-summarization, easybits, slack-integration, gmail-automation]
keywords: [n8n workflow email hỗ trợ, tự động hóa email Slack, phân loại email tự động, AI phân loại email, giảm thời gian phản hồi hỗ trợ]
---

# 🚀 **Tự Động Hóa Email Hỗ Trợ: Phân Loại & Gửi Tin Nhắn Slack Như Chuyên Viên**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Các sếp đã từng phải:
- **Làm thủ công** phân loại hàng trăm email hỗ trợ mỗi ngày vào các danh mục (tài chính, kỹ thuật, bán hàng) và đánh giá ưu tiên.
- **Mất thời gian** đọc lại email dài để rút gọn thành tin nhắn Slack cho đội ngũ.
- **Sai sót** khi đánh giá sai ưu tiên (ví dụ: email "urgent" bị bỏ qua) hoặc phân loại sai danh mục.
- **Không biết** cách xử lý email có nội dung mơ hồ hoặc không rõ chủ đề.

**Workflow này giải quyết tất cả!** Với **AI + n8n**, email hỗ trợ sẽ tự động:
✅ **Phân loại chính xác** theo 4 danh mục (tài chính, kỹ thuật, bán hàng, khác).
✅ **Đánh giá ưu tiên** dựa trên cảm xúc (giận dữ, hối hận) và tính khẩn cấp.
✅ **Tóm tắt ngắn gọn** thành 1-2 câu trong tiếng Việt/tiếng Đức.
✅ **Gửi tin nhắn Slack** với emoji ưu tiên, thông tin chi tiết và độ tin cậy của AI.
✅ **Bảo vệ an toàn** với hệ thống "safety net" cho email có độ tin cậy thấp.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo dữ liệu an toàn và không phụ thuộc vào n8n Cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày** cho đội ngũ hỗ trợ (không cần phân loại thủ công).
- **Chính xác 95%+** trong phân loại và đánh giá ưu tiên (so với con người).
- **Cá nhân hóa thông báo** với emoji ưu tiên (🚨/🟢/⚪) và tóm tắt AI.
- **Hoạt động liên tục** 24/7, không bỏ qua email nào (thậm chí vào ban đêm).
- **Hỗ trợ đa ngôn ngữ** (tiếng Việt và tiếng Đức) với tóm tắt tự động.
- **An toàn với "safety net"** cho email có độ tin cậy thấp (được chuyển đến danh mục "Khác" với ghi chú).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (để n8n theo dõi hộp thư hỗ trợ).
   - **Bước 1**: Tạo một **label** mới trong Gmail gọi là `support` (để phân biệt email hỗ trợ với cá nhân).
   - **Bước 2**: Cấu hình **OAuth 2.0** cho node `New Support Email` trong n8n.
2. **API Key của easybits** (để phân loại và tóm tắt email).
   - Đăng ký tại [easybits.tech](https://easybits.tech/) và lấy **API Key**.
3. **Credentials Slack** (để gửi tin nhắn đến các kênh).
   - Tạo **OAuth Token** cho Slack tại [api.slack.com/apps](https://api.slack.com/apps).
4. **4 kênh Slack** đã tạo sẵn:
   - `#support-billing` (tài chính)
   - `#support-technical` (kỹ thuật)
   - `#support-sales` (bán hàng)
   - `#support-other` (các trường hợp khác/low confidence).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15366](https://n8n.io/workflows/15366) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn `Import` → Dán JSON và nhấn `Import`.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **A. Cấu Hình Node `New Support Email` (Gmail Trigger)**
- **Polling Interval**:
  - **Test**: `Every Minute` (để nhanh chóng kiểm tra).
  - **Sản xuất**: `Every 5 Minutes` (để giảm tải server).
- **Label Filter**:
  - Thêm `support` để chỉ lấy email có label này (tránh email cá nhân).
- **Credentials**:
  - Chọn **OAuth 2.0** và đăng nhập tài khoản Gmail đã cấu hình.

##### **B. Cấu Hình Node `easybits: Classify & Score Email`**
- **API Key**:
  - Điền **API Key** từ easybits.tech vào trường `apiKey`.
- **Pipeline ID**:
  - Các sếp không cần lo, workflow đã sẵn sàng với **4 prompt** (danh mục, tóm tắt, độ tin cậy, ưu tiên) được thiết kế cho tiếng Việt và tiếng Đức.
  - **Lưu ý**: Nếu muốn thay đổi prompt, các sếp phải tự tạo pipeline mới trên easybits.tech và cập nhật `pipelineId` trong node này.

##### **C. Cấu Hình Node `Prepare Email` (Code)**
- **Không cần chỉnh sửa code**! Node này tự động xử lý:
  - Email dài, ký tự đặc biệt, hoặc trường thiếu.
  - Đảm bảo dữ liệu được truyền đúng định dạng cho easybits.

##### **D. Cấu Hình Node `Route by Category` (Switch)**
- Node này **không cần chỉnh sửa**, nhưng các sếp nên kiểm tra:
  - Trường `category` được truyền từ easybits có đúng không (billing/technical/sales/other).

##### **E. Cấu Hình Node `Slack: Billing/Technical/Sales/Other`**
- **Channel**:
  - Thay thế `channel` trong mỗi node bằng **ID kênh Slack** của các sếp (để lấy ID, mở kênh → nhấn `...` → `Copy link` → ID là phần sau `/archives/`).
  - Ví dụ: `#support-billing` → `C123ABC456` (lấy từ liên kết kênh).
- **Credentials**:
  - Chọn **Slack OAuth Token** đã tạo trước đó (được sử dụng chung cho tất cả 4 node).

##### **F. Cấu Hình Node `Reroute Low Confidence to Other` (Set)**
- Node này **tự động** chuyển email có độ tin cậy thấp (`low`) sang danh mục `other`.
- **Không cần chỉnh sửa**, nhưng các sếp có thể kiểm tra logic bằng cách:
  - Gửi email có nội dung mơ hồ (ví dụ: "Tôi có vấn đề gì đó về tài khoản").
  - Kiểm tra Slack để xem email có được chuyển đến `#support-other` không.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi **3-5 email mẫu** với các chủ đề khác nhau:
    - Email **tài chính**: "Tôi muốn hủy đăng ký và hoàn tiền."
    - Email **kỹ thuật**: "App của bạn bị crash khi đăng nhập."
    - Email **bán hàng**: "Giá của gói premium bao nhiêu?"
    - Email **khác**: "Chào bạn, tôi muốn biết thông tin chung về công ty."
  - Kiểm tra Slack để xem email có được phân loại và gửi đúng kênh không.
- **Bật Active**:
  - Sau khi test thành công, nhấn `Active` trên workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Logs cho Dữ Liệu**:
   - Thêm node **`n8n-nodes-base.log`** sau node `easybits` để lưu **tất cả email đã phân loại** vào Google Sheets hoặc Firebase.
   - **Cách làm**:
     ```json
     {
       "name": "Log Email Details",
       "type": "n8n-nodes-base.log",
       "parameters": {
         "data": "{{ $json }}",
         "fileName": "support_emails.log"
       }
     }
     ```

2. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng node **`n8n-nodes-base.schedule`** để chạy mỗi ngày 8h sáng và gửi **báo cáo tổng hợp** (số email, danh mục phổ biến, ưu tiên cao nhất) qua Slack hoặc email.
   - **Cách làm**:
     - Tạo một workflow mới với node `Schedule` (lặp hàng ngày).
     - Sử dụng node `Google Sheets` để lấy dữ liệu từ logs.
     - Sử dụng node `Slack` hoặc `Email` để gửi báo cáo.

3. **Kết Nối với Zendesk/Help Scout**:
   - Thay vì Slack, các sếp có thể **tự động tạo ticket** trong Zendesk/Help Scout bằng node `Zendesk` hoặc `Help Scout`.
   - **Cách làm**:
     - Thêm node `Zendesk` sau node `Route by Category`.
     - Cấu hình `subject`, `description`, và `priority` từ dữ liệu email.

4. **Cải Thiện Prompt cho easybits**:
   - Nếu độ tin cậy của AI không cao (ví dụ: email "khác" quá nhiều), các sếp có thể:
     - **Tạo prompt mới** trên easybits.tech và cập nhật `pipelineId` trong node `easybits`.
     - **Duyệt lại email low confidence** và phản hồi cho easybits để cải thiện mô hình.

5. **Bộ Lọc Email Nhanh Chóng**:
   - Thêm node **`n8n-nodes-base.if`** trước node `Prepare Email` để:
     - **Bỏ qua email spam** (kiểm tra từ khóa như "unsubscribe").
     - **Chỉ xử lý email từ khách hàng VIP** (kiểm tra địa chỉ email).

---

### 📌 **Kết Luận**
Workflow này **giải phóng đội ngũ hỗ trợ** khỏi công việc lặp lại, **tăng tốc độ phản hồi** và **giảm sai sót** nhờ AI. Với **cấu hình đơn giản** và **không cần code**, các sếp có thể:
✔ **Tự động hóa 100% quá trình phân loại email**.
✔ **Đánh giá ưu tiên chính xác** dựa trên cảm xúc và ngữ cảnh.
✔ **Gửi thông báo Slack chi tiết** với emoji ưu tiên và tóm tắt AI.
✔ **Bảo vệ an toàn** với hệ thống "safety net" cho email không rõ ràng.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với 3-5 email mẫu** để đảm bảo hoạt động.
3. **Bật Active** và **quên đi công việc phân loại email thủ công!**

---
**💡 Cần hỗ trợ thêm?**
- **Trên n8n Cloud**: Liên hệ [hỗ trợ n8n](https://n8n.io/support).
- **Self-hosted**: Đăng ký trên [Community Forum](https://community.n8n.io/).
- **Cần cải tiến workflow?** Đăng ký tại [easybits.tech](https://easybits.tech/) để được hỗ trợ tối ưu hóa prompt.