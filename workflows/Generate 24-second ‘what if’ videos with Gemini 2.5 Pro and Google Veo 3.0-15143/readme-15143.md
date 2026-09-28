---
title: "🚀 Tự động tạo video 'What If' 24 giây bằng Gemini 2.5 Pro và Google Veo thông qua n8n"
description: "Khám phá workflow n8n cực đỉnh giúp tự động hóa toàn bộ quy trình sáng tạo nội dung video ngắn đa phương thức: từ kịch bản AI, tạo giọng đọc, tạo video bằng Google Veo đến ghép nối và gửi qua Telegram."
slug: "tu-dong-tao-video-what-if-gemini-veo-n8n"
tags: [n8n, automation, ai-video, gemini, google-veo, telegram]
keywords: [n8n workflow, tạo video tự động, gemini 2.5 pro, google veo, ai content creation, automation n8n]
keywords: [n8n workflow, tạo video tự động, gemini 2.5 pro, google veo, ai content creation, automation n8n]
---

# 🚀 Tự động tạo video "What If" 24 giây bằng Gemini 2.5 Pro và Google Veo

Các sếp có bao giờ cảm thấy đuối sức khi phải liên tục lên ý tưởng, viết kịch bản, tạo giọng đọc, sinh hình ảnh/video rồi lại cặm cụi dựng hình thủ công cho các kênh Social Media không? Việc sản xuất những video ngắn cuốn hút (như thể loại "What If" - điều gì sẽ xảy ra nếu...) thường tốn hàng giờ đồng hồ cho mỗi clip. 

Workflow n8n đỉnh cao được phát triển bởi **Koulikas Giannis (Coreflow Automation)** này sinh ra chính là để giải cứu các sếp. Đây là một hệ thống tự động hóa **100% không cần code**, kết hợp sức mạnh của các mô hình AI tiên tiến nhất hiện nay (Gemini 2.5 Pro, DeepSeek, Google Veo, Text-to-Speech) để tự động sản xuất một video hoàn chỉnh dài 24 giây và gửi thẳng về Telegram cho các sếp chỉ với 1 cú click!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 với các tác vụ xử lý AI và render video nặng, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Từ một ý tưởng sơ khai, AI tự viết kịch bản chia thành các phân đoạn (Hook, Segment 1, Segment 2, CTA).
- **Chất lượng đa phương thức (Multimodal):** Tự động sinh giọng đọc, tạo video bằng Google Veo, lưu trữ cloud và tự động ghép nối thành phẩm.
- **Tiết kiệm thời gian tuyệt đối:** Thay vì mất 4-5 tiếng dựng video, hệ thống tự động hoàn thành và gửi qua **Telegram** để các sếp duyệt ngay lập tức.
- **Hoạt động linh hoạt:** Dễ dàng kích hoạt thủ công hoặc tích hợp webhook để chạy tự động theo lịch biểu.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN Đồ"]
Trước khi import workflow gồm 60 nodes này, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance** (phiên bản cập nhật hỗ trợ LangChain nodes).
- **Google Gemini API Key / Google Cloud Credentials** (cho các node `Google Chat Model`, `Google Cloud Storage` và Google Veo qua HTTP Request).
- **DeepSeek API Key** (cho `DeepSeek Chat Model`).
- **Creatomate API** (hoặc dịch vụ render video tương ứng được cấu hình trong các node `Build Creatomate Request` và `Merge Video Files`).
- **Telegram Bot Token & Chat ID** (để nhận thành phẩm video hoàn chỉnh qua node `Send Video via Telegram`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy toàn bộ mã JSON của workflow.
- Vào giao diện n8n của các sếp, chọn **Workflows** -> **Import from JSON** và dán mã vào, sau đó nhấn Save.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Do workflow này có độ phức tạp cao với 60 nodes, các sếp cần chú ý cấu hình kỹ các thành phần sau:
- **Trigger Manual Workflow:** Node khởi chạy thủ công, các sếp có thể thay thế bằng Webhook hoặc Schedule Trigger nếu muốn tự động hóa theo giờ.
- **Các node AI (`Create Story`, `Prepare Hook Prompt`, `DeepSeek Chat Model`, v.v.):** Cần kết nối đúng Credentials của Google Gemini và DeepSeek để các LLM hoạt động mượt mà.
- **Nhóm node xử lý Audio & Video (`Upload Audio Segment 1`, `Upload Video Segment 1`, ...):** Đảm bảo đã cấu hình đúng quyền truy cập **Google Cloud Storage** để các file media trung gian được lưu trữ và gọi API chính xác.
- **Nhóm node kiểm tra trạng thái (`Fetch Video Status 1`, `Wait for Rendering`, `Check Render Completion`):** Kiểm tra lại thời gian chờ (`Wait` nodes) cho phù hợp với tốc độ phản hồi của API tạo video bên thứ ba.
- **Send Video via Telegram:** Điền chính xác `Bot Token` và `Chat ID` cá nhân hoặc nhóm Telegram của các sếp để nhận video thành phẩm.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với node `Trigger Manual Workflow` để test thử dữ liệu mẫu.
- Theo dõi log chạy trên n8n Editor để đảm bảo các bước từ sinh kịch bản -> tạo audio -> tạo video -> render và gửi Telegram không bị lỗi kết nối (HTTP 4xx/5xx).
- Khi đã chạy thành công, gạt công tắc sang **Active** để hệ thống chính thức đi vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Google Sheets:** Thay vì dùng Trigger thủ công, hãy nối một Google Sheets chứa danh sách các chủ đề "What If", n8n sẽ tự động quét và sản xuất hàng loạt video mỗi ngày.
- **Lưu trữ tự động:** Thêm một bước lưu video hoàn chỉnh vào Google Drive hoặc OneDrive thay vì chỉ nhận qua Telegram.
- **Đa kênh Social:** Mở rộng workflow để tự động đăng tải video vừa nhận được lên TikTok, YouTube Shorts và Facebook Reels ngay sau khi render xong.

### 📌 Kết luận
Workflow tạo video "What If" 24 giây bằng Gemini 2.5 Pro và Google Veo là một kiệt tác tự động hóa nội dung số, giúp các sếp tối ưu hóa tối đa nguồn lực và đi đầu trong cuộc đua sáng tạo nội dung ứng dụng AI. Chúc các sếp cài đặt thành công và sở hữu những kênh video triệu view!