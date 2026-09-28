---
title: "🎓 Tự động theo dõi tuyển sinh trường học bằng Web Scraping và Gemini AI"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu website trường học, sử dụng Gemini AI phân tích thông tin tuyển sinh và gửi email thông báo tức thì."
slug: "tu-dong-theo-doi-tuyen-sinh-truong-hoc-gemini-ai"
tags: [n8n, automation, web-scraping, gemini-ai, ai-summarization, notification]
keywords: [n8n workflow, tự động hóa tuyển sinh, web scraping n8n, google gemini ai, email alert automation]
---

# 🎓 Tự động theo dõi tuyển sinh trường học bằng Web Scraping và Gemini AI

Các bậc phụ huynh hay các nhà quản lý giáo dục chắc chắn hiểu cảm giác mệt mỏi thế nào khi phải truy cập thủ công hàng loạt website của các trường học mỗi ngày chỉ để kiểm tra xem lịch tuyển sinh năm học mới (ví dụ: 2026-2027) đã mở chưa. Sót tin tức có thể lỡ mất cơ hội nộp hồ sơ của con em.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n tự động hóa 100%. Hệ thống sẽ tự động cào dữ liệu (web scraping), nhờ **Google Gemini AI** đọc hiểu nội dung trang web, và tự động bắn email cảnh báo ngay khi phát hiện trường chính thức mở cổng tuyển sinh!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Không cần phải lướt web kiểm tra thủ công hàng chục website trường học mỗi ngày.
- **Không bỏ lỡ cơ hội:** Nhận email thông báo tức thì ngay giây phút trường mở đơn tuyển sinh.
- **Trí tuệ nhân tạo chính xác:** Gemini AI đọc hiểu ngữ cảnh website cực tốt, lọc bỏ thông tin nhiễu để đưa ra kết quả chính xác (Có/Không).
- **Hoạt động 24/7 tự động:** Chạy ngầm định kỳ mỗi ngày nhờ lịch trình (Cron) đã được cấu hình sẵn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Google Gemini API Key:** Để kết nối với node AI phân tích nội dung.
- **Tài khoản SMTP:** (Gmail, SendGrid, Resend, v.v.) để cấu hình node gửi email cảnh báo.
- **Danh sách trường học:** URL website của các trường cần theo dõi tuyển sinh.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, vào giao diện n8n chọn **Add workflow** -> Nhấn `Ctrl + V` (hoặc `Cmd + V`) để dán trực tiếp vào màn hình Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 11 nodes chính được sắp xếp khoa học. Các sếp cần cấu hình chính xác các điểm sau:

- **Node `Shortlisted Schools` (Code):** 
  - Nơi các sếp cập nhật danh sách tên trường và URL website của các trường muốn theo dõi tuyển sinh.
- **Node `Get Website Content` (HTTP Request):** 
  - Thực hiện lệnh cào dữ liệu HTML từ URL của từng trường trong danh sách.
- **Node `Clean HTML` (Code):** 
  - Làm sạch mã HTML, loại bỏ các thẻ rác, script, style để lấy lại phần nội dung văn bản thuần túy, tối ưu hóa token cho AI.
- **Node `Are admissions Open` (Google Gemini):** 
  - Nhập **Google Gemini API Key** (Credentials loại `googlePalmApi`).
  - Tùy chỉnh prompt bên trong node để yêu cầu AI kiểm tra năm học hoặc cấp lớp cụ thể (ví dụ: *năm học 2026-2027 cho lớp Pre-nursery*).
- **Node `Send email` (Email Send):** 
  - Cấu hình thông tin kết nối **SMTP credentials**.
  - Điền địa chỉ email gửi (`From-Email`) và email nhận (`To-Email`) để nhận thông báo.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm thủ công với dữ liệu mẫu xem hệ thống có chạy mượt mà từ đầu đến cuối không.
- Nếu mọi thứ xanh mướt (success), các sếp gạt công tắc sang chế độ **Active** để workflow tự động chạy theo lịch trình hàng ngày của node **Daily Trigger (Cron)**.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Chat:** Thay vì chỉ nhận qua Email, các sếp có thể nối thêm node **Telegram** hoặc **Slack** để nhận thông báo ngay trên điện thoại cực kỳ tiện lợi.
- **Lưu trữ lịch sử:** Thêm node **Google Sheets** hoặc **Airtable** để ghi log lại trạng thái tuyển sinh của từng trường qua mỗi lần quét.
- **Mở rộng quy mô:** Phân chia danh sách trường thành các batch nhỏ nếu theo dõi số lượng lớn (trên 50 trường) để tối ưu hiệu suất tài nguyên.

### 📌 Kết luận
Tự động hóa theo dõi tuyển sinh chưa bao giờ dễ dàng đến thế với sự kết hợp hoàn hảo giữa Web Scraping và Gemini AI trong n8n. Hãy áp dụng ngay để không bỏ lỡ bất kỳ cột mốc quan trọng nào của con em mình, các sếp nhé!