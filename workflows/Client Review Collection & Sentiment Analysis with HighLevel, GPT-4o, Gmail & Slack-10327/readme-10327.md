---
title: "🚀 Tự Động Hóa Thu Thập & Phân Tích Sentiment Đánh Giá Khách Hàng với HighLevel, GPT-4o, Gmail & Slack (N8N)"
description: "Workflow tự động hóa hoàn toàn không code giúp các sếp thu thập đánh giá khách hàng sau khi giao dịch thành công trên HighLevel CRM, tự động gửi email yêu cầu đánh giá cá nhân hóa, phân tích tình cảm phản hồi, và báo cáo kết quả lên Slack. Tiết kiệm thời gian lên đến 80% trong quản lý CSAT."
slug: "tieu-dong-hoa-thu-thap-danh-gia-khach-hang-highlevel-gpt-4o"
tags: [n8n, automation, crm, ai-multimodal, gpt-4o, highlevel, google-sheets, slack, gmail]
keywords: [tự động hóa đánh giá khách hàng, n8n workflow crm, phân tích sentiment với gpt-4o, tự động gửi email đánh giá, báo cáo feedback slack]
---

# 🚀 **Tự Động Hóa Thu Thập & Phân Tích Sentiment Đánh Giá Khách Hàng với AI**

### **Giải pháp cho nỗi đau "Quên gửi email đánh giá" và "Không biết khách hàng nghĩ gì về dịch vụ"**
Các sếp đã bao giờ phải:
- **Gõ tay email yêu cầu đánh giá** cho từng khách hàng sau khi giao dịch thành công?
- **Chờ đợi phản hồi** trong nhiều ngày mà không biết tình cảm thực sự của khách hàng?
- **Phải tra cứu thủ công** trên Gmail để tổng hợp feedback?
- **Mất thời gian** để phân tích sentiment và báo cáo cho team?

Workflow này **tự động hóa toàn bộ quy trình** từ thu thập đánh giá đến phân tích tình cảm, giúp các sếp **tiết kiệm 80% thời gian** và **cải thiện trải nghiệm khách hàng** một cách thông minh.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy 24/7 với hiệu suất tối ưu, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo ổn định cho AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động gửi email yêu cầu đánh giá** cá nhân hóa (HTML) sau mỗi giao dịch thành công trên HighLevel.
✅ **Phân tích sentiment** phản hồi khách hàng bằng GPT-4o, phân loại thành **Tích cực/Trung lập/Xấu**.
✅ **Báo cáo tự động** lên Slack với tổng hợp feedback, giúp team **quản lý CSAT hiệu quả**.
✅ **Ghi log lỗi** vào Google Sheets để **debug nhanh chóng** khi workflow gặp vấn đề.
✅ **Hoạt động liên tục** 24/7, không phụ thuộc vào nhân viên.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản & API Key**:
   - **HighLevel CRM** (để lấy danh sách giao dịch "Won").
   - **Azure OpenAI** (để sử dụng GPT-4o).
   - **Gmail** (để gửi email và lấy phản hồi).
   - **Slack** (để báo cáo kết quả).
   - **Google Sheets** (để ghi log lỗi).
2. **Thông tin cấu hình**:
   - **ID Sheet Google** (để ghi log lỗi).
   - **Channel/Người dùng Slack** (để báo cáo feedback).
   - **Email mẫu** (nếu muốn thay đổi nội dung email).
   - **Link đánh giá Google** (cần thay đổi theo domain của công ty).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/10327](https://n8n.io/workflows/10327) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và **paste** vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **12 node**, các sếp cần chú ý cấu hình sau:

##### **A. Cấu hình Credentials (Bắt buộc)**
| Node | Credential | Ghi chú |
|------|------------|---------|
| **Fetch All Won Deals from HighLevel** | `highLevelOAuth2Api` | API Key từ HighLevel (tạo ở **Settings > API Access**). |
| **Send Review Request Email to Client** | `gmailOAuth2` | OAuth 2.0 từ Gmail (cần **Enable Less Secure Apps** nếu dùng Gmail cá nhân). |
| **Configure GPT-4o Model** | `azureOpenAiApi` | API Key từ Azure OpenAI (đăng ký tại [Azure Portal](https://portal.azure.com/)). |
| **Announce Review Summary in Slack** | `slackApi` | Token từ Slack (tạo ở **Apps > Create App > Basic Information**). |
| **Log Errors in Google Sheets** | `googleSheetsOAuth2Api` | OAuth 2.0 từ Google (cần **Share Sheet** với email n8n). |

##### **B. Cấu hình cụ thể các node quan trọng**
1. **`Fetch All Won Deals from HighLevel`**
   - **Operation**: `getAll`
   - **Resource**: `opportunity`
   - **Filter**: `status = "won"` (n8n sẽ tự động lấy giao dịch mới).

2. **`Generate Personalized Review Request Email (AI)`**
   - **Agent Prompt**: Workflow đã cấu hình sẵn, **không cần chỉnh sửa** trừ khi muốn thay đổi nội dung email.
   - **Input**: Dữ liệu từ HighLevel (tên khách hàng, email, nội dung giao dịch).
   - **Output**: Email HTML cá nhân hóa (có link đánh giá Google và form feedback nội bộ).

3. **`Send Review Request Email to Client`**
   - **From Email**: Điền email từ Gmail (ví dụ: `no-reply@congty.com`).
   - **Subject**: Cấu hình mặc định là **"Thanks for choosing us! We’d love your feedback"**.
   - **HTML Body**: Sử dụng output từ node AI.

4. **`Wait for 24 Hours Before Next Action`**
   - Thời gian chờ **24 giờ** để khách hàng có thời gian phản hồi.

5. **`Summarize Client Feedback (AI)`**
   - **Agent Prompt**: Phân tích sentiment và tổng hợp phản hồi.
   - **Input**: Nội dung email thread từ Gmail.
   - **Output**: Báo cáo Slack với format:
     ```
     📌 **Feedback từ [Tên Khách Hàng]**
     - **Tình cảm**: [Tích cực/Trung lập/Xấu]
     - **Nội dung chính**: [Tóm tắt phản hồi]
     - **Link phản hồi**: [Đường link đánh giá Google]
     ```

6. **`Log Errors in Google Sheets`**
   - **Sheet ID**: Điền ID của sheet đã chia sẻ với n8n.
   - **Tab Name**: Cấu hình mặc định là **"Error Log"**.
   - **Columns**: `Timestamp`, `Error Type`, `Details`.

##### **C. Kích hoạt ⚡️**
1. **Test Run** với một giao dịch mẫu:
   - Chọn **Execute workflow** và nhập **ID giao dịch "Won"** từ HighLevel.
   - Kiểm tra:
     - Email đã gửi thành công?
     - Slack có báo cáo feedback không?
     - Google Sheets có ghi log lỗi (nếu có) không?
2. **Bật Active**:
   - Sau khi test thành công, **bật workflow** và **lưu lại**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Zapier/Make**:
   - Nếu HighLevel không hỗ trợ API, có thể lấy dữ liệu từ **Zapier** và chuyển sang n8n.

2. **Tự động hóa định kỳ**:
   - Sử dụng **n8n Trigger** (n8n v1.0+) để chạy workflow **mỗi ngày** thay vì manual.

3. **Lưu log chi tiết hơn**:
   - Thêm node **`stickyNote`** để lưu **tất cả phản hồi khách hàng** vào Google Sheets.

4. **Báo cáo định kỳ cho CEO**:
   - Sử dụng **Google Sheets + Apps Script** để tự động tạo **báo cáo CSAT hàng tháng**.

5. **Cải thiện email với AI**:
   - Thay đổi **prompt của agent** để email trở nên **cá nhân hóa hơn** (ví dụ: nhắc lại chi tiết giao dịch).

---

### 📌 **Kết luận**
Workflow này **giải phóng các sếp** khỏi công việc thủ công, **tăng cường trải nghiệm khách hàng** và **cung cấp dữ liệu phân tích sentiment** một cách tự động. **Bắt đầu ngay** với các bước trên và **tăng hiệu suất team CRM** lên gấp đôi!

👉 **Bấm vào [n8n.io/workflows/10327](https://n8n.io/workflows/10327) để tải workflow ngay!**
👉 **Cần hỗ trợ cấu hình?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) và liên hệ team hỗ trợ!

---
**#TựĐộngHóa #N8N #CRM #AI #GPT4o #Slack #GoogleSheets**