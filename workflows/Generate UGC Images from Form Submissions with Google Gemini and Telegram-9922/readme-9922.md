---
title: "🚀 Tự động tạo ảnh UGC từ Form gửi lên với Google Gemini và Telegram trên n8n"
description: "Hướng dẫn xây dựng hệ thống tự động hóa 100% không cần code: nhận dữ liệu từ Form (ảnh + loại nhân vật), xử lý qua Google Gemini (OpenRouter) và trả kết quả ảnh kèm mô tả AI lên Telegram."
slug: "tu-dong-tao-anh-ugc-google-gemini-telegram-n8n"
tags: [n8n, automation, no-code, google-gemini, telegram, ai-content]
keywords: [n8n workflow, tạo ảnh ugc tự động, google gemini openrouter, telegram bot automation, form trigger n8n]
---

# 🚀 Tự động tạo ảnh UGC từ Form gửi lên với Google Gemini và Telegram

Các sếp đang làm trong lĩnh vực marketing, sáng tạo nội dung hay quản lý cộng đồng có cảm thấy mệt mỏi khi phải thủ công thu thập ảnh từ khách hàng/thành viên, viết mô tả, rồi lại lọ mọ đăng lên Telegram không? Quá trình này không chỉ tốn thời gian mà còn làm giảm tốc độ tương tác.

Giải pháp ở đây là gì? Hãy để workflow n8n này "gánh" thay các sếp toàn bộ quy trình từ A-Z: Nhận dữ liệu form (gồm ảnh và phân loại nhân vật), xử lý thông minh qua AI đa phương thức **Google Gemini** (qua OpenRouter) và tự động xuất bản ảnh kèm nội dung sáng tạo lên **Telegram** ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Khách hàng submit form là hệ thống tự xử lý, không cần sự can thiệp thủ công.
- **AI Đa phương thức (Multimodal):** Kết hợp hoàn hảo giữa hình ảnh đầu vào và sức mạnh phân tích/sáng tạo của Google Gemini.
- **Tương tác real-time:** Kết quả UGC hoàn chỉnh (Ảnh + Content AI) được đẩy trực tiếp lên kênh Telegram trong vòng vài giây.
- **Tiết kiệm thời gian & chi phí:** Giải phóng đội ngũ content khỏi các tác vụ lặp đi lặp lại.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **OpenRouter API Key:** Để kết nối và gọi model Google Gemini qua OpenRouter.
- **Telegram Bot & Channel:** Một Telegram Bot đã được cấp quyền gửi tin nhắn vào kênh/nhóm của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor của mình, hoặc import file JSON tải từ nguồn cấp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:
- **Form submission with character type and image (`formTrigger`):** Cấu hình các trường form gồm loại nhân vật (ví dụ: nam/nữ) và trường upload file ảnh.
- **Google gemini (`httpRequest`):** Kết nối với `openRouterApi` credentials. Điền API Key của OpenRouter và chọn model Google Gemini phù hợp trong payload.
- **Send a photo message (`telegram`):** Kết nối với `telegramApi` credentials (Token của Telegram Bot). Điền Chat ID của kênh hoặc nhóm Telegram nhận kết quả (`sendPhoto` operation).
- **Các node phụ trợ (`Extract the form file`, `Creating a data URL`, `Transform URL data`, `Download the file`):** Giữ nguyên logic xử lý dữ liệu nhị phân (Binary) sang Base64 và Data URL để truyền qua API của Gemini.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng cách điền form mẫu.
- Kiểm tra kết quả trả về trên Telegram.
- Nếu mọi thứ mượt mà, bật nút **Active** để workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ dữ liệu:** Thêm node Google Sheets hoặc Airtable ngay sau bước form submit để lưu lại lịch sử người dùng đã gửi ảnh.
- **Thông báo lỗi:** Gắn thêm nhánh Error Trigger để gửi thông báo về Telegram cá nhân nếu quá trình gọi API Gemini gặp sự cố.
- **Mở rộng kênh phân phối:** Ngoài Telegram, có thể cấu hình thêm node để đăng đồng thời lên Facebook Page hoặc Discord.

### 📌 Kết luận
Workflow này là một minh chứng tuyệt vời cho việc ứng dụng AI đa phương thức vào quy trình làm việc hàng ngày mà không cần biết lập trình. Hãy cài đặt ngay hôm nay để tối ưu hóa quy trình sáng tạo nội dung UGC cho doanh nghiệp của các sếp nhé!