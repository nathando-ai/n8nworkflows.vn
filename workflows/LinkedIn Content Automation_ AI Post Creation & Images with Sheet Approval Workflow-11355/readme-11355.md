---
title: "🚀 Tự động hóa nội dung LinkedIn: Sáng tạo bài viết, tạo ảnh AI & Kiểm duyệt qua Google Sheets với n8n"
description: "Xây dựng hệ thống tự động hóa toàn diện từ ý tưởng trên Google Sheets, nghiên cứu xu hướng bằng Tavily, viết bài bằng AI Ollama, duyệt nội dung qua Gmail đến xuất bản tự động lên LinkedIn."
slug: "tu-dong-hoa-noi-dung-linkedin-ai-google-sheets-n8n"
tags: [n8n, automation, linkedin, ai, content-creation, google-sheets, openai]
keywords: [n8n workflow, tự động hóa linkedin, viết bài bằng ai, ollama n8n, google sheets trigger, content automation]
---

# 🚀 Tự động hóa nội dung LinkedIn: Sáng tạo bài viết, tạo ảnh AI & Kiểm duyệt chuyên nghiệp

Các sếp làm marketing, chủ agency hay solopreneur có mệt mỏi với việc lên lịch, viết content và tìm hình ảnh cho LinkedIn mỗi ngày không? Việc làm thủ công này ngốn rất nhiều thời gian quý báu mà đáng lẽ các sếp nên dùng để chốt deal hoặc tối ưu chiến lược.

Hôm nay, em xin giới thiệu một siêu phẩm workflow n8n giúp tự động hóa 100% quy trình sản xuất nội dung LinkedIn. Hệ thống sẽ lấy ý tưởng từ Google Sheets, tự động nghiên cứu xu hướng qua Tavily, viết bài bằng AI, gửi email xin duyệt, tạo ảnh minh họa bằng OpenAI và cuối cùng là tự động đăng bài lên LinkedIn mà các sếp không cần đụng tay chân!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian:** Biến một dòng ý tưởng thô trên Google Sheets thành bài đăng hoàn chỉnh gồm nội dung chuẩn SEO và hình ảnh bắt mắt.
- **Kiểm soát tuyệt đối:** Tích hợp bước phê duyệt qua Gmail (`Approval Email`) giúp các sếp duyệt hoặc chỉnh sửa nội dung trước khi xuất bản.
- **Cập nhật xu hướng thời gian thực:** Sử dụng `Search` (Tavily) để quét các thông tin nóng hổi liên quan đến chủ đề bài viết.
- **Vận hành 24/7:** Chạy tự động liên tục trên nền tảng n8n Self-hosted, không bỏ lỡ bất kỳ khung giờ vàng đăng bài nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow này chạy mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- Tài khoản **Google Sheets** (để quản lý chiến dịch và nội dung).
- **Tavily API Key** (dùng cho node tìm kiếm xu hướng).
- **Ollama** (chạy local AI model) hoặc LLM tương đương kết hợp **OpenAI API Key** (để tạo hình ảnh minh họa).
- Tài khoản **Gmail** (để gửi email phê duyệt).
- **LinkedIn OAuth App** (để cấp quyền đăng bài tự động).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, vào giao diện n8n Editor, chọn **New Workflow**, nhấn tổ hợp phím `Ctrl + V` (hoặc `Cmd + V`) để dán toàn bộ các node vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống không báo lỗi, các sếp cần cấu hình chính xác các node quan trọng sau:

- **Google Sheets Trigger & Add the post to the sheet**: Kết nối tài khoản Google qua OAuth2. Trỏ đường dẫn đến file Google Sheets quản lý chiến dịch của các sếp, chọn đúng Sheet Name để hệ thống nhận diện dòng dữ liệu mới.
- **Search (Tavily)**: Điền Tavily API Key để node này có thể tìm kiếm các xu hướng và dữ liệu mới nhất trên internet phục vụ việc viết bài.
- **Content Generator & Ollama Chat Model**: Cấu hình mô hình ngôn ngữ (Ollama local hoặc OpenAI) để AI hiểu đúng persona và văn phong thương hiệu của các sếp.
- **Approval Email (Gmail)**: Kết nối tài khoản Gmail thông qua Gmail OAuth2. Thiết lập người nhận email là sếp hoặc đội ngũ kiểm duyệt nội dung.
- **Approved? (If)**: Kiểm tra logic điều kiện xem nội dung đã được duyệt qua email hay chưa để quyết định chuyển sang bước tạo ảnh hay sửa bài.
- **Generate image (OpenAI)**: Cấu hình OpenAI API Key để kích hoạt tính năng tạo ảnh minh họa chân thực dựa trên prompt từ node `Image Prompt`.
- **Create a post (LinkedIn)**: Kết nối tài khoản LinkedIn thông qua LinkedIn OAuth2 và điền chính xác LinkedIn Organization/Person ID của các sếp vào node này để bài viết được publish đúng chỗ.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thêm một dòng dữ liệu mới vào Google Sheet để test thử toàn bộ luồng chạy (data flow).
- Sau khi kiểm tra mọi thứ chạy mượt mà từ khâu viết bài, duyệt email đến tạo ảnh, các sếp bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa hơn nữa hệ thống này, các sếp có thể triển khai thêm các ý tưởng sau:
- **Tích hợp Slack/Telegram:** Thay vì chỉ gửi email duyệt bài, hãy cấu hình thêm node gửi thông báo kèm nút bấm (Interactive Buttons) qua Telegram hoặc Slack để duyệt nhanh hơn trên điện thoại.
- **Lưu log tự động:** Thêm một bước cập nhật trạng thái "Đã đăng thành công" (Published) vào Google Sheets ngay sau khi bài viết lên sóng.
- **Đa kênh hóa:** Mở rộng workflow để ngoài LinkedIn, nội dung còn tự động được tối ưu và đăng chéo lên Twitter (X) hoặc Facebook Page cùng lúc.

### 📌 Kết luận
Với workflow **LinkedIn Content Automation**, các sếp đã sở hữu trong tay một đội ngũ marketing AI tự động làm việc không lương 24/7. Hãy cài đặt ngay hôm nay để tối ưu hóa hiệu suất xây dựng thương hiệu cá nhân và doanh nghiệp trên LinkedIn!