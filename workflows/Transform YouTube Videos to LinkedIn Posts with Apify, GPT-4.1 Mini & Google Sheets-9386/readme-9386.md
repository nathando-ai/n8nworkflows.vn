---
title: "🚀 Tự động hóa YouTube sang LinkedIn: Chuyển đổi Video thành Bài viết với Apify, GPT-4.1 Mini & Google Sheets"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình chuyển đổi video YouTube thành bài viết LinkedIn chuyên nghiệp bằng công cụ n8n, Apify và trí tuệ nhân tạo"
slug: "tu-dong-hoa-youtube-sang-linkedin-voi-n8n-apify-va-gpt"
tags: [n8n, automation, no-code, linkedin, youtube]
keywords: [n8n workflow, tự động hóa nội dung, youtube to linkedin, apify, gpt-4.1 mini]
---

# 🚀 Tự động hóa YouTube sang LinkedIn: Chuyển đổi Video thành Bài viết với Apify, GPT-4.1 Mini & Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quá trình chuyển đổi nội dung từ YouTube sang LinkedIn
- Tăng hiệu quả: Tạo ra 2 bài viết LinkedIn chuyên nghiệp từ mỗi video
- Tăng tương tác: Nội dung được cá nhân hóa và tối ưu hóa cho nền tảng LinkedIn
- Hoạt động liên tục: Theo dõi và xử lý video mới tự động 24/7
- Tích hợp dễ dàng: Lưu kết quả vào Google Sheets để quản lý và lên lịch đăng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản YouTube với quyền truy cập vào kênh cần theo dõi
- Tài khoản Apify để sử dụng actor "scrapingxpert/youtube-video-to-transcript"
- API key từ OpenAI để sử dụng GPT-4.1 Mini
- Tài khoản Google với quyền truy cập vào Google Sheets
- URL feed của kênh YouTube (có dạng: https://www.youtube.com/feeds/videos.xml?channel_id=...)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào [n8n.io/workflows/9386](https://n8n.io/workflows/9386)
2. Nhấn nút "Download" để tải file JSON workflow
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **RSS Feed Trigger**:
   - Thay đổi URL feed trong node này thành URL của kênh YouTube bạn muốn theo dõi
   - Ví dụ: `https://www.youtube.com/feeds/videos.xml?channel_id=UC_x5XG1OV2P6uZZ5FSM9Ttw`

2. **Run an Actor and get dataset**:
   - Đảm bảo bạn đã tạo credentials cho Apify trong n8n
   - Kiểm tra actor ID: `scrapingxpert/youtube-video-to-transcript`

3. **Message a model**:
   - Tạo credentials cho OpenAI trong n8n
   - Đảm bảo đã chọn đúng model (gpt-4o hoặc phiên bản mới nhất)
   - Kiểm tra prompt để đảm bảo nó tạo ra đúng định dạng JSON

4. **Append row in sheet**:
   - Tạo credentials cho Google Sheets trong n8n
   - Chỉnh sửa ID của Google Sheet và tên sheet phù hợp với tài khoản của bạn
   - Đảm bảo các cột trong sheet đã được đặt tên đúng với dữ liệu đầu ra

#### 3. Kích hoạt ⚡️
1. Chạy test với một video mẫu để kiểm tra toàn bộ chuỗi xử lý
2. Kiểm tra kết quả trong Google Sheets
3. Bật Active workflow sau khi đã kiểm tra và xác nhận hoạt động đúng

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh nội dung**: Chỉnh sửa prompt trong node OpenAI để phù hợp với phong cách viết và chủ đề của bạn
2. **Lên lịch đăng**: Kết nối với các node khác để tự động lên lịch đăng bài trên LinkedIn
3. **Theo dõi hiệu suất**: Thêm node để theo dõi lượt xem và tương tác của các bài viết
4. **Xử lý nhiều kênh**: Sao chép và chỉnh sửa workflow cho nhiều kênh YouTube khác nhau

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa quá trình chuyển đổi nội dung từ YouTube sang LinkedIn. Bằng cách kết hợp công nghệ Apify, trí tuệ nhân tạo và Google Sheets, các sếp có thể tiết kiệm thời gian đáng kể và tạo ra nội dung chất lượng cao một cách hiệu quả. Hãy thử ngay và nâng cao hiệu quả truyền thông của bạn!