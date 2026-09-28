---
title: "🚀 Tự động hóa quy trình tạo và gửi thư mời nhận việc (Job Offer Letter) với OpenAI, Gmail và Slack"
description: "Hướng dẫn chi tiết workflow n8n tự động hóa 100% quy trình từ xác thực email ứng viên, dùng AI viết thư mời, chuyển đổi PDF kèm chữ ký số và gửi thông báo HR."
slug: "tu-dong-hoa-tao-va-gui-thu-moi-nhan-viec-n8n"
tags: [n8n, automation, hr-automation, openai, gmail, slack]
keywords: [n8n workflow, tao thu moi nhan viec, job offer letter automation, openai hr, tu dong hoa nhan su]
---

# 🚀 Tự động hóa quy trình tạo và gửi thư mời nhận việc với OpenAI, Gmail và Slack

Trong quy trình tuyển dụng, việc soạn thảo từng thư mời nhận việc (Job Offer Letter), chuyển đổi sang PDF, định dạng chữ ký và gửi email cho ứng viên thường chiếm rất nhiều thời gian của bộ phận Nhân sự (HR). Chưa kể đến rủi ro gửi nhầm email do lỗi chính tả hoặc email không tồn tại.

Workflow n8n này sẽ giúp các sếp giải quyết triệt để bài toán trên bằng cách tự động hóa toàn bộ quy trình: từ xác thực email ứng viên, sử dụng AI (OpenAI) để viết nội dung cá nhân hóa, thiết kế HTML kèm chữ ký SVG, xuất file PDF chuyên nghiệp, gửi email tự động qua Gmail cho ứng viên và đồng thời bắn thông báo trực quan về kênh Slack của đội ngũ HR.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** HR chỉ cần bắn thông tin ứng viên qua Webhook, mọi việc còn lại hệ thống tự lo.
- **Chính xác & Chuyên nghiệp:** Email ứng viên được kiểm tra sống/chết trước khi gửi, tránh tình trạng bounce email.
- **Cá nhân hóa cao:** AI tạo nội dung thư mời trang trọng, ấm áp, nêu bật vị trí, đãi ngộ và văn hóa công ty.
- **Đồng bộ nội bộ hoàn hảo:** Đội ngũ HR nhận được thông báo chi tiết ngay lập tức trên Slack để theo dõi tiến độ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Self-hosted hoặc Cloud).
- **Webhook endpoint** hoặc ATS (Applicant Tracking System) để trigger dữ liệu.
- **OpenAI API Key** (dùng cho node *Generate Offer Letter Content*).
- **VerifiEmail API** (dùng cho node *Email Verification*).
- **HTML-to-PDF Service API** (dùng cho node *Convert to PDF*).
- **Gmail Account / OAuth2 Credentials** (dùng cho node *Deliver Offer Letter*).
- **Slack Bot Token / Webhook** (dùng cho node *Notify HR Team*).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào giao diện n8n Editor của các sếp, hoặc tạo mới một workflow và copy/paste cấu trúc JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số và credentials sau cho từng node:
- **Webhook**: Lấy Endpoint URL để kết nối với hệ thống tuyển dụng (ATS) hoặc form nộp hồ sơ của công ty.
- **Email Verification**: Thêm `verifiEmailApi` credentials để đảm bảo lọc sạch các email ảo, email sai định dạng.
- **Check Email Validity (Node IF)**: Thiết lập điều kiện kiểm tra kết quả từ bước xác thực email (chỉ cho phép các email "valid" đi tiếp).
- **Prepare Offer Data (Node Set)**: Chuẩn hóa các trường dữ liệu đầu vào như mức lương, ngày bắt đầu làm việc, tên công ty, thông tin liên hệ.
- **Generate Offer Letter Content (Node OpenAI)**: Cấu hình `openAiApi` credentials. Tùy chỉnh System Prompt để AI viết nội dung phù hợp với văn phong và văn hóa doanh nghiệp của các sếp.
- **Build HTML with SVG Signature (Node Code)**: Chèn nhận diện thương hiệu của công ty (màu sắc, logo, tên công ty) và chữ ký số SVG của giám đốc nhân sự hoặc người đại diện.
- **Convert to PDF (Node HTML-to-PDF)**: Thêm credentials dịch vụ chuyển đổi HTML sang PDF để tạo file tài liệu đính kèm sắc nét.
- **Deliver Offer Letter (Node Gmail)**: Kết nối `gmailOAuth2` credentials để gửi email tự động kèm file PDF thư mời trực tiếp cho ứng viên.
- **Notify HR Team (Node Slack)**: Cấu hình `slackApi` credentials và chọn Channel nhận thông báo nội bộ khi có thư mời được gửi thành công.

#### 3. Kích hoạt ⚡️
- Thực hiện test run với dữ liệu mẫu (Candidate Name, Position, Email, Salary...).
- Kiểm tra kết quả hiển thị trên PDF và luồng gửi Email / Slack.
- Bật công tắc **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Google Sheets / Airtable:** Thêm một node lưu trữ thông tin ứng viên và trạng thái gửi offer vào cơ sở dữ liệu để dễ dàng tra cứu lịch sử.
- **Thêm bước Phỏng vấn / Ký số:** Tích hợp thêm các dịch vụ ký số trực tuyến (như DocuSign hoặc HelloSign) vào cuối quy trình để ứng viên có thể ký xác nhận trực tiếp.
- **Bổ sung nhánh xử lý lỗi (Error Handling):** Nếu email không hợp lệ (Invalid), tự động gửi thông báo về Slack hoặc email nội bộ cho HR để xử lý thủ công.

### 📌 Kết luận
Tự động hóa quy trình tuyển dụng chính là chìa khóa giúp doanh nghiệp ghi điểm tuyệt đối trong mắt nhân tài nhờ sự chuyên nghiệp và tốc độ. Hãy áp dụng ngay workflow này để tối ưu hóa năng suất cho đội ngũ HR của các sếp!