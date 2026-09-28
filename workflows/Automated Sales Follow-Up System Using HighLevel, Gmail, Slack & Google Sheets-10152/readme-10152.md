---
title: "🚀 Hệ Thống Theo Dõi Khách Hàng Tự Động (Sales Follow-Up) Với HighLevel, Gmail, Slack & Google Sheets – Tiết Kiệm 20h/Tháng Cho Sales"
description: "Workflow tự động hóa hoàn toàn không cần code giúp các sếp Sales gửi email follow-up tự động, theo dõi phản hồi khách hàng, và thông báo ngay lập tức trên Slack khi có phản hồi tích cực hoặc không phản hồi. Giảm thiểu công việc thủ công, tăng tỷ lệ chuyển đổi và tối ưu hóa quy trình bán hàng."
slug: "automated-sales-follow-up-highlevel-gmail-slack-google-sheets"
tags: [n8n, automation, no-code, sales-follow-up, highlevel, gmail, slack, google-sheets, lead-nurturing]
keywords: [tự động hóa sales, follow-up email tự động, n8n workflow, HighLevel CRM, Slack notification, Gmail automation, Google Sheets log]
---

# 🚀 **Hệ Thống Theo Dõi Khách Hàng Tự Động (Sales Follow-Up) – Giảm 20h Công Việc Thủ Công Cho Đội Sales**

### **Nỗi Đau Của Các Sếp Sales**
Các sếp Sales thường phải mất **giờ đồng hồ** mỗi ngày để:
- **Gửi email follow-up** cho khách hàng chưa phản hồi.
- **Theo dõi email** để biết liệu khách hàng đã trả lời hay chưa.
- **Cập nhật trạng thái** trong CRM (HighLevel) và báo cáo cho team.
- **Nhắc nhở team** khi khách hàng không phản hồi sau nhiều lần gửi email.

Kết quả? **Tỷ lệ chuyển đổi giảm**, **khách hàng mất niềm tin**, và **công việc thủ công chiếm quá nhiều thời gian** mà không mang lại giá trị thực sự.

**Workflow này giải quyết tất cả!** Với **tự động hóa hoàn toàn**, các sếp có thể:
✅ **Gửi email follow-up tự động** sau 24h nếu khách hàng chưa phản hồi.
✅ **Theo dõi phản hồi** và phân loại khách hàng (có phản hồi "Yes" hay không phản hồi).
✅ **Báo cáo ngay lập tức** trên Slack khi có phản hồi tích cực hoặc khách hàng bỏ qua.
✅ **Lưu log tất cả hoạt động** trong Google Sheets để theo dõi và phân tích.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng thay vì dùng phiên bản miễn phí (n8n.cloud).
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao, không lag)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
| **Lợi Ích** | **Chi Tiết** |
|-------------|-------------|
| **Tiết kiệm 20h/tháng** | Không cần phải gửi email thủ công, theo dõi phản hồi, hoặc nhắc nhở team. |
| **Tăng tỷ lệ chuyển đổi** | Khách hàng được theo dõi liên tục, không bị bỏ qua. |
| **Cá nhân hóa tương tác** | Email follow-up được tự động gửi với nội dung phù hợp. |
| **Báo cáo thời gian thực** | Slack thông báo ngay khi có phản hồi, giúp team phản ứng nhanh chóng. |
| **Lưu trữ log toàn diện** | Tất cả hoạt động được ghi lại trong Google Sheets, dễ dàng phân tích. |
| **Hoạt động 24/7** | Không cần phải làm việc vào ban đêm hoặc cuối tuần. |

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản HighLevel** (CRM chứa danh sách khách hàng).
✔ **Tài khoản Gmail** (để gửi email follow-up).
✔ **Tài khoản Slack** (để thông báo phản hồi).
✔ **Google Sheets** (để lưu log lỗi và hoạt động).
✔ **API Keys & Credentials**:
   - **HighLevel OAuth2 API Key** (trong n8n: `highLevelOAuth2Api`).
   - **Gmail OAuth2 API Key** (trong n8n: `gmailOAuth2`).
   - **Slack API Token** (trong n8n: `slackApi`).
   - **Google Sheets OAuth2 API Key** (trong n8n: `googleSheetsOAuth2Api`).

---
:::note[Lưu ý quan trọng]
- **Không cần code**: Workflow đã được thiết kế sẵn, chỉ cần import và cấu hình credentials.
- **Dữ liệu mẫu**: Workflow sẽ lấy dữ liệu từ HighLevel, nên **không cần nhập thủ công**.
- **Thời gian chờ 24h**: Node `Wait` đảm bảo email chỉ được gửi sau 24h nếu khách hàng chưa phản hồi.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
**Cách 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/10152](https://n8n.io/workflows/10152) (chọn **Export as JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

**Cách 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/10152](https://n8n.io/workflows/10152).
2. Trên **n8n Editor**, nhấn **Import** → Chọn **Paste JSON**.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp cần **cấu hình lại các node quan trọng** như sau:

| **Node** | **Cần Chỉnh Sửa Gì?** | **Hướng Dẫn** |
|----------|----------------------|--------------|
| **Fetch Contacts from HighLevel** | Chọn **credentials** là `highLevelOAuth2Api`. | Đảm bảo API Key đã được cấu hình trong **n8n Credentials Manager**. |
| **Log Errors in Google Sheets** | Chọn **Google Sheet** và **Sheet Name** (ví dụ: "Error_Log"). | Tạo một sheet mới trong Google Drive và chia sẻ cho n8n. |
| **Send Follow-Up Email to Contact** | Cấu hình **Gmail OAuth2** và **Subject/Body** email. | Sử dụng **Jinja2 template** để cá nhân hóa email (ví dụ: `{{ $json["name"] }}`). |
| **Wait for 24 Hours** | Thời gian chờ mặc định là 24h (không cần chỉnh). | Nếu muốn thay đổi, chỉnh số giờ trong node `Wait`. |
| **Retrieve Email Thread** | Chọn **Gmail OAuth2** và **Thread ID** (n8n sẽ tự động lấy). | Đảm bảo email được gửi từ cùng tài khoản Gmail. |
| **Notify Sales Team in Slack** | Chọn **Slack Webhook URL** và **Channel** (ví dụ: `#sales-alerts`). | Tạo một channel riêng trong Slack để nhận báo cáo. |

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Execute workflow** (node `manualTrigger`).
   - Kiểm tra **Google Sheets** để xem log lỗi (nếu có).
   - Kiểm tra **Gmail** để xem email follow-up đã được gửi chưa.
   - Kiểm tra **Slack** để xem thông báo phản hồi (nếu có).

2. **Bật Active workflow**:
   - Sau khi test thành công, chuyển **Active** sang **ON**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với AI (LLM) để tự động trả lời**
   - Sử dụng node **n8n-nodes-base.llm** để tự động phân tích email phản hồi và trả lời tự động (ví dụ: nếu khách hàng viết "Tôi muốn biết thêm thông tin", hệ thống tự động gửi link tài liệu).

2. **Lưu log hoạt động vào Google Sheets chi tiết hơn**
   - Thêm cột như **Thời gian gửi email**, **Trạng thái phản hồi**, **Action tiếp theo** để dễ dàng phân tích.

3. **Gửi báo cáo định kỳ cho team**
   - Sử dụng node **Slack** hoặc **Email** để gửi báo cáo hàng tuần về:
     - Số lượng khách hàng đã phản hồi.
     - Số lượng khách hàng chưa phản hồi.
     - Tỷ lệ chuyển đổi.

4. **Tích hợp với Zoom/Calendly để lịch hẹn tự động**
   - Nếu khách hàng phản hồi "Yes", hệ thống tự động tạo lịch hẹn trên Zoom/Calendly và thông báo cho sales.

5. **Sử dụng Sticky Note để ghi chú nội bộ**
   - Node **StickyNote** giúp ghi chú về khách hàng (ví dụ: "Khách hàng này cần ưu tiên vì là lead lớn").

---

### 📌 **Kết Luận**
Workflow **Automated Sales Follow-Up** là **giải pháp hoàn hảo** để các sếp Sales:
✔ **Tiết kiệm thời gian** (không cần làm việc thủ công).
✔ **Tăng tỷ lệ chuyển đổi** (khách hàng được theo dõi liên tục).
✔ **Cải thiện trải nghiệm khách hàng** (email cá nhân hóa, phản hồi nhanh chóng).
✔ **Quản lý team hiệu quả** (báo cáo thời gian thực trên Slack).

**Hãy áp dụng ngay workflow này và xem đội Sales của mình hoạt động như thế nào!**
👉 **[Tải workflow từ n8n.io](https://n8n.io/workflows/10152)** và bắt đầu tự động hóa ngay!

---
**Cần hỗ trợ thêm?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để workflow chạy ổn định 24/7! 🚀