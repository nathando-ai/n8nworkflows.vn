---
title: "🚀 Tự động hóa tạo bài viết Facebook viral với Google Gemini 2.0 & AI Image Generation trên n8n"
description: "Hướng dẫn chi tiết cách xây dựng hệ thống tự động tạo nội dung và hình ảnh cho Facebook Page bằng Google Gemini AI và n8n không cần code."
slug: "tu-dong-hoa-tao-bai-viet-facebook-viral-gemini-ai-n8n"
tags: [n8n, automation, facebook, ai, google-gemini, content-creation]
keywords: [n8n workflow, tạo bài viết facebook ai, google gemini 2.0, facebook automation, tự động hóa marketing]
keywords: [n8n workflow, tạo bài viết facebook ai, google gemini 2.0, facebook automation, tự động hóa marketing]
---

# 🚀 Tự động hóa tạo bài viết Facebook viral với Google Gemini 2.0 & AI Image Generation

Các sếp có đang cảm thấy mệt mỏi mỗi khi phải lên ý tưởng, viết nội dung thu hút, thiết kế hình ảnh rồi lại cặm cụi đăng bài thủ công lên Fanpage Facebook mỗi ngày? Công việc lặp đi lặp lại này ngốn rất nhiều thời gian quý báu lẽ ra dành cho chiến lược kinh doanh.

Giải pháp ở đây là gì? Hãy để workflow n8n tự động hóa 100% quy trình này! Hệ thống sẽ tiếp nhận yêu cầu qua Form, sử dụng sức mạnh siêu việt của **Google Gemini** để viết nội dung viral, tự động tạo hình ảnh minh họa bằng AI, lưu log vào **Google Sheets**, gửi thông báo qua **Gmail** và cuối cùng là tự động xuất bản bài viết lên **Facebook Fanpage**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Biến một ý tưởng sơ sài thành bài đăng hoàn chỉnh kèm hình ảnh chỉ trong vài giây.
- **Nội dung chuẩn chỉnh, sáng tạo:** Tận dụng Gemini AI để viết caption kích thích tương tác (viral) cao.
- **Tự động hóa toàn diện:** Từ khâu nhận input, xử lý AI, lưu trữ dữ liệu Google Sheets, gửi email báo cáo đến đăng trực tiếp lên Facebook.
- **Vận hành 24/7:** Chạy ngầm liên tục, không bỏ lỡ bất kỳ chiến dịch marketing nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n instance:** Bản Cloud hoặc Self-hosted (đã cấu hình sẵn).
- **Tài khoản Facebook Developer:** Để tạo App và lấy Page Access Token đăng bài.
- **Google Cloud Account:** Kích hoạt Google Sheets API, Gmail API và tạo Service Account.
- **Google AI Studio:** Lấy API Key của Google Gemini.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Sao chép toàn bộ mã JSON của workflow từ template gốc.
- Trong giao diện n8n, nhấn vào **"Import from JSON"**, dán mã vào và bấm **"Import"**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 18 nodes chính, các sếp cần cấu hình cẩn thận các thành phần sau:

- **Cấu hình Credentials:**
  - **Facebook Graph API:** Tạo thông tin xác thực với `Access Token` của Page.
  - **Google Services:** Tải file JSON của Google Service Account để kết nối Sheets & Gmail.
  - **Gemini AI (`Google PaLM API`):** Nhập API Key lấy từ Google AI Studio.

- **Cấu hình Nodes cụ thể:**
  - **Facebook Graph API** & **Facebook Upload Img**: Thay thế ID mẫu bằng **Page ID** thực tế của Fanpage Facebook.
  - **save content** & **Append row in sheet**: Thay thế Document ID mẫu bằng ID của 2 Google Sheets (Bảng log nội dung và Bảng theo dõi input).
  - **Send a message (Gmail):** Thay đổi địa chỉ email nhận báo cáo thành email cá nhân của các sếp.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) từng node hoặc test toàn bộ workflow bằng form nhập liệu mẫu.
- Kiểm tra kết quả trên Google Sheets, Gmail và Fanpage Facebook.
- Gạt công tắc sang trạng thái **Active workflow** để hệ thống chính thức tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thêm node gửi thông báo qua chat nhóm ngay khi bài viết được đăng thành công lên Facebook.
- **Kiểm duyệt nội dung (Human-in-the-loop):** Thêm bước gửi email chờ duyệt trước khi đẩy bài lên Facebook nếu muốn kiểm soát kỹ hơn chất lượng nội dung.
- **Lên lịch định kỳ:** Thay vì dùng Form Trigger, có thể kết hợp Schedule Trigger để tự động tạo bài viết theo chủ đề có sẵn trong Google Sheets mỗi ngày.

### 📌 Kết luận
Việc tự động hóa quy trình sáng tạo nội dung Facebook với Google Gemini và n8n không chỉ giúp tiết kiệm nguồn lực mà còn nâng tầm chuyên nghiệp cho hoạt động Marketing của doanh nghiệp. Hãy bắt tay vào cài đặt ngay hôm nay để tối ưu hóa hiệu suất làm việc!