---
title: "🛒 Trợ lý mua sắm thông minh trên Telegram với AI Gemini và n8n"
description: "Hướng dẫn tự động hóa hoàn toàn không cần code để tạo trợ lý mua sắm thông minh trên Telegram với AI Gemini của Google, giúp tìm kiếm sản phẩm Amazon một cách nhanh chóng và chính xác."
slug: "tro-ly-mua-sam-thong-minh-telegram-ai-gemini-n8n"
tags: [n8n, automation, no-code, telegram, ai, amazon, shopping assistant]
keywords: [n8n workflow, tự động hóa, trợ lý mua sắm, ai gemini, telegram bot, amazon scraper]
---

# 🛒 Trợ lý mua sắm thông minh trên Telegram với AI Gemini và n8n

[Các sếp đang gặp khó khăn khi phải tìm kiếm sản phẩm trên Amazon một cách thủ công, phải đọc nhiều trang web khác nhau để so sánh giá cả và đặc tính sản phẩm. Với workflow này, các sếp có thể tạo một trợ lý mua sắm thông minh hoàn toàn tự động trên Telegram, giúp tiết kiệm thời gian và tăng hiệu quả công việc.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian tìm kiếm sản phẩm trên nhiều trang web khác nhau
- Nhận được gợi ý sản phẩm phù hợp nhất từ AI Gemini
- Tự động hóa hoàn toàn quá trình mua sắm
- Tăng hiệu quả công việc và giảm thiểu công việc thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot Telegram
- API key của Google Gemini
- API key của Apify (để scrape dữ liệu từ Amazon)
- Kiến thức cơ bản về n8n và cách cấu hình workflow
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Nhấn vào nút "Import from URL" và nhập URL: [https://n8n.io/workflows/6384](https://n8n.io/workflows/6384)
3. Hoặc tải file JSON về và import từ file

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Google Gemini Chat Model1, Google Gemini Chat Model2, Google Gemini Chat Model3**: Cần cấu hình credentials cho Google Palm API
- **Telegram Message Receiver**: Cần cấu hình credentials cho Telegram API
- **Amazon Product Scraper**: Cần cấu hình API key của Apify để scrape dữ liệu từ Amazon
- **Product Query Cleaner**: Cần cấu hình code để loại bỏ các từ không cần thiết trong truy vấn sản phẩm
- **Message Intent Classifier**: Cần cấu hình agent để phân loại ý định của người dùng
- **Product vs Chat Router**: Cần cấu hình switch để chuyển hướng workflow dựa trên kết quả phân loại ý định
- **Chat Response Generator**: Cần cấu hình agent để tạo phản hồi chat cho người dùng
- **Send Chat Response**: Cần cấu hình credentials cho Telegram API để gửi phản hồi chat
- **Product Data Processor**: Cần cấu hình code để xử lý dữ liệu sản phẩm
- **Product List Combiner**: Cần cấu hình aggregate để kết hợp danh sách sản phẩm
- **Product Recommendation Engine**: Cần cấu hình agent để tạo gợi ý sản phẩm
- **Send Product Recommendations**: Cần cấu hình credentials cho Telegram API để gửi gợi ý sản phẩm

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút "Activate" để kích hoạt workflow
2. Test workflow bằng cách gửi tin nhắn đến bot Telegram
3. Kiểm tra kết quả và điều chỉnh nếu cần thiết

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với các dịch vụ khác như Slack hoặc Discord để nhận thông báo
- Lưu log các truy vấn sản phẩm để phân tích xu hướng mua sắm
- Tạo báo cáo định kỳ về các sản phẩm được tìm kiếm nhiều nhất
- Tích hợp với các dịch vụ thanh toán để tự động hóa quá trình mua hàng

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình mua sắm trên Amazon thông qua Telegram, tiết kiệm thời gian và tăng hiệu quả công việc. Các sếp chỉ cần cấu hình các credentials và kích hoạt workflow, sau đó có thể sử dụng trợ lý mua sắm thông minh ngay lập tức.