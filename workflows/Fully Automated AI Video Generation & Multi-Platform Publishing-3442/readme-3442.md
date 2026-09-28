---
title: "🚀 Tự động hóa tạo video AI hoàn chỉnh và đăng đa nền tảng với n8n"
description: "Hướng dẫn xây dựng hệ thống tạo video ngắn bằng AI tự động 100% từ Google Sheets sử dụng OpenAI, Flux, Kling, ElevenLabs, Creatomate và đăng lên TikTok, YouTube, Instagram, Facebook."
slug: "tu-dong-hoa-tao-video-ai-va-dang-da-nen-tang"
tags: [n8n, automation, ai-video, content-creation, social-media, openai]
keywords: [n8n workflow, tạo video ai tự động, flux, kling ai, elevenlabs, creatomate, đăng video đa nền tảng]
---

# 🚀 Tự động hóa tạo video AI hoàn chỉnh và đăng đa nền tảng với n8n

Việc sản xuất video ngắn (Shorts, Reels, TikTok) đều đặn hàng ngày tiêu tốn rất nhiều thời gian từ khâu lên ý tưởng, viết kịch bản, tạo giọng đọc (voiceover), thiết kế hình ảnh, dựng phim cho đến bước đăng tải lên hàng loạt nền tảng mạng xã hội. 

Workflow n8n này chính là giải pháp tự động hóa toàn diện (End-to-End Automation) giúp các sếp giải phóng hoàn toàn sức lao động. Hệ thống sẽ tự động đọc ý tưởng từ Google Sheets, sử dụng AI để tạo kịch bản, hình ảnh (Flux), video động (Kling), lồng tiếng (ElevenLabs), dựng video tự động (Creatomate) và cuối cùng là xuất bản lên TikTok, YouTube, Instagram, Facebook, LinkedIn một cách mượt mà.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%**: Từ ý tưởng thô trong Google Sheets đến video hoàn thiện mà không cần chạm tay vào Adobe Premiere hay CapCut.
- **Đa nền tự động xuất bản**: Tự động sinh mô tả chuẩn SEO và đẩy video lên TikTok, YouTube Shorts, Instagram Reels, Facebook và LinkedIn.
- **Tối ưu chi phí & thời gian**: Tích hợp sẵn cơ chế kiểm tra lỗi, retry tự động và tính toán Token usage để kiểm soát chi phí API chặt chẽ.
- **Hoạt động 24/7**: Lên lịch chạy tự động hàng ngày (`Once Per Day`) và gửi thông báo trạng thái qua Discord.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance** (Khuyến nghị phiên bản từ 1.81.4 trở lên).
- **OpenAI API Key** (Dùng cho tạo kịch bản, prompt, caption).
- **PiAPI Key** (Để gọi model Flux tạo ảnh và Kling AI tạo video).
- **ElevenLabs API Key & Voice ID** (Tạo giọng đọc lồng tiếng chuyên nghiệp).
- **Creatomate API Key & Template ID** (Dựng và render video tự động).
- **Google Cloud Console**: Bật Google Sheets API, Google Drive API và lấy OAuth 2.0 Credentials.
- **Upload-post.com API Token** (Dịch vụ hỗ trợ đăng video lên các mạng xã hội).
- **Discord Webhook URL** (Nhận thông báo khi video hoàn thành).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow (hoặc tải file JSON từ nguồn gốc) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 43 nodes được chia thành các phân đoạn logic rõ ràng. Các sếp cần chú ý cấu hình các phần sau:

- **Cấu hình API Keys (`Set API Keys` node)**: 
  Điền các thông tin xác thực quan trọng bao gồm: PiAPI Key, ElevenLabs API Key, Creatomate Template ID. 
  *(Mẹo: Tạo template trên Creatomate, bấm "Source Code" và dán mã JSON mẫu, sau đó lấy Template ID dán vào đây).*
- **Google Sheets (`Load Google Sheet` và `Update Google Sheet` nodes)**: 
  Copy mẫu Google Sheet quản lý ý tưởng video, kết nối tài khoản Google Sheets OAuth2 và liên kết với sheet của các sếp.
- **AI Prompts (`Generate Script`, `Generate Image Prompts`, `Generate Video Captions`)**: 
  Các node OpenAI này chứa các câu lệnh (prompt) mặc định. Các sếp có thể tinh chỉnh lại phong cách, ngôn ngữ (tiếng Việt) cho phù hợp với nội dung kênh của mình.
- **Tạo ảnh & Video (`Generate Image`, `Image-to-Video`)**: 
  Sử dụng PiAPI tích hợp Flux (`Qubico/flux1-dev` hoặc `schnell`) và Kling AI (`std` hoặc `pro`). 
- **Voiceover (`Generate voice` node)**: 
  Cấu hình Voice ID của ElevenLabs tại endpoint URL: `https://api.elevenlabs.io/v1/text-to-speech/{voice_id}`.
- **Đăng mạng xã hội (`Upload Video and Description to Tiktok`, `Instagram`, `Youtube`, `Facebook`, `Linkedin`)**: 
  Kết nối tài khoản từ `upload-post.com` bằng HTTP Header Auth để hệ thống tự động đẩy video và caption đã tạo lên các nền tảng.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (`Execute Workflow`) với 1 dòng dữ liệu mẫu trên Google Sheets để kiểm tra toàn bộ luồng từ OpenAI -> PiAPI -> ElevenLabs -> Creatomate.
- Sau khi test thành công, bật trạng thái **Active** để hệ thống tự động chạy theo lịch hẹn (Schedule Trigger).

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack**: Bổ sung thêm node Telegram bên cạnh Discord để nhận thông báo lỗi ngay lập tức trên điện thoại nếu có lỗi xảy ra trong quá trình gọi API AI.
- **Quản lý chi phí**: Node `Calculate Token Usage` giúp ghi lại lượng token tiêu thụ. Các sếp có thể viết thêm một bước log chi phí này vào Google Sheets để tối ưu tài chính.
- **Tùy biến Template Creatomate**: Thiết kế sẵn nhiều mẫu template video khác nhau trên Creatomate và thêm logic `If` để random mẫu video giúp kênh phong phú hơn.

### 📌 Kết luận
Với workflow này, các sếp đã sở hữu một "phòng dựng phim AI" tự động hoàn toàn, giúp tiết kiệm hàng chục giờ làm việc mỗi tuần và bùng nổ nội dung trên mọi nền tảng mạng xã hội. Hãy "lên đồ" ngay và trải nghiệm sức mạnh tự động hóa của n8n nhé!