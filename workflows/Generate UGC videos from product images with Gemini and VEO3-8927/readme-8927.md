---
title: "🚀 Tự động tạo video UGC triệu view từ ảnh sản phẩm với Gemini và VEO3 trên n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động hóa toàn bộ quy trình biến ảnh sản phẩm thành video UGC chuyên nghiệp qua Telegram bằng AI."
slug: "tao-ugc-video-tu-anh-san-pham-gemini-veo3-n8n"
tags: [n8n, automation, ai, telegram, gemini, anthropic, video-generation]
keywords: [n8n workflow, tạo video ugc, gemini ai, veo3, tự động hóa telegram, claude sonnet, content creation]
---

# 🚀 Tự động tạo video UGC triệu view từ ảnh sản phẩm với Gemini và VEO3

Việc sản xuất video UGC (User Generated Content) thủ công để chạy quảng cáo TikTok, Instagram Reels hay YouTube Shorts thường ngốn rất nhiều thời gian, công sức và chi phí thuê KOL/KOC. Các sếp có bao giờ nghĩ đến việc chỉ cần **gửi 1 tấm ảnh sản phẩm qua Telegram**, nhập vài dòng yêu cầu và hệ thống sẽ tự động phân tích, viết kịch bản, render video sinh động bằng AI chưa?

Workflow n8n này do **Growth AI** phát triển sẽ giải quyết triệt để bài toán trên, giúp các sếp tự động hóa hoàn toàn quy trình sáng tạo nội dung đa phương tiện (Multimodal AI) từ A đến Z mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, xử lý các tệp hình ảnh và video nặng mà không lo sập nguồn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tốc độ thần tốc:** Biến ảnh sản phẩm thành video UGC hoàn chỉnh chỉ trong vài phút, sẵn sàng đăng tải.
- **Chất lượng điện ảnh:** Ứng dụng Gemini AI, Claude Sonnet và VEO3 Fast để tạo ra hình ảnh sắc nét, kịch bản tự nhiên và video chuyển động mượt mà (định dạng dọc 9:16).
- **Tương tác mượt mà qua Telegram:** Quản lý toàn bộ quy trình nhận ảnh, hỏi ý tưởng kịch bản và trả kết quả video ngay trên ứng dụng chat quen thuộc.
- **Hoạt động 24/7:** Bot tự động túc trực, kiểm tra trạng thái render video và ghép nối các phân đoạn tự động.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow "lên đồ" mượt mà, các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Telegram Bot:** Tạo qua `@BotFather` để lấy token.
- **OpenRouter API:** Tài khoản có quyền truy cập Gemini (dùng qua OpenRouter).
- **Anthropic API:** Key truy cập Claude 4 Sonnet cho việc viết kịch bản.
- **KIE.AI Account:** Token xác thực (`httpBearerAuth`) để gọi dịch vụ tạo video VEO3 Fast.
- **n8n Instance:** Máy chủ n8n đang hoạt động ổn định.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn gốc hoặc copy toàn bộ mã JSON, sau đó paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 23 nodes được chia thành các phase rõ ràng. Các sếp cần cấu hình chính xác các điểm sau:
- **Telegram Trigger & các node Telegram (`Send message and wait for response`, `Get a file`, `Send a video`...):** Chọn đúng `telegramApi` credentials đã tạo từ BotFather.
- **HTTP Request (Gemini qua OpenRouter):** Điền `openRouterApi` credentials và kiểm tra model Gemini được gọi để tối ưu hóa/nâng cấp ảnh sản phẩm sang khung hình vuông (1:1).
- **Basic LLM Chain & Anthropic Chat Model:** Cấu hình `anthropicApi` credentials, chọn model `claude-sonnet-4-20250514` để phân tích ảnh, kết hợp ý tưởng của người dùng và tạo kịch bản 2 phân đoạn (mỗi phân đoạn 7-8 giây).
- **HTTP Request1, HTTP Request2 (VEO3):** Sử dụng `httpBearerAuth` credentials với token từ KIE.AI để gửi yêu cầu tạo video từ prompt của Claude và theo dõi trạng thái.
- **Edit Fields:** Cập nhật lại các biến môi trường hoặc Telegram Token nếu cần thiết để đảm bảo luồng truyền dữ liệu chính xác.

#### 3. Kích hoạt ⚡️
- Gửi một bức ảnh sản phẩm thử nghiệm tới Bot Telegram của sếp.
- Làm theo các bước hướng dẫn của bot trên chat (gửi ý tưởng hội thoại/lời thoại).
- Kiểm tra kết quả trả về và gạt công tắc **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ Log Google Sheets:** Kết nối thêm node Google Sheets để lưu lại lịch sử ảnh khách hàng gửi và video đã tạo nhằm dễ dàng quản lý chiến dịch.
- **Thông báo đội ngũ (Slack/Telegram Group):** Thêm node gửi thông báo về nhóm nội bộ mỗi khi có video UGC hoàn thành.
- **Tích hợp kho lưu trữ:** Đẩy video render xong tự động lên Google Drive hoặc AWS S3 thay vì chỉ nhận qua Telegram.

### 📌 Kết luận
Workflow tạo UGC video tự động này là vũ khí tối tân giúp các đội ngũ marketing và nhà sáng tạo nội dung tiết kiệm hàng chục giờ làm việc mỗi tuần. Hãy thiết lập ngay hôm nay để tối ưu hóa hiệu suất làm video quảng cáo của doanh nghiệp các sếp nhé!