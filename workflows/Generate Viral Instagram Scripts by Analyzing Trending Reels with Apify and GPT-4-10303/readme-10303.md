---
title: "🚀 Tự động tạo kịch bản Instagram Reels triệu view bằng Apify và GPT-4"
description: "Hướng dẫn cài đặt workflow n8n tự động cào xu hướng Reels từ hashtag, phiên âm video, phân tích cấu trúc và viết lại kịch bản viral bằng AI."
slug: "tu-dong-tao-kich-ban-instagram-reels-voi-apify-gpt4"
tags: [n8n, automation, no-code, instagram, ai-agent, openai]
keywords: [n8n workflow, tao kich bản instagram, apify instagram scraper, ai viết kịch bản reels, gpt-4 automation]
---

# 🚀 Tự động tạo kịch bản Instagram Reels triệu view bằng Apify và GPT-4

Việc sáng tạo nội dung trên Instagram Reels đòi hỏi các nhà sáng tạo phải liên tục bắt trend, phân tích các video triệu view và tìm kiếm ý tưởng kịch bản mới mỗi ngày. Quá trình làm thủ công này ngốn rất nhiều thời gian từ việc tìm hashtag, xem video, nghe lại nội dung cho đến việc vắt óc lên ý tưởng.

Workflow n8n này sẽ giúp các sếp tự động hóa **100% quy trình nghiên cứu và sản xuất kịch bản**: Tự động cào các Reels hot từ hashtag, phiên âm nội dung, dùng AI (GPT-4) phân tích cấu trúc tâm lý và nhịp điệu để viết ra những kịch bản hoàn toàn mới nhưng giữ nguyên công thức "viral" của đối thủ.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần phải cặm cụi lướt Instagram hay ngồi gõ lại lời thoại từ video nữa.
- **Bắt trend chính xác:** Khai thác dữ liệu thực tế từ những Reels đang có lượt tương tác cao nhất theo hashtag mục tiêu.
- **Cấu trúc viral chuẩn chỉnh:** AI Agent phân tích ngữ điệu, cấu trúc câu chuyện (hook, body, CTA) của video gốc để tạo ra kịch bản độc quyền cho riêng sếp.
- **Báo cáo tự động:** Tổng hợp kết quả và gửi thẳng qua Gmail ngay khi hoàn tất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Apify API Key:** Dùng để cào dữ liệu Reels và phiên âm video ([Tạo tài khoản Apify miễn phí tại đây](https://apify.com?fpr=eg224f)).
- **OpenAI API Key:** Sử dụng mô hình GPT-4 để phân tích và viết kịch bản.
- **Google Sheet:** Lưu trữ danh sách video và kịch bản AI ([Copy Google Sheet mẫu tại đây](https://docs.google.com/spreadsheets/d/1XupKy-R6zPvCfeh5q9co5O-wPMI64D7xvavFkz0yQqk/edit?usp=sharing)).
- **Gmail Account:** Để nhận báo cáo hoàn thành workflow.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc sử dụng tính năng import file JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các node sau:
- **On form submission:** Node dạng Form Trigger để người dùng nhập hashtag muốn phân tích trực tiếp trên giao diện web.
- **Scrape Hashtag & Transcribe Video:** Cấu hình thông tin kết nối Apify API Key và kiểm tra lại endpoint gọi Actor của Apify trong node `httpRequest`.
- **Add to the sheet, Update sheet & Add AI script:** Kết nối tài khoản Google Sheets của các sếp (`googleSheetsOAuth2Api`), sau đó trỏ tới file Google Sheet vừa copy ở phần chuẩn bị.
- **OpenAI Chat Model:** Chọn credential OpenAI và cấu hình model (ví dụ: `gpt-4o-mini` hoặc `gpt-4`) để AI thực hiện nhiệm vụ phân tích và viết kịch bản.
- **Send a message:** Cấu hình tài khoản Gmail (`gmailOAuth2`) để nhận thông báo tổng kết số lượng kịch bản đã tạo thành công.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng cách điền một hashtag bất kỳ vào Form Trigger để kiểm tra từng bước cào dữ liệu và sinh kịch bản.
- Sau khi test thành công, bật công tắc **Active** để đưa workflow vào trạng thái hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thay vì chỉ nhận báo cáo qua Gmail, các sếp có thể thêm node Telegram/Slack để bắn thông báo ngay khi có kịch bản mới ra lò.
- **Lưu trữ nâng cao:** Mở rộng Google Sheet thành một "Content Hub" dài hạn để phân loại kịch bản theo ngách (Niche) hoặc độ tuổi người xem.
- **Đa dạng hóa AI Model:** Thử nghiệm kết hợp thêm các mô hình như Claude 3.5 Sonnet (thông qua Langchain node) để có văn phong viết kịch bản tự nhiên và bén hơn.

### 📌 Kết luận
Việc bắt trend trên Instagram chưa bao giờ dễ dàng và tự động hóa đến thế. Hãy "lên đồ" ngay bộ workflow này để tối ưu hóa hiệu suất sản xuất nội dung video ngắn cho doanh nghiệp hoặc kênh cá nhân của các sếp!