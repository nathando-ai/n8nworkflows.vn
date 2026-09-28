---
title: "🚀 Tự động đồng bộ Testimonials từ Feedspace vào HubSpot CRM với n8n"
description: "Hướng dẫn kết nối Feedspace với HubSpot CRM bằng n8n giúp tự động tạo contact và lưu trữ đánh giá khách hàng ngay khi có phản hồi mới."
slug: "dong-bo-feedspace-testimonials-vao-hubspot-crm-n8n"
tags: [n8n, automation, no-code, hubspot, feedspace, crm, marketing]
keywords: [n8n workflow, feedspace to hubspot, tự động hóa crm, quản lý đánh giá khách hàng, n8n webhook]
---

# 🚀 Tự động đồng bộ Testimonials từ Feedspace vào HubSpot CRM với n8n

Việc thu thập đánh giá (testimonials), review và phản hồi từ khách hàng qua **Feedspace** là một bước tuyệt vời để xây dựng độ uy tín cho thương hiệu. Tuy nhiên, nếu các sếp cứ phải copy-paste thủ công thông tin khách hàng và nội dung đánh giá từ Feedspace vào **HubSpot CRM**, đội ngũ sales và marketing sẽ tốn rất nhiều thời gian và dễ bỏ sót các leads tiềm năng.

Giải pháp ở đây chính là workflow n8n tự động hóa 100% này! Ngay khi có khách hàng gửi đánh giá (dạng text, video, hoặc audio) qua Feedspace, workflow sẽ tự động ghi nhận, tạo hoặc cập nhật contact trong HubSpot CRM và đính kèm trực tiếp nội dung đánh giá làm ghi chú (note) cực kỳ chuyên nghiệp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Loại bỏ hoàn toàn khâu nhập liệu thủ công từ Feedspace sang HubSpot CRM.
- **Không bỏ lỡ Lead:** Kiểm tra thông tin email hợp lệ trước khi đẩy dữ liệu vào hệ thống, đảm bảo dữ liệu CRM luôn sạch.
- **Lưu trữ trực quan:** Đính kèm chi tiết nội dung đánh giá (kèm link video/audio nếu có) vào thẳng Profile khách hàng trên HubSpot dưới dạng Note.
- **Hoạt động 24/7:** Phản hồi webhook tức thì ngay khi khách hàng bấm nút gửi review.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Feedspace** đã cấu hình sẵn trang thu thập review.
- Tài khoản **HubSpot CRM** kèm quyền tạo/cập nhật Contact và Note.
- **HubSpot App Token** (hoặc Private App Access Token) để xác thực kết nối API.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc sử dụng tính năng import file JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình các node sau:

- **Receive Testimonial (Webhook Node):** 
  - Lấy đường dẫn Webhook URL được tạo ra từ node này.
  - Mang URL đó dán vào phần cài đặt Webhook/Integration trên bảng điều khiển của **Feedspace** để bắt đầu nhận dữ liệu.
- **Extract Testimonial Data (Code Node):** 
  - Node này dùng ngôn ngữ JavaScript để chuẩn hóa dữ liệu thô (tên, email, nội dung review, link media) từ Feedspace gửi sang. Các sếp không cần sửa gì trừ khi cấu trúc dữ liệu của Feedspace thay đổi.
- **Has Email? (IF Node):** 
  - Kiểm tra xem payload gửi lên có chứa địa chỉ email hợp lệ hay không. Nếu không, workflow sẽ điều hướng qua nhánh phản hồi lỗi qua node **Respond - No Email**.
- **Upsert Contact (HubSpot Node):** 
  - Chọn credentials HubSpot của các sếp.
  - Cấu hình hành động tạo hoặc cập nhật contact dựa trên địa chỉ email (Upsert).
- **Prepare Note Content (Set Node):** 
  - Chuẩn bị nội dung định dạng văn bản cho phần Note chứa lời chứng thực của khách hàng.
- **Create Testimonial Note (HTTP Request Node):** 
  - Sử dụng thông tin `hubspotAppToken` để gọi API tạo ghi chú gắn liền với ID của contact vừa được tạo/cập nhật trên HubSpot.
- **Respond - Success / Respond - No Email (Respond to Webhook Nodes):** 
  - Trả về mã trạng thái HTTP thích hợp cho Feedspace sau khi xử lý xong yêu cầu.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi thử một đánh giá mẫu từ Feedspace để kiểm tra luồng chạy.
- Sau khi test thành công, bật nút **Active** ở góc trên cùng bên phải để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm thông báo qua Telegram/Slack:** Nối thêm một node Telegram hoặc Slack sau bước "Create Testimonial Note" để báo động ngay cho đội ngũ Sales/Marketing mỗi khi có khách hàng VIP để lại review 5 sao!
- **Phân loại đánh giá:** Tận dụng Code Node để phân loại điểm số review (Positive/Negative) để gán nhãn (Tag/Lifecycle Stage) tương ứng trong HubSpot.
- **Gửi email cảm ơn tự động:** Kết hợp thêm node Gmail hoặc SendGrid để gửi mã giảm giá cảm ơn tự động cho khách hàng ngay khi họ hoàn thành đánh giá trên Feedspace.

### 📌 Kết luận
Workflow này là cầu nối hoàn hảo giúp tự động hóa quy trình chăm sóc khách hàng và tối ưu hóa dữ liệu đánh giá từ Feedspace vào HubSpot CRM. Triển khai ngay hôm nay để không bỏ lỡ bất kỳ phản hồi giá trị nào từ khách hàng của các sếp!