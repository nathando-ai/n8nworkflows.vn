---
title: "🎥 Tự Động Hoàn Thành Script Video Loom Từ Job Upwork Với AI Claude - Giảm Thời Gian Outreach 90%"
description: "Workflow này tự động phân tích và tạo ra bộ tài liệu outreach hoàn chỉnh (script Loom, so sánh trước-sau, flow diagram, snippet proposal) từ mô tả công việc Upwork chỉ trong 60 giây - không cần code. Phù hợp cho freelancer, agency, consultant cần tăng hiệu suất outreach."
slug: "tay-dong-hoan-thanh-script-loom-tu-job-upwork-voi-ai-claude"
tags: [n8n, automation, no-code, ai-claude, upwork, loom, google-docs, google-sheets, slack]
keywords: [tự động hóa outreach upwork, tạo script loom tự động, ai Claude n8n, workflow n8n content creation, giảm thời gian outreach, tự động hóa công việc freelancer]
---

# 🚀 **Tự Động Hoàn Thành Script Video Loom Từ Job Upwork Với AI Claude - Giảm Thời Gian Outreach 90%**

### **Nỗi Đau Của Các Sếp**
Các sếp freelancer, agency hoặc consultant thường phải mất **30-60 phút** để phân tích một job Upwork, viết script Loom, so sánh trước-sau, và chuẩn bị proposal. Điều này không chỉ tốn thời gian mà còn dễ gây **chán nản** khi phải làm thủ công hàng ngày. Kết quả là:
- **Outreach chậm**, mất cơ hội liên hệ với khách hàng tiềm năng.
- **Chất lượng script không đồng nhất**, phụ thuộc vào tâm trạng của cá nhân.
- **Không theo dõi được hiệu suất**, không biết ai là khách hàng tiềm năng tốt nhất.

**Workflow này giải quyết tất cả đó!** Chỉ cần **dán mô tả công việc Upwork** vào form, AI Claude sẽ tự động phân tích và tạo ra **bộ outreach hoàn chỉnh** (script Loom, so sánh trước-sau, flow diagram, snippet proposal) trong **60 giây**, đồng thời lưu log và thông báo qua Slack.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng thay vì dùng phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 90% thời gian outreach** – Từ 30-60 phút xuống còn **60 giây**.
✅ **Script Loom cá nhân hóa 100%** – Phù hợp với từng khách hàng, không cần sửa chữa.
✅ **So sánh trước-sau và flow diagram** – Giúp khách hàng dễ dàng hiểu giá trị của dịch vụ.
✅ **Lưu log tự động** – Theo dõi tất cả khách hàng tiềm năng trong Google Sheets.
✅ **Thông báo Slack** – Biết ngay khi workflow thành công hoặc lỗi.
✅ **Không cần code** – Sử dụng **n8n + AI Claude** để tự động hóa hoàn toàn.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Upwork** (để lấy mô tả công việc).
✔ **API Key Claude AI** (từ [Anthropic](https://www.anthropic.com/)).
✔ **Tài khoản Google** (để tạo Google Docs và Sheets).
✔ **Tài khoản Slack** (để nhận thông báo).
✔ **Folder Google Drive** (để lưu tài liệu outreach).
✔ **Google Sheet mẫu** (cần có các cột: Timestamp, Prospect Name, Industry, Pain Point, Tokens Used, Google Doc Link).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/11965) và import vào n8n Editor.
- **Copy JSON** từ link trên và **paste** vào n8n Editor (tab "Import").

:::note[Lưu ý]
- **Không** sử dụng phiên bản cloud n8n miễn phí (có giới hạn node và thời gian chạy).
- **Self-host n8n** trên VPS để workflow hoạt động **24/7** mà không bị gián đoạn.
:::

---

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **11 node**, nhưng các sếp cần chú ý đặc biệt đến **5 node quan trọng** sau:

##### **A. Thiết Lập Credentials (Bắt Buộc)**
| Node | Yêu Cầu | Hướng Dẫn |
|------|----------|------------|
| **Analyze Job with AI** | API Key Claude AI | - Đăng ký tại [Anthropic](https://www.anthropic.com/) <br> - Thêm vào n8n dưới **HTTP Header Auth** với header: `x-api-key` |
| **Create Output Doc** | Google Docs OAuth2 | - Tạo **Google Drive folder** để lưu tài liệu <br> - Thêm credential trong n8n và chọn **folder ID** |
| **Log Lead to Sheets** | Google Sheets OAuth2 | - Tạo **Google Sheet mới** với cột: `Timestamp | Prospect Name | Industry | Pain Point | Tokens Used | Google Doc Link` <br> - Chọn **Sheet ID** trong node |
| **Send Success/Error Notification** | Slack API Token | - Tạo **Slack App** và lấy **Bot Token** <br> - Thêm vào n8n và chọn **channel ID** |

##### **B. Cấu Hình Cụ Thể Các Node**
1. **Job Intake Form (formTrigger)**
   - Đặt **path** là `upwork-loom-generator` (không cần thay đổi).
   - Các trường cần hiển thị trong form:
     - `Job Title` (tiêu đề công việc)
     - `Job Description` (mô tả chi tiết)
     - `Prospect Name` (tên khách hàng)
     - `Prospect Email` (email liên hệ)

2. **Generate Loom Script with AI (httpRequest)**
   - **Prompt AI** (cần chỉnh sửa để phù hợp với **background** của các sếp):
     ```plaintext
     You are an expert in [niche của bạn, ví dụ: "marketing digital cho startup"].
     Analyze this Upwork job and generate a **Loom script** that:
     - Highlights **pain points** of the prospect.
     - Shows **before/after** comparison.
     - Includes a **flow diagram** of how your service solves their problem.
     - Ends with a **strong CTA** (e.g., "Let's discuss how we can achieve this in 30 days!").
     - Use **industry-specific examples** and **pricing guidance**.
     ```
   - **Thêm biến động** (`{{ $json["Job Description"] }}`) vào request body.

3. **Structure Generated Content (code)**
   - Node này **sắp xếp lại** nội dung từ AI thành định dạng chuẩn.
   - **Không cần chỉnh sửa** trừ khi muốn thay đổi cấu trúc output.

4. **Create Output Doc & Add Content to Doc (googleDocs)**
   - **Folder ID** phải trùng với folder đã tạo trong Google Drive.
   - **Tên tài liệu** tự động tạo từ `Prospect Name + Timestamp`.

5. **Log Lead to Sheets (googleSheets)**
   - **Operation** là `append` (thêm mới).
   - **Sheet ID** phải trùng với sheet đã tạo.

---

#### **3. Kích Hoạt ⚡️ Workflow**
Sau khi cấu hình xong:
1. **Test Run** với một job mẫu (ví dụ: dán mô tả công việc từ Upwork).
2. Kiểm tra:
   - **Google Doc** có tạo thành công không?
   - **Google Sheets** có ghi log không?
   - **Slack** có nhận thông báo không?
3. **Bật Active** workflow nếu test thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM ĐẸP HƠN]
1. **Thêm Slack/Telegram Bot** để nhận thông báo khi có job mới.
   - Sử dụng node **Slack** hoặc **Telegram Bot** để gửi tin nhắn tự động.
2. **Lưu log lỗi** vào Google Sheets hoặc Notion.
   - Thêm node **StickyNote** hoặc **Google Sheets** để ghi lỗi khi AI không phân tích được.
3. **Tự động gửi email** với link Loom cho khách hàng.
   - Kết hợp với node **Email** (Gmail/SendGrid) để gửi tự động.
4. **Tối ưu hóa prompt AI** cho từng ngành nghề.
   - Ví dụ:
     - **Freelancer thiết kế UI/UX**: Nhấn mạnh vào **UX research** và **prototyping**.
     - **Consultant marketing**: Tăng cường phần **data analysis** và **CTR optimization**.
5. **Tạo template Loom chuẩn** cho từng loại khách hàng.
   - Sử dụng node **Code** để thay đổi template dựa trên **industry** của khách hàng.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **quyết định chiến lược** thay vì làm thủ công. Với **AI Claude + n8n**, các sếp có thể:
✔ **Tăng hiệu suất outreach** lên **5-10x**.
✔ **Cải thiện chất lượng script** nhờ AI phân tích sâu.
✔ **Theo dõi khách hàng** một cách chuyên nghiệp.

**Hành động ngay!**
1. **Self-host n8n** trên VPS (để workflow chạy 24/7).
2. **Import workflow** và cấu hình credentials.
3. **Test với 1-2 job** và bắt đầu tự động hóa outreach!

**🚀 Còn chờ gì nữa?** Hãy **tự động hóa outreach** của mình ngay hôm nay! 🚀