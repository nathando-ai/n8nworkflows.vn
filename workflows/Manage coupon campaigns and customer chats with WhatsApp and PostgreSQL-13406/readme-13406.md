---
title: "🚀 Tự động hóa chiến dịch mã giảm giá và chăm sóc khách hàng WhatsApp kết hợp PostgreSQL trên n8n"
description: "Xây dựng hệ thống quản lý mã giảm giá (Coupon Bot), Dashboard quản trị và tích hợp chatbot WhatsApp tự động 100% bằng n8n và cơ sở dữ liệu PostgreSQL."
slug: "quan-ly-coupon-whatsapp-postgresql-n8n"
tags: [n8n, automation, no-code, whatsapp, postgresql, chatbot]
keywords: [n8n workflow, quản lý coupon, whatsapp chatbot, postgresql n8n, tự động hóa marketing, coupon bot dashboard]
---

# 🚀 Tự động hóa chiến dịch mã giảm giá và chăm sóc khách hàng WhatsApp kết hợp PostgreSQL trên n8n

Các sếp đang đau đầu vì phải thủ công tạo mã giảm giá, gửi thông tin qua lại cho khách hàng trên WhatsApp và quản lý danh sách công ty, chương trình khuyến mãi một cách rời rạc? Việc thiếu một hệ thống tự động hóa đồng bộ giữa giao diện quản trị (Dashboard) và kênh chat không chỉ tốn thời gian mà còn dễ gây nhầm lẫn, bỏ lỡ khách hàng tiềm năng.

Giải pháp toàn diện ở đây chính là workflow n8n **Manage coupon campaigns and customer chats with WhatsApp and PostgreSQL**. Đây là hệ thống "all-in-one" giúp các sếp tự động hóa toàn bộ quy trình: từ việc cung cấp một Web Dashboard trực quan, hệ thống REST API hoàn chỉnh, quản lý trạng thái hội thoại (Session-based State Management) cho đến tích hợp trực tiếp với WhatsApp Business API.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, xử lý các webhook từ WhatsApp và truy vấn database liên tục mà không bị gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình cấp mã:** Khách hàng nhắn tin qua WhatsApp sẽ tự động nhận danh sách công ty, chọn mã giảm giá và nhận chi tiết ngay lập tức mà không cần nhân sự túc trực.
- **Dashboard quản trị trực quan:** Tích hợp giao diện Web (Vue.js & Tailwind CSS) ngay trong n8n qua Webhook, giúp quản lý toàn bộ công ty, mã giảm giá, thống kê và hộp thư đến (Inbox) real-time.
- **Phân quyền Admin/Customer thông minh:** Tự động nhận diện số điện thoại Admin để hiển thị menu quản trị qua WhatsApp, trong khi khách hàng thường sẽ nhận luồng tương tác nhận mã khuyến mãi.
- **Quản lý trạng thái phiên (Session State):** Theo dõi chính xác ngữ cảnh hội thoại của từng người dùng qua cơ sở dữ liệu PostgreSQL, đảm bảo bot không bao giờ "quên" khách đang ở bước nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã kích hoạt và sẵn sàng import workflow (khuyến nghị bản self-hosted).
- **PostgreSQL Database:** Cơ sở dữ liệu để lưu trữ thông tin khách hàng, công ty, coupon, lịch sử tin nhắn và session.
- **WhatsApp Business API:** Tài khoản Meta Business, Phone Number ID và Access Token (Bearer Auth) để gửi/nhận tin nhắn qua Graph API v22.0.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã JSON từ nguồn cấp.
- Mở n8n Editor, chọn **Add workflow** -> Nhấp vào menu ba chấm (...) ở góc trên bên phải -> Chọn **Import from File** hoặc **Paste JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Vì workflow này có quy mô lớn (hơn 110 nodes) phục vụ cả Web Dashboard lẫn WhatsApp Bot, các sếp cần chú ý cấu hình kỹ các thành phần sau:
- **Node `Postgres Init` & các node Postgres khác:** Cấu hình thông tin kết nối Database PostgreSQL của các sếp (`credentials: postgres`). Sau khi import, hãy chạy endpoint khởi tạo database (`/execute-init` hoặc node `Postgres Init`) để tự động tạo các bảng cần thiết (`customers`, `companies`, `coupons`, `messages`, `records`, `sessions`, `settings`).
- **Node `WhatsApp Webhook`:** Đặt đường dẫn webhook khớp với cấu hình trên Meta App Dashboard (`/webhook/whatsapp`).
- **Các node gửi tin nhắn (`Send Companies List`, `Send Coupons List`, `Ask Admin Input`, v.v. sử dụng loại `httpRequest`):** Đảm bảo đã thiết lập đúng **HTTP Bearer Auth** kết nối với WhatsApp Graph API (`v22.0/{phone_number_id}/messages`).
- **Cài đặt Admin:** Sau khi chạy Dashboard, truy cập giao diện web tại endpoint `/coupon-bot/dashboard` và thiết lập số điện thoại của quản trị viên (`admin_phone`) trong mục Settings.

#### 3. Kích hoạt ⚡️
- Kiểm tra lại các kết nối Database và WhatsApp API bằng cách thực hiện vài thao tác test.
- Bật công tắc **Active** ở góc trên cùng bên phải của n8n để workflow chính thức vận hành tự động 24/7.

---
![Dashboard Screenshot](https://jobotai.site/1.png)
---
![Dashboard Screenshot](https://jobotai.site/4.png)
---
![Dashboard Screenshot](https://jobotai.site/5.png)

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Kết hợp thêm các node Telegram hoặc Slack để gửi cảnh báo về hệ thống ngay khi có khách hàng nhận mã giảm giá giá trị cao.
- **Lưu trữ Log định kỳ:** Tận dụng bảng `records` và `messages` sẵn có trong PostgreSQL để tạo các báo cáo thống kê hàng tuần gửi về email cho ban quản lý.
- **Tùy biến giao diện Dashboard:** Vì giao diện được serve trực tiếp qua HTML/Vue.js (`Respond with Dashboard HTML`), các sếp có thể chỉnh sửa lại mã nguồn giao diện cho phù hợp với nhận diện thương hiệu công ty.

### 📌 Kết luận
Workflow **Manage coupon campaigns and customer chats with WhatsApp and PostgreSQL** là một cỗ máy tự động hóa cực kỳ mạnh mẽ, biến n8n thành một nền tảng CRM kết hợp Chatbot chuyên nghiệp. Hãy triển khai ngay trên VPS của các sếp để tối ưu hóa chiến dịch marketing và nâng cấp trải nghiệm chăm sóc khách hàng lên một tầm cao mới!