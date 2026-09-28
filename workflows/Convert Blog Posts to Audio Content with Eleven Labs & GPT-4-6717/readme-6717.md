---
title: "🎧 Tự Động Hóa Blog Thành Podcast: Kết Hợp GPT-4 & ElevenLabs"
description: "Biến bài viết blog thành file audio chuyên nghiệp chỉ trong vài phút. Workflow n8n tự động trích xuất nội dung, tạo giọng đọc AI và phân phối qua Email/Slack."
slug: "tu-dong-hoa-blog-thanh-podcast-gpt4-elevenlabs"
tags: [n8n, automation, ai, elevenlabs, content-marketing, podcast]
keywords: [n8n workflow, tự động hóa podcast, elevenlabs n8n, gpt-4 audio, content repurposing]
---

# 🎧 Tự Động Hóa Blog Thành Podcast: Kết Hợp GPT-4 & ElevenLabs

Trong kỷ nguyên nội dung đa phương tiện, người dùng không chỉ đọc nữa mà còn "nghe". Tuy nhiên, việc chuyển đổi hàng trăm bài viết blog thành các tập podcast chất lượng cao là một gánh nặng khổng lồ về thời gian và chi phí nhân sự. Quay phim, thu âm, chỉnh sửa âm thanh... tất cả đều tốn kém và chậm chạp.

Workflow **"Convert Blog Posts to Audio Content with Eleven Labs & GPT-4"** ra đời để giải quyết triệt để vấn đề này. Đây là giải pháp tự động hóa 100% không cần code, giúp các sếp biến nội dung văn bản có sẵn thành tài nguyên audio chuyên nghiệp, sẵn sàng phân phối cho khán giả hoặc đội ngũ nội bộ.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các tác vụ AI nặng, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian sản xuất:** Tự động hóa toàn bộ quy trình từ khi bài blog mới được đăng tải cho đến khi file audio hoàn chỉnh.
- **Chất lượng giọng đọc tự nhiên:** Sử dụng công nghệ TTS (Text-to-Speech) của ElevenLabs, giọng đọc AI cực kỳ chân thực, có cảm xúc.
- **Tối ưu SEO & Metadata:** GPT-4 tự động sinh ra tiêu đề, mô tả và thẻ tag phù hợp cho file audio, giúp dễ dàng quản lý và tìm kiếm.
- **Phân phối đa kênh:** Tự động lưu trữ trên Google Drive, ghi log vào Google Sheets và thông báo qua Email/Slack cho đội ngũ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị các tài khoản và credentials sau:
1. **Tài khoản n8n:** Có quyền tạo workflow mới.
2. **RSS Feed URL:** Địa chỉ RSS của blog hoặc website nguồn nội dung.
3. **ElevenLabs API Key:** Đăng ký tại [elevenlabs.io](https://elevenlabs.io) và tạo API Key.
4. **OpenAI API Key:** Dùng cho GPT-4 để sinh metadata (đăng ký tại [platform.openai.com](https://platform.openai.com)).
5. **Google Credentials:**
   - **Google Drive:** Để lưu trữ file audio.
   - **Google Sheets:** Để ghi log lịch sử sản xuất audio.
   - **Gmail:** Để gửi thông báo email.
6. **Slack Webhook URL:** (Tùy chọn) Nếu muốn nhận thông báo nội bộ qua Slack.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể thực hiện theo 2 cách:
- **Cách 1 (Khuyến nghị):** Tải file JSON của workflow về máy, vào n8n Editor, chọn **Import from File**.
- **Cách 2:** Copy toàn bộ mã JSON của workflow và dán vào n8n Editor (chọn **Import from URL** hoặc dán trực tiếp vào khung nhập liệu nếu phiên bản n8n hỗ trợ).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình lại các node quan trọng sau:

- **Node: `RSS Feed Trigger`**
  - Mở node này và điền **URL RSS** của blog/website mà các sếp muốn chuyển đổi thành audio.
  - Thiết lập tần suất kiểm tra (ví dụ: mỗi 15 phút hoặc 1 giờ) để đảm bảo không bỏ sót bài viết mới.

- **Node: `Convert Text to Speech` (ElevenLabs)**
  - Chọn **Credentials** của ElevenLabs đã tạo ở bước chuẩn bị.
  - Chọn **Voice ID** mong muốn (các sếp có thể test nhiều giọng khác nhau trên trang web ElevenLabs trước khi chọn ID phù hợp nhất với thương hiệu).
  - Kiểm tra tham số `model_id` (khuyến nghị dùng `eleven_multilingual_v2` hoặc `eleven_turbo_v2` để có chất lượng tốt và tốc độ nhanh).

- **Node: `Generate Metadata` (OpenAI)**
  - Chọn **Credentials** của OpenAI.
  - Kiểm tra **Prompt** trong node: Đảm bảo prompt yêu cầu GPT-4 tạo ra tiêu đề podcast, mô tả ngắn và các thẻ tag dựa trên nội dung bài viết gốc. Các sếp có thể tùy chỉnh prompt để phù hợp với giọng văn thương hiệu của mình.

- **Node: `Upload Audio File` (Google Drive)**
  - Chọn **Credentials** của Google Drive.
  - Điền **Folder ID** của thư mục nơi các sếp muốn lưu trữ các file audio. (Mẹo: Tạo một thư mục riêng trên Drive và copy ID từ URL).

- **Node: `Log Audio Production` (Google Sheets)**
  - Chọn **Credentials** của Google Sheets.
  - Chọn **Spreadsheet ID** và **Sheet Name** (tên tab) nơi các sếp muốn ghi lại lịch sử.
  - Đảm bảo các cột trong Sheet khớp với dữ liệu output của node (ví dụ: Tiêu đề, Link Audio, Ngày tạo, v.v.).

- **Node: `Is for Email Distribution?` (If Node)**
  - Đây là node điều kiện. Các sếp có thể chỉnh sửa logic để quyết định khi nào thì gửi email (ví dụ: chỉ gửi khi bài viết có tag "Featured" hoặc luôn gửi).

- **Node: `Send Audio Notification via Email` (Gmail)**
  - Chọn **Credentials** của Gmail.
  - Điền **To Email Address** (địa chỉ nhận email).
  - Tùy chỉnh **Subject** và **Message** nếu muốn.

- **Node: `Notify Internal Team` (Slack)**
  - Nếu không dùng Slack, các sếp có thể xóa node này hoặc để nó ở trạng thái tắt.
  - Nếu dùng, điền **Webhook URL** của kênh Slack cần thông báo.

#### 3. Kích hoạt ⚡️
1. **Test Run:** Nhấn nút **Execute Workflow** (hoặc chọn một item mẫu) để chạy thử. Kiểm tra xem file audio có được tạo ra, lưu lên Drive và ghi vào Sheet không.
2. **Bật Active:** Sau khi kiểm tra kỹ lưỡng, bật công tắc **Active** ở góc trên bên phải để workflow chạy tự động liên tục.

### ✍️ Mẹo & gợi ý nâng cao
- **Tạo nhiều giọng đọc:** Thay vì dùng 1 giọng duy nhất, các sếp có thể tạo logic để chọn giọng đọc khác nhau dựa trên chủ đề bài viết (ví dụ: giọng trầm cho tin tức, giọng vui vẻ cho giải trí).
- **Thêm hình ảnh Thumbnail:** Kết hợp thêm node để tạo thumbnail tự động từ tiêu đề bài viết và upload cùng file audio lên Drive hoặc YouTube.
- **Tích hợp lên nền tảng Podcast:** Thay vì chỉ lưu trên Drive, các sếp có thể thêm node để upload trực tiếp lên Spotify for Creators, Apple Podcasts hoặc RSS feed podcast riêng.
- **Phân tích hiệu suất:** Kết nối Google Sheets với Looker Studio hoặc Power BI để theo dõi số lượng audio đã tạo, thời gian xử lý và phản hồi từ người dùng.

### 📌 Kết luận
Việc chuyển đổi nội dung blog thành podcast không còn là rào cản kỹ thuật hay tài chính với các sếp nữa. Với workflow n8n kết hợp sức mạnh của GPT-4 và ElevenLabs, các sếp có thể xây dựng một máy in nội dung audio hoạt động 24/7, giúp mở rộng tầm ảnh hưởng thương hiệu và tiếp cận lượng khán giả mới yêu thích hình thức nghe hơn là đọc. Hãy áp dụng ngay để tối ưu hóa quy trình content marketing của mình!