---
title: "🎙️ Tạo Podcast Wikipedia Tự Động qua Telegram với AI - Workflow n8n"
description: "Tự động hóa việc tạo podcast từ Wikipedia chỉ với tin nhắn Telegram. Giải pháp tiết kiệm thời gian cho các nhà sáng tạo nội dung."
slug: "tao-podcast-wikipedia-tu-dong-qua-telegram-voi-ai"
tags: [n8n, automation, no-code, telegram, ai, podcast, wikipedia]
keywords: [n8n workflow, tự động hóa, podcast, wikipedia, telegram, ai, text-to-speech]
---

# 🎙️ Tạo Podcast Wikipedia Tự Động qua Telegram với AI - Workflow n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các nhà sáng tạo nội dung khi phải tìm kiếm, biên tập và chuyển đổi nội dung Wikipedia thành podcast thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian biên tập podcast từ Wikipedia
- Tự động chuyển đổi nội dung Wikipedia thành podcast chất lượng cao
- Hỗ trợ cả tin nhắn văn bản và giọng nói
- Tạo nội dung chuyên nghiệp với giọng nói tự nhiên
- Tăng khả năng tiếp cận nội dung cho người dùng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot API key
- API key từ Anthropic (Claude 4 Sonnet)
- API key từ OpenAI (cho chức năng chuyển giọng nói thành văn bản)
- API key từ ElevenLabs (cho chức năng chuyển văn bản thành giọng nói)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link: https://n8n.io/workflows/4496
3. Hoặc tải file JSON về và import từ local

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Telegram Trigger** (Node đầu tiên):
   - Cấu hình credentials cho Telegram API
   - Đảm bảo bot của bạn có quyền nhận tin nhắn từ người dùng

2. **Anthropic Chat Model**:
   - Chọn model "claude-sonnet-4-20250514"
   - Cấu hình credentials cho Anthropic API

3. **Get Voice Message**:
   - Cấu hình credentials cho Telegram API
   - Đảm bảo bot có quyền truy cập file âm thanh

4. **Transcribe Voice Message**:
   - Cấu hình credentials cho OpenAI API
   - Chọn operation "transcribe" và resource "audio"

5. **ElevenLabs Text to Speech**:
   - Cấu hình credentials cho ElevenLabs API
   - Chọn resource "speech"

6. **Send Voice Response**:
   - Cấu hình credentials cho Telegram API
   - Chọn operation "sendAudio"

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Bật Active workflow để bắt đầu nhận tin nhắn từ người dùng

### ✍️ Mẹo & gợi ý nâng cao
- Thêm chức năng lưu trữ podcast đã tạo vào Google Drive hoặc Dropbox
- Tích hợp với Slack hoặc Discord để chia sẻ podcast với nhóm
- Thêm chức năng gửi báo cáo hàng tuần về số lượng podcast đã tạo
- Tùy chỉnh giọng nói và tốc độ đọc trong node ElevenLabs Text to Speech
- Thêm chức năng lưu trữ lịch sử tìm kiếm Wikipedia để phân tích xu hướng nội dung

### 📌 Kết luận
Workflow này mang lại giải pháp toàn diện cho việc tự động hóa việc tạo podcast từ Wikipedia chỉ với tin nhắn Telegram. Với khả năng xử lý cả văn bản và giọng nói, cùng với giọng nói tự nhiên từ ElevenLabs, workflow này giúp tiết kiệm thời gian đáng kể cho các nhà sáng tạo nội dung. Hãy thử ngay và biến Wikipedia thành nguồn nội dung podcast chất lượng cao!