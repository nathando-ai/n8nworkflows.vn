---
title: "🚀 Hệ Thống Giao Templates Tự Động Hóa Với Stripe, GPT-4o & Gmail (Không Cần Code)"
description: "Workflow tự động hóa hoàn toàn gửi email cá nhân hóa, bao gồm link truy cập, mật khẩu, hướng dẫn onboarding và chữ ký, cho khách hàng sau mỗi giao dịch thành công trên Stripe. Giảm thiểu công việc thủ công 90% và tăng trải nghiệm khách hàng."
slug: "huyen-luy-thu-templates-tu-dong-hoa-stripe-gpt-4o-gmail"
tags: [n8n, automation, no-code, CRM, AI, Stripe, Gmail, GPT-4o, GoogleSheets, AI Agent]
keywords: [n8n workflow Stripe, tự động hóa email cá nhân hóa, GPT-4o tự động hóa, Stripe + AI, gửi email tự động hóa, CRM tự động hóa]
---

# 🚀 **Hệ Thống Giao Templates Tự Động Hóa Với Stripe, GPT-4o & Gmail**

## **Tại sao các sếp cần workflow này?**
Hiện nay, khi khách hàng mua sản phẩm/ dịch vụ từ website, các sếp thường phải:
- **Thủ công** gửi email xác nhận, link truy cập, mật khẩu và hướng dẫn sử dụng.
- **Tốn thời gian** để kiểm tra đơn hàng, chuẩn bị nội dung email và gửi từng khách hàng một.
- **Rủi ro sai sót** khi thiếu thông tin hoặc nội dung email không phù hợp với từng khách hàng.

**Workflow này tự động hóa toàn bộ quy trình:**
✅ **Lấy dữ liệu giao dịch** từ Stripe (chỉ giữ lại đơn hàng thành công).
✅ **Tìm kiếm thông tin sản phẩm** và khách hàng trong Google Sheets.
✅ **Sử dụng GPT-4o** để tạo email cá nhân hóa (được tối ưu hóa cho từng sản phẩm).
✅ **Gửi email tự động** với subject, nội dung HTML và chữ ký chuyên nghiệp.
✅ **Lưu log** tất cả giao dịch đã xử lý để theo dõi và báo cáo.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Xử lý hàng trăm đơn hàng mỗi ngày chỉ trong vài giây.
- **Cá nhân hóa hoàn toàn**: Email được tạo riêng cho từng khách hàng, sản phẩm và đơn hàng.
- **Chính xác 100%**: Không sai sót trong thông tin (link, mật khẩu, hướng dẫn).
- **Hoạt động 24/7**: Khách hàng nhận email ngay sau khi thanh toán thành công.
- **Dễ dàng mở rộng**: Thêm sản phẩm mới hoặc logic mới chỉ bằng cách cập nhật Google Sheets.
:::

---
## 🔧 **Yêu cầu cần thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
### **1. Tài khoản và API Keys**
| Dịch vụ               | Thông tin cần thiết                                                                 |
|-----------------------|--------------------------------------------------------------------------------------|
| **Stripe**            | API Key (tìm tại [Stripe Dashboard](https://dashboard.stripe.com/test/apikeys))       |
| **Google Sheets**      | OAuth 2.0 Credentials (tạo tại [Google Cloud Console](https://console.cloud.google.com/)) |
| **Gmail**             | OAuth 2.0 Credentials (sử dụng email chính thức của doanh nghiệp)                   |
| **Azure OpenAI**       | API Key và Endpoint (đăng ký tại [Azure Portal](https://portal.azure.com/))           |

### **2. Google Sheets chuẩn bị**
Workflow cần **2 bảng Google Sheets** với cấu trúc sau:
1. **"n8n Automations – Zip Files"**
   - Cột: `product_name` (tên sản phẩm), `automation_template` (nội dung template email).
   - Ví dụ:
     | product_name       | automation_template                                                                 |
     |--------------------|-----------------------------------------------------------------------------------|
     | "n8n Pro License"  | "Xin chào {customer_name}, đây là link truy cập và mật khẩu của bạn..."            |
     | "AI Agent Template"| "Chúc mừng bạn đã mua sản phẩm AI Agent! Dưới đây là hướng dẫn..."               |

2. **"Automation Purchase Sheet"**
   - Cột: `order_reference`, `customer_name`, `email`, `product_name`, `status`, `email_sent`.
   - Dùng để lưu log tất cả đơn hàng đã xử lý.

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/10145](https://n8n.io/workflows/10145) (chọn **Export as JSON**).
2. Trên n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/10145](https://n8n.io/workflows/10145).
2. Trên n8n Editor, nhấn **Import** → Chọn **Paste JSON** và dán mã.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **25 node**, nhưng các sếp chỉ cần chú ý đến các node sau:

#### **🔹 Node quan trọng 1: Stripe Data Collection**
- **Mục đích**: Lấy tất cả các giao dịch từ Stripe và lọc chỉ giữ lại giao dịch thành công (`status = succeeded`).
- **Cấu hình**:
  - Điền **Stripe API Key** vào `stripeApi` (tạo tại [Stripe Dashboard](https://dashboard.stripe.com/test/apikeys)).
  - Node này sẽ trả về danh sách `charges` (đơn hàng).

#### **🔹 Node quan trọng 2: Azure OpenAI Chat Model (GPT-4o-mini)**
- **Mục đích**: Sử dụng AI để tạo email cá nhân hóa.
- **Cấu hình**:
  - Điền **Azure OpenAI API Key** và **Endpoint** vào `azureOpenAiApi`.
  - **Prompt mẫu** (cần chỉnh sửa theo template của doanh nghiệp):
    ```json
    {
      "role": "user",
      "content": "Tạo email cá nhân hóa cho khách hàng {customer_name} mua sản phẩm {product_name}. Nội dung phải bao gồm:
      - Link truy cập: {receipt_url}
      - Mật khẩu: {password}
      - Hướng dẫn onboarding: {onboarding_tip}
      - Chữ ký: {signature}
      - Subject: 'Xin chào {customer_name}, đây là thông tin đăng ký {product_name}'
      - Nội dung HTML phải đẹp và chuyên nghiệp."
    }
    ```
  - **Output Parser Structured**: Chọn `JSON` để AI trả về dữ liệu có cấu trúc.

#### **🔹 Node quan trọng 3: Google Sheets Lookup**
- **Mục đích**: Tìm kiếm template email phù hợp với sản phẩm khách hàng mua.
- **Cấu hình**:
  - Chọn **Google Sheets OAuth2 API** (`googleSheetsOAuth2Api`).
  - **Sheet Name**: `"n8n Automations – Zip Files"`.
  - **Range**: `"A2:B"` (giả sử cột `A` là `product_name`, cột `B` là `automation_template`).

#### **🔹 Node quan trọng 4: Gmail (Send a message)**
- **Mục đích**: Gửi email tự động cho khách hàng.
- **Cấu hình**:
  - Chọn **Gmail OAuth2** (`gmailOAuth2`).
  - **Subject**: `{email_subject}` (được AI tạo).
  - **HTML Body**: `{email_body}` (nội dung HTML từ AI).
  - **To**: `{email}` (địa chỉ email khách hàng).

#### **🔹 Node quan trọng 5: Schedule Trigger**
- **Mục đích**: Lấy dữ liệu mới mỗi ngày lúc 7h sáng (IST).
- **Cấu hình**:
  - Chọn **Daily** và đặt thời gian là **7:00 AM**.

---
### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** và chọn **Test Execution**.
   - Chọn **Stripe Data Collection** → **Filter – Successful Charges** → **Merge Charge + PaymentIntent + Product**.
   - Kiểm tra dữ liệu trả về có logic không (nếu có lỗi, sửa lại cấu hình).

2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động hàng ngày.

---
## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tối ưu hóa Google Sheets**
- **Tạo cột `email_sent`** để theo dõi trạng thái đã gửi email chưa.
- **Sử dụng công thức `IF`** để tự động cập nhật trạng thái khi email được gửi thành công.

### **2. Kết hợp với Slack/Telegram**
- Thêm node **Slack/Telegram Webhook** sau node **Send a message (Gmail)** để thông báo khi email được gửi thành công.

### **3. Lưu log chi tiết**
- Thêm node **HTTP Request** (với API của Google Sheets) để lưu log chi tiết vào một sheet riêng biệt.

### **4. Xử lý lỗi tự động**
- Thêm node **Code** sau **Check Required Fields** để xử lý trường hợp thiếu dữ liệu:
  ```javascript
  // Ví dụ: Nếu thiếu email, gửi email cảnh báo cho admin
  if (!json.email) {
    return { error: "Email missing", shouldContinue: false };
  }
  ```

### **5. Mở rộng với nhiều sản phẩm**
- Thêm nhiều hàng vào **n8n Automations – Zip Files** để hỗ trợ nhiều sản phẩm khác nhau.

---
## 📌 **Kết luận**
Workflow này **giải phóng các sếp khỏi công việc thủ công gửi email**, đồng thời **tăng trải nghiệm khách hàng** bằng cách cung cấp thông tin cá nhân hóa ngay sau khi thanh toán. Với **GPT-4o**, email được tạo tự động và chuyên nghiệp, trong khi **Stripe + Google Sheets** đảm bảo dữ liệu chính xác và cập nhật.

**🚀 Hãy áp dụng ngay và tiết kiệm thời gian cho đội ngũ!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Lưu ý cuối cùng**: Nếu gặp khó khăn trong quá trình cấu hình, các sếp có thể liên hệ với cộng đồng n8n tại [n8n Community](https://community.n8n.io/) hoặc [Discord n8n](https://discord.gg/n8n).