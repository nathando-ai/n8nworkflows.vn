---
title: "🚀 Tự động hóa sản xuất video ngắn kinh dị (Faceless Shorts) bằng AI và n8n"
description: "Xây dựng kênh YouTube Faceless tự động 100% với n8n, OpenAI GPT-4o, TTS, Replicate Video và YouTube API. Tạo cốt truyện, lồng tiếng, dựng hình và đăng video không cần lộ mặt."
slug: "tu-dong-hoa-tao-video-nghin-luot-xem-kinh-di-n8n"
tags: [n8n, automation, youtube-shorts, openai, ai-video, content-creation]
keywords: [n8n workflow, tạo video tự động, faceless shorts, youtube automation, openai tts, replicate video]
---

# 🚀 Tự động hóa sản xuất video ngắn kinh dị (Faceless Shorts) bằng AI và n8n

Việc xây dựng một kênh YouTube Faceless (không lộ mặt) chủ đề kinh dị đòi hỏi rất nhiều công sức thủ công: từ lên ý tưởng, viết kịch bản, tạo giọng đọc (TTS), sinh hình ảnh/video minh họa, cho đến bước edit video phức tạp và đăng tải. 

Nếu các sếp đang tìm kiếm một giải pháp tự động hóa toàn diện từ A-Z bằng AI, thì workflow này chính là "vũ khí bí mật". Chỉ với các câu lệnh đơn giản qua chat, hệ thống sẽ tự động hóa toàn bộ quy trình sản xuất video ngắn (Shorts) kinh dị một cách mượt mà nhờ n8n kết hợp OpenAI, Replicate, Google Drive và YouTube.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Từ kịch bản, giọng đọc, tạo hình ảnh/video đến ghép nối FFmpeg và đăng YouTube.
- **Tiết kiệm 90% thời gian:** Không cần tốn hàng giờ đồng hồ dựng video thủ công trên CapCut hay Premiere.
- **Chất lượng chuyên nghiệp:** Sử dụng GPT-4o-mini, OpenAI TTS-1-HD và các mô hình AI tạo ảnh/video hàng đầu qua Replicate.
- **Kiểm soát linh hoạt:** Dễ dàng duyệt kịch bản, chỉnh sửa qua Google Sheets và kiểm soát trạng thái xuất bản qua Chat Trigger.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **OpenAI API Key** (Cho GPT-4o-mini và OpenAI TTS).
- **Replicate API Key / Header Auth** (Cho việc sinh hình ảnh và video AI).
- **Google Sheets & Google Drive Credentials** (Lưu trữ kịch bản, quản lý file tạm và video thành phẩm).
- **YouTube OAuth2 API** (Để tự động upload video lên kênh).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn gốc hoặc copy trực tiếp mã nguồn JSON, sau đó paste vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 46 nodes được chia làm 4 bước vận hành chính dựa trên chat trigger:

- **Bước 1: Generate Story Beats (Lên ý tưởng & Kịch bản)**
  - Cấu hình các node `Story Beat Generator`, `Story Beat Generator5`, `Story Beat Generator6` (sử dụng model `gpt-4o-mini`). Đảm bảo đã liên kết `openAiApi` credentials.
  - Kết nối `Google Sheet Idea Log` và `Get Story Idea` với Google Sheets của các sếp theo định dạng chuẩn.
  - *Lưu ý:* Nhập từ khóa `idea` vào `When chat message received` để kích hoạt kịch bản. Giữ nội dung ngắn gọn dưới 20 từ mỗi beat và tránh dùng ký tự đặc biệt (' và ").

- **Bước 2: Create Video (Dựng video từ AI)**
  - Cấu hình các node `🎨 Image Generator`, `HTTP Request`, và `🎨 Video Generator` liên kết với API của Replicate (thông qua `httpHeaderAuth`).
  - Cấu hình node `Generate Beat Audio` sử dụng `openAi` credentials với model `tts-1-hd`.
  - Kiểm tra các node thực thi lệnh hệ thống như `Run FFmpeg to Merge Media`, `Video Audio Merge Command`, `Generate Final Video` để đảm bảo môi trường n8n hỗ trợ FFmpeg (nếu chạy Docker, hãy chắc chắn image có cài đặt sẵn FFmpeg).
  - Quản lý thư mục tạm trên `Google Drive` để lưu các beat video trước khi ghép nối thành phẩm.

- **Bước 3: Publish Video (Đăng tải YouTube)**
  - Cấu hình node `YouTube Video Upload` và `Prepare YouTube Upload` sử dụng `youTubeOAuth2Api`.
  - Đảm bảo trạng thái (`status`) trong Google Sheets đổi thành `ready` trước khi gõ lệnh `publish` qua chat. Video sẽ được tải lên ở chế độ `Private` để các sếp kiểm duyệt trước khi chuyển sang `Public`.

- **Bước 4: Remove Temporary files (Dọn dẹp hệ thống)**
  - Sau khi video lên sóng, gõ lệnh `clean drive` để workflow tự động tìm và xóa các file beat tạm thời trên Google Drive thông qua node `Search Temporary Files to Delete` và `Delete Temporary Files`.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test run) từng bước hoặc test qua `When chat message received`.
- Khi mọi thứ trơn tru, hãy bật công tắc **Active** cho workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Thay vì dùng chat trigger mặc định của n8n, các sếp có thể đổi trigger sang Telegram Bot để ra lệnh tạo video (`/idea`, `/create`, `/publish`) ngay trên điện thoại cực kỳ tiện lợi.
- **Tự động chuyển Public:** Sau khi video upload thành công, có thể thêm một bước kiểm tra hoặc tự động đổi trạng thái YouTube sang Public sau một khoảng thời gian nhất định nếu đã tin tưởng chất lượng kịch bản AI.
- **Lưu trữ Log:** Sử dụng thêm Google Sheets log lại thời gian hoàn thành và link video YouTube để dễ dàng theo dõi hiệu suất kênh.

### 📌 Kết luận
Workflow tạo Faceless Shorts kinh dị này là một mô hình tự động hóa tuyệt vời giúp các sếp tối ưu hóa quy trình sản xuất nội dung số. Hãy triển khai ngay trên VPS của mình và bắt đầu tạo ra những video triệu view mà không cần tốn chút công sức dựng hình thủ công nào!