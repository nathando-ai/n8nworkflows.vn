---
title: "🚀 Tự động hóa báo giá thông minh với AI, Gmail và Supabase trong n8n"
description: "Xây dựng hệ thống tự động nhận yêu cầu báo giá từ Email và Form, dùng AI phân tích, tính toán giá thông minh và lưu trữ Supabase."
slug: "tu-dong-hoa-bao-gia-ai-gmail-supabase-n8n"
tags: [n8n, automation, ai, openai, supabase, gmail, slack]
keywords: [n8n workflow, tự động hóa báo giá, AI sales quote, OpenAI n8n, Supabase n8n, Gmail automation]
---

# 🚀 Tự động hóa quy trình báo giá bán hàng tích hợp AI, Gmail và Supabase

Các sếp có đang mệt mỏi vì mỗi ngày phải tốn hàng giờ đọc email, lọc các yêu cầu báo giá rác (spam), tính toán giá thủ công rồi mới soạn email gửi khách? Quá trình thủ công này vừa chậm trễ, vừa dễ bỏ sót khách hàng tiềm năng lớn.

Workflow n8n này sẽ giúp các sếp **tự động hóa 100% quy trình báo giá** từ lúc khách hàng gửi yêu cầu qua Gmail hoặc Website Form cho đến khi tạo sẵn bản nháp báo giá thông minh bằng AI, lưu trữ vào Supabase và cảnh báo qua Slack nếu là khách VIP.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần thủ công lọc email, đánh giá độ khó và tính tiền nữa. AI sẽ làm thay từ A-Z.
- **Phản hồi siêu tốc:** Khách vừa gửi yêu cầu là hệ thống đã có sẵn dữ liệu và bản nháp báo giá 3 mức (Good/Better/Best).
- **Không bỏ sót khách VIP:** Tự động bắn thông báo qua Slack ngay khi có khách hàng tiềm năng có giá trị lớn ($\ge \$10,000$).
- **Quản lý tập trung:** Toàn bộ thông tin, trạng thái (Chờ duyệt, Đã gửi) được lưu trữ gọn gàng trên Supabase Database.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Gmail Account** (để cấu hình Gmail Trigger và Gmail Send).
- **OpenAI API Key** (cho các node AI phân tích, lọc email và tính giá).
- **Supabase Account & Project** (để lưu trữ dữ liệu khách hàng và lịch sử báo giá).
- **Slack Workspace** (tùy chọn, để nhận thông báo đơn hàng lớn).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow, sau đó vào giao diện n8n Editor, chọn **Add workflow** -> Click vào dấu `...` ở góc trên bên phải -> Chọn **Import from Clipboard** và dán mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Gmail Trigger & Gmail - Send Quote**: Kết nối tài khoản Gmail của công ty thông qua `gmailOAuth2` để hệ thống tự động quét hộp thư đến mỗi phút và gửi email báo giá khi được phê duyệt.
- **OpenAI - Email Filter / Extract / Pricing / Generate Draft**: Cần cấu hình credentials `openAiApi` cho toàn bộ các node OpenAI. Đảm bảo sử dụng các model như `gpt-4o` hoặc `gpt-4o-mini` để có kết quả phân tích chính xác nhất.
- **Supabase - Save Initial / Search Similar / Update Complete / Mark Sent**: Cấu hình credentials `supabaseApi` với URL và Service Role Key của dự án Supabase. Các sếp nhớ tạo sẵn bảng (table) phù hợp để lưu trữ thông tin khách hàng, ngân sách, phân loại và trạng thái báo giá (`PROCESSING`, `PENDING_REVIEW`, `SENT`).
- **Slack - High Value Alert**: Kết nối `slackOAuth2Api` để nhận thông báo khi có yêu cầu giá trị cao ($\ge \$10,000$). Có thể thay thế bằng node Telegram nếu các sếp thích dùng Telegram.
- **Webhook - Form Submission & Webhook - Send Quote**: Cấu hình đường dẫn Webhook chuẩn để tích hợp với website form và hệ thống dashboard quản trị (như Replit/NextJS).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test workflow) bằng cách gửi một email yêu cầu báo giá mẫu đến Gmail hoặc bắn một POST request vào Webhook Form.
- Kiểm tra dữ liệu trên Supabase xem đã ghi nhận chính xác chưa.
- Bật công tắc **Active** để hệ thống chính thức vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Zalo**: Thay thế hoặc bổ sung node Slack bằng Telegram Bot để nhận thông báo tức thì trên điện thoại cá nhân.
- **Mở rộng Dashboard kiểm duyệt**: Sử dụng Replit, Retool hoặc Vercel kết hợp Supabase để tạo một giao diện Web đơn giản cho nhân viên sales bấm nút "Phê duyệt & Gửi" (*Approve & Send*).
- **Thêm bước kiểm tra Blacklist**: Thêm một node IF trước AI Filter để loại bỏ ngay lập tức các tên miền email rác hoặc đối thủ cạnh tranh cố tình phá hoại.

### 📌 Kết luận
Với workflow n8n này, quy trình báo giá vốn phức tạp và mất thời gian nay đã được tự động hóa thông minh nhờ sức mạnh của AI và Supabase. Hãy triển khai ngay hôm nay để tối ưu hóa đội ngũ sales và chốt đơn nhanh hơn đối thủ!