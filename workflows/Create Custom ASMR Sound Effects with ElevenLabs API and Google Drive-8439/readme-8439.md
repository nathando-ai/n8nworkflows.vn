---
title: "🚀 Tạo Hiệu Ứng Âm Thanh ASMR Tùy Chỉnh với ElevenLabs & Google Drive"
description: "Tự động tạo file MP3 ASMR từ mô tả văn bản, lưu lên Google Drive và nhận link nghe ngay, không cần viết code."
slug: "tao-amr-sound-effects-elevenlabs-google-drive"
tags: [n8n, automation, no-code, AI, ElevenLabs, GoogleDrive]
keywords: [n8n workflow, tự động hóa, ElevenLabs, ASMR, Google Drive, AI voice]
---

# 🚀 Tạo Hiệu Ứng Âm Thanh ASMR Tùy Chỉnh với ElevenLabs & Google Drive

Bạn có bao giờ muốn tạo một đoạn âm thanh ASMR độc đáo chỉ bằng một câu mô tả, nhưng lại phải mất hàng giờ quay video, chỉnh âm, tải lên và chia sẻ?  
Việc làm thủ công này không chỉ tốn thời gian mà còn dễ gây lỗi, khó đồng bộ giữa các công cụ và không thể mở rộng cho nhiều dự án.  

**Workflow này** sẽ giải quyết mọi rắc rối: người dùng nhập mô tả vào một form web, AI ElevenLabs ngay lập tức sinh ra file MP3, tự động lưu vào Google Drive và trả về link nghe ngay trên giao diện. Hoàn toàn **không cần viết một dòng code nào** – chỉ cần cấu hình vài node và bật chạy.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Từ mô tả tới file MP3 chỉ trong vài giây.  
- **Độ chính xác cao**: AI ElevenLabs tạo âm thanh chuẩn chất lượng studio.  
- **Tự động lưu & chia sẻ**: File được lưu vào Google Drive và link được trả về ngay.  
- **Hoạt động liên tục**: Không cần can thiệp thủ công, workflow chạy 24/7.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản ElevenLabs** – để lấy **API Key** (truy cập https://try.elevenlabs.io/sound-fx).  
- **Tài khoản Google** – để cấp quyền **Google Drive OAuth2** cho node `Upload mp3`.  
- **n8n** – cài đặt trên môi trường tự host hoặc cloud (đề xuất VPS).  
- **Kết nối internet** – để gọi API ElevenLabs và tải lên Drive.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Vào **n8n → Workflows → Import**.  
2. Chọn **Upload JSON** và tải file JSON của workflow (hoặc copy toàn bộ JSON vào ô **Paste JSON**).  
3. Nhấn **Import** → **Save**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌  
Dưới đây là danh sách các node quan trọng và cách cấu hình:

| Node | Loại | Hướng dẫn cấu hình |
|------|------|-------------------|
| **AI ASMR Generator** | `formTrigger` | - Đặt **Name** tùy ý.<br>- URL sẽ được tạo tự động, sao chép để chia sẻ với người dùng. |
| **display mp3** | `form` | - `Operation` → **completion** (đã được set sẵn).<br>- Trong **Fields**, để trống; node này chỉ dùng để hiển thị link trả về từ node `prepare reponse`. |
| **prepare reponse** | `html` | - **HTML**: `<a href="{{ $json["fileUrl"] }}" target="_blank">Nghe MP3 của bạn</a>`.<br>- Đảm bảo **Output** là **JSON** để node `display mp3` nhận được `fileUrl`. |
| **Upload mp3** | `googleDrive` | - **Credentials**: chọn **Google Drive OAuth2 API** đã kết nối.<br>- **Operation** → **Upload**.<br>- **File Name**: `{{$json["fileName"]}}.mp3`.<br>- **Folder ID**: ID thư mục Google Drive nơi lưu file (có thể để trống để lưu vào root). |
| **API Key** | `set` | - Thêm **Field**: `apiKey` → dán **API Key** ElevenLabs của bạn.<br>- Đánh dấu **Keep Only Set** để chỉ truyền `apiKey` tới node tiếp theo. |
| **elevenlabs_api** | `httpRequest` | - **Method**: `POST`.<br>- **URL**: `https://api.elevenlabs.io/v1/sound-generation` (hoặc endpoint chính xác từ ElevenLabs).<br>- **Authentication**: **Header** → `xi-api-key: {{$json["apiKey"]}}`.<br>- **Body** (JSON): `{ "text": "{{$json[\"description\"]}}", "voice_settings": { "stability": 0.75, "similarity_boost": 0.75 } }`.<br>- **Response Format**: **File** (MP3). |
| **(Optional) Sticky Note** | `stickyNote` | Dùng để ghi chú nội bộ, không cần cấu hình. |

> **Lưu ý:** Các trường `{{$json["..."]}}` là biểu thức n8n, đảm bảo tên biến khớp với output của node trước. Kiểm tra **Execution Log** nếu có lỗi.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** lần đầu với dữ liệu mẫu (ví dụ: mô tả “tiếng mưa nhẹ rơi”).  
2. Kiểm tra **Output** của node `Upload mp3` → nhận được `fileUrl`.  
3. Nếu mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc phải).  
4. Chia sẻ URL của node `AI ASMR Generator` (form trigger) cho người dùng cuối.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` để tự động gửi link MP3 vào kênh nhóm.  
- **Lưu log chi tiết**: Dùng node `Write Binary File` hoặc `Google Sheets` để ghi lại lịch sử tạo âm thanh (ngày, mô tả, link).  
- **Tự động xóa file cũ**: Thêm node `Google Drive` → **Delete** dựa trên thời gian tạo > 30 ngày để tránh đầy dung lượng.  
- **Tùy chỉnh giọng**: ElevenLabs hỗ trợ nhiều voice ID, bạn có thể thêm một `Set` node để chọn voice dựa trên dropdown trong form.

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động tạo và chia sẻ âm thanh ASMR** chỉ trong vài giây, giảm thiểu công việc lặp lại và nâng cao trải nghiệm khách hàng. Hãy triển khai ngay, bật chạy và bắt đầu thu thập phản hồi từ người dùng – mọi thứ đã sẵn sàng, chỉ cần **cấu hình API Key & Google Drive**! 🚀