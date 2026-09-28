---
title: "🚀 Trích xuất và cấu trúc văn bản từ Google Drive tự động bằng NVIDIA NIM và n8n"
description: "Hướng dẫn tự động theo dõi thư mục Google Drive, trích xuất text từ mọi định dạng file (PDF, Ảnh, Google Docs, TXT, CSV), chuẩn hóa bằng AI NVIDIA NIM, lưu vào Google Sheets và thông báo qua Telegram."
slug: "trich-xuat-van-ban-google-drive-nvidia-nim-n8n"
tags: [n8n, automation, nvidia-nim, google-drive, ai-summarization, google-sheets]
keywords: [n8n workflow, tự động hóa google drive, trích xuất văn bản nvidia nim, ai document extraction, n8n google sheets telegram]
---

# 🚀 Trích xuất và cấu trúc văn bản từ Google Drive tự động bằng NVIDIA NIM và n8n

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thủ công tải file từ Google Drive lên, đọc nội dung, tóm tắt, rồi copy paste vào Google Sheets mỗi khi có tài liệu mới được gửi vào thư mục chung? Việc này không chỉ tốn thời gian mà còn dễ dẫn đến sai sót và bỏ lỡ thông tin quan trọng.

Đừng lo lắng nữa! Bài viết này sẽ hướng dẫn các sếp triển khai một hệ thống tự động hóa hoàn chỉnh (được phát triển bởi **Cordexa Technologies**) giúp theo dõi thư mục Google Drive 24/7, tự động trích xuất nội dung từ bất kỳ định dạng nào (PDF, hình ảnh, Google Docs, file text, CSV), sử dụng sức mạnh AI của **NVIDIA NIM** để phân tích, tóm tắt và phân loại cấu trúc, sau đó tự động lưu vào Google Sheets và gửi thông báo qua Telegram. Tất cả hoàn toàn tự động, không cần code tay!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Theo dõi thư mục Drive liên tục, xử lý ngay lập tức khi có file mới tải lên.
- **Đa định dạng thông minh:** Xử lý mượt mà từ PDF, văn bản thô (TXT, CSV), Google Docs cho đến hình ảnh nhờ công nghệ AI thị giác máy tính.
- **Cấu trúc hóa dữ liệu chuẩn xác:** AI NVIDIA NIM tự động trích xuất tiêu đề, tóm tắt, danh mục, ngôn ngữ, các ý chính và mức độ tin cậy.
- **Đồng bộ thời gian thực:** Tự động ghi log vào Google Sheets và bắn thông báo xác nhận thành công qua Telegram ngay lập tức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Tài khoản Google:** Cần quyền truy cập Google Drive, Google Docs và Google Sheets (để cấu hình OAuth2 credentials).
- **NVIDIA NIM API Key:** Tài khoản NVIDIA NIM để gọi các mô hình AI (`nvidia/llama-3.3-nemotron-super-49b-v1.5` và mô hình vision).
- **Telegram Bot Token & Chat ID:** Dùng để nhận tin báo cáo kết quả và cảnh báo file không hỗ trợ.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp tiến hành tải file JSON của workflow này từ [n8n.io/workflows/14188](https://n8n.io/workflows/14188), sau đó mở n8n Editor, chọn **Import from File** hoặc dán trực tiếp mã JSON vào giao diện.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Hệ thống gồm 25 nodes hoạt động nhịp nhàng, các sếp cần chú ý cấu hình kỹ các điểm sau trước khi chạy:

- **Google Drive Trigger:** Thay thế `REPLACE_WITH_GOOGLE_DRIVE_FOLDER_ID` bằng ID thư mục Google Drive thực tế mà các sếp muốn hệ thống theo dõi.
- **Normalize Input:** Điền `REPLACE_WITH_TELEGRAM_CHAT_ID` bằng Chat ID Telegram nhận thông báo của các sếp.
- **Analyze Image with NVIDIA & Structure Output with NVIDIA (HTTP Request Nodes):** Cấu hình **HTTP Header Auth** với API Key của NVIDIA NIM (định dạng `Authorization: Bearer YOUR_API_KEY`). Cả hai node này đều sử dụng các mô hình đỉnh cao từ NVIDIA NIM để xử lý thị giác và cấu trúc văn bản.
- **Append Row in Sheet (Google Sheets):** 
  - Thay thế `REPLACE_WITH_GOOGLE_SHEET_ID` bằng ID bảng tính Google Sheets của các sếp.
  - Đảm bảo Google Sheet có một tab tên là `Extract_Log` với các cột tương ứng khớp với các trường dữ liệu mà workflow map sang (Tiêu đề, tóm tắt, danh mục, v.v.).
- **Credentials:** Kết nối đầy đủ các tài khoản Google Drive, Google Docs, Google Sheets, Telegram Bot và HTTP Header Auth (cho NVIDIA) vào các node tương ứng.

#### 3. Kích hoạt ⚡️
- Thực hiện chạy thử nghiệm thủ công (Test run) lần lượt từng loại file: PDF, file text, CSV, hình ảnh và Google Docs để kiểm tra luồng dữ liệu.
- Sau khi tất cả các nhánh chạy mượt mà và ghi nhận đủ dòng dữ liệu vào Google Sheets, các sếp gạt công tắc sang **Active workflow** để hệ thống tự động hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ gửi Telegram cá nhân, các sếp có thể tích hợp thêm node Slack hoặc Microsoft Teams để gửi báo cáo tóm tắt tài liệu vào kênh chung của team.
- **Lưu trữ file backup:** Thêm một bước tự động chuyển file đã xử lý sang thư mục "Processed" trên Google Drive để tránh việc xử lý trùng lặp.
- **Xử lý đa ngôn ngữ:** Tận dụng khả năng xử lý ngôn ngữ siêu việt của NVIDIA NIM để tự động dịch các tài liệu tiếng nước ngoài sang tiếng Việt trước khi ghi vào Google Sheets.

### 📌 Kết luận
Với workflow tự động hóa kết hợp giữa n8n và sức mạnh AI của NVIDIA NIM, việc quản lý và tổng hợp tài liệu từ Google Drive chưa bao giờ trở nên dễ dàng và chuyên nghiệp đến thế. Hãy cài đặt ngay hôm nay để giải phóng thời gian cho đội ngũ của các sếp!