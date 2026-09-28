---
title: "🚀 Tự động hóa tìm việc trên LinkedIn: Match Resume với AI, Viết Cover Letter và Báo cáo qua Telegram"
description: "Khám phá workflow n8n giúp tự động tìm kiếm việc làm trên LinkedIn, chấm điểm độ phù hợp CV bằng AI, tự động viết Cover Letter và gửi cảnh báo qua Telegram."
slug: "tu-dong-hoa-tim-viec-linkedin-ai-cover-letter-telegram"
tags: [n8n, automation, no-code, AI, LinkedIn, Telegram, OpenAI]
keywords: [n8n workflow, tự động hóa tìm việc, LinkedIn job search AI, AI match resume, viết cover letter tự động, Telegram alerts]
---

# 🚀 Tự động hóa tìm việc trên LinkedIn: Match Resume với AI, Viết Cover Letter và Báo cáo qua Telegram

Các sếp đang đi tìm việc hoặc làm tuyển dụng và cảm thấy mệt mỏi khi phải lướt LinkedIn hàng giờ, thủ công copy từng mô tả công việc, tự viết hàng tá thư xin việc (Cover Letter) nhàm chán? 

Workflow n8n này sẽ "cân" hết các công việc đó! Hệ thống sẽ tự động quét các công việc mới nhất trên LinkedIn dựa trên tiêu chí của các sếp, đọc CV từ Google Drive, dùng AI (OpenAI/GPT) để chấm điểm mức độ phù hợp (từ 0-100), tự động viết Cover Letter cực kỳ chuyên nghiệp và bắn thông báo ngay lập tức qua **Telegram** nếu tìm thấy công việc "chân ái". Tất cả hoàn toàn tự động 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần thủ công tìm kiếm, lọc và phân tích từng tin tuyển dụng trên LinkedIn.
- **Chấm điểm thông minh (AI Match):** AI sẽ đọc CV và JD (Job Description) để chấm điểm độ phù hợp khách quan từ 0-100.
- **Cá nhân hóa Cover Letter:** Tự động tạo thư xin việc bám sát kinh nghiệm thực tế của các sếp và yêu cầu của nhà tuyển dụng.
- **Cảnh báo tức thì:** Nhận thông báo qua Telegram ngay khi có công việc có điểm số phù hợp (mặc định > 50 điểm).
- **Lưu trữ tự động:** Toàn bộ danh sách việc làm, điểm số và link ứng tuyển được lưu gọn gàng vào Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Tài khoản Google Drive:** Nơi lưu trữ file CV định dạng PDF của các sếp.
- **Google Sheets:** Bản sao của [Template Google Sheets Quản lý việc làm](https://docs.google.com/spreadsheets/d/1mtKVxj_z_QCLGXMx0mJVihWSgS41SzHfU1Rv4r_mRY0).
- **OpenAI API Key (hoặc mô hình AI tương đương):** Dùng cho node **OpenAI Chat Model** để phân tích CV và viết Cover Letter.
- **Telegram Bot Token:** Để gửi tin nhắn cảnh báo về điện thoại của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào giao diện n8n Editor của các sếp (hoặc copy toàn bộ JSON và dán vào canvas).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node trọng điểm sau:
- **Schedule Trigger:** Mặc định workflow chạy lúc 5 giờ chiều mỗi ngày. Các sếp có thể đổi lịch chạy tùy ý.
- **Download file (Google Drive):** Kết nối tài khoản Google Drive và chọn file CV (định dạng `.pdf`) đã được tải lên sẵn.
- **Get row(s) in sheet & Append or update row in sheet (Google Sheets):** Kết nối Google Sheets API và trỏ tới file Sheet quản lý việc làm (đã copy từ template ở trên) để đọc bộ lọc tìm kiếm và lưu kết quả.
- **OpenAI Chat Model:** Điền thông tin `credentials` cho OpenAI API và chọn mô hình mong muốn (như `gpt-4.1-mini`).
- **Score Filter:** Mặc định workflow lọc các job có điểm số `> 50`. Các sếp có thể tăng giảm ngưỡng này tùy theo nhu cầu tuyển chọn.
- **Send a text message (Telegram):** Kết nối Telegram Bot Token và điền Chat ID của các sếp để nhận thông báo.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) thủ công để kiểm tra quá trình đọc CV từ Google Drive, gọi API tìm kiếm LinkedIn và phản hồi từ AI Agent.
- Sau khi test thành công, bật công tắc **Active workflow** để hệ thống tự động chạy ngầm mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Kết hợp thêm node Discord hoặc Slack bên cạnh Telegram để nhận job ở nhiều nền tảng chat khác nhau.
- **Tự động hóa nộp đơn:** Nếu tìm được các job dạng "Easy Apply", các sếp có thể nghiên cứu tích hợp thêm Puppeteer/Playwright node để tự động gửi hồ sơ luôn.
- **Lưu lịch sử chạy:** Sử dụng thêm node Error Trigger để gửi cảnh báo về Telegram nếu quá trình quét job gặp lỗi (do thay đổi cấu trúc HTML của LinkedIn).

### 📌 Kết luận
Với workflow này, hành trình tìm kiếm công việc mơ ước trên LinkedIn không còn là gánh nặng tốn thời gian. Hãy "lên đồ" ngay một con VPS, import workflow và để AI làm thay phần việc nặng nhọc nhất cho các sếp! Chúc các sếp sớm tìm được công việc như ý!