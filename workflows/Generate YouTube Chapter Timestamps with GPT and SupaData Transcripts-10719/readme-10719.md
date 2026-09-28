---
title: "🚀 Tự động tạo YouTube Chapter Timestamps bằng AI GPT-4o và SupaData trong n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động lấy transcript video YouTube mới qua RSS, dùng AI GPT-4o tạo mốc thời gian (chapters) và cập nhật trực tiếp lên video."
slug: "tu-dong-tao-youtube-chapter-timestamps-voi-gpt-va-supadata"
tags: [n8n, automation, youtube, openai, airtable, ai-summarization]
keywords: [n8n workflow, youtube chapters, supadata, openai gpt-4o, tu dong hoa youtube, airtable deduplication]
---

# 🚀 Tự động tạo YouTube Chapter Timestamps bằng AI GPT-4o và SupaData

Các sếp làm nội dung trên YouTube chắc chắn hiểu cảm giác tốn thời gian thế nào khi phải xem lại video, ghi chép lại nội dung từng phân đoạn để làm mốc thời gian (Chapter Timestamps) thủ công. Việc này không chỉ mất hàng giờ đồng hồ mà còn làm chậm tiến độ xuất bản video.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa 100%: Lắng nghe kênh YouTube, lấy transcript qua SupaData API, nhờ GPT-4o phân tích và tự động gắn mốc thời gian chuyên nghiệp vào mô tả video!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Không còn phải thủ công tóm tắt hay tua đi tua lại video để tìm mốc thời gian.
- **Tối ưu SEO YouTube:** Video có cấu trúc Chapter rõ ràng giúp tăng trải nghiệm người xem và được YouTube ưu tiên đề xuất.
- **Vận hành tự động:** Tự động bắt sự kiện video mới qua RSS, lọc trùng lặp thông minh qua Airtable.
- **Cá nhân hóa AI:** GPT-4o phân tích sâu nội dung để chia chương cực kỳ logic và chính xác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance** (Self-hosted hoặc Cloud).
- **YouTube RSS Feed URL** của kênh bạn.
- **SupaData API Key** (để lấy transcript video).
- **OpenAI API Key** (sử dụng mô hình GPT-4o).
- **Airtable Account & Token** (để lưu lịch sử, tránh xử lý trùng lặp video đã chạy).
- **YouTube OAuth2 Credentials** (để cập nhật mô tả video).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, vào giao diện n8n, chọn **Add workflow** -> Nhấn `Ctrl + V` (hoặc `Cmd + V`) để dán trực tiếp vào Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Get New YouTube Video (`rssFeedReadTrigger`):** Điền đường dẫn RSS của kênh YouTube theo định dạng:
  `https://www.youtube.com/feeds/videos.xml?channel_id=YOUR_CHANNEL_ID`
- **Check Airtable & Save to Airtable (`airtable`):** 
  - Kết nối `airtableTokenApi`.
  - Sử dụng Airtable Template mẫu để tracking video: [Duplicate Airtable Base](https://airtable.com/appUJQfAXniGZzwL8/shraiQrFHLF3xxhX7).
  - Node này giúp kiểm tra xem video đã được tạo chapter chưa, tránh việc chạy lặp lại tốn tài nguyên.
- **Fetch Transcript (`httpRequest`):** 
  - Cấu hình Header Auth cho SupaData API.
  - Endpoint gọi API: `https://api.supadata.ai/v1/transcript?url=https://youtu.be/{{ $json.videoId }}`.
- **OpenAI Chat Model & AI: Generate Chapters (`agent` & `lmChatOpenAi`):**
  - Chọn model `gpt-4o` để đảm bảo chất lượng phân tích ngữ cảnh tốt nhất.
  - Truyền dữ liệu transcript từ bước `Prepare Transcript + Duration` vào để AI tiến hành phân chia mốc thời gian.
- **Fetch Current Description & Update Description (`youTube`):**
  - Kết nối `youTubeOAuth2Api`.
  - Node `Fetch Current Description` lấy mô tả gốc của video, sau đó AI-generated chapters sẽ được nối (append) vào cuối mô tả cũ và cập nhật ngược lại YouTube qua node `Update Description`.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với một video mẫu để kiểm tra toàn bộ luồng chạy (từ đọc RSS -> Check Airtable -> Lấy transcript -> AI xử lý -> Cập nhật YouTube).
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Gợi ý & Mẹo nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm một node Telegram ngay sau bước cập nhật thành công để nhận thông báo về điện thoại xem video nào vừa được tự động thêm Chapter.
- **Mở rộng lưu trữ:** Thay vì dùng Airtable, các sếp có thể thay thế bằng Google Sheets hoặc PostgreSQL để quản lý lịch sử video đã xử lý.
- **Tùy biến Prompt AI:** Trong node Agent, có thể điều chỉnh prompt để AI tạo phong cách viết tiêu đề chapter ngắn gọn, hài hước hoặc trang trọng tùy thuộc vào chủ đề kênh của các sếp.

### 📌 Kết luận
Việc tối ưu hóa quy trình sản xuất nội dung chưa bao giờ dễ dàng đến thế với n8n và AI. Hãy thiết lập ngay workflow này để tối ưu hóa thời gian và bứt phá kênh YouTube của các sếp ngay hôm nay!