---
title: "🚀 Tự động hóa tóm tắt và phân tích video YouTube với Apify và Gemini Pro trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động trích xuất nội dung, phụ đề và phân tích video YouTube bằng AI Gemini Pro & Apify cực kỳ mạnh mẽ."
slug: "tu-dong-hoa-tom-tat-va-phan-tich-video-youtube-apify-gemini"
tags: [n8n, automation, ai, gemini, apify, youtube-automation]
keywords: [n8n workflow, tự động hóa youtube, apify youtube downloader, gemini pro video analysis, tóm tắt video youtube ai]
---

# 🚀 Tự động hóa tóm tắt và phân tích video YouTube với Apify và Gemini Pro

Các sếp có bao giờ cảm thấy ngợp khi phải xem qua những video YouTube dài hàng tiếng đồng hồ chỉ để tìm vài ý chính hoặc cắt dựng các phân đoạn nổi bật (Shorts/Reels)? Việc xem thủ công, ghi chép timestamp và phân tích nội dung vừa tốn thời gian, vừa dễ bỏ sót các chi tiết đắt giá.

Giải pháp là đây! Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình: Nhận URL video -> Tải video & Lấy transcript qua **Apify** -> Phân tích hình ảnh, khoảnh khắc ý nghĩa bằng **Google Gemini Pro** và **OpenAI**. Không cần code phức tạp, chỉ cần vài cú click là hệ thống tự chạy.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Tự động hóa hoàn toàn việc xem, tóm tắt và tìm khoảnh khắc đắt giá trong video.
- **Phân tích đa phương thức (Multimodal):** Kết hợp sức mạnh của Gemini Pro để "xem" video và trích xuất khoảng thời gian (start/end timestamp) cực kỳ chính xác.
- **Tối ưu hóa nội dung:** Dễ dàng lấy transcript sạch sẽ thông qua Apify mà không cần xử lý âm thanh phức tạp.
- **Hoạt động 24/7:** Giao diện Form trực quan, nhận URL bất cứ lúc nào và trả về kết quả cấu trúc rõ ràng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance:** (Self-hosted hoặc Cloud).
- **Apify Account & API Key:** Dùng cho các node trích xuất và tải video YouTube.
- **Google Gemini (Google Palm) API Key:** Dùng cho node phân tích video thông minh (`Analyse Video`).
- **OpenAI API Key:** Dùng cho node `AI Section Analyzer1`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ nguồn cung cấp và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON thông qua menu tuỳ chọn trong n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình lại các node cốt lõi sau:
- **YouTube URL Form (`formTrigger`):** Node này tạo sẵn một Webhook Form để người dùng nhập link YouTube. Các sếp có thể tuỳ chỉnh giao diện form nếu muốn.
- **Apify YouTube Downloader & Transcript (`@apify/n8n-nodes-apify.apify`):** Kết nối tài khoản Apify thông qua `apifyApi` credentials. Đảm bảo các Actor ID được cấu hình đúng để tải video và lấy phụ đề (transcript) mượt mà.
- **Analyse Video (`googleGemini`):** Chọn credentials `googlePalmApi`. Node này sẽ sử dụng khả năng phân tích video multimodal của Gemini để phát hiện các khoảnh khắc ý nghĩa, trả về khoảng thời gian (timestamp) và hành động mô tả chi tiết.
- **AI Section Analyzer1 (`openAi`):** Cấu hình `openAiApi` credentials để xử lý phân tích các phân đoạn sâu hơn.
- **Call 'Shorts Creation'1 (`executeWorkflow`):** (Tuỳ chọn) Nếu các sếp có workflow con chuyên cắt dựng Shorts, hãy trỏ đường dẫn tới workflow đó tại đây.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng một URL YouTube bất kỳ trên form để kiểm tra dữ liệu trả về ở các node Code (`Set Video Data`, `Parse Key Actions`).
- Nếu mọi thứ chạy xanh mướt (success), hãy gạt công tắc sang **Active** để đưa workflow vào trạng thái vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để gửi thẳng kết quả tóm tắt và timestamp các khoảnh khắc hay về điện thoại ngay khi phân tích xong.
- **Lưu trữ Google Sheets:** Đưa dữ liệu phân tích (tiêu đề, timestamp, mô tả action) vào Google Sheets để xây dựng kho tàng content ideas cho kênh của các sếp.
- **Tự động tạo Shorts:** Kết hợp node `executeWorkflow` với các công cụ dựng video tự động để cắt ngay các đoạn video ngắn dựa trên timestamp mà Gemini tìm được.

### 📌 Kết luận
Workflow tích hợp Apify và Gemini Pro này là một "vũ khí tối thượng" cho các nhà sáng tạo nội dung, marketer hoặc những ai muốn khai thác tri thức từ video YouTube một cách tự động và thông minh. Hãy cài đặt ngay lên VPS của các sếp để tối ưu hóa hiệu suất công việc nhé!