---
title: "🚀 Tự động phân loại và chấm điểm khách hàng tiềm năng (Lead) với JotForm, Google Gemini AI và Slack"
description: "Xây dựng hệ thống tự động lọc spam, chấm điểm lead (Hot/Warm/Cold) từ JotForm bằng Gemini AI, gửi thông báo Slack và phản hồi email cá nhân hóa tự động 100%."
slug: "tu-dong-phan-loai-cham-diem-lead-jotform-gemini-ai-slack"
tags: [n8n, automation, ai, google-gemini, jotform, slack, crm]
keywords: [n8n workflow, cham diem lead, tu dong hoa ban hang, jotform gemini ai, slack notification]
---

# 🚀 Tự động phân loại và chấm điểm khách hàng tiềm năng (Lead) với JotForm, Google Gemini AI và Slack

Các sếp có bao giờ cảm thấy quá tải khi mỗi ngày phải kiểm tra hàng chục form đăng ký từ website, trong đó một nửa là spam, phần còn lại thì không biết ai là khách hàng tiềm năng thực sự (Hot Lead) để chăm sóc trước? Việc lọc thủ công vừa tốn thời gian, vừa khiến doanh nghiệp bỏ lỡ cơ hội vàng chốt sale vì phản hồi chậm.

Workflow n8n này sẽ giải quyết triệt để bài toán trên bằng cách tự động hóa 100% quy trình: **Nhận thông tin từ Form -> AI lọc spam & chấm điểm -> Thông báo lên Slack -> Gửi email chăm sóc tự động theo phân khúc (Hot/Warm/Cold)** mà không cần tốn một phút thao tác thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Lọc sạch rác 100%:** Google Gemini AI tự động nhận diện và chặn đứng các form điền linh tinh, spam trước khi làm phiền đội ngũ sales.
- **Chấm điểm thông minh (Lead Scoring):** Phân loại khách hàng thành Hot, Warm, Cold dựa trên nội dung yêu cầu và quy mô công ty.
- **Phản hồi tức thì (Instant Follow-up):** Khách hàng nhận được email phản hồi cá nhân hóa ngay lập tức dựa theo mức độ tiềm năng.
- **Cảnh báo thời gian thực:** Đội ngũ Sales nhận ngay thông báo chi tiết qua Slack khi có khách hàng tiềm năng chất lượng cao đăng ký.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **JotForm** để tạo form nhận thông tin.
- Tài khoản **Google Cloud / Google AI** để lấy API Key dùng cho mô hình Gemini.
- Workspace **Slack** và quyền kết nối Bot/Webhook để gửi thông báo.
- Tài khoản **Gmail (OAuth2)** để gửi email tự động cho khách hàng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor của mình, hoặc tải file JSON về và import lên hệ thống.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình các node sau:

- **JotForm Trigger:** Kết nối tài khoản JotForm của các sếp. Đảm bảo form đăng ký có các trường chuẩn: *Full Name*, *Work Email*, *Role*, *Number of Employees*, và *How can we help you?* (nội dung câu hỏi/tin nhắn).
- **Google Gemini Chat Model & AI Agent:** Kết nối credentials Google Palm/Gemini API. Kiểm tra lại câu Prompt trong AI Agent để chắc chắn biến truyền vào khớp với tên trường nội dung trong Jotform của các sếp.
- **If Spam:** Node này tự động đọc kết quả `is_spam` từ AI. Nếu là spam, tiến trình sẽ dừng lại ở node **Nothing to do for spams!** (NoOp).
- **Send lead alert to sales (Slack):** Kết nối Slack Credentials, chọn kênh Slack chuyên nhận lead (ví dụ: `#sales-leads`) để đội ngũ túc trực chốt đơn.
- **Switch:** Bộ lọc phân loại điểm số (`lead_score`) từ AI để chia thành 3 nhánh: Hot, Warm, Cold.
- **Hot Reply / Warm Reply / Cold Reply (Gmail):** Kết nối Gmail OAuth2 cho cả 3 node này. **Cực kỳ quan trọng:** Các sếp phải viết lại nội dung email cho phù hợp với văn phong công ty và thay thế các placeholder link (như link Calendly đặt lịch hẹn) thành URL thật của doanh nghiệp.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test workflow) với một vài dữ liệu đăng ký giả lập trên Jotform để kiểm tra luồng chạy của AI và email.
- Bật công tắc **Active** để đưa workflow vào vận hành thực tế 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Đồng bộ CRM:** Mở rộng workflow bằng cách gắn thêm node HubSpot, Notion hoặc Google Sheets ngay sau bước cảnh báo Slack để lưu trữ thông tin khách hàng tự động.
- **Tích hợp Telegram/Zalo:** Ngoài Slack, các sếp có thể nhân bản nhánh thông báo sang Telegram Bot để nhận lead mọi lúc mọi nơi trên điện thoại cá nhân.
- **Tinh chỉnh Prompt AI:** Thêm các tiêu chí cụ thể hơn vào Prompt của Gemini AI để định nghĩa chính xác thế nào là một "Hot Lead" phù hợp với đặc thù sản phẩm/dịch vụ của công ty các sếp.

### 📌 Kết luận
Một hệ thống tự động hóa tinh gọn nhưng cực kỳ mạnh mẽ giúp đội ngũ sales không bỏ lỡ bất kỳ khách hàng tiềm năng nào. Hãy cài đặt ngay workflow này để tối ưu hóa phễu bán hàng của doanh nghiệp ngay hôm nay các sếp nhé!