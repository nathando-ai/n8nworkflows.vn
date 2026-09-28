---
title: "🚀 Tự động tạo caption mạng xã hội từ Google Autocomplete với Dumpling AI và GPT-4o trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy từ khóa từ Google Sheets, gọi Dumpling AI lấy gợi ý tìm kiếm, sử dụng GPT-4o viết caption và lưu lại kết quả."
slug: "tu-dong-tao-caption-mang-xa-hoi-dumpling-ai-gpt-4o-n8n"
tags: [n8n, automation, ai, marketing, gpt-4o, google-sheets]
keywords: [n8n workflow, tạo caption tự động, dumpling ai, gpt-4o, google sheets automation, content marketing]
---

# 🚀 Tự động tạo caption mạng xã hội từ Google Autocomplete với Dumpling AI và GPT-4o

Các sếp làm marketing hay sáng tạo nội dung chắc hẳn đều hiểu cảm giác "cạn kiệt ý tưởng" khi phải nghĩ hàng chục caption mỗi tuần cho Facebook, TikTok hay Instagram. Việc ngồi tra Google Search, xem các từ khóa gợi ý (autocomplete) rồi tự viết từng câu caption thủ công cực kỳ tốn thời gian và nhàm chán.

Đừng lo, workflow n8n này sẽ giúp các sếp giải quyết triệt để vấn đề đó. Hệ thống sẽ tự động quét các ý tưởng tìm kiếm nổi bật từ Google thông qua **Dumpling AI**, sau đó tận dụng sức mạnh của **GPT-4o** để biến chúng thành những chiếc caption siêu cuốn hút, sẵn sàng để đăng tải — hoàn toàn tự động 100% không cần tốn một giọt mồ hôi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn phải thủ công đi tìm từ khóa gợi ý hay ngồi vắt óc viết từng dòng caption.
- **Bắt trúng xu hướng:** Khai thác trực tiếp từ dữ liệu gợi ý tìm kiếm thực tế của Google (Autocomplete), giúp nội dung luôn sát với nhu cầu tìm kiếm của khách hàng.
- **Cá nhân hóa thông minh:** GPT-4o tạo ra các nội dung ngắn gọn, sáng tạo, phù hợp cho các nền tảng mạng xã hội.
- **Hoạt động tự động 24/7:** Chạy định kỳ mỗi ngày để chuẩn bị sẵn kho nội dung dồi dào trên Google Sheets cho các sếp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Google Sheets account:** Để lưu danh sách từ khóa gốc và nhận lại kết quả caption đã tạo.
- **Dumpling AI API Key:** Dùng để gọi API lấy danh sách gợi ý tìm kiếm từ Google Autocomplete (`/get-autocomplete`).
- **OpenAI API Key:** Để kết nối với mô hình GPT-4o tạo nội dung.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ hệ thống hoặc sao chép mã nguồn JSON, sau đó dán trực tiếp vào n8n Editor của các sếp bằng cách chọn **New** -> **Import from JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 7 nodes chính phối hợp nhịp nhàng với nhau. Các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Run Every Day at 12 PM (`scheduleTrigger`):** 
  - Mặc định lịch chạy là 12 giờ trưa hàng ngày. Các sếp có thể bấm vào node này để đổi lại khung giờ phù hợp với múi giờ hoặc chiến dịch của đội ngũ.
- **Get Search Keywords from Google Sheet (`googleSheets`):** 
  - Kết nối tài khoản Google Sheets của các sếp (`googleSheetsOAuth2Api`).
  - Chọn file Google Sheets và Sheet chứa danh sách các từ khóa gốc (seed keywords) mà các sếp muốn phân tích.
- **Fetch Autocomplete Suggestions (Dumpling AI) (`httpRequest`):** 
  - Sử dụng Authentication kiểu Header Auth (`httpHeaderAuth`) với API Key của Dumpling AI.
  - Trỏ đến endpoint `/get-autocomplete` để lấy các gợi ý tìm kiếm liên quan đến từ khóa từ Google.
- **Format Suggestions into Array & Loop Through Each Autocomplete Suggestion (`set` & `splitOut`):** 
  - Các node này giúp chuẩn hóa dữ liệu trả về từ API thành mảng và bóc tách từng gợi ý riêng lẻ để xử lý tuần tự (loop). Không cần chỉnh sửa gì nhiều ở đây trừ khi các sếp muốn tùy biến cấu trúc dữ liệu.
- **Generate Caption from Suggestion (GPT-4o) (`openAi`):** 
  - Kết nối `openAiApi` với tài khoản OpenAI của các sếp.
  - Cấu hình Prompt trong node này để ra lệnh cho GPT-4o đóng vai trò là chuyên gia Social Media, viết caption ngắn gọn, kèm hashtag dựa trên từ khóa gợi ý nhận được từ bước trước.
- **Save Keyword & Generated Caption to Google Sheet (`googleSheets`):** 
  - Cấu hình lại thông tin Google Sheets để lưu cặp dữ liệu gồm `Keyword gốc/Gợi ý` và `Caption do AI tạo` vào một dòng mới (Operation: `append`).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để test thử nghiệm với một vài từ khóa mẫu, kiểm tra xem dữ liệu đã được đẩy về Google Sheets chuẩn chưa.
- Sau khi mọi thứ mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo:** Nối thêm node Telegram hoặc Slack vào cuối chuỗi để bot bắn tin nhắn báo cáo ngay cho các sếp mỗi khi tạo xong loạt caption mới trong ngày.
- **Đa dạng hóa AI:** Các sếp có thể thay thế hoặc thử nghiệm mô hình khác ngoài GPT-4o (như Claude 3.5 Sonnet) để xem văn phong nào hợp với brand của mình nhất.
- **Mở rộng nguồn từ khóa:** Thay vì lấy từ Google Sheets cố định, có thể kết hợp thêm các trigger nhận từ khóa qua Webhook từ trang web hoặc form đăng ký của khách hàng.

### 📌 Kết luận
Workflow này là một "vũ khí bí mật" giúp tiết kiệm hàng tá thời gian sáng tạo nội dung mỗi tuần. Hãy thiết lập ngay hôm nay để tự động hóa quy trình content marketing của các sếp và tập trung vào những chiến lược kinh doanh lớn hơn!