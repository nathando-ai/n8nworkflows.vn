---
title: "🚀 Tự động hóa lưu biên lai từ Telegram vào Excel 365 với Tesseract OCR và GPT-4o-mini"
description: "Hướng dẫn xây dựng workflow n8n tự động trích xuất hóa đơn, biên lai từ Telegram qua OCR & AI, chống trùng lặp và lưu trữ trực tiếp vào Microsoft Excel 365."
slug: "tu-dong-hoa-luu-bien-lai-telegram-vao-excel-365"
tags: [n8n, automation, tesseract-ocr, openai, microsoft-excel, telegram-bot]
keywords: [n8n workflow, doc bien lai telegram, tesseract ocr n8n, luu hoa don vao excel, ai phan tich hoa don]
---

# 🚀 Tự động hóa lưu biên lai từ Telegram vào Excel 365 với Tesseract OCR và AI

Các sếp có đang đau đầu vì mỗi cuối tháng phải gom nhặt từng tấm hình chụp hóa đơn, biên lai chuyển khoản từ nhân viên hoặc khách hàng rồi gõ tay vào Excel không? Việc này vừa tốn thời gian, dễ sai sót lại chẳng thể kiểm soát được dòng tiền thời gian thực.

Giải pháp ở đây là gì? Hãy để **n8n workflow** thay các sếp làm việc đó 100% tự động! Chỉ cần gửi ảnh chụp biên lai vào Telegram Bot, hệ thống sẽ tự động đọc chữ (OCR), dùng AI phân tích thông tin tài chính, kiểm tra trùng lặp và lưu thẳng vào Microsoft Excel 365 trong vòng chưa đầy 5 giây.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Loại bỏ 100% nhập liệu thủ công:** Không còn cảnh ngồi gõ từng con số từ ảnh chụp mờ nhòe.
- **Chống trùng lặp thông minh:** Tự động tạo khóa giao dịch (duplicate key) để ngăn chặn việc lưu một biên lai 2 lần.
- **Độ chính xác cao nhờ AI:** Kết hợp giữa Tesseract OCR và GPT-4.1-mini giúp bóc tách đúng ngày tháng, số tiền, nhà cung cấp, nội dung.
- **Phản hồi tức thì:** Gửi tin nhắn thông báo thành công hoặc cảnh báo lỗi ngay trên khung chat Telegram cho người gửi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** Đang chạy (Cloud hoặc Self-hosted).
- **Telegram Bot Token:** Tạo qua `@BotFather`.
- **Microsoft Excel 365 Account:** File Excel lưu trên OneDrive/SharePoint có bảng dữ liệu (Table) sẵn sàng.
- **OpenAI API Key:** Dùng cho model `gpt-4.1-mini`.
- **Tesseract OCR:** Cần được cài đặt trên môi trường chạy n8n (đối với bản Self-hosted).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, vào giao diện n8n chọn **New Workflow** -> Bấm tổ hợp `Ctrl + V` (hoặc `Cmd + V`) để dán trực tiếp lên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các credentials và tham số cho các node sau:

- **Telegram Trigger** & **Telegram Get File** & Các node **Send Notification**: 
  - Chọn hoặc tạo mới `Telegram API Credentials` bằng Bot Token đã tạo từ `@BotFather`.
- **Tesseract OCR**: 
  - Đảm bảo server n8n của các sếp đã cài đặt gói Tesseract. Nếu dùng n8n Cloud thì node này hoạt động mặc định.
- **OpenAI Chat Model** & **Parse receipt data with AI**: 
  - Cấu hình `OpenAI API Credentials` và chọn model `gpt-4.1-mini` để tối ưu chi phí và tốc độ bóc tách text. Viết system prompt hướng dẫn AI trả về định dạng JSON chuẩn (ngày, số tiền, nội dung, người chuyển...).
- **Get Configurations**, **Check existing transaction in Excel**, **Save transaction to Excel**:
  - Kết nối tài khoản `Microsoft Excel 365 OAuth2 API`.
  - Trỏ đúng đường dẫn file Excel trên OneDrive và chọn đúng tên Bảng (Table) chứa dữ liệu giao dịch (`TRANSACTIONS`).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi một tấm ảnh biên lai/hóa đơn bất kỳ vào Telegram Bot của các sếp để test thực tế.
- Sau khi test thành công, gạt công tắc sang **Active** để đưa workflow vào vận hành chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống kế toán mini này xịn sò hơn nữa, các sếp có thể mở rộng:
- **Tích hợp thêm Google Sheets / Airtable:** Ngoài Excel 365, có thể đồng thời lưu bản backup sang Google Sheets.
- **Thêm bước duyệt (Approval):** Nếu số tiền giao dịch vượt quá 5 triệu VNĐ, chuyển tin nhắn đến nhóm Telegram của sếp lớn để bấm nút Phê duyệt/Từ chối trước khi lưu vào Excel.
- **Báo cáo định kỳ:** Tạo thêm một workflow chạy vào 18:00 hằng ngày để tổng kết tổng tiền đã chi tiêu trong ngày lên Telegram.

### 📌 Kết luận
Việc tự động hóa quy trình ghi nhận hóa đơn từ Telegram vào Excel 365 không chỉ giúp tiết kiệm hàng chục giờ nhập liệu mỗi tháng mà còn mang lại sự minh bạch tuyệt đối cho dòng tiền doanh nghiệp. Hãy triển khai ngay hôm nay để tối ưu hóa vận hành cho đội ngũ của mình nhé!