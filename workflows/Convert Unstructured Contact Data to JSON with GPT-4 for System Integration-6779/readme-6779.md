---
title: "🤖 Chuyển Dữ Liệu Liên Lạc Bất Định Sang JSON Với GPT-4 – Tự Động Hóa CRM/ERP Miễn Code"
description: "Workflow này tự động chuyển đổi thông tin liên lạc không định dạng (từ email, tin nhắn) thành JSON chuẩn, giúp các sếp tiết kiệm 80% thời gian nhập liệu thủ công và giảm sai sót trong CRM/ERP như Dolibarr, Odoo hay ERP nội bộ."
slug: "chuyen-doi-du-lieu-lien-lac-sang-json-gpt-4"
tags: [n8n, automation, ai-agent, gpt-4, crm-integration, no-code]
keywords: [n8n workflow tự động hóa, chuyển đổi dữ liệu liên lạc sang JSON, GPT-4 cho CRM, tự động hóa nhập liệu, Dolibarr n8n, ERP integration]
---

# 🚀 **Chuyển Dữ Liệu Liên Lạc Bất Định Sang JSON Với GPT-4 – Tự Động Hóa CRM/ERP Miễn Code**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Các sếp thường phải **nhập liệu thủ công** thông tin khách hàng từ email, tin nhắn, hoặc các tài liệu không định dạng (chẳng hạn như:
- **Email dài** với thông tin phân tán (địa chỉ, số điện thoại, tên công ty...)
- **Tin nhắn WhatsApp/Telegram** không có định dạng
- **File PDF/Word** chứa thông tin liên lạc không rõ ràng
và phải **chuyển sang định dạng JSON** để nhập vào CRM (Dolibarr, Odoo) hoặc ERP.

**Kết quả?**
- **Tốn thời gian** (1-2 giờ/ngày cho 100 khách hàng)
- **Sai sót cao** (do nhập liệu thủ công)
- **Không thể tích hợp tự động** với hệ thống hiện có

**Workflow này giải quyết tất cả!** Dùng **AI Agent + GPT-4**, nó **tự động extraxt** và **chuyển đổi** dữ liệu thành JSON chuẩn, sẵn sàng để **tích hợp vào CRM/ERP** mà **không cần viết một dòng code nào!**

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian nhập liệu** – Dữ liệu tự động chuyển đổi từ text sang JSON.
✅ **Giảm sai sót 100%** – AI extraxt chính xác hơn con người với các trường như:
   - **Tên công ty** (Company Name)
   - **Địa chỉ** (Address)
   - **Số điện thoại** (Phone)
   - **Email** (Email)
   - **Họ tên** (First Name, Last Name)
✅ **Tích hợp dễ dàng** – JSON đầu ra chuẩn để **nạp vào Dolibarr, Odoo, ERP nội bộ, hoặc API của bạn**.
✅ **Hoạt động 24/7** – Chỉ cần một **webhook**, workflow tự động xử lý mọi request.
✅ **Tùy chỉnh linh hoạt** – Thay đổi **prompt AI** để extraxt các trường dữ liệu khác.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** (để sử dụng GPT-4.1-nano):
   - [Đăng ký tài khoản OpenAI](https://platform.openai.com/signup) (miễn phí với giới hạn API).
   - **API Key** (đăng ký ở [trang tài khoản OpenAI](https://platform.openai.com/account/api-keys)).
2. **n8n Self-hosted** (để workflow hoạt động 24/7):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:

**Cách 1: Từ file JSON**
1. Tải workflow từ [n8n.io](https://n8n.io/workflows/6779) (ấn **Export**).
2. Trên **n8n Editor**, nhấn **Import** và chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

**Cách 2: Copy/Paste JSON**
1. Copy toàn bộ JSON từ [n8n.io/workflows/6779](https://n8n.io/workflows/6779).
2. Trên **n8n Editor**, nhấn **Import** → **Paste JSON** → **Import**.

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **5 node chính**, các sếp cần **cấu hình kỹ** các phần sau:

##### **🔹 Node 1: Webhook (Điểm Nhập Dữ Liệu)**
- **Địa chỉ Webhook**:
  ```
  https://[your-n8n-domain]/webhook/contact_data_converter
  ```
  (Thay `[your-n8n-domain]` bằng domain của n8n self-hosted).
- **Phương thức HTTP**: `POST`.
- **Thông tin gửi request**:
  - **Body**: JSON với key `"prompt"` chứa **dữ liệu liên lạc không định dạng** (ví dụ email hoặc tin nhắn).
  ```json
  {
    "prompt": "Tên công ty: ABC Corp\nĐịa chỉ: 123 Street, New York\nSĐT: +1234567890\nEmail: contact@abc.com\nHọ tên: John Doe"
  }
  ```

##### **🔹 Node 2: AI Agent (Extraxt Dữ Liệu)**
- **Prompt mặc định** đã được tối ưu để extraxt:
  - `Company Name`, `Address`, `Phone`, `Email`, `First Name`, `Last Name`.
- **Nếu muốn extraxt thêm trường dữ liệu**:
  - Mở node **AI Agent** → **Edit** → **Change prompt** để thêm các trường mới (ví dụ: `Website`, `Industry`).

##### **🔹 Node 3: OpenAI Chat Model (GPT-4.1-nano)**
- **Credentials**:
  - Chọn **openAiApi** (đã cấu hình trước khi import).
- **Model**: Đã mặc định là `gpt-4.1-nano` (rẻ và hiệu quả).
- **Lưu ý**:
  - Nếu muốn dùng **GPT-4** (đắt hơn), thay đổi model ở **keyParameters → model → value**.

##### **🔹 Node 4: Code (Chuyển String → JSON)**
- **Lógica mặc định** đã loại bỏ **Markdown code block** (nếu AI trả về dạng ````json ... ````).
- **Nếu AI trả về JSON không đúng định dạng**, node này sẽ **báo lỗi** để các sếp debug.

##### **🔹 Node 5: Respond to Webhook (Trả Lại Kết Quả)**
- **Output**: JSON chuẩn sẵn sàng để **tích hợp vào CRM/ERP**.
- **Ví dụ kết quả**:
  ```json
  {
    "Company Name": "ABC Corp",
    "Address": "123 Street, New York",
    "Phone": "+1234567890",
    "Email": "contact@abc.com",
    "First Name": "John",
    "Last Name": "Doe"
  }
  ```

---

#### **3. Kích Hoạt ⚡️**
1. **Test run** với dữ liệu mẫu:
   - Gửi request POST đến webhook với body như ví dụ trên.
   - Kiểm tra **output** trong node **Respond to Webhook**.
2. **Bật Active workflow**:
   - Nhấn **Active** trên tab workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH TIẾP CẬN THÊM]
1. **Tích hợp với Slack/Telegram**:
   - Sau khi extraxt JSON, **gửi kết quả** về Slack/Telegram bằng node **Slack** hoặc **Telegram Bot**.
   - **Cách làm**:
     - Thêm node **Slack** → Chọn **credentials** → Điền **Webhook URL** từ Slack.
     - Sử dụng **JSON Path** để lấy dữ liệu từ output (ví dụ: `$.Company Name`).

2. **Lưu log vào Google Sheets**:
   - Thêm node **Google Sheets** → Chọn sheet cần lưu.
   - Sử dụng **JSON Path** để extraxt các trường cần lưu (ví dụ: `$.Email`, `$.Phone`).

3. **Gửi báo cáo định kỳ**:
   - Dùng node **Set** để lưu dữ liệu vào **variable**.
   - Thêm node **Schedule** (n8n Premium) để **tổng hợp và gửi báo cáo** hàng ngày.

4. **Tùy chỉnh prompt AI**:
   - Nếu muốn extraxt **trường dữ liệu khác** (ví dụ: `Website`, `Industry`), mở node **AI Agent** → **Edit prompt** như sau:
     ```plaintext
     Extract structured data from the following text. Return in JSON format with these fields:
     - Company Name
     - Address
     - Phone
     - Email
     - First Name
     - Last Name
     - Website (if available)
     - Industry (if available)
     ```
---

### 📌 **Kết Luận**
Workflow này **giải phóng các sếp** khỏi việc **nhập liệu thủ công** và **tự động hóa** quá trình extraxt dữ liệu liên lạc sang JSON. **Kết quả?**
✅ **Tiết kiệm thời gian** (80% so với nhập liệu thủ công).
✅ **Giảm sai sót** (AI extraxt chính xác hơn).
✅ **Tích hợp dễ dàng** với CRM/ERP (Dolibarr, Odoo, ERP nội bộ).

**Hành động ngay!**
1. **Cài n8n self-hosted** trên VPS (để workflow hoạt động 24/7).
2. **Import workflow** và cấu hình **OpenAI API Key**.
3. **Test với dữ liệu mẫu** và **bật Active**.
4. **Tích hợp vào hệ thống** của bạn!

**🚀 CÓ THỂ BẮT ĐẦU NGAY!** [Tải workflow từ n8n.io](https://n8n.io/workflows/6779) và **tự động hóa CRM/ERP** của mình!

---