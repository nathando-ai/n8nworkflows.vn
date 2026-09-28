---
title: "🚀 Xây dựng Trợ lý Bất động sản AI trên LINE với Google Gemini và n8n"
description: "Tự động phản hồi khách hàng bất động sản trên LINE bằng AI Gemini, phân loại nhu cầu, lưu Google Sheets và cảnh báo khách VIP cho sales."
slug: "tu-dong-hoa-bat-dong-san-line-gemini-n8n"
tags: [n8n, automation, ai-chatbot, line-bot, google-gemini, real-estate]
keywords: [n8n workflow, line real estate chatbot, google gemini ai, tu dong hoa bat dong san, line messaging api]
keywords: [n8n workflow, line real estate chatbot, google gemini ai, tu dong hoa bat dong san, line messaging api]
---

# 🚀 Xây dựng Trợ lý Bất động sản AI trên LINE với Google Gemini và n8n

Việc quản lý và phản hồi tin nhắn của khách hàng quan tâm đến bất động sản trên LINE thủ công thường tốn rất nhiều thời gian, dễ bỏ sót khách hàng tiềm năng lớn. Khách hàng hỏi về giá, diện tích, số phòng nhưng nếu nhân viên sales trả lời chậm, họ có thể tìm đến đối thủ.

Workflow n8n này sẽ giúp các sếp giải quyết triệt để bài toán trên bằng cách tự động hóa 100% quy trình: nhận tin nhắn từ LINE, dùng **Google Gemini AI** tư vấn chuyên nghiệp, lưu thông tin vào Google Sheets, đồng thời tự động lọc khách hàng giá trị cao (High-value leads) để gửi email cảnh báo ngay lập tức cho đội ngũ sales.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản hồi tức thì 24/7:** Khách nhắn tin trên LINE là AI trả lời ngay lập tức bằng văn phong chuyên nghiệp (Kigo/K-go tiếng Nhật hoặc tiếng Việt tùy cấu hình).
- **Phân loại nhu cầu thông minh:** Tự động trích xuất ngân sách, số phòng, khu vực và phân loại nhu cầu (thuê/mua/xem nhà).
- **Không bỏ sót khách VIP:** Tự động nhận diện khách hàng có ý định mua hoặc ngân sách lớn để gửi email báo động đỏ cho đội ngũ sale chốt đơn.
- **Quản lý data tập trung:** Mọi cuộc trò chuyện và nhu cầu khách hàng đều được lưu trữ tự động vào Google Sheets để remarketing.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **LINE Official Account & Messaging API:** Lấy được Channel Access Token.
- **Google Gemini API Key:** Để kết nối với mô hình AI LLM.
- **Google Sheets:** File Google Sheets chuẩn bị sẵn các cột lưu thông tin khách hàng.
- **SMTP Server / Email:** Để gửi cảnh báo cho bộ phận sales (Gmail, SendGrid, Resend...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này và dán trực tiếp vào n8n Editor (hoặc import file JSON).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 9 nodes chính hoạt động nhịp nhàng. Các sếp cần cấu hình kỹ các điểm sau:

- **LINE Webhook:** Đặt đường dẫn Webhook path (`line-realestate-webhook`) và cấu hình URL này lên LINE Developer Console.
- **Parse LINE Message & Process AI Response (Code Nodes):** Xử lý trích xuất dữ liệu JSON từ tin nhắn LINE và định dạng lại độ dài câu trả lời (giới hạn dưới 200 ký tự phù hợp cho khung chat LINE).
- **Google Gemini Chat Model & AI Property Advisor:** Kết nối tài khoản Google Gemini Credentials, chọn model (khuyên dùng `Gemini 1.5 Flash`) và viết system prompt định hướng AI trở thành chuyên viên tư vấn bất động sản chuyên nghiệp.
- **Log to Google Sheets:** Chọn kết nối Google Sheets tài khoản của bạn, trỏ tới file Sheet quản lý lead và map các trường dữ liệu (Tên, Ngân sách, Nhu cầu, AI Response).
- **High-Value Lead Check (If Node):** Thiết lập điều kiện lọc (Ví dụ: `Nhu cầu = Mua` HOẶC `Ngân sách > 30,000,000 JPY/VNĐ`).
- **Send LINE Reply (HTTP Request):** Cấu hình gọi API của LINE để gửi câu trả lời của AI ngược lại thiết bị của khách hàng. Sử dụng Header chứa Bearer Token là LINE Channel Access Token.
- **Send Sales Alert (Email Send):** Điền thông tin SMTP của bạn để nhận email thông báo ngay khi có khách hàng VIP xuất hiện qua bộ lọc ở trên.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một tin nhắn test trên LINE OA của bạn để kiểm tra luồng chạy từ đầu đến cuối.
- Kiểm tra xem Google Sheets đã nhận dòng dữ liệu mới chưa và LINE có nhận lại phản hồi từ AI không.
- Bật công tắc **Active** để đưa bot vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Thay vì chỉ nhận email qua node `Send Sales Alert`, các sếp có thể đổi thành node Telegram/Slack để bắn thông báo chuông reo "ting ting" trực tiếp vào group chat của sales.
- **Lưu lịch sử chat:** Kết nối thêm một bảng Google Sheets phụ hoặc cơ sở dữ liệu (PostgreSQL/Supabase) để lưu toàn bộ lịch sử trò chuyện (chat history), giúp AI có ngữ cảnh (memory) thông minh hơn trong các lần nhắn tin tiếp theo.
- **Đa ngôn ngữ:** Tùy biến prompt của Gemini để bot có thể phục vụ cả khách nước ngoài (tiếng Anh, tiếng Nhật, tiếng Việt) tùy theo thị trường bất động sản của doanh nghiệp.

### 📌 Kết luận
Tự động hóa chăm sóc khách hàng bất động sản trên LINE chưa bao giờ dễ dàng và tối ưu chi phí đến thế. Hãy triển khai ngay workflow này để giải phóng thời gian cho đội ngũ CSKH và không bỏ lỡ bất kỳ khách hàng tiềm năng nào!