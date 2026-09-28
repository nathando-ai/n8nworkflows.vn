---
title: "🚀 Tự động tạo bản nháp Newsletter từ RSS Feed bằng GPT-4 và Gmail trên n8n"
description: "Hướng dẫn xây dựng workflow tự động tóm tắt bài viết từ nguồn RSS bằng AI GPT-4 và tạo bản nháp email trên Gmail, giúp tiết kiệm hàng giờ viết nội dung thủ công."
slug: "tu-dong-tao-newsletter-tu-rss-feed-gpt4-gmail"
tags: [n8n, automation, no-code, openai, gpt-4, gmail, rss, ai-newsletter]
keywords: [n8n workflow, tự động hóa newsletter, tóm tắt rss bằng ai, gpt-4 n8n, tạo draft gmail tự động]
---

# 🚀 Tự động tạo bản nháp Newsletter từ RSS Feed bằng GPT-4 và Gmail

Các sếp có đang tốn hàng giờ mỗi tuần để lướt các trang tin tức, đọc bài viết, tổng hợp và viết lại nội dung làm bản tin (Newsletter) gửi khách hàng không? Việc này không chỉ tốn thời gian mà còn dễ bị ngắt quãng khi bận rộn. 

Đừng lo, với workflow n8n cực đỉnh này do **Patrik Schick** thiết kế, mọi thứ sẽ được tự động hóa 100%. Hệ thống sẽ tự động quét các bài viết mới từ nguồn RSS Feed yêu thích của các sếp, sử dụng AI (GPT-4) để trích xuất, tóm tắt thông tin theo văn phong mong muốn, và cuối cùng là lưu thẳng vào Gmail dưới dạng một bản nháp (Draft) sẵn sàng để gửi đi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần copy-paste thủ công từ web này sang web khác hay tự tóm tắt bài viết.
- **Nội dung cá nhân hóa:** AI sử dụng Tone of Voice (giọng điệu) riêng của các sếp để viết bản tin cực kỳ tự nhiên.
- **Chủ động kiểm soát:** Nội dung được lưu ở mục Draft (Bản nháp) trong Gmail, các sếp hoàn toàn có thể kiểm tra và chỉnh sửa trước khi bấm nút gửi.
- **Hoạt động tự động:** Chạy ngầm 24/7, tự động cập nhật ngay khi có bài viết mới trên các trang RSS.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn các tài nguyên sau:
- Một server **n8n** đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản **OpenAI API Key** (đã nạp tiền để sử dụng mô hình GPT-4).
- Tài khoản **Google (Gmail)** để cấu hình kết nối OAuth2 gửi/tạo bản nháp email.
- Đường dẫn **RSS Feed** của trang tin tức/blog mà các sếp muốn theo dõi.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow trống trên n8n, sau đó copy toàn bộ JSON của workflow hoặc import file JSON trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 5 nodes chính, các sếp cần cấu hình kỹ các điểm sau:

- **RSS Feed Trigger**: 
  - Tại đây, các sếp cần dán đường dẫn RSS Feed của trang tin tức vào ô **URL**. Node này sẽ đóng vai trò "radar" quét bài viết mới liên tục.
- **Information Extractor**: 
  - Node này chịu trách nhiệm trích xuất thông tin quan trọng từ bài viết gốc. 
  - *Lưu ý quan trọng:* Trong phần System Prompt của node này, hãy đổi ngôn ngữ thành tiếng Việt (hoặc ngôn ngữ các sếp muốn dùng cho bản tin).
- **OpenAI Chat Model**: 
  - Chọn model AI (mặc định là `gpt-4.1-mini` hoặc các dòng GPT-4 mạnh mẽ khác).
  - Kết nối với thông tin **OpenAI API Key** của các sếp.
- **Message a model (OpenAI)**: 
  - Nơi AI tổng hợp lại nội dung từ bước trích xuất.
  - *Mẹo:* Tại System Prompt, hãy nhận dữ liệu từ Extractor. Ở Assistant Prompt, hãy định nghĩa rõ Tone of Voice (giọng văn hài hước, trang trọng, chuyên gia...) để AI viết đúng cá tính thương hiệu của các sếp.
- **Create a draft (Gmail)**: 
  - Chọn resource là `draft`.
  - Kết nối tài khoản Gmail thông qua **OAuth2**.
  - Điền tiêu đề email và nội dung lấy kết quả đầu ra từ node AI để tạo sẵn một bản nháp hoàn chỉnh trong hòm thư.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để test thử với một bài viết mẫu và kiểm tra kết quả trong mục Draft của Gmail.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa nguồn tin:** Các sếp có thể nối nhiều node RSS Feed khác nhau vào chung một luồng xử lý của AI để tạo ra một bản tin tổng hợp (Digest Newsletter) hàng tuần.
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để thông báo cho các sếp biết: *"Ê, có bản nháp newsletter mới vừa được tạo trong Gmail kìa!"*.
- **Lưu trữ lịch sử:** Thêm node Google Sheets để lưu lại danh sách các bài viết đã được xử lý, tránh việc trùng lặp nội dung.

### 📌 Kết luận
Việc xây dựng một hệ thống tạo nội dung tự động chưa bao giờ dễ dàng đến thế với n8n và AI. Hãy áp dụng ngay workflow này để tối ưu hóa quy trình làm content marketing và chăm sóc khách hàng của doanh nghiệp mình nhé các sếp!