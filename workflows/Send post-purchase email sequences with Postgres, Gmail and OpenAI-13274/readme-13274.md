---
title: "🚀 Tự động hóa chuỗi email sau mua hàng với Postgres, Gmail và OpenAI"
description: "Hướng dẫn tự động hóa chuỗi email sau mua hàng với n8n, Postgres, Gmail và OpenAI. Tiết kiệm thời gian, tăng doanh số và cải thiện trải nghiệm khách hàng."
slug: "tu-dong-hoa-chuoi-email-sau-mua-hang"
tags: [n8n, automation, no-code, email-marketing, ai-automation]
keywords: [n8n workflow, tự động hóa email, chuỗi email sau mua hàng, OpenAI, Postgres]
---

# 🚀 Tự động hóa chuỗi email sau mua hàng với Postgres, Gmail và OpenAI

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian quản lý chuỗi email sau mua hàng
- Tăng doanh số thông qua các đề xuất sản phẩm cá nhân hóa
- Cải thiện trải nghiệm khách hàng với nội dung hữu ích
- Tự động hóa hoàn toàn quy trình mà không cần lập trình
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail với quyền truy cập API
- Cơ sở dữ liệu Postgres chứa thông tin đơn hàng và trạng thái giao hàng
- API key từ OpenAI để sử dụng các tính năng AI
- Thông tin xác thực SMTP (nếu sử dụng dịch vụ email khác Gmail)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào [n8n.io/workflows/13274](https://n8n.io/workflows/13274)
2. Nhấp vào nút "Download" để tải file JSON của workflow
3. Trong giao diện n8n, nhấp vào biểu tượng "+" ở góc trái màn hình
4. Chọn "Import from File" và chọn file JSON vừa tải về
5. Hoặc copy toàn bộ nội dung JSON và dán vào ô "Import from JSON"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Schedule Trigger** (Node 6):
   - Cấu hình lịch chạy phù hợp với tần suất kiểm tra đơn hàng mới
   - Ví dụ: Chạy mỗi giờ để kiểm tra đơn hàng mới

2. **Execute a SQL query** (Node 7):
   - Cập nhật truy vấn SQL để phù hợp với cấu trúc bảng đơn hàng của bạn
   - Đảm bảo truy vấn trả về các trường: order_id, customer_email, product_details, delivery_status

3. **Select rows from a table** (Node 8):
   - Cấu hình kết nối đến bảng đơn hàng trong Postgres
   - Chọn các trường cần thiết: order_id, customer_email, product_details, delivery_status

4. **Order Placed Ack.** (Node 3):
   - Cấu hình thông tin email xác nhận đơn hàng
   - Điền nội dung email phù hợp với thương hiệu của bạn
   - Kiểm tra các biến động như {{order_id}}, {{customer_email}}...

5. **Message a model** (Node 14) và **Message a model1** (Node 15):
   - Cấu hình credentials OpenAI
   - Kiểm tra và điều chỉnh các prompt AI để phù hợp với sản phẩm của bạn
   - Đảm bảo các biến động như {{product_details}} được bao gồm trong prompt

6. **Format AI response3** (Node 10):
   - Kiểm tra mã JavaScript để định dạng phản hồi AI
   - Điều chỉnh nếu cần thiết để phù hợp với định dạng email mong muốn

7. **Send Tips to User** (Node 4) và **Send Tips to User1** (Node 5):
   - Cấu hình thông tin email gửi lời khuyên sử dụng sản phẩm
   - Điền nội dung email phù hợp với thương hiệu của bạn
   - Kiểm tra các biến động như {{ai_tips}}...

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, nhấp vào nút "Activate" ở góc trên bên phải
2. Chọn "Error Workflow" để xử lý lỗi nếu có
3. Nhấp vào "Save" để lưu workflow
4. Kiểm tra bằng cách tạo một đơn hàng mẫu và theo dõi quá trình thực thi của workflow

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack hoặc Telegram để nhận thông báo khi workflow chạy
2. Thêm node lưu log để theo dõi hoạt động của workflow
3. Tạo báo cáo định kỳ về hiệu suất của chuỗi email
4. Kết hợp với các công cụ phân tích để theo dõi tỷ lệ mở email và tỷ lệ chuyển đổi

### 📌 Kết luận
Workflow này giúp tự động hóa hoàn toàn chuỗi email sau mua hàng, từ xác nhận đơn hàng đến gửi lời khuyên sử dụng sản phẩm và đề xuất sản phẩm bổ sung. Bằng cách áp dụng workflow này, các sếp có thể tiết kiệm thời gian, tăng doanh số và cải thiện trải nghiệm khách hàng một cách hiệu quả.