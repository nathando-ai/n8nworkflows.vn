---
title: "🚀 Tự động hóa chiến dịch Email Marketing với MailerLite, Google Sheets và Claude AI qua OpenRouter"
description: "Xây dựng trợ lý AI quản lý chiến dịch email marketing chuyên nghiệp ngay trong n8n, tích hợp MailerLite, Google Sheets và Claude AI để tạo nội dung, báo cáo và tái tương tác."
slug: "quan-ly-email-campaign-mailerlite-google-sheets-claude-ai"
tags: [n8n, automation, no-code, mailerlite, ai-agent, google-sheets]
keywords: [n8n workflow, tự động hóa email marketing, mailerlite automation, claude ai openrouter, quản lý chiến dịch email]
---

# 🚀 Xây dựng Trợ lý AI Quản lý Email Marketing Toàn diện với n8n

Việc quản lý và vận hành các chiến dịch email marketing thủ công thường ngốn rất nhiều thời gian: từ việc lên ý tưởng nội dung, phân loại đối tượng, tạo bản nháp trên MailerLite, gửi chiến dịch, cho đến việc tổng hợp báo cáo số liệu và kích hoạt lại khách hàng cũ. 

Workflow này cung cấp một **trợ lý AI nội bộ hoạt động qua giao diện chat của n8n**, giúp các sếp tự động hóa toàn bộ quy trình trên chỉ bằng vài câu lệnh văn bản đơn giản mà không cần rời khỏi màn hình làm việc.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 3 nghiệp vụ chính:** Gửi chiến dịch mới, báo cáo số liệu chiến dịch, và tái tương tác với khách hàng lạnh (cold subscribers).
- **AI thông minh qua OpenRouter:** Sử dụng các mô hình Claude 3.5 Haiku mạnh mẽ để phân tích ý định (intent) và viết nội dung email hấp dẫn, tự nhiên.
- **An toàn với cơ chế Draft-First:** Hệ thống luôn tạo bản nháp (Draft) trên MailerLite để kiểm duyệt trước khi chính thức gửi hoặc lên lịch, tránh sai sót.
- **Log dữ liệu minh bạch:** Tự động ghi lại lịch sử tác vụ, trạng thái và metadata vào Google Sheets để dễ dàng theo dõi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản MailerLite** kèm API Key / HTTP Bearer Auth. Đảm bảo email người gửi đã được phê duyệt trên MailerLite.
- **Tài khoản OpenRouter** để sử dụng các mô hình AI (Claude).
- **Google Sheets** để lưu log tác vụ (Task Logging).
- **Postgres Database** (hoặc cơ sở dữ liệu tương đương) để lưu trữ bộ nhớ chat (Chat Memory).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cung cấp hoặc copy trực tiếp mã JSON, sau đó dán vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow vận hành trơn tru, các sếp cần chú ý cấu hình các thành phần sau:
- **Credentials:** 
  - Kết nối `OpenRouter API` cho các node `Intent OpenRouter Chat Model`, `Creative OpenRouter Chat Model`, v.v.
  - Cấu hình `HTTP Bearer Auth` hoặc Header Auth cho các node gọi API của MailerLite (`Fetch Groups`, `Create Send Draft`, `Schedule Or Send Draft`,...).
  - Kết nối `Google Sheets OAuth2` cho các node ghi log (`Log Task`, `Log Task Campaign`,...).
  - Kết nối `Postgres` cho node `Postgres Chat Memory`.
- **Cấu hình tuỳ chỉnh trong Code Nodes:**
  - Kiểm tra node **`Prepare Chat Context`**: Cấu hình chính xác `sender_email` và `reply_to` (email này bắt buộc phải được phê duyệt trên MailerLite).
  - Đảm bảo tài khoản MailerLite của các sếp đã tạo sẵn các nhóm (Groups) và phân khúc (Segments) phù hợp, đặc biệt là segment có tên **`Re-engage`** nếu sử dụng tính năng tái tương tác khách hàng.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test run) với dữ liệu mẫu được cung cấp sẵn (ví dụ: yêu cầu gửi chiến dịch cho VIP users qua Chat Trigger).
- Kiểm tra kết quả trên MailerLite và Google Sheets.
- Bật công tắc **Active** để đưa workflow vào hoạt động chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat đa dạng:** Thay vì dùng giao diện Chat mặc định của n8n, các sếp có thể kết nối workflow với Slack, Telegram hoặc WhatsApp để ra lệnh cho trợ lý AI mọi lúc mọi nơi.
- **Lưu trữ Brand Voice:** Kết nối thêm cơ sở dữ liệu lưu trữ phong cách thương hiệu (Brand Voice) để AI viết nội dung email sát với văn phong doanh nghiệp hơn.
- **Ứng dụng RAG:** Tích hợp RAG để AI học hỏi từ các mẫu email thành công trước đó, từ đó nâng cao chất lượng nội dung tự động sinh ra.

### 📌 Kết luận
Workflow này là một cỗ máy tự động hóa hoàn hảo cho các nhà làm marketing muốn ứng dụng AI vào quy trình vận hành hàng ngày mà vẫn giữ được sự kiểm soát tuyệt đối thông qua cơ chế duyệt bản nháp. Hãy triển khai ngay để tối ưu hóa hiệu suất làm việc của các sếp!