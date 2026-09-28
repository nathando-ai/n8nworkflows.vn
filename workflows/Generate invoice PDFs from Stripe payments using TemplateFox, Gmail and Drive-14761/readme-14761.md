---
title: "🚀 Tự động tạo hóa đơn PDF từ Stripe, gửi Gmail và lưu Google Drive với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động tạo hóa đơn PDF chuyên nghiệp khi có thanh toán Stripe thành công, gửi email cho khách hàng và lưu trữ trên Google Drive."
slug: "tu-dong-tao-hoa-don-pdf-stripe-gmail-google-drive"
tags: [n8n, automation, stripe, gmail, google-drive, invoice-processing]
keywords: [n8n workflow, tự động hóa hóa đơn, stripe trigger, templatefox, tạo pdf tự động, gửi email hóa đơn]
---

# 🚀 Tự động hóa tạo và gửi hóa đơn PDF từ Stripe thanh toán thành công

Việc xuất và gửi hóa đơn thủ công mỗi khi khách hàng thanh toán qua Stripe không chỉ tốn thời gian mà còn dễ dẫn đến sai sót, chậm trễ, ảnh hưởng đến trải nghiệm chuyên nghiệp của doanh nghiệp. 

Giải pháp tuyệt vời cho các sếp chính là workflow n8n này: Tự động hóa 100% quy trình lắng nghe sự kiện thanh toán từ Stripe, lấy thông tin chi tiết sản phẩm, tạo file hóa đơn PDF chuyên nghiệp qua TemplateFox, đồng thời gửi trực tiếp qua Gmail cho khách hàng và lưu trữ an toàn trên Google Drive.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Không cần can thiệp thủ công từ lúc khách trả tiền đến khi nhận hóa đơn.
- **Chuyên nghiệp hóa:** Khách hàng nhận được hóa đơn PDF thiết kế đẹp mắt ngay lập tức sau khi thanh toán thành công.
- **Lưu trữ khoa học:** Tự động back-up toàn bộ hóa đơn vào thư mục Google Drive được chỉ định để dễ dàng đối soát kế toán.
- **Hoạt động liên tục 24/7:** Không bỏ sót bất kỳ giao dịch nào của khách hàng.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Tài khoản Stripe** (Cần Stripe Secret Key loại `sk_live_` hoặc `sk_test_`).
- **Tài khoản TemplateFox** (Cần API Key, lấy miễn phí tại [app.pdftemplateapi.com](https://app.pdftemplateapi.com) và cài đặt community node `n8n-nodes-templatefox`).
- **Tài khoản Google** (Kết nối Gmail OAuth2 và Google Drive OAuth2).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy đoạn mã JSON của workflow và dán trực tiếp vào n8n Editor, hoặc import file JSON thông qua giao diện n8n của các sếp. Workflow bao gồm 7 nodes chính xử lý từ đầu đến cuối chuỗi tác vụ.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số quan trọng sau trong các node:
- **Stripe Trigger:** Kết nối tài khoản Stripe và cấu hình webhook để lắng nghe sự kiện thanh toán thành công (`checkout.session.completed`).
- **Get Line Items (HTTP Request):** Lấy danh sách sản phẩm/dịch vụ từ Stripe Checkout session. Cần đảm bảo credentials kết nối Stripe được thêm đúng.
- **Format Invoice Data (Code Node):** Tinh chỉnh cấu trúc dữ liệu, định dạng số hóa đơn hoặc thêm bớt các trường thông tin hiển thị sao cho khớp với template.
- **TemplateFox:** Cài đặt community node `n8n-nodes-templatefox`, nhập API Key và chọn mẫu Template invoice đã tạo sẵn trên TemplateFox.
- **Download PDF (HTTP Request):** Tải file PDF vừa được tạo từ TemplateFox về n8n để chuẩn bị chuyển qua các bước tiếp theo.
- **Email Invoice (Gmail):** Kết nối tài khoản Gmail OAuth2, tùy chỉnh tiêu đề, nội dung email gửi kèm file PDF hóa đơn cho khách hàng.
- **Save to Google Drive (Google Drive Node):** Kết nối tài khoản Google Drive và điền **Folder ID** của thư mục chứa hóa đơn trên Drive của các sếp.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thực hiện một giao dịch test trên Stripe (hoặc dùng chế độ Test Mode của Stripe) để kiểm tra luồng dữ liệu.
- Sau khi kiểm tra mọi thứ chạy mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack/Telegram Notification:** Gắn thêm node thông báo vào Slack hoặc Telegram ngay sau node Google Drive để đội ngũ sale/kế toán nắm bắt ngay khi có đơn hàng và hóa đơn mới.
- **Lưu log vào Google Sheets:** Thêm bước ghi lại thông tin khách hàng, mã hóa đơn và link file Drive vào Google Sheets để tiện thống kê doanh thu.
- **Tùy biến nội dung email:** Viết nội dung email chăm sóc khách hàng cá nhân hóa dựa trên tên và sản phẩm họ vừa mua.

### 📌 Kết luận
Workflow tự động hóa tạo và gửi hóa đơn từ Stripe qua TemplateFox, Gmail và Google Drive là một mảnh ghép không thể thiếu cho các mô hình kinh doanh số, SaaS hoặc thương mại điện tử hiện đại. Hãy thiết lập ngay hôm nay để tiết kiệm thời gian vận hành và mang lại trải nghiệm tuyệt vời nhất cho khách hàng của các sếp!