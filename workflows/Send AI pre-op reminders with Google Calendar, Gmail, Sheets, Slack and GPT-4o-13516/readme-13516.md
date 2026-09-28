---
title: "🚀 Hệ Thống Nhắc Nhở Trước Phẫu Thuật AI Tự Động: Gửi Email, Google Calendar, Sheets & Slack (GPT-4o)"
description: "Tự động hóa nhắc nhở chuẩn bị trước phẫu thuật cho bệnh nhân với email cá nhân hóa, theo dõi xác nhận tự động, và cảnh báo Slack cho y bác sĩ khi bệnh nhân không phản hồi. Giảm thiểu việc bỏ qua, tăng cường sẵn sàng và giảm rủi ro cho cả bệnh nhân và đội ngũ y tế."
slug: "ai-pre-op-reminder-n8n"
tags: [n8n, tự động hóa y tế, AI chatbot, Google Calendar, Gmail, Google Sheets, Slack, GPT-4o, workflow tự động]
keywords: [n8n tự động hóa y tế, nhắc nhở trước phẫu thuật AI, GPT-4o trong y tế, tự động hóa nhắc nhở bệnh nhân, workflow Google Calendar Gmail Sheets Slack]
---

# 🚀 **Hệ Thống Nhắc Nhở Trước Phẫu Thuật AI Tự Động: Từ Email Cá Nhân Hóa Đến Cảnh Báo Slack**

### **Giải quyết vấn đề gì?**
Các bác sĩ và nhân viên y tế thường phải mất thời gian thủ công để nhắc nhở bệnh nhân chuẩn bị trước phẫu thuật, theo dõi xác nhận, và xử lý trường hợp bỏ qua. **Workflow này tự động hóa toàn bộ quy trình:**
- **Gửi email nhắc nhở** với danh sách chuẩn bị trước phẫu thuật (ăn nhẹ, mang hồ sơ, đến sớm) **cá nhân hóa** bằng AI (GPT-4o).
- **Tạo liên kết xác nhận duy nhất** cho mỗi bệnh nhân, theo dõi hành vi click.
- **Cập nhật trạng thái xác nhận** tự động vào Google Sheets.
- **Cảnh báo Slack** cho y bác sĩ khi bệnh nhân **không phản hồi** trong thời gian quy định.
- **Giảm thiểu rủi ro** bằng cách đảm bảo tất cả bệnh nhân đều sẵn sàng trước khi phẫu thuật.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhắc nhở thủ công hàng ngày.
- **Chính xác cao**: AI tự động tạo email phù hợp với từng loại phẫu thuật.
- **Theo dõi tự động**: Xác nhận bệnh nhân được ghi lại trong Google Sheets.
- **Cảnh báo kịp thời**: Slack thông báo ngay khi có bệnh nhân bỏ qua.
- **Giảm rủi ro**: Đội ngũ y tế có thời gian tập trung vào việc chăm sóc thực tế.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Calendar** (để lấy danh sách phẫu thuật hàng ngày).
2. **API Key Azure OpenAI** (để sử dụng GPT-4o tạo email AI).
3. **Tài khoản Gmail** (để gửi email nhắc nhở).
4. **Google Sheets** (để lưu trạng thái xác nhận bệnh nhân).
5. **Slack Workspace** (để cảnh báo khi bệnh nhân không phản hồi).
6. **Liên kết Google OAuth** cho tất cả dịch vụ trên.
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13516](https://n8n.io/workflows/13516) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON → Chọn **"Import"**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **16 node**, mỗi node đều quan trọng. Dưới đây là hướng dẫn chi tiết:

#### **A. Cấu hình Credentials (Bắt buộc)**
| Node | Yêu cầu cấu hình |
|------|------------------|
| **Google Calendar** | OAuth2 (thiết lập trong **n8n Credentials** → **Google Calendar OAuth2Api**) |
| **Azure OpenAI (GPT-4o)** | API Key (thiết lập trong **n8n Credentials** → **azureOpenAiApi**) |
| **Gmail** | OAuth2 (thiết lập trong **n8n Credentials** → **gmailOAuth2**) |
| **Google Sheets** | OAuth2 (thiết lập trong **n8n Credentials** → **googleSheetsOAuth2Api**) |
| **Slack** | Token (thiết lập trong **n8n Credentials** → **slackApi**) |

#### **B. Cấu hình cụ thể cho các node quan trọng**
1. **`Schedule Trigger: Daily 9:00 AM`**
   - Đảm bảo **timezone** phù hợp với khu vực hoạt động của bệnh viện.
   - *Lưu ý*: Nếu muốn thay đổi giờ, chỉnh trong **keyParameters** của node này.

2. **`Google Calendar: Fetch Today’s Events`**
   - Chọn **Google Calendar OAuth2Api** trong **Credentials**.
   - Kiểm tra **scope** đã bao gồm `calendar.readonly` (nếu chưa, thêm vào trong **OAuth Consent Screen** của Google Cloud).

3. **`AI: Generate Pre-Op Checklist Email` (Agent Node)**
   - **Prompt Template**: Workflow đã định sẵn template, nhưng các sếp có thể **cập nhật** trong **`lmChatAzureOpenAi`** node để phù hợp với quy trình của bệnh viện.
   - *Ví dụ*: Thêm thông tin về **thời gian đến sớm**, **drugs cần ngừng**, hoặc **hồ sơ bắt buộc**.

4. **`Webhook: Patient Checklist Confirmation`**
   - **Path**: Đặt là `/confirm` (không thay đổi).
   - **Method**: Chọn **GET**.
   - *Lưu ý*: Sau khi bệnh nhân click liên kết, workflow sẽ **cập nhật trạng thái** trong Google Sheets.

5. **`Google Sheets: Upsert Patient Confirmation Status`**
   - Chọn **Sheet Name** phù hợp (ví dụ: `"Pre-Op Confirmations"`).
   - **Range**: Đặt là `A1:Z` (hoặc tùy chỉnh theo cột bạn sử dụng).
   - *Lưu ý*: Cột `patient_id` và `confirmedAt` **bắt buộc** để workflow hoạt động.

6. **`IF: Confirmed = true`**
   - Kiểm tra **logic** trong node này để đảm bảo chỉ **bệnh nhân chưa xác nhận** mới được cảnh báo Slack.

7. **`Slack: Alert Nurse/Owner`**
   - Chọn **channel** phù hợp (ví dụ: `#pre-op-alerts`).
   - **Message Template**: Workflow đã định sẵn, nhưng các sếp có thể **cập nhật** để bao gồm:
     - Tên bệnh nhân.
     - Thời gian phẫu thuật.
     - Loại phẫu thuật.
     - Liên kết Google Calendar (nếu cần).

#### **C. Test Run & Kích hoạt ⚡️**
1. **Chạy thử (Test Run)** với **1-2 bệnh nhân mẫu** để kiểm tra:
   - Email có được gửi không?
   - Liên kết xác nhận có hoạt động không?
   - Slack có cảnh báo khi bỏ qua không?
2. **Bật Active** sau khi kiểm tra thành công.

---
## ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm SMS Reminder**
   - Kết hợp với **Twilio** hoặc **Google Voice** để gửi SMS nhắc nhở cho bệnh nhân không phản hồi email.

2. **Nâng cao Logic Cảnh Báo Slack**
   - Thêm **thông tin chi tiết** như:
     - **Lịch sử xác nhận** (nếu bệnh nhân đã bỏ qua nhiều lần).
     - **Yêu cầu đặc biệt** (ví dụ: bệnh nhân có bệnh tiểu đường cần nhắc nhở đặc biệt).

3. **Tự động Gửi Báo Cáo Hàng Tuần**
   - Sử dụng **node `scheduleTrigger`** để chạy hàng tuần và gửi báo cáo tổng hợp:
     - Tỷ lệ xác nhận.
     - Danh sách bệnh nhân chưa xác nhận.
     - *Cách làm*: Thêm **node `gmail`** hoặc **`slack`** để gửi báo cáo tự động.

4. **Kết hợp với CRM Y Tế**
   - Nếu sử dụng **Epic, Meditech, hoặc hệ thống CRM y tế khác**, có thể **pull dữ liệu bệnh nhân** từ đó thay vì Google Calendar.

5. **Lưu Log Tất Cả Hoạt Động**
   - Thêm **node `stickyNote`** để ghi lại:
     - Thời gian gửi email.
     - Trạng thái xác nhận.
     - Lỗi nếu có.

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho đội ngũ y tế bằng cách tự động hóa quy trình nhắc nhở trước phẫu thuật, từ **gửi email AI** đến **cảnh báo Slack** khi có bệnh nhân bỏ qua. **Đặc biệt phù hợp** cho:
- **Bệnh viện đa khoa** cần quản lý hàng trăm ca phẫu thuật hàng ngày.
- **Phòng khám chuyên khoa** muốn giảm thiểu rủi ro trước phẫu thuật.
- **Đội ngũ y tế** muốn tập trung vào chăm sóc chứ không phải quản lý nhắc nhở.

**👉 Hãy import workflow ngay và tự động hóa quy trình của mình!**
Nếu có vấn đề, **hãy comment bên dưới** hoặc liên hệ với cộng đồng n8n Việt Nam trên [Facebook](https://facebook.com/groups/n8nvietnam) để hỗ trợ.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**#TựĐộngHóaYTế #n8nViệtNam #AITrongYTế**