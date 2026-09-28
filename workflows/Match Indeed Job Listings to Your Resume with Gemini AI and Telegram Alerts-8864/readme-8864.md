---
title: "🚀 Tự Động So Khớp Việc Làm Indeed Với Hồ Sơ Của Bạn Bằng Gemini AI & Gửi Cảnh Báo Telegram"
description: "Hướng dẫn xây dựng hệ thống tự động cào dữ liệu việc làm từ Indeed, đối chiếu thông minh với CV bằng Google Gemini AI và gửi thông báo công việc phù hợp qua Telegram."
slug: "tu-dong-so-khop-viec-lam-indeed-gemini-ai-telegram"
tags: [n8n, automation, ai-agent, google-gemini, telegram, web-scraping]
keywords: [n8n workflow, tim viec tu dong, indeed scraper, gemini ai agent, telegram notification]
---

# 🚀 Tự Động So Khớp Việc Làm Indeed Với Hồ Sơ Của Bạn Bằng Gemini AI & Gửi Cảnh Báo Telegram

Các sếp có đang mệt mỏi vì mỗi ngày phải lướt hàng giờ trên Indeed để tìm việc, đọc từng mô tả công việc (JD) rồi tự hỏi xem mình có phù hợp không? Việc tìm kiếm việc làm thủ công ngốn rất nhiều thời gian và năng lượng.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ thông minh: Tự động cào dữ liệu việc làm mới nhất từ Indeed, sử dụng **Google Gemini AI** để đọc hiểu CV của các sếp, phân tích độ phù hợp với từng công việc, cấu trúc hóa kết quả và bắn thẳng thông báo những cơ hội tốt nhất về **Telegram** của các sếp ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần tự tìm kiếm thủ công, hệ thống tự động cào và lọc việc làm theo lịch trình.
- **AI thông minh cá nhân hóa:** Google Gemini AI đóng vai trò như một chuyên gia tuyển dụng nhân sự (HR Recruiter) đọc kỹ CV và chọn ra các vị trí matching nhất.
- **Nhận tin tức thời gian thực:** Kết quả phân tích được gửi gọn gàng, súc tích qua Telegram để các sếp ứng tuyển ngay lập tức.
- **Tiết kiệm hàng giờ mỗi ngày:** Chỉ tập trung vào những công việc thực sự phù hợp với năng lực và định hướng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Self-hosted hoặc Cloud).
- Tài khoản **BrowserAct** (để cào dữ liệu web và Template "Job Market Intelligence").
- Tài khoản **Google Gemini API** (cho AI Agent).
- **Telegram Bot Token** và **Chat ID/Channel ID** để nhận thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này hoặc tải file template từ n8n.io (ID: `8864`), sau đó dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 13 nodes, các sếp cần chú ý cấu hình các điểm mấu chốt sau:
- **HTTP Request / HTTP Request1 (Nodes gọi BrowserAct):** Cần điền Bearer Authentication token của BrowserAct và thay thế `workflow_id` tương ứng với template "Job Market Intelligence" của các sếp trên BrowserAct.
- **AI Agent & Gemini (Nodes AI):** Kết nối credentials của Google Gemini (`googlePalmApi`). Quan trọng nhất: Trong prompt của **AI Agent**, các sếp hãy nhớ **dán nội dung CV của chính mình** vào để AI biết và so sánh với JD.
- **Structured Output Parser:** Giúp ép kiểu đầu ra của AI trả về đúng định dạng JSON chuẩn để các node phía sau xử lý dễ dàng.
- **Code in JavaScript:** Biến dữ liệu JSON thô từ AI thành văn bản trình bày đẹp mắt, dễ đọc.
- **Send a text message (Telegram Node):** Kết nối Telegram API credentials và điền chính xác ID kênh hoặc chat ID cá nhân của các sếp.

#### 3. Kích hoạt ⚡️
- Bấm nút **‘Execute workflow’** thủ công để test lần đầu xem dữ liệu từ BrowserAct có trả về không, AI có đọc CV và Telegram có báo tin không.
- Sau khi test thành công, bật công tắc **Active workflow** để hệ thống chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Thay vì chỉ gửi Telegram, các sếp có thể nhân bản nhánh cuối để lưu thẳng các công việc phù hợp vào Google Sheets hoặc Notion để theo dõi tiến trình ứng tuyển.
- **Thêm lịch trình (Cron/Schedule Trigger):** Thay thế node `When clicking ‘Execute workflow’` bằng node `Schedule Trigger` để tự động chạy quét việc làm mỗi sáng (ví dụ: 8h sáng hàng ngày).
- **Lọc theo mức lương:** Tinh chỉnh prompt trong AI Agent để tự động loại bỏ các công việc có mức lương thấp hơn kỳ vọng của các sếp.

### 📌 Kết luận
Với workflow n8n kết hợp BrowserAct và Gemini AI này, việc tìm việc làm chưa bao giờ nhẹ nhàng và chuyên nghiệp đến thế. Hãy cài đặt ngay để không bỏ lỡ bất kỳ cơ hội nghề nghiệp mơ ước nào các sếp nhé!