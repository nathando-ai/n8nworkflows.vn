---
title: "🚀 Xây dựng Trợ lý Y tế & Kiểm tra Triệu chứng thông minh với GPT-4-mini trên n8n"
description: "Hướng dẫn chi tiết cách tự động hóa trợ lý y tế ảo tích hợp AI phân tích triệu chứng, phát hiện tình huống khẩn cấp và đưa ra lời khuyên sức khỏe an toàn."
slug: "tro-ly-y-te-ai-kiem-tra-trieu-chung-n8n-gpt-4-mini"
tags: [n8n, automation, no-code, AI Chatbot, OpenAI, Healthcare]
keywords: [n8n workflow, trợ lý y tế AI, kiểm tra triệu chứng, gpt-4-mini, tự động hóa y tế, chatbot hỗ trợ sức khỏe]
---

# 🚀 Xây dựng Trợ lý Y tế & Kiểm tra Triệu chứng thông minh với GPT-4-mini

Các phòng khám, doanh nghiệp chăm sóc sức khỏe hoặc các nhà phát triển thường gặp khó khăn trong việc xây dựng một hệ thống tư vấn sức khỏe ban đầu vừa nhanh chóng, vừa đảm bảo tính an toàn pháp lý (cảnh báo khẩn cấp khi người dùng gặp nguy hiểm). Việc xây dựng thủ công tốn rất nhiều nhân lực và dễ bỏ sót các ca cấp cứu.

Workflow **Medical Symptom Checker & Health Assistant with GPT-4-mini** trên n8n sẽ giải quyết triệt để vấn đề này. Hệ thống hoạt động như một trợ lý ảo 24/7, tự động phân tích triệu chứng người dùng gửi đến qua Webhook, kiểm tra các dấu hiệu khẩn cấp (như khó thở, đau ngực), sử dụng sức mạnh của OpenAI GPT-4-mini để tư vấn sức khỏe tổng quát một cách thông minh, và lưu trữ lịch sử tương tác an toàn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản hồi tức thì 24/7:** Giải đáp các thắc mắc về triệu chứng, sức khỏe tổng quát ngay lập tức cho người dùng.
- **An toàn tối đa với chế độ khẩn cấp (Emergency Detection):** Tự động nhận diện các từ khóa nguy hiểm (đau ngực, khó thở, đột quỵ...) để đưa ra cảnh báo gọi cấp cứu ngay lập tức.
- **Tích hợp AI thông tin sức khỏe:** Sử dụng OpenAI GPT-4-mini để phân tích ngữ cảnh, hỗ trợ đa ngôn ngữ và đưa ra lời khuyên khoa học, kèm theo lời khuyên thăm khám bác sĩ chuyên khoa.
- **Bảo mật và ghi log:** Tùy chọn lưu trữ lịch sử nhật ký (Audit Log) lên Airtable để kiểm soát và cải thiện chất lượng dịch vụ.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **OpenAI API Key:** Tài khoản và API Key để kết nối với mô hình GPT-4-mini.
- **Airtable Account (Tùy chọn):** Nếu các sếp muốn sử dụng tính năng ghi log yêu cầu của người dùng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc sao chép toàn bộ mã nguồn JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dùng tổ hợp phím `Ctrl+V` để dán trực tiếp vào canvas).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow vận hành trơn tru, các sếp cần chú ý cấu hình các node cốt lõi sau:

- **Health Query Webhook (`webhook`):** Node điểm đầu nhận dữ liệu `POST` từ giao diện chat hoặc ứng dụng của các sếp. Hãy kiểm tra đường dẫn endpoint (`/health-assistant`) và đảm bảo phương thức là `POST`.
- **Safety Check & Categorization (`code`):** Node lập trình JavaScript chạy ngầm để lọc các từ khóa nhạy cảm, phân loại triệu chứng và phát hiện tình huống nguy hiểm.
- **Emergency Router (`if`):** Dựa vào kết quả phân tích từ node code phía trước, node này sẽ chia nhánh: Nếu là ca khẩn cấp -> chuyển hướng ngay lập tức; Nếu là yêu cầu thông thường -> đẩy sang AI xử lý.
- **Emergency Response (`set`):** Thiết lập sẵn nội dung phản hồi cấp cứu (Ví dụ: *"CẢNH BÁO: Triệu chứng của bạn có dấu hiệu nguy hiểm. Hãy gọi cấp cứu ngay lập tức!"*).
- **Health Information AI (`openAi`):** 
  - Kết nối `OpenAI API Credentials` của các sếp.
  - Chọn model: `gpt-4-mini`.
  - Cấu hình System Prompt phù hợp để định hướng AI chỉ cung cấp thông tin y tế mang tính tham khảo và luôn nhắc nhở người dùng gặp bác sĩ.
- **Format Health Response & Compile Final Response (`set` & `code`):** Chuẩn hóa lại đầu ra từ AI hoặc nhánh khẩn cấp thành cấu trúc JSON thống nhất gửi về cho người dùng.
- **Send Response (`respondToWebhook`):** Gửi kết quả cuối cùng trả về client đã gọi API.
- **Audit Log (Optional) (`airtable`):** Kết nối tài khoản Airtable nếu muốn lưu vết các câu hỏi của người dùng phục vụ cho việc kiểm tra chất lượng sau này.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một request mẫu bằng Postman hoặc cURL tới Webhook URL để test thử.
- Sau khi test thành công, gạt công tắc sang **Active** để đưa workflow vào trạng thái hoạt động tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat:** Kết nối Webhook này với Telegram Bot, WhatsApp Business hoặc Web Chat Widget trên website của các sếp để người dùng dễ dàng tương tác.
- **Lưu trữ lịch sử thông minh:** Thay vì Airtable, các sếp có thể kết nối với Google Sheets hoặc PostgreSQL để lưu trữ log dài hạn với chi phí tối ưu.
- **Thông báo khẩn cấp:** Mở rộng workflow bằng cách tích hợp thêm node gửi tin nhắn SMS hoặc thông báo qua Slack/Telegram cho đội ngũ trực chăm sóc khách hàng khi phát hiện ca khẩn cấp.

### 📌 Kết luận
Workflow **Medical Symptom Checker & Health Assistant with GPT-4-mini** là một giải pháp mẫu tuyệt vời giúp tự động hóa khâu tư vấn sức khỏe ban đầu, vừa tiết kiệm thời gian, vừa đảm bảo các tiêu chuẩn an toàn y tế cơ bản nhờ cơ chế phát hiện khẩn cấp tự động. Hãy import ngay vào hệ thống n8n của các sếp để nâng cấp trải nghiệm người dùng ngay hôm nay!