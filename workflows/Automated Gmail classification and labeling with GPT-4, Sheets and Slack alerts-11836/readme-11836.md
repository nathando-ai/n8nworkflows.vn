---
title: "🤖 **Tự Động Hóa Gmail: Phân Loại & Nhãn Email Bằng AI GPT-4 + Slack Cảnh Báo (N8N)**"
description: "Workflow tự động hóa phân loại email Gmail bằng AI GPT-4, gán nhãn tự động và cảnh báo Slack cho email ưu tiên. Giúp các sếp tiết kiệm **20% thời gian** quản lý email hàng ngày, giảm thiểu lỗi nhãn và tối ưu hóa phản hồi khách hàng."
slug: "tieu-dong-hoa-gmail-phan-loai-nhan-email-ai-gpt4-slack"
tags: [n8n, automation, ai-summarization, gmail, slack, google-sheets, self-hosted]
keywords: [tự động hóa email gmail, phân loại email bằng ai, nhãn email tự động, n8n workflow gmail, cảnh báo slack email ưu tiên, gpt-4 tự động hóa]
---

# 🚀 **Tự Động Hóa Gmail: Phân Loại Email Bằng AI GPT-4 + Slack Cảnh Báo (N8N)**

Hàng ngày, các sếp phải mất **giờ đồng hồ** để phân loại, nhãn và quản lý email trong Gmail. Nhưng với **workflow này**, các sếp có thể **tự động hóa 100% quy trình** này bằng AI GPT-4, đồng thời nhận cảnh báo Slack cho email ưu tiên và lưu lịch sử vào Google Sheets. Kết quả? **Tiết kiệm 20% thời gian**, giảm thiểu lỗi nhãn và phản hồi khách hàng nhanh hơn.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 20% thời gian** quản lý email hàng ngày.
✅ **Phân loại chính xác** email vào 9 danh mục (Hỏi đáp, Yêu cầu hỗ trợ, Tin tức, Marketing, Cá nhân, Gấp, Spam, Hóa đơn, Yêu cầu cuộc họp).
✅ **Nhãn tự động** với cảm xúc (tích cực/tiêu cực) và mức độ ưu tiên (cao/ trung/ thấp).
✅ **Cảnh báo Slack** cho email ưu tiên/ gấp.
✅ **Lưu lịch sử** tất cả email vào Google Sheets (bao gồm cả lỗi phân loại).
✅ **Hoạt động liên tục** 24/7, không phụ thuộc vào người dùng.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
- **Tài khoản Gmail** (để workflow đọc email và gán nhãn).
- **API Key OpenAI** (để sử dụng GPT-4.1-mini).
- **Tài khoản Slack** (để gửi cảnh báo email ưu tiên).
- **Google Sheets** (để lưu lịch sử email và lỗi phân loại).
- **N8N Self-hosted** (để workflow chạy ổn định).

---
:::note[CHUẨN BỊ]
- **Gmail API** phải được kích hoạt trong [Google Cloud Console](https://console.cloud.google.com/).
- **Slack App** cần quyền `chat:write` và `files:write` (xem [hướng dẫn tạo Slack App](https://api.slack.com/apps)).
- **Google Sheets** cần chia sẻ quyền cho n8n (định dạng: `https://docs.google.com/spreadsheets/d/[ID_SHEET]/edit`).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/11836](https://n8n.io/workflows/11836).
2. Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON.
3. Hoặc copy toàn bộ JSON và paste vào **Import Workflow** trong Editor.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này có **21 node**, các sếp cần chú ý cấu hình các node quan trọng sau:

##### **A. Cấu hình Gmail Trigger**
- Node: **"Gmail Check Every 2 Min"**
  - **Credentials**: Chọn tài khoản Gmail đã kết nối.
  - **Label Filter**: Để trống để đọc tất cả email mới.
  - **Polling Interval**: Đặt thành **2 phút** (để workflow kiểm tra email thường xuyên).

##### **B. Cấu hình AI Agent (GPT-4.1-mini)**
- Node: **"Classify and Extract Entities" (Agent)**
  - **System Message**: Các sếp có thể **tùy chỉnh danh sách phân loại** (ví dụ: thêm/loại bỏ danh mục).
  - **Example Input**: Sử dụng email mẫu để AI học phân loại chính xác.
  - **Output Parser**: Đảm bảo cấu hình đúng định dạng JSON trả về (ví dụ: `{ "category": "Support", "priority": "High" }`).

##### **C. Cấu hình Switch Node (Phân loại email)**
- Node: **"Route by Category"**
  - Các sếp cần **đảm bảo tên nhãn trong Gmail** khớp với danh mục trong AI Agent (ví dụ: `Inquiry`, `Support Request`).
  - Nếu AI phân loại sai, email sẽ được gán nhãn **"Unclassified"** và lưu vào **Error Log Sheet**.

##### **D. Cấu hình Slack Alert**
- Node: **"Send Urgent Email Alert"**
  - **Credentials**: Chọn Slack App đã kết nối.
  - **Channel**: Chọn kênh Slack để gửi cảnh báo (ví dụ: `#urgent-emails`).
  - **Message Template**: Tùy chỉnh nội dung cảnh báo (ví dụ: `🚨 Email ưu tiên từ [Tên người gửi]`).

##### **E. Cấu hình Google Sheets Logging**
- Node: **"Log All Emails"** và **"Log Classification Errors"**
  - **Credentials**: Chọn Google Sheets OAuth2 API.
  - **Sheet Name**: Đặt tên sheet chính (`Main Log`) và sheet lỗi (`Error Log`).
  - **Headers**: Đảm bảo cột trong Sheets khớp với dữ liệu trả về từ workflow (ví dụ: `Email ID`, `Category`, `Priority`, `Error Message`).

#### **3. Kích hoạt ⚡️**
1. **Test Run** với email mẫu:
   - Gửi email mẫu vào Gmail → Kiểm tra workflow có phân loại và gán nhãn chính xác không.
   - Xem kết quả trong **Google Sheets** và **Slack**.
2. **Bật Active**:
   - Nhấn **Active** trên workflow trong n8n Editor.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh danh mục phân loại**:
   - Mở node **"Classify and Extract Entities"** → Sửa **System Message** để thêm/loại bỏ danh mục (ví dụ: thêm `Contract`, `Invoice`).
   - Cập nhật **Switch Node** để khớp với danh mục mới.

2. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n Schedule Node** để gửi báo cáo tổng hợp email vào cuối ngày qua **Email** hoặc **Slack**.

3. **Lưu log email vào Google Drive**:
   - Thay thế node **Google Sheets** bằng **Google Drive** để lưu email dưới dạng PDF (sử dụng node `@n8n/nodes-base.googleDrive`).

4. **Kết hợp với Zapier/Integromat**:
   - Nếu cần gửi email đến CRM (HubSpot, Salesforce), các sếp có thể kết nối với **Zapier** hoặc **Integromat** từ node **Gmail**.

5. **Optimize AI Prompt**:
   - Nếu AI phân loại sai, các sếp có thể **cập nhật Example Input** trong node Agent để cải thiện độ chính xác.

---

### 📌 **Kết luận**
Workflows này **giải phóng thời gian** cho các sếp khỏi công việc nhàn nhạt là phân loại email, đồng thời **tăng cường hiệu quả** với nhãn tự động và cảnh báo Slack. **Bắt đầu tự động hóa ngay hôm nay** và giảm thiểu **20% thời gian** quản lý email!

👉 **Bước đầu tiên**: Import workflow và cấu hình tài khoản Gmail, OpenAI, Slack và Google Sheets. Sau đó, **test run** với email mẫu và bật **Active** để workflow hoạt động 24/7.

---
**Cần hỗ trợ tùy chỉnh workflow?** Liên hệ với **Chris Mielke** (tác giả workflow) qua [link này](https://n8n.io/workflows/11836) để có giải pháp **đặc biệt** cho doanh nghiệp của các sếp!