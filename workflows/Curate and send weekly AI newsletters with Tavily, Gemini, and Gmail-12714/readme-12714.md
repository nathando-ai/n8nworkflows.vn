---
title: "🚀 Tự động hóa bản tin AI hàng tuần với Tavily, Gemini và Gmail trên n8n"
description: "Xây dựng hệ thống tự động tổng hợp tin tức ngành và bài viết blog nội dung, sử dụng AI Gemini để viết bản tin và gửi tự động qua Gmail mỗi tuần."
slug: "tu-dong-hoa-ban-tin-ai-hang-tuan-voi-tavily-gemini-gmail"
tags: [n8n, automation, no-code, ai-newsletter, tavily, gemini, gmail]
keywords: [n8n workflow, tự động hóa bản tin, AI newsletter, Tavily AI, Google Gemini, Gmail automation]
---

# 🚀 Tự động hóa bản tin AI hàng tuần với Tavily, Gemini và Gmail

Việc biên tập và gửi bản tin (newsletter) hàng tuần cho khách hàng hoặc nội bộ công ty là một công việc cực kỳ tốn thời gian. Các sếp thường phải mất hàng giờ đồng hồ để lướt web tìm kiếm tin tức, chọn lọc các bài viết blog mới nhất của công ty, viết lời mở đầu, định dạng HTML và gửi thủ công. 

Giờ đây, với workflow n8n này, toàn bộ quy trình nghiên cứu, tổng hợp, viết nội dung bằng AI và gửi email sẽ được tự động hóa 100% mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Tự động hoàn toàn từ khâu tìm kiếm thông tin đến khi gửi email.
- **Nội dung thông minh, chuyên nghiệp:** Kết hợp khéo léo giữa tin tức thị trường bên ngoài và cập nhật blog nội bộ nhờ sức mạnh của AI Gemini.
- **Hoạt động tự động 24/7:** Chạy đúng lịch trình hàng tuần (Weekly Schedule) mà không cần con người can thiệp.
- **Định dạng HTML đẹp mắt:** Bản tin được trau chuốt tỉ mỉ, sẵn sàng gây ấn tượng với người nhận.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- **Tavily API Key:** Dùng để tìm kiếm thông tin chuyên sâu (Lấy key tại [tavily.com](https://tavily.com)).
- **Google Gemini API Key:** Dùng cho AI tạo nội dung (Google AI Studio).
- **Tài khoản Gmail:** Cấu hình OAuth2 để gửi email tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n (hoặc copy toàn bộ JSON) và paste trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 13 nodes hoạt động nhịp nhàng. Các sếp cần chú ý cấu hình các điểm sau:

- **Weekly schedule trigger:** Cấu hình thời gian chạy định kỳ mong muốn (ví dụ: Thứ Hai hàng tuần lúc 8:00 sáng).
- **Set newsletter config:** Mở node này để tùy chỉnh các thông số cốt lõi: Chủ đề bản tin (`topic`), tên bản tin (`newsletter name`), đường dẫn logo (`logo URL`), và đường dẫn blog công ty (`blog URL`).
- **Search company blog (Tavily)** & **Search external news (Tavily):** Thêm **Tavily API credentials** để cho phép node thực hiện tìm kiếm song song.
- **Gemini 1.5 Flash** & **Generate newsletter content:** Thêm **Google Gemini API credentials** và tinh chỉnh prompt nếu muốn AI đổi giọng văn (Tone of voice).
- **Send newsletter (Gmail):** Kết nối tài khoản **Gmail OAuth2** và cập nhật địa chỉ email người nhận (hoặc danh sách nhận bản tin).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Test run**) ở từng bước hoặc toàn bộ workflow để kiểm tra kết quả trả về từ Tavily và Gemini.
- Sau khi kiểm tra email nháp/gửi thành công, bật nút **Active** để workflow tự động chạy theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Kết hợp thêm node Slack hoặc Telegram để gửi bản thông báo (notification) nội bộ ngay khi bản tin được phát hành thành công.
- **Lưu lịch sử:** Thêm node Google Sheets hoặc Airtable để lưu lại nội dung các bản tin đã gửi nhằm dễ dàng tra cứu về sau.
- **Cá nhân hóa người nhận:** Thay vì gửi một email cố định, có thể kết nối với danh sách khách hàng từ CRM để gửi email cá nhân hóa hàng loạt.

### 📌 Kết luận
Workflow này là một "vũ khí" tuyệt vời giúp các sếp tối ưu hóa hoạt động Marketing, chăm sóc khách hàng và xây dựng thương hiệu cá nhân/doanh nghiệp mà không tốn nhiều nguồn lực. Hãy import và "lên đồ" ngay hôm nay!