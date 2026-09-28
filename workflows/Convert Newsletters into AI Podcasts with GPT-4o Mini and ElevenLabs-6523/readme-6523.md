---
title: "🎙️ Chuyển Tạp San Thông Tin Sang Podcast AI Tự Động Với GPT-4o Mini & ElevenLabs (N8n)"
description: "Workflow tự động hóa chuyển đổi nội dung tạp san email thành podcast AI sống động với hai giọng nói khác biệt, tiết kiệm thời gian và nâng cao trải nghiệm người dùng. Kết quả: Audio podcast tự động được tạo và gửi về email mỗi khi có tin mới."
slug: "chuyen-tap-san-thong-tin-sang-podcast-ai"
tags: [n8n, automation, content-creation, multimodal-ai, email-automation, elevenlabs, openai]
keywords: [n8n workflow podcast, tự động hóa podcast từ email, GPT-4o Mini, ElevenLabs, tự động hóa nội dung, podcast AI, tự động hóa tạp san]
---

# 🚀 Chuyển Tạp San Email Sang Podcast AI Tự Động – Giải Pháp Tiết Kiệm Thời Gian Cho Các Sếp

## 📉 Nỗi Đau Của Các Sếp
Các sếp thường phải mất nhiều thời gian để đọc và tổng kết nội dung từ các tạp san email hàng ngày. Thông thường, việc này yêu cầu:
- **Đọc và phân tích** từng tin tức, báo cáo, hoặc bài viết dài.
- **Tóm tắt** nội dung phức tạp thành dạng dễ hiểu.
- **Tạo nội dung đa phương tiện** như podcast để chia sẻ với đội ngũ hoặc khách hàng.

Với **Workflow này**, các sếp có thể **tự động hóa toàn bộ quá trình** chỉ với một cú nhấp chuột. Hệ thống sẽ:
✅ **Lấy tin tức mới** từ email (hoặc webhook).
✅ **Tự động chuyển đổi** nội dung thành cuộc đối thoại AI sống động giữa hai nhân vật.
✅ **Synthesize giọng nói** với chất lượng cao bằng ElevenLabs.
✅ **Ghép audio** thành một podcast hoàn chỉnh.
✅ **Gửi podcast về email** (hoặc các kênh khác) một cách tự động.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết Quả Các Sếp Nhận Được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần đọc và tóm tắt thủ công.
- **Nội dung cá nhân hóa**: Podcast được tạo từ nội dung email riêng của bạn.
- **Chất lượng cao**: Giọng nói tự nhiên, âm thanh chuyên nghiệp.
- **Hoạt động liên tục**: Podcast được tạo và gửi tự động mỗi khi có tin mới.
- **Tăng cường trải nghiệm**: Nội dung phức tạp trở nên dễ tiếp cận hơn.
:::

---

### 🔧 Yêu Cầu Cần Thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (để lấy tin tức và gửi podcast).
2. **API Key ElevenLabs** (để synthesize giọng nói).
3. **API Key OpenAI** (để sử dụng GPT-4o Mini).
4. **FFmpeg** (để ghép audio, chỉ cần thiết nếu tự host n8n).
5. **Thư mục lưu trữ** (để lưu tạm các file audio).
:::

---

## 🚀 Cách Import & Lưu Ý Khi "Lên Đồ"

### 1. Import Workflow 📥
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n Editor](https://n8n.io/editor).
2. Nhấp vào **Import** và chọn file JSON hoặc dán JSON vào ô nhập liệu.
3. Nhấp **Import** để hoàn tất.

---

### 2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌

#### **Node 1: Get Newsletter (GmailTrigger)**
- **Cấu hình**:
  - Chọn **Credentials**: `gmailOAuth2`.
  - Thiết lập **filter** để lấy tin tức từ email cụ thể (ví dụ: `from:your_newsletter@domain.com`).
  - Nếu muốn lấy từ webhook, thay thế bằng **Webhook Node** và cấu hình URL nhận dữ liệu.

#### **Node 2: Generate Dialogue Script (OpenAI)**
- **Cấu hình**:
  - Chọn **Credentials**: `openAiApi`.
  - Đảm bảo **model** là `gpt-4o-mini`.
  - **Prompt** đã được tối ưu để tạo cuộc đối thoại tự nhiên giữa hai nhân vật (`men1` và `men2`).
  - **Input**: `{{$('Get Newsletter').first().json.text}}`.

#### **Node 3-6: Split Script & Loop Over Items**
- **Node Split Script (Code)**:
  - Chức năng: Chia nội dung thành các đoạn riêng biệt theo speaker.
  - **Lưu ý**: Không cần chỉnh sửa, chỉ cần đảm bảo input từ node trước là chính xác.
- **Node Loop Over Items (SplitInBatches)**:
  - Chức năng: Lặp qua từng đoạn để synthesize giọng nói.
  - **Lưu ý**: Đảm bảo **batch size** hợp lý (ví dụ: 1 đoạn/lần).

#### **Node 7-8: Prepare FFmpeg List & Merge Audio**
- **Node Generate `concat_list.txt` (Code)**:
  - **Lưu ý**: Chỉ cần chạy trên môi trường **self-hosted** với FFmpeg cài đặt.
  - **Thư mục mặc định**: `/newsletter2podcast/tmp/`.
- **Node Join audio chucks (ExecuteCommand)**:
  - **Lệnh FFmpeg**:
    ```bash
    ffmpeg -y -f concat -safe 0 -i /newsletter2podcast/tmp/concat_list.txt -c copy /newsletter2podcast/tmp/final_merged.mp3
    ```
  - **Lưu ý**:
    - FFmpeg phải được cài đặt và có quyền truy cập.
    - Xóa các file tạm sau khi ghép xong.

#### **Node 9: Send Audio (Gmail)**
- **Cấu hình**:
  - **Credentials**: `gmailOAuth2`.
  - **Người nhận**: Địa chỉ email của bạn hoặc động (ví dụ: `{{$json.email}}`).
  - **Đính kèm**: File `final_merged.mp3` từ thư mục `/newsletter2podcast/tmp/`.

---

### 3. Kích Hoạt ⚡️
1. **Test Run**:
   - Nhấp **Run Workflow** và kiểm tra kết quả.
   - Đảm bảo podcast được tạo và gửi thành công.
2. **Bật Active**:
   - Sau khi test thành công, nhấp **Active** để workflow chạy tự động.

---

## ✍️ Mẹo & Gợi Ý Nâng Cao
1. **Thêm Slack/Telegram Notification**:
   - Sau khi podcast được tạo, gửi thông báo đến Slack/Telegram để các sếp biết tin tức mới đã được chuyển đổi.
   - **Cách làm**: Thêm **Slack/Telegram Node** sau node `Send Audio`.

2. **Lưu Log & Báo Cáo**:
   - Thêm **Google Sheets Node** để lưu lịch sử podcast đã tạo.
   - **Cách làm**: Sau node `Send Audio`, thêm node `Google Sheets` để ghi dữ liệu.

3. **Tùy Chỉnh Giọng Nói**:
   - Thay đổi **voice ID** trong ElevenLabs để phù hợp với phong cách của podcast.
   - **Cách làm**: Trong node `HTTP Request`, thay đổi `YOUR_VOICE_ID` bằng ID giọng mới.

4. **Tự Động Cập Nhật Podcast**:
   - Nếu muốn podcast được cập nhật định kỳ (ví dụ: hàng tuần), thêm **Schedule Node** để chạy workflow theo lịch.

---

## 📌 Kết Luận
Workflow này là **giải pháp hoàn hảo** để các sếp tự động hóa việc chuyển đổi tạp san email thành podcast AI sống động. Không cần viết code, chỉ cần cấu hình và chạy. Kết quả là:
✔ **Tiết kiệm thời gian** đọc và tổng kết.
✔ **Nội dung đa phương tiện** dễ tiếp cận hơn.
✔ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**Hãy áp dụng ngay workflow này và nâng cao hiệu suất công việc của mình!** 🚀

---
**Lưu ý**: Nếu gặp vấn đề, liên hệ với tác giả [Luis Acosta](mailto:Luis.acosta@news2podcast.com) để hỗ trợ.