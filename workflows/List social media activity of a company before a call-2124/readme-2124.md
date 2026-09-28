---
title: "🚀 Tự động tổng hợp hoạt động mạng xã hội của khách hàng trước lịch hẹn với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động quét bài đăng Twitter, LinkedIn của khách hàng tiềm năng mỗi sáng và gửi email tóm tắt trước cuộc gọi sale."
slug: "tu-dong-tong-hop-hoat-dong-mang-xa-hoi-truoc-cuoc-goi"
tags: [n8n, automation, sales, clearbit, twitter, linkedin, gmail]
keywords: [n8n workflow, tu dong hoa sales, tong hop social media, clearbit api, google calendar automation]
---

# 🚀 Tự động tổng hợp hoạt động mạng xã hội của khách hàng trước lịch hẹn

Trước mỗi cuộc gọi sales (Discovery call), các sếp thường mất bao nhiêu thời gian để "soi" trang cá nhân LinkedIn, Twitter (X) hay website của khách hàng để tìm chủ đề trò chuyện? Việc làm thủ công này không chỉ tốn thời gian mà đôi khi còn bỏ sót những thông tin đắt giá như bài đăng gần đây, dự án mới hay nỗi đau của khách hàng.

Đừng lo, workflow n8n cực kỳ thông minh này sẽ thay các sếp làm tất cả! Hệ thống sẽ tự động quét lịch họp mỗi sáng, nhận diện công ty của khách tham gia, "đào" dữ liệu hoạt động mới nhất trên Twitter và LinkedIn thông qua ClearBit và RapidAPI, sau đó tổng hợp thành một bản tin gọn gàng gửi thẳng vào Gmail trước khi cuộc gọi diễn ra.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Hiểu sâu về khách hàng:** Nắm bắt ngay các bài đăng, hoạt động mới nhất trên mạng xã hội của khách hàng trước khi bước vào cuộc họp.
- **Tiết kiệm 100% thời gian nghiên cứu:** Không cần mở chục tab trình duyệt tra cứu thủ công nữa.
- **Tạo ấn tượng mạnh mẽ:** Chủ động nhắc đến các chủ đề khách hàng đang quan tâm, tăng tỷ lệ chốt deal (conversion rate).
- **Tự động hoàn toàn:** Chạy ngầm mỗi sáng đúng lịch hẹn trên Google Calendar, không cần thao tác tay.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Calendar Account** (Để lấy danh sách lịch họp trong ngày).
- **Clearbit API** (Dùng node `Enrich attendee company` để tìm thông tin công ty dựa trên email).
- **RapidAPI Account** với các gói đăng ký API sau:
  - [Fresh LinkedIn Profile Data](https://rapidapi.com/freshdata-freshdata-default/api/fresh-linkedin-profile-data)
  - [Twitter API](https://rapidapi.com/omarmhaimdat/api/twitter154)
- **Gmail Credentials** (OAuth2 để gửi email tổng hợp).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy toàn bộ mã JSON từ n8n và dán trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node quan trọng sau đây để workflow chạy mượt mà:

- **Node `Every morning @ 7` (`scheduleTrigger`):** Đặt lịch thời gian chạy tự động mỗi sáng (ví dụ: 7:00 AM) để hệ thống quét lịch họp trong ngày.
- **Node `Get meetings for today` (`googleCalendar`):** Kết nối tài khoản Google Calendar của các sếp để lấy toàn bộ sự kiện diễn ra trong ngày hiện tại (`getAll`).
- **Node `Setup` (`set`):** Đây là nơi cấu hình cực kỳ quan trọng theo hướng dẫn trên canvas:
  - Nhập API Key của RapidAPI vào các trường `linkedInAPIKey` và `twitterAPIKey`.
  - Điền danh sách email người nhận báo cáo vào trường `emails`.
- **Node `Gmail` (`gmail`):** Thiết lập kết nối OAuth2 với tài khoản Gmail của các sếp để gửi email tự động.
- **Các node `Get recetn tweets` & `Get recent LinkedIn posts` (`httpRequest`):** Gọi đến RapidAPI sử dụng các API key đã được cấu hình ở node `Setup`.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử với dữ liệu giả lập hoặc lịch họp thực tế để kiểm tra luồng chạy qua các node `Switch`, `Filter`, `Merge` và `Prepare email template`.
- Sau khi test thành công, gạt công tắc **Active** ở góc trên cùng bên phải để bật chế độ tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Thay vì chỉ gửi qua Gmail, các sếp có thể nối thêm node Telegram hoặc Slack để bắn thông báo ngay lập tức vào nhóm sales trước giờ họp 15 phút.
- **Lưu trữ dữ liệu:** Lưu lịch sử các công ty đã tra cứu vào Google Sheets hoặc Airtable để làm dữ liệu chăm sóc khách hàng về sau (CRM lightweight).
- **Tích hợp AI (LLM):** Sử dụng OpenAI node để tóm tắt các bài đăng mạng xã hội thành 3 gạch đầu dòng ngắn gọn (Key Takeaways) giúp đội ngũ sales đọc lướt nhanh hơn nữa.

### 📌 Kết luận
Với workflow **List social media activity of a company before a call**, việc chuẩn bị trước mỗi cuộc gọi khách hàng trở nên chuyên nghiệp và nhanh chóng hơn bao giờ hết. Hãy cài đặt ngay hôm nay để nâng cao năng lực sales của đội ngũ nhé các sếp!