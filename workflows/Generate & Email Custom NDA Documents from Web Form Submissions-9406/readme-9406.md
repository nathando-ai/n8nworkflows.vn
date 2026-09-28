---
title: "🚀 Tự động tạo và gửi tài liệu NDA tùy chỉnh từ Web Form với n8n"
description: "Hướng dẫn chi tiết cách xây dựng hệ thống tự động hóa thu thập thông tin từ form, tạo tài liệu thỏa thuận bảo mật (NDA) dưới dạng DOCX và gửi email tự động cho khách hàng."
slug: "tu-dong-tao-va-gui-tai-lieu-nda-tu-chi-tu-web-form-n8n"
tags: [n8n, automation, no-code, webhook, pdf-toolkit, email-automation]
keywords: [n8n workflow, tự động hóa NDA, tạo tài liệu docx tự động, gửi email n8n, webhook n8n]
keywords: [n8n workflow, tự động hóa, tạo hợp đồng tự động, gửi email tự động, webhook n8n]
---

# 🚀 Tự động tạo và gửi tài liệu NDA tùy chỉnh từ Web Form với n8n

Trong quy trình làm việc với đối tác, khách hàng hoặc freelancer, việc soạn thảo và ký kết Thỏa thuận bảo mật thông tin (NDA) là bước bắt buộc nhưng lại cực kỳ tốn thời gian nếu làm thủ công. Các sếp thường phải copy thông tin, điền vào mẫu, xuất file và gửi email. Quá trình này vừa chậm chạp lại dễ xảy ra sai sót.

Giải pháp ở đây là gì? Hãy để n8n lo! Workflow này sẽ tự động hóa toàn bộ quy trình: cung cấp landing page nhận thông tin, xử lý dữ liệu từ form, tự động sinh tài liệu NDA định dạng Word (DOCX) chuẩn chỉnh và gửi thẳng vào email của người điền form chỉ trong tích tắc.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Khách hàng điền form là hệ thống tự sinh hợp đồng và gửi email, không cần sự can thiệp thủ công.
- **Chuyên nghiệp và chính xác:** Loại bỏ hoàn toàn tình trạng quên điền tên, sai sót thông tin pháp lý giữa các lần soạn thảo.
- **Tiết kiệm thời gian:** Giảm từ 15-20 phút soạn thảo hợp đồng xuống còn 0 phút cho mỗi đối tác.
- **Hoạt động 24/7:** Hệ thống luôn sẵn sàng nhận thông tin và xử lý bất kể ngày đêm.
:::

### 📦 Các thành phần chính trong Workflow
Workflow gồm 8 nodes được bố trí mạch lạc:
1. **Landingpage Endpoint & HTML for Landingpage:** Tạo và hiển thị giao diện Web Form để thu thập thông tin người ký NDA.
2. **FormData Endpoint & Respond to Webhook:** Nhận dữ liệu do người dùng gửi từ form và phản hồi lại trình duyệt.
3. **Set Form Endpoint:** Xử lý và chuẩn hóa dữ liệu đầu vào.
4. **NDA (HTML Version):** Tạo cấu trúc nội dung HTML cho tài liệu NDA dựa trên thông tin đã thu thập.
5. **HTML to Docx (`@custom-js/n8n-nodes-pdf-toolkit.Html2Docx`):** Chuyển đổi mã HTML thành file tài liệu Word (.docx) chuyên nghiệp.
6. **Send email:** Gửi email đính kèm file NDA vừa tạo tới hộp thư của đối tác.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Hệ thống n8n:** Đã cài đặt phiên bản n8n đang hoạt động.
- **Tài khoản SMTP:** Thông tin kết nối SMTP (Gmail, SendGrid, Amazon SES, v.v.) để gửi email tự động.
- **Credentials tùy chỉnh:** API Key cho Custom-JS PDF Toolkit (`customJsApi`) để sử dụng node chuyển đổi HTML sang Docx.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã JSON.
- Mở giao diện n8n Editor, chọn **Add workflow** -> Nhấn tổ hợp `Ctrl + V` (hoặc `Cmd + V`) để dán workflow vào bảng làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node Landingpage Endpoint & FormData Endpoint:** Kiểm tra đường dẫn Webhook path (`2f94bacb-f629-4053-a204-cab2ac8fd326`). Đảm bảo cấu hình URL phù hợp với domain n8n của các sếp (Production URL hoặc Test URL).
- **Node HTML for Landingpage & NDA (HTML Version):** Tùy chỉnh nội dung HTML của form nhập liệu và nội dung điều khoản NDA bên trong cho phù hợp với doanh nghiệp của các sếp.
- **Node HTML to Docx:** Thiết lập kết nối với `customJsApi` credentials để node có quyền xử lý định dạng tài liệu.
- **Node Send email:** Điền cấu hình SMTP của các sếp (Host, Port, User, Password) và thiết lập tiêu đề, nội dung email kèm file đính kèm là tài liệu Word (.docx) được tạo ra từ bước trước.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách truy cập vào trang landing page vừa tạo để điền thông tin mẫu.
- Kiểm tra hộp thư xem email đã được gửi thành công kèm file NDA chưa.
- Nếu mọi thứ hoạt động trơn tru, hãy chuyển trạng thái workflow sang **Active** để chính thức vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ dữ liệu:** Thêm node **Google Sheets** hoặc **Airtable** ngay sau bước nhận Form Data để lưu lại lịch sử những ai đã yêu cầu NDA.
- **Thông báo nội bộ:** Tích hợp thêm node **Telegram** hoặc **Slack** để gửi thông báo về group nội bộ mỗi khi có khách hàng vừa điền form nhận NDA.
- **Tự động ký số:** Kết hợp thêm các dịch vụ ký điện tử (như DocuSign, HelloSign) để tự động hóa toàn bộ quy trình ký kết hợp đồng.

### 📌 Kết luận
Với workflow này, các sếp đã sở hữu một "thư ký ảo" chuyên nghiệp giúp tự động hóa khâu làm thủ tục pháp lý ban đầu với khách hàng. Hãy triển khai ngay lên hệ thống n8n của mình để nâng cấp tốc độ xử lý công việc lên một tầm cao mới nhé!