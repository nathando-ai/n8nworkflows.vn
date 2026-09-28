---
title: "🚀 Tự động lưu trữ email Gmail mới vào Google Sheets với n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động quét và đồng bộ email Gmail mới vào Google Sheets để làm CRM thu gọn hoặc quản lý công việc."
slug: "tu-dong-luu-tru-gmail-vao-google-sheets-n8n"
tags: [n8n, automation, gmail, google-sheets, crm, no-code]
keywords: [n8n workflow, tự động hóa gmail, lưu email vào google sheets, n8n gmail integration, crm mini n8n]
---

# 🚀 Tự động lưu trữ email Gmail mới vào Google Sheets với n8n

Các sếp có đang cảm thấy mệt mỏi mỗi khi phải kiểm tra hộp thư đến liên tục, copy thủ công thông tin khách hàng hoặc đối tác từ Gmail vào Google Sheets để theo dõi không? Việc này vừa tốn thời gian, dễ sót việc lại cực kỳ nhàm chán.

Giải pháp ở đây là gì? Workflow n8n do chuyên gia Robert Breen thiết kế sẽ giúp các sếp tự động hóa 100% quy trình này: hệ thống sẽ tự động quét các tin nhắn Gmail mới kể từ lần chạy cuối cùng và ghi nhận ngay lập tức vào Google Sheets. Không cần viết code, thiết lập cực kỳ nhanh chóng!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Không còn cảnh copy/paste thủ công từng nội dung email vào bảng tính.
- **Quản lý thông minh:** Xây dựng một CRM mini cực kỳ gọn nhẹ trực tiếp trên Google Sheets để theo dõi lead, yêu cầu hỗ trợ hoặc đơn hàng từ email.
- **Không bỏ sót thông tin:** Workflow tự động tính toán thời gian chạy cuối cùng để chỉ lấy email mới phát sinh, tránh trùng lặp dữ liệu.
- **Hoạt động tự động 24/7:** Chạy ngầm liên tục mà không cần sự can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Google / Gmail** để lấy API kết nối.
- Bản sao **Google Sheet Template** để lưu dữ liệu email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy và paste trực tiếp vào giao diện n8n Editor của mình. Workflow bao gồm 7 nodes chính phối hợp nhịp nhàng: `manualTrigger`, `Code`, `Summarize`, `Merge`, `Gmail`, và 2 node `Google Sheets`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các thành phần sau:

- **Node `Get new messages` (Gmail):**
  - Tạo Credentials mới: Vào **n8n → Credentials → New → Gmail OAuth2**.
  - Đăng nhập bằng tài khoản Gmail của các sếp và cấp quyền truy cập.
  - Gắn credential này vào node `Get new messages` (với thao tác `getAll`).

- **Node `Get Current Emails` & `Add Emails to Sheets` (Google Sheets):**
  - Copy [Google Sheet template mẫu tại đây](https://docs.google.com/spreadsheets/d/1t5VXtbo9g7SvGDPmeZok4HG1K-WI1PS0DNBylzmhVwg/edit?usp=drivesdk) vào Google Drive của các sếp.
  - Tạo Credentials: Vào **n8n → Credentials → New → Google Sheets (OAuth2)** và đăng nhập tài khoản Google.
  - Trong các node Google Sheets của workflow, chọn đúng **Spreadsheet ID** và **Worksheet** (mặc định là `Sheet1`) để hệ thống biết nơi đọc và ghi dữ liệu.

#### 3. Kích hoạt ⚡️
- Nhấn nút **‘Execute workflow’** (`manualTrigger`) để chạy thử nghiệm với dữ liệu mẫu và kiểm tra kết quả đổ về Google Sheets.
- Sau khi test thành công, hãy gạt công tắc **Active** để workflow tự động chạy theo lịch trình mong muốn.

### ✍️ Mẹo & gợi ý nâng cao
Các sếp hoàn toàn có thể mở rộng workflow này thành một hệ thống tự động hóa mạnh mẽ hơn:
- **Tích hợp thông báo:** Thêm node **Slack** hoặc **Telegram** phía sau để bắn thông báo ngay lập tức về điện thoại mỗi khi có email quan trọng từ khách VIP.
- **Lọc thông minh:** Tùy chỉnh node Gmail để chỉ quét các email có chứa từ khóa cụ thể (ví dụ: "Báo giá", "Hợp tác", "Đơn hàng").
- **Tự động phản hồi (Auto-reply):** Kết hợp thêm AI (OpenAI/Claude node) để đọc sơ lược nội dung email và tự động draft sẵn câu trả lời phù hợp.

### 📌 Kết luận
Việc tự động hóa lưu trữ email Gmail vào Google Sheets là bước đầu tiên cực kỳ hiệu quả để chuyên nghiệp hóa quy trình làm việc cá nhân cũng như doanh nghiệp. Hãy cài đặt ngay hôm nay để tối ưu hóa thời gian của các sếp!