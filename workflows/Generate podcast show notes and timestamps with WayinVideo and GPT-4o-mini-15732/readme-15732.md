---
title: "🚀 Tự động tạo Show Notes và Timestamp Podcast chuẩn SEO với WayinVideo và GPT-4o-mini qua n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa toàn bộ quy trình: nhận diện giọng nói từ audio podcast, phân tích nội dung bằng AI và lưu trữ kết quả lên Google Sheets."
slug: "tu-dong-tao-podcast-show-notes-wayinvideo-gpt-4o-mini-n8n"
tags: [n8n, automation, ai-agent, openai, google-sheets, podcast]
keywords: [n8n workflow, tạo show notes podcast, wayinvideo api, gpt-4o-mini, tự động hóa content]
---

# 🚀 Tự động tạo Show Notes và Timestamp Podcast chuẩn SEO với WayinVideo & GPT-4o-mini

Các sếp làm podcast có thấy cảnh tốn từ 30 đến 60 phút chỉ để nghe lại bản ghi, tóm tắt ý chính, viết mô tả chuẩn SEO, chèn timestamp và soạn lời kêu gọi hành động (CTA) cho mỗi tập phát sóng không? Công việc thủ công này cực kỳ ngốn thời gian và làm giảm năng lượng sáng tạo.

Giải pháp đây rồi! Workflow n8n này sẽ tự động hóa 100% quy trình: Nhận file ghi âm qua Form 👉 Chuyển đổi giọng nói thành văn bản (Transcription) qua **WayinVideo** 👉 Sử dụng **AI Agent (GPT-4o-mini)** để phân tích, viết nội dung chi tiết 👉 Lưu trữ gọn gàng lên **Google Sheets** với đầy đủ 19 cột chuyên nghiệp, sẵn sàng đưa lên Spotify hay Apple Podcasts.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Bỏ hoàn toàn khâu nghe lại audio và viết ghi chú thủ công.
- **Nội dung chuẩn SEO & Chuyên nghiệp:** AI tự động chia thành 8 phần mạch lạc (Tiêu đề, Mô tả SEO, Key takeaways, Timestamp highlights, Bio khách mời, CTA...).
- **Linh hoạt đa dạng format:** Tự động nhận diện đây là tập phỏng vấn hay độc thoại (solo episode) để điều chỉnh văn phong phù hợp.
- **Lưu trữ tự động:** Mọi thứ được đồng bộ thẳng vào Google Sheets dưới dạng bản nháp (Draft), sẵn sàng publish bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **WayinVideo API Key:** Tài khoản và API key từ dịch vụ WayinVideo Transcription.
- **OpenAI API Credential:** Kết nối tài khoản OpenAI (sử dụng model `gpt-4o-mini`).
- **Google Sheets account:** Tài khoản Google có quyền tạo và chỉnh sửa file Sheets.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy đoạn JSON của workflow hoặc tải file JSON về, sau đó mở n8n Editor, chọn **Import from File** hoặc dán trực tiếp vào giao diện làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:
- **Node 2 & 4 (WayinVideo — Submit/Get Transcript):** Thay thế đoạn `YOUR_WAYINVIDEO_API_KEY` bằng API key thực tế của các sếp trong phần Header/Auth.
- **Node 9 (OpenAI — GPT-4o-mini Model):** Chọn kết nối OpenAI Credentials đã tạo sẵn trên n8n của các sếp.
- **Node 11 (Google Sheets — Save Show Notes Library):** 
  - Kết nối tài khoản Google Sheets OAuth2.
  - Thay `YOUR_GOOGLE_SHEET_ID` bằng ID của file Google Sheet trên Drive của sếp.
  - Tạo sẵn một Sheet tab tên là **Show Notes Library** với đúng 19 cột tiêu đề sau:
    * `Episode Number`, `Episode Title`, `Podcast Name`, `Host`, `Guest`, `Topic`, `Duration`, `Recording URL`, `SEO Description`, `Key Takeaways`, `Resources Mentioned`, `Timestamped Highlights`, `Guest Bio`, `CTA Block`, `Full Show Notes`, `Word Count`, `CTA Link`, `Generated On`, `Status`.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng cách điền thông tin vào Form đầu vào để kiểm tra toàn bộ luồng dữ liệu.
- Sau khi test thành công, bật nút **Active** góc trên cùng bên phải để hệ thống tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay về máy khi AI đã generate xong show notes cho tập mới.
- **Tự động đăng bài:** Kết nối thêm các node như WordPress hoặc Webflow để tự động tạo bài viết trên website podcast của sếp từ dữ liệu trong Google Sheets.
- **Email thông báo khách mời:** Gửi email cảm ơn kèm theo phần Bio và Show Notes nháp cho khách mời xem trước trước khi publish chính thức.

### 📌 Kết luận
Với workflow tự động hóa này, việc sản xuất nội dung podcast từ audio thô đến show notes chuyên nghiệp chưa bao giờ dễ dàng đến thế. Hãy "lên đồ" ngay hôm nay để tối ưu hóa thời gian và tập trung vào chất lượng nội dung cùng khách mời nhé các sếp!