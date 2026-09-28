---
title: "🚀 Tự động tạo video UGC AI từ tin nhắn thoại Telegram với OpenAI & HeyGen"
description: "Chuyển đổi tin nhắn thoại Telegram thành video AI chất lượng cao chỉ trong vài giây, không cần viết code."
slug: "tu-dong-tao-video-ugc-ai-tu-telegram-voice-notes"
tags: [n8n, automation, no-code, AI, video, telegram]
keywords: [n8n workflow, tự động hóa, AI video, Telegram voice notes, HeyGen, OpenAI transcription]
---

# 🚀 Tự động tạo video UGC AI từ tin nhắn thoại Telegram với OpenAI & HeyGen

**Bạn có bao giờ nhận được những tin nhắn thoại trên Telegram, muốn biến chúng thành video quảng cáo, nội dung mạng xã hội hay bản tin nội bộ nhưng lại phải mất hàng giờ để chỉnh sửa, lồng tiếng, dựng hình?**  
Việc làm thủ công không chỉ tốn thời gian mà còn dễ gây lỗi, không đồng nhất và khó mở rộng.  

**Giải pháp:** Workflow n8n này sẽ tự động:

1. Nhận tin nhắn thoại từ Telegram.  
2. Tải file âm thanh về, chuyển đổi thành văn bản bằng OpenAI Whisper.  
3. Gửi nội dung văn bản tới HeyGen để tạo video AI (UGC) chỉ trong vài giây.  
4. Trả lại link video ngay trên Telegram.

Kết quả: **tự động hoá 100 % quy trình tạo video UGC, không cần viết code, giảm chi phí sản xuất nội dung và tăng tốc độ phản hồi**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Từ vài phút thủ công xuống chỉ vài giây tự động.  
- **Độ chính xác cao:** Transcription của OpenAI Whisper giảm lỗi hiểu sai.  
- **Nội dung đồng nhất:** Video được tạo theo mẫu HeyGen chuẩn, thương hiệu luôn nhất quán.  
- **Hoạt động liên tục 24/7:** Không cần nhân lực giám sát, workflow tự chạy khi có tin nhắn mới.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Telegram Bot** (API Token) – để nhận và gửi tin nhắn.  
- **OpenAI API Key** – dùng cho node `openAi` (Whisper).  
- **HeyGen API Key** – để gọi API tạo video.  
- **n8n** (cài đặt self‑hosted hoặc cloud) với ít nhất **10 GB RAM** để xử lý audio.  
- **Địa chỉ webhook** (nếu chạy trên server riêng) để Telegram có thể gọi lại.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow (được cung cấp ở phần cuối của tài liệu này) hoặc sao chép toàn bộ JSON.  
2. Vào n8n → **Workflows** → **Import** → Dán JSON → **Import**.  
3. Đặt tên cho workflow (mặc định: *Create AI UGC Videos from Telegram Voice Notes*).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là danh sách các node quan trọng và cách cấu hình chúng:

| Node | Loại | Hướng dẫn cấu hình chi tiết |
|------|------|-----------------------------|
| **Message Trigger** | `telegramTrigger` | - Chọn **Credentials**: Telegram Bot API Token.<br>- **Event**: `Message`. <br>- **Chat Type**: `Private` hoặc `Group` tùy nhu cầu.<br>- Lưu ý bật **Webhook URL** trong Telegram Bot Settings để nhận tin nhắn. |
| **Downloading File** | `telegram` | - **Credentials**: Same Telegram Bot.<br>- **Operation**: `Get File`. <br>- **File ID**: `{{$json["message"]["voice"]["file_id"]}}` (đối với voice note). |
| **Transcribing voice memo** | `openAi` (LangChain) | - **Credentials**: OpenAI API Key.<br>- **Model**: `whisper-1` (hoặc `gpt-4o-mini` nếu muốn dùng text‑to‑text).<br>- **Input**: `{{$binary["data"].data}}` (binary data từ node trước). |
| **Setting ID Fields** | `set` | - Thêm các trường: `videoId`, `statusUrl` (được lấy từ phản hồi HeyGen). <br>- Dùng **Expression**: `{{$json["id"]}}`… để lưu lại. |
| **Generating Video** | `httpRequest` | - **Method**: `POST`.<br>- **URL**: `https://api.heygen.ai/v1/videos` (hoặc endpoint hiện tại).<br>- **Headers**: `Authorization: Bearer <HEYGEN_API_KEY>`.<br>- **Body (JSON)**: <br>```json<br>{<br>  "script": "{{$node["Transcribing voice memo"].json["text"]}}",<br>  "style": "ugc",<br>  "voice": "en_us_1"<br>}<br>``` |
| **Video Status Update** | `httpRequest` | - **Method**: `GET`.<br>- **URL**: `{{$node["Generating Video"].json["statusUrl"]}}`.<br>- **Loop**: Kết hợp với node `wait` để kiểm tra trạng thái mỗi 10 giây. |
| **10s Buffer** | `wait` | - **Time**: `10` seconds. Dùng để chờ HeyGen xử lý video. |
| **Setting Output** | `set` | - Tạo trường `videoUrl` từ phản hồi cuối cùng: `{{$json["result"]["video_url"]}}`. |
| **Sending Video URL** | `telegram` | - **Credentials**: Telegram Bot.<br>- **Operation**: `Send Message`.<br>- **Chat ID**: `{{$json["message"]["chat"]["id"]}}` (hoặc ID cố định).<br>- **Message**: `Video của bạn đã sẵn sàng! 👉 {{$node["Setting Output"].json["videoUrl"]}}`. |
| **is Completed** | `if` | - Kiểm tra `{{$json["status"]}} === "completed"` để quyết định có gửi video hay không. |

> **Lưu ý:** Các trường JSON/Binary cần dùng cú pháp `{{$...}}` để truyền dữ liệu giữa các node. Đảm bảo bật **Binary Data** trong node `Downloading File` để truyền file âm thanh sang node `openAi`.

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi một voice note tới bot, quan sát log trong n8n → **Execution**.  
2. Kiểm tra: Bạn sẽ nhận lại tin nhắn chứa link video HeyGen.  
3. Khi mọi thứ ổn, bật **Active** trên workflow để chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Slack/Telegram nhóm:** Thêm node `slack` để gửi thông báo video tới kênh marketing.  
- **Lưu log vào Google Sheets:** Dùng node `googleSheets` để ghi lại `user_id`, `voice_text`, `video_url`, `timestamp`.  
- **Tự động chia sẻ lên TikTok/YouTube:** Sử dụng API của các nền tảng để đăng video ngay sau khi tạo.  
- **Thêm bước kiểm duyệt nội dung:** Dùng OpenAI `moderation` endpoint trước khi gửi tới HeyGen để tránh nội dung không phù hợp.  

### 📌 Kết luận
Với workflow này, các sếp có thể **biến mọi tin nhắn thoại trên Telegram thành video AI chuyên nghiệp trong tích tắc**, giảm chi phí sản xuất nội dung, tăng tốc độ phản hồi và duy trì tính nhất quán thương hiệu. Hãy triển khai ngay, thử nghiệm và mở rộng theo nhu cầu thực tế của doanh nghiệp! 🚀