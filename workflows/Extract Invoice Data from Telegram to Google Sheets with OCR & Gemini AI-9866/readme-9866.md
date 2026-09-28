---
title: "🚀 Tự động trích xuất hóa đơn từ Telegram vào Google Sheets bằng AI & Gemini"
description: "Hướng dẫn xây dựng workflow n8n tự động nhận hóa đơn qua Telegram, bóc tách dữ liệu bằng OCR.space và Gemini AI, lưu trữ file vào Google Drive và ghi nhận vào Google Sheets."
slug: "trich-xuat-hoa-don-telegram-google-sheets-gemini-ai"
tags: [n8n, automation, ai, google-sheets, telegram, gemini]
keywords: [n8n workflow, trích xuất hóa đơn, telegram bot, google sheets, gemini ai, ocr space]
---

# 🚀 Tự động trích xuất hóa đơn từ Telegram vào Google Sheets bằng AI & Gemini

Các sếp có đang cảm thấy mệt mỏi mỗi khi phải nhập liệu thủ công từng hóa đơn, chứng từ nhận được qua Telegram vào file Excel hay Google Sheets? Việc này vừa tốn thời gian, dễ sai sót lại chẳng mang lại giá trị gia tăng nào cho doanh nghiệp.

Workflow n8n này sẽ giải quyết triệt để bài toán đó bằng cách tự động hóa 100% quy trình: nhận hóa đơn (ảnh/PDF) từ Telegram, quét OCR, dùng **Gemini AI** để phân tích cấu trúc dữ liệu, lưu file gốc vào **Google Drive**, ghi nhận thông số vào **Google Sheets** và phản hồi lại kết quả ngay trên Telegram cho các sếp. Không cần code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Biến chiếc bot Telegram thành trợ lý kế toán ảo nhận diện và xử lý hóa đơn tức thì.
- **Độ chính xác cao:** Kết hợp OCR mạnh mẽ và Gemini AI để bóc tách chính xác các trường dữ liệu phức tạp (Số hóa đơn, ngày tháng, tổng tiền, hạn thanh toán...).
- **Lưu trữ khoa học:** Tự động lưu file hóa đơn gốc vào Google Drive theo chuẩn ngày tháng và ghi log chi tiết vào Google Sheet.
- **Phản hồi thời gian thực:** Bot Telegram sẽ gửi lại bảng tóm tắt kèm link Google Sheet ngay sau khi xử lý xong.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **Telegram Bot Token**: Tạo qua BotFather trên Telegram để cấu hình node `Telegram Trigger1`, `Download File1`, `Telegram1`, `Reply1`.
- **Google Sheets & Google Drive**: Tài khoản Google có quyền chỉnh sửa file Sheet và thư mục Drive mục tiêu.
- **Gemini API Key**: Lấy từ Google AI Studio để kết nối với các node `Google Gemini Chat Model1` & `Google Gemini Chat Model2`.
- **OCR.space API Key**: Đăng ký một tài khoản miễn phí tại OCR.space để lấy API key cho node `Analyze Image1` (HTTP Request).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và paste trực tiếp vào n8n Editor của mình, hoặc import file JSON thông qua menu giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không lỗi, các sếp cần cấu hình chính xác các node sau:
- **Node `Analyze Image1` (HTTP Request)**: Điền API Key của OCR.space vào phần Header với tên khóa là `apikey`.
- **Node `Update Database1` (Google Sheets)**: Dán `Document ID` của file Google Sheets vào, chọn đúng tên Sheet tab (hoặc `gid`). Đảm bảo các cột trong Sheet khớp với định dạng: `Invoice Number | Date | Total Amount ($) | Billing Address | Due Date | Notes`.
- **Node `Add Invoice Image to Drive1` (Google Drive)**: Cung cấp `Folder ID` của thư mục chứa hóa đơn trên Google Drive. Có thể tùy chỉnh định dạng tên file lưu trữ tại đây (mặc định đang để `Invoice [MMMM-dd-yyyy]`).
- **Node `Invoice Agent1` & `AI Agent`**: Tùy chỉnh system prompt nếu các sếp muốn bot phản hồi theo văn phong hoặc ngôn ngữ khác (tiếng Việt chẳng hạn).

#### 3. Kích hoạt ⚡️
- Gửi thử một file PDF hoặc ảnh chụp hóa đơn vào bot Telegram (⚠️ **Lưu ý:** Gửi dưới dạng *File/Document* chứ không gửi dạng ảnh nén *Compressed photo*).
- Kiểm tra tab **Executions** trong n8n để xem luồng dữ liệu chạy từ Download ➔ OCR ➔ AI ➔ Sheets ➔ Drive ➔ Telegram.
- Nếu mọi thứ xanh mướt (success), các sếp hãy bật công tắc **Active** cho workflow chạy chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Slack/Telegram Group:** Mở rộng workflow bằng cách kết nối thêm node Slack hoặc gửi tin nhắn vào một nhóm Telegram nội bộ của phòng kế toán mỗi khi có hóa đơn mới được duyệt.
- **Xử lý ngoại lệ (Error Handling):** Thêm Error Trigger để bot tự động thông báo về một kênh chat riêng nếu OCR đọc lỗi hoặc file không đúng định dạng.
- **Tích hợp thêm duyệt tự động:** Thêm bước hỏi ý kiến quản lý qua Telegram (Interactive buttons) trước khi chính thức ghi nhận vào bảng lương/chi phí.

### 📌 Kết luận
Với workflow n8n cực kỳ thông minh này, các sếp đã có thể tiết kiệm hàng chục giờ nhập liệu mỗi tháng, loại bỏ hoàn toàn sai sót thủ công. Hãy triển khai ngay hôm nay để tối ưu hóa quy trình vận hành tài chính cho doanh nghiệp của mình nhé!