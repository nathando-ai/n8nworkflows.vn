---
title: "🚀 Tự Động Hóa Lịch Trình Theo Dõi Nhà Cung Cấp Từ Airtable Sang Google Calendar Với AI, Slack & Email – Giảm 80% Thời Gian Theo Dõi PO"
description: "Workflow này tự động phát hiện đơn đặt hàng (PO) quá hạn trong Airtable, sử dụng AI để tạo agenda cuộc họp thông minh, lập lịch trên Google Calendar và gửi thông báo tự động qua Slack và Email. Giúp các sếp tiết kiệm 80% thời gian theo dõi PO thủ công và cải thiện hiệu quả quản lý nhà cung cấp."
slug: "tu-dong-hoa-theo-doi-nha-cung-cap-airtable-google-calendar-ai"
tags: [n8n, automation, no-code, airtable, google-calendar, ai-agent, slack, gmail, project-management]
keywords: [tự động hóa n8n, theo dõi đơn đặt hàng quá hạn, ai tự động hóa, lập lịch google calendar từ airtable, giảm thời gian quản lý nhà cung cấp, workflow n8n ai agent]
---

# 🚀 **Tự Động Hóa Lịch Trình Theo Dõi Nhà Cung Cấp Từ Airtable Sang Google Calendar Với AI, Slack & Email**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải mất **giờ đồng hồ** để:
- **Tìm kiếm** đơn đặt hàng (PO) quá hạn trong Airtable.
- **Lập lịch** cuộc họp theo dõi với nhà cung cấp thủ công.
- **Tạo agenda** và chuẩn bị nội dung cho cuộc họp.
- **Gửi thông báo** cho team và nhà cung cấp qua Email/Slack.

**Kết quả?** PO quá hạn vẫn bị bỏ quên, hiệu quả quản lý nhà cung cấp giảm, và team phải làm việc ngoài giờ để theo dõi.

**Workflow này giải quyết tất cả!**
- **Tự động phát hiện** PO quá hạn (trên 30 ngày) trong Airtable.
- **Sử dụng AI (GPT-4)** để tạo **agenda cuộc họp thông minh** và **đề xuất hành động** cho mỗi nhà cung cấp.
- **Lập lịch tự động** trên Google Calendar và **cập nhật liên kết** về Airtable.
- **Gửi thông báo** đến Slack và Email (cả nhà cung cấp và team trong doanh nghiệp).
- **Chỉ chạy vào thứ 2-5 sáng 10h**, không làm phiền team vào cuối tuần.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian** theo dõi PO thủ công.
✅ **Cải thiện hiệu quả** quản lý nhà cung cấp với agenda cuộc họp được AI tối ưu.
✅ **Hoạt động liên tục** (không cần can thiệp thủ công).
✅ **Cập nhật tự động** lịch họp và trạng thái PO trong Airtable.
✅ **Gửi thông báo đa kênh** (Slack + Email) để đảm bảo không bỏ lỡ.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Airtable**:
   - **Base** chứa bảng PO với các trường bắt buộc:
     - `PO ID` (ID đơn đặt hàng)
     - `Supplier Name` (Tên nhà cung cấp)
     - `Supplier Email` (Email liên hệ)
     - `Status` (Trạng thái PO)
     - `PO Date` (Ngày đặt hàng)
     - `Follow-up Link` (Liên kết lịch họp)
     - `Follow-up Status` (Trạng thái theo dõi)
     - `Notes` (Ghi chú)
   - **Personal Access Token** của Airtable (để kết nối API).

2. **Google Calendar**:
   - **OAuth2 Credentials** (để tạo sự kiện mới).

3. **Slack**:
   - **API Token** và **Channel ID** để gửi thông báo.

4. **Gmail**:
   - **OAuth2 Credentials** (để gửi Email xác nhận).

5. **OpenAI API Key**:
   - Để sử dụng **GPT-4** tạo agenda cuộc họp.

6. **Email địa chỉ**:
   - Địa chỉ Email mặc định để gửi thông báo (ví dụ: `team@doanhnghiep.com`).
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/11297](https://n8n.io/workflows/11297) (chọn **Export as JSON**).
2. Trên **n8n Editor**, nhấn **Import** và chọn file JSON vừa tải.
3. Chọn **Workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/11297](https://n8n.io/workflows/11297).
2. Trên **n8n Editor**, nhấn **Import** → **Paste JSON** và dán mã.
3. Chọn **Workflow** và nhấn **Import**.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **16 node** quan trọng, nhưng các sếp cần chú ý đặc biệt đến các node sau:

#### **🔹 Node "Schedule Trigger" (Lập lịch chạy hàng ngày)**
- **Cấu hình**:
  - **Schedule**: `0 10 * * 1-5` (Chạy hàng ngày từ thứ 2 đến thứ 5, lúc 10h sáng).
  - **Time Zone**: Chọn múi giờ phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).
- **Lưu ý**:
  - Nếu muốn chạy vào giờ khác, chỉnh sửa biểu thức `cron` tương ứng.

#### **🔹 Node "Fetch Overdue POs from Airtable" (Lấy PO quá hạn)**
- **Cấu hình**:
  - **Airtable Base ID**: Điền ID của Base Airtable (thường là chuỗi dài như `app123abc`).
  - **Table Name**: Điền tên bảng chứa PO (ví dụ: `Purchase_Orders`).
  - **Filter**: Cấu hình query để lấy PO:
    ```json
    {
      "filterByFormula": "AND({Status} = 'Open', DATEDIFF(NOW(), {PO Date}) > 30, ISBLANK({Follow-up Link}))"
    }
    ```
    - **Giải thích**:
      - `Status = 'Open'` → Chỉ lấy PO đang mở.
      - `DATEDIFF(NOW(), {PO Date}) > 30` → PO quá hạn hơn 30 ngày.
      - `ISBLANK({Follow-up Link})` → PO chưa có lịch họp.

#### **🔹 Node "AI Model: GPT-4 Screening Engine" (AI tạo agenda)**
- **Cấu hình**:
  - **Model**: Đặt mặc định là `gpt-4o-mini` (nếu có API key cho model này).
  - **Prompt Template**: Workflow đã cấu hình sẵn, nhưng các sếp có thể tùy chỉnh:
    ```json
    "prompt": "You are an expert procurement agent. For the following purchase order details, generate a concise meeting agenda with action items for the supplier follow-up:\n\nPO ID: {{PO ID}}\nSupplier: {{Supplier Name}}\nPO Date: {{PO Date}}\nStatus: {{Status}}\nNotes: {{Notes}}\n\nOutput format:\n1. **Meeting Purpose**: [Brief reason for follow-up]\n2. **Key Discussion Points**: [Bullet points of what to cover]\n3. **Action Items**: [Tasks for supplier to complete]\n4. **Next Steps**: [Follow-up plan after meeting]\n\nBe professional and concise."
    ```
  - **OpenAI API Key**: Điền vào **Credentials** của node này.

#### **🔹 Node "Create Calendar Event" (Tạo sự kiện Google Calendar)**
- **Cấu hình**:
  - **Calendar ID**: Chọn Calendar phù hợp (ví dụ: `primary` hoặc Calendar riêng).
  - **Event Details**:
    - **Title**: `Follow-up: {{Supplier Name}} - PO#{{PO ID}}`
    - **Description**: Nội dung từ AI (agenda).
    - **Start Time**: `{{PO Date}} + 7 days` (hoặc tùy chỉnh).
    - **End Time**: `{{PO Date}} + 7 days + 1 hour`.

#### **🔹 Node "Send Email Confirmation" (Gửi Email xác nhận)**
- **Cấu hình**:
  - **To**: Điền Email nhà cung cấp từ trường `Supplier Email` trong Airtable.
  - **Subject**: `Meeting Follow-up Scheduled: PO#{{PO ID}}`
  - **Body**: Nội dung Email mẫu:
    ```html
    <p>Xin chào {{Supplier Name}},</p>
    <p>Cuộc họp theo dõi đơn đặt hàng PO#{{PO ID}} đã được lập lịch vào ngày <strong>{{Event Start Time}}</strong>.</p>
    <p><strong>Agenda:</strong></p>
    {{Agenda}}
    <p><strong>Liên kết Google Calendar:</strong></p>
    <a href="{{Follow-up Link}}">Xem lịch họp</a>
    <p>Trân trọng,</p>
    <p>Team Quản lý Nhà Cung Cấp</p>
    ```

#### **🔹 Node "Save Calendar Link to Airtable" (Cập nhật liên kết vào Airtable)**
- **Cấu hình**:
  - **Record ID**: Lấy từ PO trong Airtable.
  - **Fields to Update**:
    ```json
    {
      "Follow-up Link": "{{Event Link}}",
      "Follow-up Status": "Scheduled"
    }
    ```

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** với 1 PO mẫu:
   - Chọn **Run Workflow** và chọn 1 PO quá hạn để kiểm tra.
   - Kiểm tra:
     - AI có tạo agenda không?
     - Sự kiện có xuất hiện trên Google Calendar không?
     - Email/Slack có được gửi không?

2. **Bật Active**:
   - Sau khi test thành công, chuyển **Schedule Trigger** sang **Active**.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Notion/Confluence**:
   - Thay vì chỉ gửi Email, có thể **tạo bài viết tự động** trong Notion với agenda cuộc họp.

2. **Lưu log hoạt động**:
   - Sử dụng **StickyNote** hoặc **Google Sheets** để ghi lại lịch sử PO đã xử lý.

3. **Gửi báo cáo định kỳ**:
   - Tạo 1 workflow phụ để **tổng hợp thống kê** PO quá hạn và gửi báo cáo hàng tuần cho CEO.

4. **Tùy chỉnh AI Prompt**:
   - Nếu muốn agenda chuyên sâu hơn, cập nhật **Prompt Template** trong node `lmChatOpenAi` với nội dung phù hợp với ngành nghề.

5. **Xử lý lỗi tự động**:
   - Nếu PO không có Email hợp lệ, workflow có thể **bỏ qua** hoặc gửi **thông báo lỗi** đến Slack.
:::

---
## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để các sếp:
✔ **Tự động hóa 100%** quá trình theo dõi PO quá hạn.
✔ **Tiết kiệm thời gian** và tập trung vào công việc chiến lược.
✔ **Cải thiện hiệu quả** quản lý nhà cung cấp với agenda cuộc họp được AI tối ưu.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với 1 PO mẫu** trước khi kích hoạt.
3. **Bật Schedule Trigger** và để AI làm việc cho bạn!

**🎁 Mã giảm giá VPS TinoHost (Self-hosted n8n):**
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) với mã **VPSN8N** (giảm tới 39%).

---
**🚀 Chúc các sếp thành công với tự động hóa!** 🚀