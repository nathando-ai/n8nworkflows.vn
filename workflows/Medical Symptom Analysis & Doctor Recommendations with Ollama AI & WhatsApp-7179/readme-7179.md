---
title: "🚀 Xây dựng trợ lý y tế thông minh phân tích triệu chứng & gợi ý bác sĩ với Ollama AI và n8n"
description: "Tự động hóa quy trình phân tích triệu chứng bệnh, đánh giá mức độ khẩn cấp, tìm kiếm bác sĩ chuyên khoa phù hợp và gửi kết quả đa kênh qua WhatsApp và Email."
slug: "tro-ly-y-te-thong-minh-ollama-ai-whatsapp-n8n"
tags: [n8n, automation, no-code, ollama, ai-agent, healthcare]
keywords: [n8n workflow, trợ lý y tế ai, phân tích triệu chứng, ollama ai, whatsapp business api, tự động hóa y tế]
---

# 🚀 Xây dựng trợ lý y tế thông minh phân tích triệu chứng & gợi ý bác sĩ với Ollama AI và n8n

Việc tiếp nhận thông tin, phân loại triệu chứng và tìm kiếm bác sĩ chuyên khoa phù hợp cho bệnh nhân theo cách thủ công thường tốn rất nhiều thời gian, dễ xảy ra sai sót, đặc biệt trong các tình huống cần đánh giá mức độ khẩn cấp. 

Workflow này ra đời nhằm giải quyết triệt để bài toán trên bằng cách ứng dụng AI cục bộ (**Ollama AI**) kết hợp với tự động hóa **n8n**. Hệ thống sẽ tự động phân tích triệu chứng, đánh giá mức độ nguy hiểm, tìm kiếm bác sĩ chuyên khoa qua API và gửi báo cáo chi tiết cho người dùng qua WhatsApp và Email một cách nhanh chóng, chính xác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phân tích thông minh:** AI tự động bóc tách triệu chứng, dự đoán bệnh lý tiềm năng và đánh giá mức độ khẩn cấp (Emergency Detection).
- **Gợi ý chuyên gia:** Tự động tìm kiếm bác sĩ hoặc cơ sở y tế chuyên khoa phù hợp với vị trí của người dùng.
- **Đa kênh tương tác:** Tự động gửi kết quả tư vấn y tế qua WhatsApp và Email ngay lập tức.
- **Hoạt động 24/7:** Quy trình tự động hóa khép kín giúp tiết kiệm thời gian phản hồi và hỗ trợ kịp thời các ca cấp cứu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Khuyến nghị Self-hosted trên VPS).
- **Ollama:** Đã cài đặt và cấu hình model `llama3.2-16000:latest` (hoặc model tương tự) chạy cục bộ hoặc trên server riêng.
- **BetterDoctor API (hoặc tương tự):** Dữ liệu thư mục bác sĩ.
- **WhatsApp Business API:** Tài khoản Meta Developer để gửi tin nhắn tự động.
- **SMTP Email Server:** Cấu hình tài khoản gửi email thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy đoạn mã JSON từ hệ thống.
- Trong giao diện n8n, chọn **Add workflow** -> Nhấp vào biểu tượng ba chấm ở góc trên bên phải -> Chọn **Import from File / Clipboard** và dán dữ liệu vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node quan trọng sau đây để hệ thống vận hành trơn tru:

- **Medical AI Model (`lmChatOllama`):** 
  - Cấu hình thông tin kết nối đến Ollama API.
  - Đảm bảo tên model được thiết lập chính `=llama3.2-16000:latest` hoặc model AI các sếp đang sử dụng trên Ollama.
- **Symptom Input Webhook (`webhook`):** 
  - Lấy URL Endpoint để tích hợp với ứng dụng hoặc form thu thập thông tin triệu chứng của bệnh nhân.
  - Định dạng JSON đầu vào mẫu:
    ```json
    {
      "symptoms": "headache, fever, nausea",
      "age": 30,
      "gender": "male",
      "duration": "2 days",
      "phone": "+1234567890",
      "email": "user@email.com",
      "location": "New York, NY"
    }
    ```
- **Find Doctors (`httpRequest`):** Cấu hình API endpoint và thông tin xác thực để kết nối với dịch vụ tìm kiếm bác sĩ dựa trên vị trí (`location`).
- **Send WhatsApp Response (`httpRequest`):** Kết nối với WhatsApp Business API để gửi tin nhắn tự động đến số điện thoại người bệnh.
- **Send Email Response (`emailSend`):** Chọn thông tin xác thực SMTP (`smtp`) của doanh nghiệp để gửi email kết quả.

#### 3. Kích hoạt ⚡️
- Thực hiện **Test run** bằng cách gửi một POST request với dữ liệu mẫu qua Webhook node để kiểm tra toàn bộ luồng dữ liệu.
- Sau khi kiểm tra không có lỗi phát sinh, gạt công tắc sang chế độ **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ dữ liệu:** Tích hợp thêm node Google Sheets hoặc Airtable để lưu lại lịch sử tư vấn, phục vụ việc phân tích dữ liệu y tế (Analytics).
- **Cảnh báo nhân sự:** Kết nối thêm node Telegram hoặc Slack để gửi thông báo khẩn cấp cho đội ngũ trực tổng đài khi phát hiện ca bệnh nguy hiểm (`Check Emergency`).
- **Cải tiến AI Agent:** Tinh chỉnh Prompt trong AI Symptom Analysis để tuân thủ chặt chẽ hơn các quy chuẩn y tế (HIPAA-compliant data handling).

### 📌 Kết luận
Workflow **Medical Symptom Analysis & Doctor Recommendations** là giải pháp tuyệt vời giúp tự động hóa khâu tiếp nhận và phân tích sơ bộ y tế, mang lại trải nghiệm nhanh chóng, chuyên nghiệp cho người dùng. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa vận hành ngay hôm nay!