---
title: "🚀 Tự động tạo mã giảm giá trên Paddle bằng n8n"
description: "Giải pháp tự động hóa 100% tạo mã giảm giá trên Paddle khi nhấn nút, giúp doanh nghiệp tiết kiệm thời gian và giảm sai sót."
slug: "tua-dong-tao-ma-giam-gia-paddle"
tags: [n8n, automation, no-code, paddle, sales]
keywords: [n8n workflow, tự động hóa, paddle coupon, giảm giá, bán hàng]
---

# 🚀 Tự động tạo mã giảm giá trên Paddle bằng n8n

Bạn đang phải tạo mã giảm giá thủ công trên Paddle mỗi khi có khách hàng mới hoặc khi cần khuyến mãi? Việc nhập liệu lặp đi lặp lại không chỉ tốn thời gian mà còn dễ gây sai sót, ảnh hưởng đến trải nghiệm khách hàng và doanh thu.  
Workflow **Create a coupon on Paddle** giúp bạn **tự động tạo mã giảm giá 100% không cần code** chỉ bằng một cú nhấn nút. Bạn chỉ cần cấu hình một vài thông số và workflow sẽ thực hiện mọi thao tác trên Paddle cho bạn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút tạo thủ công xuống ngay lập tức.  
- **Độ chính xác cao**: Không còn lỗi nhập liệu, mã giảm giá được tạo đúng cấu hình.  
- **Tự động hóa linh hoạt**: Có thể tích hợp với các trigger khác (webhook, email, Slack…) để kích hoạt khi cần.  
- **Quản lý dễ dàng**: Mọi thao tác đều được ghi lại trong lịch sử workflow, thuận tiện cho audit.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Tài khoản Paddle** với quyền quản trị để tạo coupon.  
- **API Key** của Paddle (được tạo trong phần *Developer* của dashboard Paddle).  
- **n8n** đã được cài đặt và chạy (đề nghị sử dụng phiên bản mới nhất).  
- **Kết nối internet ổn định** để n8n có thể gọi API Paddle.  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON của workflow từ trang gốc:  
   <https://n8n.io/workflows/659>  
   hoặc sao chép toàn bộ nội dung JSON.  
2. Mở **n8n Editor** → **Import** → **Upload JSON** hoặc **Paste JSON**.  
3. Nhấn **Import** và workflow sẽ xuất hiện trong danh sách workflow của bạn.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Mô tả | Cấu hình cần chỉnh |
|------|-------|---------------------|
| **On clicking 'execute'** | Trigger thủ công | Không cần cấu hình thêm. Khi muốn chạy, chỉ cần nhấn nút *Execute* trong giao diện n8n. |
| **Paddle** | Tạo coupon trên Paddle | 1️⃣ **Credentials**: Chọn *paddleApi* đã tạo trước. <br>2️⃣ **Action**: Chọn *Create Coupon*. <br>3️⃣ **Coupon Code**: Nhập mã giảm giá (ví dụ `SUMMER21`). <br>4️⃣ **Discount Type**: `percentage` hoặc `fixed`. <br>5️⃣ **Discount Value**: Giá trị giảm (ví dụ `10` cho 10%). <br>6️⃣ **Validity**: Thời gian có hiệu lực (tùy chọn). <br>7️⃣ **Other options**: Số lần sử dụng, khách hàng áp dụng, v.v. |

> **Tip**: Nếu muốn tạo coupon tự động dựa trên dữ liệu từ nguồn khác (ví dụ Google Sheets), hãy thêm node *Google Sheets* trước *Paddle* và map các trường tương ứng.

### 3. Kích hoạt ⚡️

1. **Test run**: Nhấn *Execute* trên node *On clicking 'execute'* để kiểm tra xem coupon có được tạo thành công không. Kiểm tra phản hồi trong tab *Output*.  
2. **Bật Active**: Khi mọi thứ chạy đúng, chuyển workflow sang trạng thái *Active* để tự động chạy khi trigger được kích hoạt.  

## ✍️ Mẹo & gợi ý nâng cao

:::tip[Đẩy mạnh tự động hóa]
1. **Slack/Telegram Notification**: Thêm node *Slack* hoặc *Telegram* sau node *Paddle* để gửi thông báo khi coupon được tạo.  
2. **Lưu log vào Google Sheets**: Ghi lại thông tin coupon (code, discount, thời gian) vào sheet để theo dõi.  
3. **Trigger tự động**: Thay *Manual Trigger* bằng *Webhook* hoặc *Schedule* để tự động tạo coupon theo lịch hoặc khi có sự kiện.  
4. **Quản lý lỗi**: Thêm node *Error Trigger* để gửi email khi có lỗi trong quá trình tạo coupon.  
:::

## 📌 Kết luận

Workflow **Create a coupon on Paddle** là công cụ tuyệt vời giúp các sếp giảm bớt công việc thủ công, tăng tính chính xác và nhanh chóng phản ứng với nhu cầu khuyến mãi.  
Hãy thử ngay, import workflow, cấu hình credentials và chạy thử! Nếu muốn mở rộng, hãy kết hợp với các node khác như Slack, Google Sheets, hay webhook để tạo một hệ thống tự động hoàn chỉnh.  

Chúc các sếp thành công và tiết kiệm thời gian!