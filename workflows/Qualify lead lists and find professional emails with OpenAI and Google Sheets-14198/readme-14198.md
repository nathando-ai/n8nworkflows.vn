---
title: "🚀 Tự Động Hóa Xác Minh Lead & Tìm Email Nghiệp Dụng Với OpenAI & Google Sheets (Không Cần Code)"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp Sales/Marketing tự động hóa việc xác minh danh sách lead, tìm kiếm email chuyên nghiệp bằng AI, và phân loại thành lead chất lượng (có email) và lead không chất lượng (không có email) chỉ trong vài phút. Giúp tiết kiệm thời gian lên đến 80% so với cách làm thủ công."
slug: "tieu-dong-hoa-xac-minh-lead-tim-email-nghiep-dung"
tags: [n8n, automation, lead-generation, ai-summarization, google-sheets, openai, no-code]
keywords: [n8n workflow lead generation, tự động hóa xác minh lead, tìm email chuyên nghiệp bằng AI, Google Sheets tự động hóa, OpenAI API tự động hóa, Sales automation]
---

# 🚀 **Tự Động Hóa Xác Minh Lead & Tìm Email Nghiệp Dụng Với OpenAI & Google Sheets**

### **🔥 Nỗi Đau Của Các Sếp Sales/Marketing**
Các sếp thường phải mất **giờ đồng hồ** để:
- **Tìm kiếm email** của lead từ LinkedIn, website công ty hoặc thông tin công khai.
- **Xác minh tính chính xác** của email (nhiều email fake hoặc không hoạt động).
- **Phân loại lead** thành chất lượng và không chất lượng (có email vs không có email).
- **Cập nhật dữ liệu** vào Google Sheets một cách thủ công, dễ bị lỗi và mất thời gian.

**Kết quả?** **Tỉ lệ chuyển đổi thấp**, **tốn nhiều thời gian** và **dữ liệu không chính xác**.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 80% thời gian** so với cách làm thủ công.
✅ **Tự động tìm kiếm email chuyên nghiệp** với độ chính xác cao (dùng AI OpenAI).
✅ **Phân loại lead tự động** thành **Qualified (có email)** và **Unqualified (không có email)**.
✅ **Cập nhật dữ liệu liên tục** vào Google Sheets mà không cần can thiệp.
✅ **Giảm thiểu lỗi nhân sự** (không còn phải copy-paste thủ công).

---
### **🔧 Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
📌 **Tài khoản & API Key:**
- **Google Drive & Google Sheets OAuth2** (để đọc và ghi dữ liệu).
- **OpenAI API Key** (để sử dụng AI tìm kiếm email).
- **Mã API Key** từ [OpenAI](https://platform.openai.com/api-keys) (miễn phí 5 triệu token/tháng).

📌 **File & Cấu Trúc Dữ Liệu:**
- **Tạo một folder trên Google Drive** để lưu file Excel/CSV chứa danh sách lead.
- **File Excel/CSV phải có các cột sau** (định dạng chuẩn):
  - `firstName`, `lastName`, `company`, `companyWebsite`, `linkedinIndustry`, `linkedinUrl`, `jobTitle`, `location`.
- **Tạo một file Google Sheets mới** với **2 tab**:
  - **Qualified** (lead có email).
  - **Unqualified** (lead không có email).
  - Các cột bắt buộc:
    - `fullName`, `companyName`, `companyWebsite`, `linkedinUrl`, `jobTitle`, `location`, `email`, `source`, `confidence`.

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ **file JSON** hoặc **copy/paste JSON** vào n8n Editor:
- **Tải workflow từ link gốc**: [Qualify Lead Lists & Find Professional Emails](https://n8n.io/workflows/14198).
- **Import vào n8n**:
  - Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON hoặc dán JSON vào.
  - **Hoặc** copy toàn bộ JSON từ [đây](https://n8n.io/workflows/14198) và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp **phải cấu hình** các node quan trọng sau:

##### **🔹 Node 1: "Watch For New Leads" (Google Drive Trigger)**
- **Chọn credentials**: `googleDriveOAuth2Api` (đã cấu hình trước khi import).
- **Cấu hình folder ID**:
  - Mở Google Drive → Chọn folder muốn theo dõi → **Chia sẻ** → **Lấy liên kết** → **Sao chép ID folder** (phần cuối của URL).
  - Điền vào **Folder ID** trong node này.

##### **🔹 Node 2 & 10: "Read Lead Sheet" & "Save Qualified/Unqualified Lead" (Google Sheets)**
- **Chọn credentials**: `googleSheetsOAuth2Api` (đã cấu hình trước).
- **Cấu hình sheet ID**:
  - Mở file Google Sheets mới tạo → **Chia sẻ** → **Lấy liên kết** → **Sao chép ID sheet** (phần cuối của URL).
  - Điền vào **Sheet ID** trong node này.
- **Chọn tab**:
  - Node **Read Lead Sheet**: Chọn tab chứa dữ liệu lead ban đầu.
  - Node **Save Qualified Lead**: Chọn tab **Qualified**.
  - Node **Save Unqualified Lead**: Chọn tab **Unqualified**.

##### **🔹 Node 5: "Find Email via OpenAI" (OpenAI)**
- **Chọn credentials**: `openAiApi` (đã cấu hình trước).
- **Cấu hình Prompt**:
  - Workflow đã sử dụng **Prompt mặc định** để tìm email chuyên nghiệp.
  - Nếu muốn **tối ưu hóa**, các sếp có thể chỉnh sửa Prompt trong node này để phù hợp với ngành nghề cụ thể.

##### **🔹 Node 6: "Rate Limit Delay" (Wait)**
- **Thời gian chờ mặc định**: 1.5 giây (để tránh bị chặn API).
- **Nếu dùng API miễn phí**, các sếp nên **giảm batch size** (node 4) để tránh bị giới hạn rate.

##### **🔹 Node 7: "Parse Email Results" (Set)**
- **Không cần chỉnh sửa** (n8n tự động xử lý kết quả từ OpenAI).

##### **🔹 Node 8: "Has Valid Email?" (If)**
- **Không cần chỉnh sửa** (n8n tự động phân loại lead có email vs không).

---
#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhấn **Run Workflow** với **dữ liệu mẫu** (1-2 lead) để kiểm tra.
  - Kiểm tra **tab Qualified** và **Unqualified** trong Google Sheets.
- **Bật Active**:
  - Sau khi test thành công, **bật Active** để workflow chạy tự động mỗi khi có file mới trong Google Drive.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Tối ưu hóa chi phí OpenAI**:
   - Thay **GPT-4o** bằng **GPT-3.5** (rẻ hơn) nếu không cần độ chính xác cao.
   - **Giảm batch size** (node 4) từ 3 xuống 1-2 để tránh bị giới hạn API.

2. **Lưu log hoạt động**:
   - Thêm node **Google Drive** để lưu **log hoạt động** (thời gian chạy, lead nào bị lỗi).

3. **Gửi báo cáo định kỳ**:
   - Thêm node **Email** (n8n-nodes-base.email) để gửi **báo cáo hàng tuần** về số lead được xác minh.

4. **Kết hợp với Slack/Telegram**:
   - Thêm node **Webhook** để thông báo kết quả lên Slack/Telegram khi có lead mới được xác minh.

5. **Tự động hóa từ nhiều nguồn**:
   - Thay vì chỉ đọc từ Google Drive, các sếp có thể **đọc từ CRM** (HubSpot, Salesforce) bằng node **HTTP Request**.

---
### **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp Sales/Marketing muốn:
✔ **Tự động hóa việc xác minh lead** mà không cần code.
✔ **Tìm kiếm email chuyên nghiệp** với độ chính xác cao.
✔ **Phân loại lead tự động** vào 2 tab riêng biệt.
✔ **Tiết kiệm thời gian và tăng hiệu suất** lên gấp nhiều lần.

**👉 Hãy áp dụng ngay và bắt đầu tự động hóa Sales của mình!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💬 Cần hỗ trợ thêm?**
- **Hỏi Devon Toh (Tác giả)**: [Đăng ký cuộc gọi 30 phút](https://cal.com/devon-toh-vrmdab/30min).
- **Hỏi cộng đồng n8n**: [Forum n8n](https://community.n8n.io/).