---
title: "🚀 Tự động chia sẻ sản phẩm Shopify lên WordPress, Facebook, Instagram, LinkedIn và hơn thế nữa bằng OpenAI"
description: "Tự động hóa việc chia sẻ sản phẩm mới từ Shopify lên các nền tảng mạng xã hội và WordPress với công nghệ AI, tiết kiệm thời gian và tăng hiệu quả marketing"
slug: "tu-dong-chia-se-san-pham-shopify-voi-openai"
tags: [n8n, automation, no-code, shopify, wordpress, social media, openai]
keywords: [n8n workflow, tự động hóa, shopify, wordpress, facebook, instagram, linkedin, openai]
---

# 🚀 Tự động chia sẻ sản phẩm Shopify lên WordPress, Facebook, Instagram, LinkedIn và hơn thế nữa bằng OpenAI

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quy trình chia sẻ sản phẩm mới
- Tăng hiệu quả marketing: Đẩy sản phẩm lên nhiều nền tảng cùng lúc
- Cá nhân hóa nội dung: Sử dụng AI để tạo mô tả ngắn gọn phù hợp với từng nền tảng
- Hoạt động liên tục: Không cần can thiệp thủ công 24/7
- Tăng tương tác: Tối ưu nội dung cho từng mạng xã hội khác nhau
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Shopify với quyền truy cập API
- Tài khoản WordPress với quyền quản trị
- Tài khoản Facebook Page với quyền quản trị
- Tài khoản Instagram Business với quyền quản trị
- Tài khoản LinkedIn với quyền đăng bài
- Tài khoản Telegram với quyền gửi tin nhắn
- Tài khoản Discord với quyền gửi tin nhắn
- Tài khoản Gmail với quyền gửi email
- Tài khoản Microsoft Teams (tùy chọn)
- Tài khoản WhatsApp Business (tùy chọn)
- API Key từ OpenAI
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/13413)
2. Click vào nút "Copy Workflow Code"
3. Trong n8n Editor của bạn, click vào "Import from Clipboard"
4. Dán mã workflow đã copy và click "Import"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Shopify Trigger** (node đầu tiên):
   - Chọn credentials của Shopify
   - Cấu hình trigger để nhận thông báo khi có sản phẩm mới

2. **Create Product URL**:
   - Thiết lập URL cơ bản của cửa hàng Shopify (ví dụ: `https://yourstore.myshopify.com/products/`)

3. **Converts product descriptions (HTML) into short**:
   - Chọn credentials OpenAI
   - Cấu hình prompt để chuyển đổi mô tả HTML sang văn bản ngắn gọn
   - Ví dụ prompt: "Convert this HTML product description to a short, engaging text suitable for social media: [HTML_CONTENT]"

4. **Create WordPress Post**:
   - Chọn credentials WordPress
   - Cấu hình các tham số như:
     - Post Title: `{{$node["Shopify Trigger"].json["title"]}}`
     - Post Content: `{{$node["Converts product descriptions (HTML) into short"].json["content"]}}`
     - Featured Image: Sẽ được tự động xử lý bởi các node tiếp theo

5. **Post on Facebook page**:
   - Chọn credentials Facebook
   - Cấu hình ID của Facebook Page
   - Nội dung bài viết: `{{$node["Converts product descriptions (HTML) into short"].json["content"]}}`

6. **Publish Post to Instagram**:
   - Chọn credentials Facebook (cùng với Instagram Business)
   - Cấu hình ID của Instagram Business Account
   - Nội dung bài viết: `{{$node["Converts product descriptions (HTML) into short"].json["content"]}}`

7. **Post on LinkkedIN Profile**:
   - Chọn credentials LinkedIn
   - Cấu hình nội dung bài viết: `{{$node["Converts product descriptions (HTML) into short"].json["content"]}}`

8. **Post on LinkedN page**:
   - Chọn credentials LinkedIn
   - Cấu hình ID của LinkedIn Page
   - Nội dung bài viết: `{{$node["Converts product descriptions (HTML) into short"].json["content"]}}`

9. **Post on telegram Channel**:
   - Chọn credentials Telegram
   - Cấu hình ID của Telegram Channel
   - Nội dung tin nhắn: `{{$node["Converts product descriptions (HTML) into short"].json["content"]}}`

10. **Post on Discord Channel**:
    - Chọn credentials Discord
    - Cấu hình ID của Discord Channel
    - Nội dung tin nhắn: `{{$node["Converts product descriptions (HTML) into short"].json["content"]}}`

11. **Send a Notification mail**:
    - Chọn credentials Gmail
    - Cấu hình địa chỉ email nhận thông báo
    - Tiêu đề email: "New Product Published: {{$node["Shopify Trigger"].json["title"]}}"
    - Nội dung email: `{{$node["Converts product descriptions (HTML) into short"].json["content"]}}`

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu bằng cách kích hoạt workflow với một sản phẩm Shopify mẫu
2. Kiểm tra từng node để đảm bảo nội dung được chia sẻ đúng trên các nền tảng
3. Sau khi kiểm tra thành công, bật Active workflow để chạy tự động khi có sản phẩm mới

### ✍️ Mẹo & gợi ý nâng cao
1. **Tối ưu hình ảnh**: Sử dụng node "Edit Image" để điều chỉnh kích thước và chất lượng hình ảnh trước khi chia sẻ
2. **Lịch trình đăng bài**: Thêm node "Schedule" để đặt lịch đăng bài cho các nền tảng khác nhau
3. **Báo cáo hiệu suất**: Thêm node để gửi báo cáo hàng ngày về số lượng bài viết đã chia sẻ và tương tác
4. **Quản lý nội dung**: Sử dụng node "Sticky Note" để lưu trữ các mẫu nội dung tiêu chuẩn cho từng nền tảng

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình chia sẻ sản phẩm mới từ Shopify lên nhiều nền tảng mạng xã hội và WordPress, đồng thời sử dụng công nghệ AI để tối ưu nội dung. Với việc tự động hóa này, các sếp có thể tiết kiệm thời gian quý giá và tập trung vào các chiến lược marketing quan trọng hơn. Hãy thử ngay và nâng cao hiệu quả kinh doanh của bạn!