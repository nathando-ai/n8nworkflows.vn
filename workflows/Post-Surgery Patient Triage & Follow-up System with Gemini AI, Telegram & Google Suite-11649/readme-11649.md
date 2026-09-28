---
title: "🏥 **Hệ Thống Triển Khám & Theo Dõi Bệnh Nhân Sau Phẫu Thuật Tự Động Hóa với Gemini AI, Telegram & Google Suite**"
description: "Tự động hóa toàn bộ quy trình theo dõi bệnh nhân sau phẫu thuật từ gửi tin nhắn chăm sóc cá nhân hóa đến phân loại mức độ lo ngại, lịch hẹn tự động và thông báo khẩn cấp cho bác sĩ. Giảm 80% công việc thủ công cho nhân viên y tế!"
slug: "huyen-dong-bien-phap-sau-phau-thuat-ai-telegram-google"
tags: [n8n, automation, no-code, y tế, AI Gemini, Telegram Bot, Google Sheets, Google Calendar, Gmail API]
keywords: [tự động hóa y tế, AI chăm sóc bệnh nhân, Telegram Bot y khoa, Google Sheets tự động hóa, Gemini AI y tế, triển khám sau phẫu thuật tự động]
---

# 🚀 **Hệ Thống Triển Khám & Theo Dõi Bệnh Nhân Sau Phẫu Thuật Tự Động Hóa với AI Gemini**

## **💥 Bệnh nhân sau phẫu thuật cần chăm sóc liên tục, nhưng nhân viên y tế lại bị chìm trong công việc thủ công?**
- **Gửi tin nhắn chăm sóc cá nhân hóa** cho hàng trăm bệnh nhân mỗi ngày?
- **Phân loại mức độ lo ngại** từ tin nhắn Telegram để phản hồi chính xác?
- **Lịch hẹn tự động** cho bệnh nhân có triệu chứng nhẹ, nhưng phải **thông báo khẩn cấp** cho bác sĩ khi có dấu hiệu nghiêm trọng?
- **Gọi điện tự động** cho bác sĩ khi cần xử lý khẩn cấp?

**Workflow này giải quyết tất cả!** Sử dụng **Gemini AI** phân tích tin nhắn bệnh nhân, **Telegram Bot** gửi tin nhắn chăm sóc tự động, và **Google Suite** quản lý lịch hẹn và thông báo khẩn cấp. **Không cần code, chỉ cần cấu hình!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** với độ tin cậy cao, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) để tránh giới hạn của phiên bản Cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao cho AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian** của nhân viên y tế trong việc theo dõi bệnh nhân sau phẫu thuật.
✅ **Chăm sóc cá nhân hóa** với tin nhắn AI động viên dựa trên tình trạng hồi phục.
✅ **Phân loại tự động** mức độ lo ngại (nhẹ/moderate/khẩn cấp) và phản hồi phù hợp.
✅ **Lịch hẹn tự động** cho bệnh nhân có triệu chứng nhẹ, **thông báo khẩn cấp** cho bác sĩ khi cần.
✅ **Gọi điện tự động** (thông qua API VAPI.ai) khi có trường hợp nghiêm trọng.
✅ **Báo cáo tự động** trong Google Sheets để theo dõi tình trạng toàn bộ bệnh nhân.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu trữ dữ liệu bệnh nhân).
2. **Tài khoản Telegram Bot** (để gửi tin nhắn chăm sóc và nhận phản hồi).
3. **API Key Google Gemini** (để AI phân tích tin nhắn bệnh nhân).
4. **Tài khoản Google Calendar** (để lịch hẹn tự động).
5. **Tài khoản Gmail** (để gửi email thông báo khẩn cấp cho bác sĩ).
6. **API Key VAPI.ai** (để gọi điện tự động cho bác sĩ).
7. **VPS n8n** (để chạy workflow 24/7).

---
:::info[CHUẨN BỊ]
- **Google Sheets**: Tạo một bảng với các cột: `PatientName`, `PhoneNumber`, `TelegramID`, `SurgeryDate`, `RecoveryPeriod`, `Status`.
- **Telegram Bot**: Tạo bot trên [@BotFather](https://t.me/BotFather) và lấy **API Token**.
- **Google Gemini API**: Đăng ký tại [Google AI Studio](https://aistudio.google.com/) và lấy **API Key**.
- **Google Calendar & Gmail**: Cung cấp quyền OAuth 2.0 cho n8n.
- **VAPI.ai API Key**: Đăng ký tại [VAPI.ai](https://vapi.ai/) để gọi điện tự động.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/11649](https://n8n.io/workflows/11649) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **36 node** và được chia thành **4 phần chính**:
- **Phần 1: Lấy dữ liệu bệnh nhân từ Google Sheets** (Schedule Trigger + Get row(s) in sheet).
- **Phần 2: Gửi tin nhắn chăm sóc tự động** (Telegram Bot).
- **Phần 3: Phân loại mức độ lo ngại** (Gemini AI + AI Agent).
- **Phần 4: Xử lý phản hồi** (Lịch hẹn, gọi điện, thông báo khẩn cấp).

##### **🔹 Cấu hình quan trọng trong workflow:**
| **Node** | **Lưu ý cấu hình** |
|----------|---------------------|
| **Schedule Trigger** | Đặt lịch chạy hàng ngày (ví dụ: 9h sáng). |
| **Get row(s) in sheet** | Chọn **Google Sheets OAuth 2.0** và **Sheet Name** (ví dụ: "Bệnh nhân sau phẫu thuật"). |
| **Telegram Trigger** | Chọn **Telegram API** và **Chat ID** của bot. |
| **Google Gemini Chat Model** | Điền **API Key** từ Google AI Studio. |
| **AI Agent** | Cấu hình **Prompt** để AI phân loại mức độ lo ngại (low/moderate/high). |
| **Google Calendar Tool** | Chọn **Google Calendar OAuth 2.0** và **Event Name** (ví dụ: "Lịch hẹn kiểm tra"). |
| **Gmail Tool** | Chọn **Gmail OAuth 2.0** và cấu hình **Email Template** cho thông báo khẩn cấp. |
| **HTTP Request (VAPI.ai)** | Điền **API Key** và **Phone Number** để gọi điện tự động. |

##### **🔹 Cấu hình AI Agent (Phân loại mức độ lo ngại)**
- **Prompt mẫu**:
  ```
  Analyze the patient's message and classify the concern level (low, moderate, high).
  If the message contains keywords like "pain," "dizziness," or "bleeding," classify as high.
  If the message is general (e.g., "How am I doing?"), classify as low.
  Return the result in JSON format: {"concern_level": "low/moderate/high", "response": "..."}.
  ```

##### **🔹 Cấu hình Switch Case (Phản hồi tự động)**
- **Low Concern**: Gửi tin nhắn động viên + lịch hẹn tự động.
- **Moderate Concern**: Gửi tin nhắn khuyến nghị + lịch hẹn.
- **High Concern**: Gọi điện tự động + email thông báo cho bác sĩ.

#### **3. Kích hoạt ⚡️**
1. **Test Run**: Chạy thử với **1-2 bệnh nhân mẫu** để kiểm tra logic.
2. **Active Workflow**: Bật chế độ **Active** sau khi kiểm tra thành công.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm tính năng nhắc nhở** cho bác sĩ trước khi gọi điện (sử dụng **Google Calendar Alerts**).
2. **Lưu log tất cả tin nhắn** trong Google Sheets để theo dõi lịch sử.
3. **Kết nối với CRM y tế** (như **Zoho One** hoặc **Meditech**) để đồng bộ hóa dữ liệu.
4. **Tự động gửi báo cáo hàng tuần** cho quản lý bằng **Gmail + Google Sheets**.
5. **Thêm tính năng chatbot 24/7** cho bệnh nhân (sử dụng **n8n + Telegram Bot**).

---
### 📌 **Kết luận**
**Workflow này không chỉ tiết kiệm thời gian mà còn cải thiện chất lượng chăm sóc bệnh nhân sau phẫu thuật!**
- **Bệnh nhân** nhận được **chăm sóc cá nhân hóa** và **phản hồi nhanh chóng**.
- **Nhân viên y tế** được **giải phóng** khỏi công việc thủ công.
- **Bác sĩ** được **thông báo kịp thời** khi có trường hợp khẩn cấp.

**Hãy áp dụng ngay và biến quy trình y tế của bạn thành tự động hóa!** 🚀
👉 **[Tải workflow ngay](https://n8n.io/workflows/11649)** và **cài đặt VPS n8n** để bắt đầu!

---
**💬 Cần hỗ trợ?** Đăng ký **hỗ trợ chuyên nghiệp** từ **Pixcels Themes** tại [pixcels.themes](https://pixcels.themes) để tối ưu hóa workflow!