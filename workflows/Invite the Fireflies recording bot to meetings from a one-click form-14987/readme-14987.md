---
title: "🚀 Tự động mời Fireflies AI Bot tham gia họp chỉ với 1 cú click form n8n"
description: "Giải pháp tự động hóa giúp bạn mời bot ghi âm Fireflies.ai vào các cuộc họp Google Meet/Zoom ngay lập tức thông qua một biểu mẫu tùy chỉnh duy nhất."
slug: "moi-fireflies-recording-bot-tu-dong-tu-form"
tags: [n8n, automation, no-code, fireflies, crm, ai-bot]
keywords: [n8n workflow, tự động hóa fireflies, bot ghi âm họp, form trigger n8n, tich hop fireflies ai]
---

# 🚀 Tự động mời Fireflies AI Bot tham gia họp chỉ với 1 cú click form

Các sếp có bao giờ cảm thấy mệt mỏi vì quên mời bot AI (như Fireflies.ai) vào các cuộc họp quan trọng, dẫn đến việc thiếu biên bản cuộc họp, quên task hoặc mất đi những ý tưởng đắt giá? Việc phải thao tác thủ công trên giao diện web của Fireflies cho từng lịch hẹn tốn rất nhiều thời gian và dễ xảy ra sai sót.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n cực kỳ thông minh: **Invite the Fireflies recording bot to meetings from a one-click form**. Chỉ với một biểu mẫu (Form) đơn giản, các sếp chỉ cần điền thông tin và bot sẽ tự động được gửi đến cuộc họp một cách mượt mà!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tối đa:** Không cần thao tác thủ công trên trang chủ Fireflies, chỉ mất 5 giây điền form là xong.
- **Không bao giờ bỏ lỡ biên bản họp:** Đảm bảo 100% các cuộc họp quan trọng đều có bot AI túc trực ghi chép và tóm tắt.
- **Quy trình chuyên nghiệp:** Chuẩn hóa cách thức yêu cầu ghi âm cuộc họp cho toàn bộ team hoặc bộ phận CSKH, Sales.
- **Hoạt động 24/7:** Vận hành tự động hoàn toàn trên nền tảng n8n mạnh mẽ, không cần can thiệp thủ công.
:::

### 📦 Các loại Nodes chính trong Workflow
Workflow này sử dụng các built-in nodes tiêu chuẩn của n8n, giúp dễ dàng triển khai và không tốn kém chi phí phức tạp:
- **Form Trigger (`n8n-nodes-base.formTrigger`):** Tạo giao diện biểu mẫu trực quan để thu thập thông tin cuộc họp (Link meeting, tên cuộc họp, email người nhận,...).
- **If (`n8n-nodes-base.if`):** Kiểm tra và phân nhánh logic điều kiện (ví dụ: định dạng link hợp lệ, loại cuộc họp...).
- **Set (`n8n-nodes-base.set`):** Chuẩn hóa và làm sạch dữ liệu đầu vào từ form trước khi gửi đi.
- **HTTP Request (`n8n-nodes-base.httpRequest`):** Giao tiếp trực tiếp với API của Fireflies.ai để ra lệnh cho bot tham gia cuộc họp.
- **Respond to Webhook (`n8n-nodes-base.respondToWebhook`):** Trả về thông báo thành công hoặc thất bại trực tiếp lên màn hình trình duyệt cho người điền form.
- **Sticky Note (`n8n-nodes-base.stickyNote`):** Các ghi chú hướng dẫn chi tiết được ghim trực tiếp trên workspace giúp dễ đọc, dễ hiểu.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản **Fireflies.ai** và **API Key** (hoặc tích hợp ứng dụng) để cấp quyền cho bot tham gia cuộc họp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cung cấp (hoặc copy toàn bộ mã JSON).
- Mở n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng ba chấm (...) ở góc trên bên phải -> Chọn **Import from File** (hoặc Paste trực tiếp JSON).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Form Trigger Node:** Tùy chỉnh các trường dữ liệu (Fields) trên form theo ý muốn của các sếp (Ví dụ: Thêm trường Tên khách hàng, Link Google Meet/Zoom, Ghi chú...).
- **HTTP Request Node (Gửi lệnh tới Fireflies):** 
  - Cấu hình Authentication (Bearer Token hoặc API Key) tương ứng với tài khoản Fireflies.ai của các sếp.
  - Kiểm tra lại Endpoint URL của API Fireflies để đảm bảo payload gửi đi đúng định dạng cấu trúc mà Fireflies yêu cầu (thường bao gồm `meeting_url` và `title`).
- **Respond to Webhook Node:** Tùy chỉnh thông điệp hiển thị (HTML hoặc Text) để báo cho người dùng biết bot đã được điều phối thành công.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền thông tin vào link form do n8n cung cấp.
- Kiểm tra kết quả trả về và xem bot Fireflies có được mời vào lịch họp hay không.
- Nếu mọi thứ chạy mượt mà, hãy bật nút **Active** ở góc trên bên phải để workflow chính thức đi vào hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack / Telegram:** Thêm node thông báo vào kênh chat chung của team ngay sau khi form được gửi thành công, giúp mọi người biết cuộc họp này sẽ có AI ghi âm.
- **Lưu lịch sử vào Google Sheets / Airtable:** Thêm một node lưu trữ thông tin các cuộc họp đã gọi bot vào database để dễ dàng quản lý, kiểm tra lại sau này.
- **Xác thực người dùng:** Kết hợp thêm các bước kiểm tra email nội bộ để tránh việc form bị spam từ bên ngoài.

### 📌 Kết luận
Với workflow n8n siêu tiện lợi này, việc quản lý và điều phối bot AI ghi âm cuộc họp chưa bao giờ dễ dàng đến thế. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa thời gian và nâng cao hiệu suất làm việc nhóm lên một tầm cao mới!