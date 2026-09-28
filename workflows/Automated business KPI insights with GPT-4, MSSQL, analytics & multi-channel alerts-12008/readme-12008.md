---
title: "🚀 Tự Động Hóa Báo Cáo KPI Doanh Nghiệp với AI GPT-4, MSSQL & Cảnh Báo Multi-Channel (WhatsApp/Email)"
description: "Workflow tự động hóa thu thập dữ liệu từ MSSQL, Google Analytics, Google Sheets và phân tích KPI doanh nghiệp bằng AI GPT-4, sau đó gửi báo cáo và cảnh báo thông minh qua WhatsApp/Email. Giúp các sếp tiết kiệm 10+ giờ/tuần và đưa ra quyết định dựa trên dữ liệu thực thời."
slug: "tự-dộng-hoa-kpi-doanh-nghiệp-ai-gpt-4"
tags: [n8n, automation, ai-chatbot, business-intelligence, mssql, google-analytics, gpt-4, no-code]
keywords: [n8n workflow KPI, tự động hóa báo cáo doanh nghiệp, AI phân tích dữ liệu, cảnh báo WhatsApp Email, GPT-4 tự động hóa]
---

# 🚀 **Tự Động Hóa Báo Cáo KPI Doanh Nghiệp với AI GPT-4, MSSQL & Cảnh Báo Multi-Channel**

### **Giải pháp cho các sếp muốn:**
- **Tiết kiệm 10+ giờ/tuần** viết báo cáo thủ công.
- **Nhận báo cáo KPI chính xác** từ dữ liệu MSSQL, Google Analytics và chi phí marketing.
- **Được AI GPT-4 tổng hợp** những insight quan trọng và cảnh báo nguy cơ/ cơ hội.
- **Nhận cảnh báo thông minh** qua WhatsApp, Email (không cần Slack).

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động hóa 100%**: Không cần viết code hoặc sử dụng Excel thủ công.
✅ **Dữ liệu chính xác**: Thu thập từ MSSQL, Google Analytics và Google Sheets.
✅ **AI phân tích sâu**: GPT-4 tự động tổng hợp báo cáo và cảnh báo nguy cơ.
✅ **Cảnh báo multi-channel**: Nhận thông báo qua WhatsApp (Twilio) hoặc Email.
✅ **Hoạt động 24/7**: Chạy tự động hàng ngày, không cần can thiệp.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
- **MSSQL Database**: Trả về dữ liệu doanh thu, số lượng người dùng mới và tổng người dùng.
- **Google Analytics Account**: API OAuth2 để lấy dữ liệu traffic.
- **Google Sheets**: Dữ liệu chi phí marketing (cần cấu hình sheet với định dạng phù hợp).
- **OpenAI API Key**: Để sử dụng GPT-4.1-mini (hoặc thay thế bằng Gemini).
- **Twilio WhatsApp API** (hoặc SMTP cho Email): Để gửi cảnh báo.
- **n8n Self-hosted**: Để workflow chạy ổn định 24/7 (không dùng phiên bản cloud).
:::

---
## 🎯 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/12008](https://n8n.io/workflows/12008) hoặc copy JSON từ link trên.
- **Mở n8n Editor** → Nhấn **Import Workflow** → Dán JSON và nhấn **Import**.

### **2. Các bước cấu hình BẮT BUỘC**
#### **A. Cấu hình Credentials (Tài khoản API)**
| **Node**               | **Credentials cần thiết**       | **Hướng dẫn**                                                                 |
|------------------------|----------------------------------|-------------------------------------------------------------------------------|
| **MSSQL**              | `microsoftSql`                   | Thêm connection mới trong **n8n Credentials** → Chọn **Microsoft SQL** → Điền server, database, username, password. |
| **Google Analytics**   | `googleAnalyticsOAuth2`          | Tạo OAuth2 trong Google Cloud Console → Cấu hình trong n8n.                   |
| **Google Sheets**      | `googleApi`                      | Tạo OAuth2 trong Google Cloud Console → Chọn scope `https://www.googleapis.com/auth/spreadsheets.readonly`. |
| **OpenAI (GPT-4)**     | `openAiApi`                      | Tạo API Key tại [OpenAI](https://platform.openai.com/) → Điền vào credentials. |
| **WhatsApp (Twilio)**  | `whatsAppApi`                    | Tạo API Key tại [Twilio](https://www.twilio.com/) → Cấu hình trong n8n.       |
| **Email (SMTP)**       | `smtp`                           | Thêm SMTP của Gmail/Outlook → Cấu hình host, port, username, password.       |

#### **B. Cấu hình Query SQL (MSSQL)**
- **Yesterday's Revenue**:
  ```sql
  SELECT SUM(amount) AS total_revenue FROM sales WHERE date = DATEADD(day, -1, GETDATE());
  ```
- **Yesterday's Registered Users**:
  ```sql
  SELECT COUNT(*) AS new_users FROM users WHERE registration_date = DATEADD(day, -1, GETDATE());
  ```
- **Yesterday's Total Users**:
  ```sql
  SELECT COUNT(*) AS total_users FROM users;
  ```

#### **C. Cấu hình Google Sheets (Chi phí Marketing)**
- **Sheet Name**: Đặt tên sheet là `Marketing_Expenses`.
- **Range**: `Sheet1!A2:B100` (cột A: Ngày, cột B: Chi phí).

#### **D. Cấu hình AI (GPT-4)**
- **Prompt mẫu** (có thể tùy chỉnh):
  ```
  Analyze the following business metrics and provide a concise summary with key insights:
  - Revenue: {{ $json["revenue"] }}
  - New Users: {{ $json["new_users"] }}
  - Total Users: {{ $json["total_users"] }}
  - Marketing Spend: {{ $json["marketing_spend"] }}
  Highlight any risks or opportunities.
  ```

#### **E. Cấu hình Cảnh báo (WhatsApp/Email)**
- **WhatsApp**: Điền số điện thoại và API Key Twilio.
- **Email**: Điền địa chỉ email và SMTP.

---
### **3. Kích hoạt ⚡️**
- **Test Run**: Nhấn **Run Workflow** với dữ liệu mẫu để kiểm tra.
- **Bật Active**: Sau khi kiểm tra thành công, nhấn **Active** để workflow chạy tự động hàng ngày.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[TIPS THỰC TIỆN]
🔹 **Thay đổi lịch chạy**: Thay `scheduleTrigger` từ `0 0 * * *` (hàng ngày) thành `0 8 * * *` (8h sáng) nếu muốn báo cáo vào buổi sáng.
🔹 **Thêm Slack/Telegram**: Thay thế node `whatsApp` bằng `slack` hoặc `telegramBot`.
🔹 **Lưu log**: Thêm node `stickyNote` để lưu lịch sử báo cáo.
🔹 **Báo cáo định kỳ**: Sử dụng `emailSend` để gửi báo cáo tuần/month.
🔹 **Tùy chỉnh AI**: Thay đổi prompt trong `lmChatOpenAi` để phù hợp với ngành nghề.
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc viết báo cáo thủ công, đồng thời **cung cấp dữ liệu chính xác** từ nhiều nguồn khác nhau. Với **AI GPT-4**, bạn sẽ nhận được **báo cáo tổng hợp và cảnh báo nguy cơ** một cách tự động, giúp đưa ra quyết định nhanh chóng.

🚀 **Hãy áp dụng ngay** và tiết kiệm **10+ giờ/tuần** cho công ty!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Liên hệ tác giả**: [n8n.abubakkar@gmail.com](mailto:n8n.abubakkar@gmail.com) (Mohamed Abubakkar - Full Stack Developer chuyên tự động hóa AI).