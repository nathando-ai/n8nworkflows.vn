---
title: "🚀 Tự động tạo mô tả sản phẩm bằng AI và đăng lên Shopify từ hình ảnh"
description: "Hướng dẫn chi tiết workflow n8n tự động phân tích hình ảnh sản phẩm bằng Google Gemini, tạo nội dung chuẩn SEO và đăng bán trực tiếp lên Shopify."
slug: "tu-dong-tao-mo-ta-san-pham-shopify-bang-ai-gemini"
tags: [n8n, automation, shopify, google-gemini, ai, ecommerce, content-creation]
keywords: [n8n workflow, shopify automation, google gemini ai, tu dong hoa shopify, tao mo ta sanpham ai]
---

# 🚀 Tự động tạo mô tả sản phẩm bằng AI và đăng lên Shopify từ hình ảnh

Các sếp kinh doanh thương mại điện tử có thấy cảnh mỗi lần nhập hàng mới là phải "vắt óc" viết mô tả sản phẩm, nghĩ tiêu đề chuẩn SEO, gắn thẻ (tags) và up ảnh lên kho lưu trữ cực kỳ tốn thời gian không? Việc làm thủ công này vừa nhàm chán vừa làm chậm tốc độ đưa sản phẩm lên kệ.

Được phát triển bởi **Pixcels Themes**, workflow n8n này sinh ra để giải quyết triệt để nỗi đau đó! Hệ thống sẽ tự động nhận dữ liệu hình ảnh và thông tin cơ bản, gọi AI phân tích, viết nội dung hấp dẫn và đẩy thẳng lên cửa hàng Shopify của các sếp chỉ trong vài giây.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần tự viết mô tả hay chỉnh sửa ảnh thủ công nữa.
- **Nội dung chuẩn SEO & Thu hút:** Google Gemini phân tích trực quan sản phẩm từ hình ảnh để viết tiêu đề, mô tả và gắn thẻ chuẩn xác nhất.
- **Tự động hóa toàn diện:** Đồng bộ ảnh lên ImgBB và tạo sản phẩm mới trực tiếp trên Shopify không cần chạm tay.
- **Hoạt động 24/7:** Kích hoạt tức thì thông qua Webhook ngay khi có yêu cầu từ hệ thống nguồn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **n8n Instance:** Đã cài đặt n8n (bản Cloud hoặc Self-hosted).
- **Google Gemini (PaLM) API Key:** Dùng cho node AI phân tích hình ảnh.
- **ImgBB Account & API Key:** Dùng cho node lưu trữ hình ảnh sản phẩm trực tuyến.
- **Shopify Store & Admin API Access Token:** Dùng để tạo sản phẩm mới (thông qua node HTTP Request).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow, sau đó dán trực tiếp vào n8n Editor thông qua tính năng `Import from Clipboard` hoặc thêm mới một workflow trống và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình các node sau:
- **Webhook:** Lấy URL Webhook cung cấp và cấu hình hệ thống nguồn của các sếp (CRM, Form, hoặc App nội bộ) gửi dữ liệu dạng POST bao gồm các trường: `product_name`, `material_type`, `file` (hình ảnh sản phẩm), `vendor`, `product_type`, `options`, và `variants`.
- **Analyze image (GoogleGemini):** Kết nối tài khoản Google Gemini bằng Credentials của các sếp, cấu hình để nhận hình ảnh và tạo ra tiêu đề, mô tả, thẻ, metadata chuẩn SEO.
- **imgbb (HTTP Request):** Nhập API Key của ImgBB để tải hình ảnh sản phẩm lên cloud và lấy URL công khai.
- **HTTP Request (Shopify):** Cấu hình kết nối API của Shopify với quyền truy cập (Admin API Access Token) để gửi dữ liệu sản phẩm hoàn chỉnh lên cửa hàng.
- **Code in JavaScript & Edit Fields:** Dùng để xử lý, format lại cấu trúc dữ liệu trước khi đẩy sang Shopify.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một dữ liệu mẫu để kiểm tra từng bước từ Webhook -> Gemini -> ImgBB -> Shopify.
- Sau khi test thành công, bật công tắc **Active** để workflow chính thức vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để gửi thông báo về máy ngay khi sản phẩm mới được tạo thành công trên Shopify.
- **Lưu lịch sử vào Google Sheets:** Thêm node Google Sheets để ghi lại danh sách các sản phẩm đã được AI tạo mô tả và đăng bán nhằm dễ dàng kiểm tra đối soát.
- **Đa dạng hóa ngôn ngữ:** Tinh chỉnh Prompt trong Google Gemini để tự động dịch hoặc viết mô tả sản phẩm bằng nhiều ngôn ngữ khác nhau (Anh, Trung, Nhật...) phục vụ khách hàng quốc tế.

### 📌 Kết luận
Tự động hóa quy trình đăng sản phẩm lên Shopify bằng AI không chỉ giúp tiết kiệm chi phí nhân sự mà còn tăng tốc độ phủ hàng lên gian hàng trực tuyến. Hãy áp dụng ngay workflow này để tối ưu hóa cửa hàng của các sếp ngày hôm nay!