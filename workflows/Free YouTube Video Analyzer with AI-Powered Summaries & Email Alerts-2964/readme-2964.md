---
title: "🚀 Phân tích và tóm tắt video YouTube tự động bằng AI với n8n"
description: "Tự động hóa quy trình lấy transcript YouTube, phân tích nội dung chi tiết bằng AI (OpenAI, DeepSeek, OpenRouter) và gửi email tóm tắt cực nhanh."
slug: "phan-tich-tom-tat-video-youtube-ai-n8n"
tags: [n8n, automation, no-code, youtube, ai, openai, deepseek]
keywords: [n8n workflow, tự động hóa youtube, tóm tắt video bằng ai, deepseek r1, openai gpt-4o-mini]
---

# 🚀 Phân tích và tóm tắt video YouTube tự động bằng AI với n8n

Các sếp có bao giờ cảm thấy mất quá nhiều thời gian để xem hết các video YouTube dài hàng tiếng đồng hồ chỉ để tìm vài ý chính phục vụ cho việc nghiên cứu nội dung, làm marketing hay học tập? Việc xem thủ công, ghi chép lại từng đoạn thực sự là một "cực hình" ngốn rất nhiều thời gian quý báu.

Đừng lo, giải pháp ở đây rồi! Workflow **Free YouTube Video Analyzer with AI-Powered Summaries & Email Alerts** (do tác giả Davide phát triển) sẽ giúp các sếp tự động hóa 100% quy trình: trích xuất transcript từ YouTube, dùng AI phân tích chuyên sâu, tạo tiêu đề hấp dẫn và gửi thẳng kết quả vào email. Tất cả diễn ra chỉ trong vài giây mà không cần tốn một giọt mồ hôi nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần xem hết video dài, AI sẽ đọc và chắt lọc những ý cốt lõi nhất.
- **Tóm tắt chuyên sâu & Cấu trúc rõ ràng:** Kết quả trả về theo định dạng chuẩn (Structured Output), dễ đọc, dễ áp dụng ngay cho việc lên ý tưởng content.
- **Linh hoạt chọn lựa AI Model:** Hỗ trợ nhiều mô hình mạnh mẽ như OpenAI GPT-4o-mini, DeepSeek (Reasoner), hoặc OpenRouter.
- **Tự động hóa thông báo:** Gửi báo cáo phân tích trực tiếp qua Email ngay khi hoàn tất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **YouTube Transcript API:** Tài khoản miễn phí trên `youtube-transcript.io` để lấy API Key (Authentication cho HTTP Request).
- **AI API Key:** Một trong các API Key của OpenAI, DeepSeek hoặc OpenRouter (tùy model các sếp muốn dùng).
- **SMTP Credentials:** Thông tin cấu hình gửi mail (Gmail SMTP, SendGrid, Resend,...) để node `Send Email` hoạt động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và paste trực tiếp vào n8n Editor của mình, hoặc import file JSON tải từ nguồn chính thức.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không gặp lỗi, các sếp nhớ cấu hình kỹ các node trọng điểm sau:

- **Set YouTube URL (`Set YouTube URL` node):** Điền đường dẫn video YouTube mà các sếp muốn phân tích vào biến cấu hình.
- **YouTube Video ID (`YouTube Video ID` node - Code):** Node này dùng Javascript để bóc tách ID ngắn gọn từ URL YouTube.
- **Generate transcript (`Generate transcript` node - HTTP Request):** Cấu hình Header Authentication bằng API Key lấy từ `youtube-transcript.io`.
- **Exist? (`Exist?` node - IF):** Kiểm tra xem video có bản dịch transcript hay không (vì không phải video nào trên YouTube cũng có sẵn transcript).
- **AI Chat Models (`OpenAI Chat Model` / `DeepSeek Chat Model` / `OpenRouter Chat Model`):** Chọn model AI ưa thích và kết nối đúng credentials tương ứng (ví dụ: `openAiApi`, `deepSeekApi` hoặc `openRouterApi`).
- **Analyze LLM Chain & Structured Output Parser:** Đảm bảo cấu trúc prompt và output được thiết lập đúng chuẩn để AI trả về kết quả theo đúng ý muốn (tiêu đề, tóm tắt ý chính, bài học rút ra,...).
- **Send Email (`Send Email` node):** Điền thông tin cấu hình SMTP của các sếp, chọn email người nhận và kéo nội dung phân tích từ AI vào phần body email.

#### 3. Kích hoạt ⚡️
- Nhấn nút **`When clicking ‘Test workflow’`** (`manualTrigger`) để chạy thử nghiệm với một video mẫu.
- Kiểm tra kết quả trả về ở các node và hộp thư đến xem email đã nhận được chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để sẵn sàng sử dụng bất cứ lúc nào.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thay vì chỉ nhận email, các sếp có thể gắn thêm node Slack hoặc Telegram để bắn thông báo tóm tắt video thẳng vào nhóm chat công việc.
- **Lưu trữ vào Google Sheets:** Thêm node Google Sheets để lưu lại lịch sử các video đã phân tích, tạo thành một cơ sở tri thức (Knowledge Base) cực xịn xò cho team Marketing.
- **Chạy tự động hàng loạt:** Kết hợp thêm Webhook hoặc Schedule Trigger để tự động phân tích các video mới ra mắt từ kênh YouTube yêu thích của đối thủ hoặc Influencer trong ngành.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ lợi hại cho các nhà sáng tạo nội dung, marketer và nhà nghiên cứu muốn tối ưu hóa thời gian xử lý thông tin từ video. Hãy cài đặt ngay lên hệ thống n8n của các sếp và trải nghiệm sức mạnh tự động hóa bằng AI ngay hôm nay nhé!