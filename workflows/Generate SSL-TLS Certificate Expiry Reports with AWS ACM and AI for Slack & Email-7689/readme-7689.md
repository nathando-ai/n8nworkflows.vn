---
title: "🚀 Tự động tạo và gửi báo cáo SSL/TLS Certificate từ AWS ACM qua Slack & Email với AI"
description: "Workflow n8n giúp tự động quét hạn chứng chỉ SSL/TLS trên AWS ACM hàng tuần, dùng AI tổng hợp thành báo cáo chuyên nghiệp dạng Markdown/HTML rồi gửi qua Slack và Email."
slug: "tu-dong-tao-bao-cao-ssl-tls-aws-acm-ai-slack-email"
tags: [n8n, automation, aws-acm, openai, slack, sendgrid, ai-agents]
keywords: [n8n workflow, aws acm certificate expiry, tu dong hoa ssl tls, openai agent n8n, gui bao cao slack sendgrid]
---

# 🚀 Tự động tạo và gửi báo cáo SSL/TLS Certificate từ AWS ACM qua Slack & Email với AI

Các sếp làm DevOps, quản trị hạ tầng hay bảo mật chắc hẳn đã từng ít nhất một lần "đau đầu" vì chứng chỉ SSL/TLS hết hạn đột ngột, dẫn đến sập hệ thống hoặc cảnh báo bảo mật cho khách hàng. Việc kiểm tra thủ công danh sách chứng chỉ trên AWS Certificate Manager (ACM) vừa tốn thời gian, vừa dễ bỏ sót.

Workflow n8n này sinh ra để giải quyết triệt để vấn đề đó! Hệ thống sẽ tự động quét toàn bộ chứng chỉ SSL/TLS trên AWS ACM hàng tuần, sử dụng Trí tuệ nhân tạo (OpenAI) để phân tích, tổng hợp thành báo cáo trực quan dưới dạng Markdown (chuyển thành PDF gửi qua Slack) và HTML (gửi qua Email).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Không bao giờ quên hạn SSL**: Tự động hóa hoàn toàn lịch kiểm tra hàng tuần mà không cần thao tác thủ công.
- **Báo cáo thông minh bằng AI**: Sử dụng OpenAI (GPT-5-mini / GPT-4.1-mini) để phân tích dữ liệu thô từ AWS thành báo cáo tóm tắt cực kỳ dễ đọc.
- **Đa kênh thông báo**: Gửi file PDF báo cáo trực tiếp vào kênh Slack của team kỹ thuật và gửi bản HTML chi tiết qua Email cho ban quản lý/kiểm toán.
- **Giảm thiểu rủi ro**: Nhận diện sớm các chứng chỉ sắp hết hạn hoặc không đủ điều kiện gia hạn tự động để xử lý kịp thời.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt sẵn n8n (Self-hosted hoặc Cloud).
- **AWS Account**: Tài khoản AWS có quyền truy cập AWS Certificate Manager (ACM) (`GetManyCertificates`).
- **OpenAI API Key**: Để cung cấp cho các node AI Agent phân tích và viết báo cáo.
- **Slack OAuth2 API**: Quyền kết nối để upload file PDF lên kênh Slack chỉ định.
- **SendGrid API / SMTP**: Dịch vụ gửi email để bắn báo cáo HTML.
- **Google Drive OAuth2 API**: Dùng cho node tạo file tài liệu và chuyển đổi định dạng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n template hoặc copy trực tiếp đoạn JSON, sau đó paste vào giao diện n8n Editor của các sếp qua tính năng **Import from JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các credentials và thông số sau trong các node:
- **Get many certificates**: Chọn AWS Credentials (`aws`) đã cấu hình quyền đọc AWS ACM.
- **Weekly schedule trigger**: Thiết lập thời gian chạy định kỳ (Ví dụ: 08:00 sáng thứ Hai hàng tuần).
- **OpenAI Chat Model** & **OpenAI Chat Model1**: Điền OpenAI API Key và chọn model phù hợp (như `gpt-5-mini` hoặc `gpt-4.1-mini`).
- **Certificate Summary Markdown Agent** & **Certificate Summary HTML Agent**: Kiểm tra lại System Prompt nếu muốn tùy chỉnh văn phong hoặc cấu trúc báo cáo theo ý muốn doanh nghiệp.
- **Create document file** & **Convert to PDF**: Kết nối với Google Drive Credentials (`googleDriveOAuth2Api`) để xử lý file tạm.
- **Send Weekly ACM Report PDF**: Chọn kênh Slack đích (ví dụ: `#it-security` hoặc `#cloud-ops`).
- **Send Weekly ACM Report Email**: Cấu hình SendGrid Credentials (`sendGridApi`) và điền địa chỉ email nhận báo cáo.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** trên từng node để kiểm tra luồng chạy với dữ liệu mẫu từ AWS.
- Sau khi test thành công không báo lỗi, gạt công tắc sang **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Có thể tích hợp thêm Microsoft Teams, Discord hoặc Telegram bên cạnh Slack để đa dạng hóa kênh nhận tin.
- **Tạo Task tự động**: Kết hợp thêm node JIRA hoặc GitHub Issues để tự động tạo ticket giao việc cho nhân sự phụ trách khi phát hiện chứng chỉ `EXPIRED`.
- **Lọc theo điều kiện**: Tùy chỉnh node `Parse ACM Data` để chỉ báo cáo các chứng chỉ sắp hết hạn trong vòng 30 ngày tới thay vì liệt kê toàn bộ.

### 📌 Kết luận
Việc tự động hóa quy trình quản lý chứng chỉ SSL/TLS với AWS ACM và AI không chỉ giúp đội ngũ DevOps tiết kiệm hàng giờ kiểm tra thủ công mỗi tuần mà còn loại bỏ hoàn toàn rủi ro sập hệ thống do quên gia hạn. Hãy áp dụng ngay workflow này vào hệ thống của các sếp!