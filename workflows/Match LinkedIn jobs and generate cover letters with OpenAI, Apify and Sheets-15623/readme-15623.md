---
title: "🚀 Tự động hóa tìm việc LinkedIn, chấm điểm CV và viết Cover Letter bằng AI với n8n"
description: "Hướng dẫn xây dựng hệ thống tự động tìm kiếm việc làm trên LinkedIn bằng Apify, so khớp CV bằng OpenAI, lưu Google Sheets và gửi thông báo qua Telegram."
slug: "tu-dong-hoa-tim-viec-linkedin-cv-cover-letter-openai-apify"
tags: [n8n, automation, openai, apify, google-sheets, telegram, ai]
keywords: [n8n workflow, tim viec linkedin, apify linkedin scraper, ai viet cover letter, tu dong hoa hr]
---

# 🚀 Tự động hóa tìm việc LinkedIn, chấm điểm CV và viết Cover Letter bằng OpenAI & Apify

Các sếp có đang mệt mỏi vì mỗi ngày phải lên LinkedIn thủ công tìm việc, đọc từng mô tả công việc (JD), rồi lại ngồi vắt óc viết từng chiếc Cover Letter (thư xin việc) dài dòng? Việc này không chỉ tốn hàng giờ đồng hồ mà còn dễ bỏ lỡ các cơ hội việc làm tốt.

Giải pháp đây rồi! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ do chuyên gia **Jitesh Dugar** thiết kế. Hệ thống này sẽ **tự động 100%**: quét việc làm LinkedIn theo tiêu chí của các sếp, đọc CV từ Google Drive, dùng AI (OpenAI) để chấm điểm mức độ phù hợp, tự động viết Cover Letter cá nhân hóa, lưu tất cả vào Google Sheets và bắn thông báo nóng hổi qua Telegram khi có job "ngon".

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Tự động tìm kiếm, phân tích và lọc hàng chục job mỗi ngày mà không cần động tay.
- **Cover Letter chuẩn chỉnh:** AI tự động phân tích JD và CV để viết thư xin việc riêng biệt, tối ưu cho từng vị trí.
- **Không bỏ lỡ cơ hội:** Nhận cảnh báo ngay lập tức qua Telegram khi có công việc có độ phù hợp cao (Score ≥ 50).
- **Quản lý khoa học:** Toàn bộ danh sách việc làm, điểm số và thư xin việc được lưu trữ tự động vào Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Drive & Google Sheets:** Nơi lưu trữ file CV (PDF) và file cấu hình từ khóa tìm kiếm/lưu kết quả.
- **Apify Account:** Để sử dụng Actor quét dữ liệu LinkedIn Jobs.
- **OpenAI API Key:** Dành cho AI Agent chấm điểm CV và viết Cover Letter (`gpt-4.1-mini`).
- **Telegram Bot Token & Chat ID:** Để nhận thông báo việc làm phù hợp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn gốc hoặc tạo mới n8n workflow và cấu hình lần lượt 12 nodes theo danh sách bên dưới.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy trơn tru, các sếp cần chú ý cấu hình các node chủ chốt sau:

- **Schedule Trigger:** Thiết lập lịch chạy tự động hàng ngày (ví dụ: 8 giờ sáng mỗi ngày).
- **Download file (Google Drive):** Kết nối tài khoản Google Drive và chọn đến file CV định dạng `.pdf` của các sếp.
- **Extract from File:** Đảm bảo node này trích xuất toàn bộ text từ file PDF CV ở bước trên.
- **Get row(s) in sheet (Google Sheets):** Trỏ tới Google Sheet chứa các từ khóa tìm kiếm (Keyword, Location, Easy Apply).
- **Run an Actor and get dataset (Apify):** Cấu hình Apify API Key và kết nối với Actor LinkedIn Job Scraper để nhận đầu vào từ Google Sheets.
- **OpenAI Chat Model & Job Matcher (AI Agent):** Chọn model `gpt-4.1-mini`, nạp API Key của OpenAI. Agent sẽ nhận dữ liệu từ CV và JD để chấm điểm và viết thư.
- **Parse AI Output (Edit Fields):** Biến đổi dữ liệu đầu ra từ AI thành các trường sạch như `score` và `coverLetter`.
- **Append or update row in sheet (Google Sheets):** Lưu kết quả vào Google Sheets, sử dụng đường dẫn LinkedIn Job làm khóa chính (Matching column) để tránh trùng lặp dòng.
- **High Match Score Filter (If Node):** Thiết lập điều kiện lọc (`Score ≥ 50`). Các job đạt điểm từ 50 trở lên mới được đẩy tiếp.
- **Send a text message (Telegram):** Kết nối Telegram Bot để bắn tin nhắn chi tiết (Tên công việc, Công ty, Điểm số, Link apply) về máy của các sếp.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) thủ công từng node hoặc toàn bộ workflow để kiểm tra dữ liệu trả về từ Apify và OpenAI.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ dùng Telegram, các sếp có thể tích hợp thêm node **Slack** hoặc **Discord** để team cùng theo dõi các cơ hội việc làm.
- **Tùy chỉnh tiêu chuẩn lọc:** Thay đổi điểm số ở node *Score Filter* lên `>= 70` nếu các sếp chỉ muốn nhận những job cực kỳ chất lượng.
- **Tự động hóa nộp đơn:** Nếu nền tảng hỗ trợ API hoặc Apify hỗ trợ tự động điền form, các sếp có thể mở rộng workflow để tự động apply luôn (cần cân nhắc chính sách của LinkedIn).

### 📌 Kết luận
Một hệ thống tự động hóa tìm việc thông minh sẽ giúp các sếp luôn ở thế chủ động trên thị trường lao động mà không tốn chút sức lực thủ công nào. Hãy thiết lập ngay workflow này để tối ưu hóa hành trình sự nghiệp của mình nhé các sếp!