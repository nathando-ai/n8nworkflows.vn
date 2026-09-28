---
title: "🚀 Tự Động Hóa Gửi 10% Khuyến Mãi WhatsApp Sau Mua Hàng (AI + Odoo) - Khai Thác 100% Mới"
description: "Workflow tự động hóa gửi tin nhắn WhatsApp cá nhân hóa với 10% giảm giá cho khách hàng đã mua hàng 10 ngày trước, sử dụng Odoo, OpenAI và Evolution API. Giúp doanh nghiệp tăng tỷ lệ chuyển đổi, tiết kiệm thời gian và tối ưu hóa chiến dịch marketing."
slug: "tieu-dong-hoa-gui-10-percent-khuyen-mai-whatsapp-sau-mua-hang"
tags: [n8n, automation, lead-nurturing, ai-chatbot, odoo-integration, whatsapp-business]
keywords: [tự động hóa n8n, gửi tin nhắn whatsapp tự động, ai copywriting, odoo automation, marketing automation, evolution api whatsapp]
---

# 🚀 **Tự Động Hóa Gửi 10% Khuyến Mãi WhatsApp Sau Mua Hàng (AI + Odoo) – Giải Pháp Marketing Tự Chạy 24/7**

### **Nỗi Đau Của Các Sếp**
Các sếp đang phải mất **thời gian và công sức** để:
- Theo dõi khách hàng đã mua hàng **10 ngày trước** để gửi tin nhắn khuyến mãi.
- **Viết thủ công** hàng trăm tin nhắn cá nhân hóa, mất thời gian và dễ gây nhầm lẫn.
- Lo ngại **bị chặn** khi gửi tin nhắn WhatsApp quá nhanh, ảnh hưởng đến chiến dịch marketing.
- Không có cách nào **tự động hóa** quá trình này mà vẫn giữ được tính cá nhân hóa và hiệu quả.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lấy danh sách khách hàng** đã mua hàng **10 ngày trước** từ Odoo.
✅ **Tạo tin nhắn WhatsApp cá nhân hóa** bằng AI (OpenAI) với giọng điệu **thân mật, tự nhiên** (tiếng Ả Rập).
✅ **Gửi tin nhắn một cách an toàn** với **thời gian chờ 1 phút giữa mỗi tin** để tránh bị chặn.
✅ **Hoạt động tự động hàng ngày** (10:01 AM) **không cần can thiệp** của bạn.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần viết tin nhắn thủ công, tự động hóa toàn bộ quá trình.
- **Tăng tỷ lệ chuyển đổi**: Khuyến mãi cá nhân hóa (10% giảm giá) và tin nhắn tự nhiên tăng khả năng khách hàng mua lại.
- **Tối ưu hóa chiến dịch marketing**: Gửi tin nhắn **một cách an toàn** (không bị chặn) với tốc độ hợp lý.
- **Hiệu quả cao**: Khách hàng được nhắc nhở **kịp thời** (10 ngày sau mua hàng), tăng cơ hội mua lại.
- **Dễ dàng mở rộng**: Có thể kết nối với **Slack, Telegram, hoặc email** để báo cáo kết quả.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Odoo**:
   - **URL Odoo** (ví dụ: `https://your-odoo-domain.com`).
   - **Tên người dùng** và **mật khẩu API** (hoặc **token OAuth2**).
   - **Database Name** và **Module Name** (để lấy dữ liệu hóa đơn và thông tin khách hàng).

2. **Tài khoản OpenAI**:
   - **API Key** từ [OpenAI](https://platform.openai.com/account/api-keys).
   - **Model** (gợi ý: `gpt-3.5-turbo` hoặc `gpt-4`).

3. **Tài khoản Evolution API (WhatsApp Business)**:
   - **API Key** và **Phone Number ID** từ [Evolution API](https://evolutionapi.com/).
   - **Number** (số điện thoại WhatsApp của doanh nghiệp).

4. **VPS cho n8n (khuyến nghị)**:
   - Để workflow chạy **24/7** mà không bị gián đoạn.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow bằng **2 cách**:
- **Tải file JSON** từ [n8n.io/workflows/14829](https://n8n.io/workflows/14829) và import vào **n8n Editor**.
- **Copy & Paste JSON** vào **n8n Editor** (đường dẫn: `https://your-n8n-instance/n8n` → **Create Workflow** → **Import JSON**).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **7 node chính**, các sếp cần **cấu hình kỹ lưỡng** các node sau:

##### **🔹 Node 1: Daily Check (10:01 AM) - `scheduleTrigger`**
- **Không cần chỉnh sửa gì** (n8n sẽ tự kích hoạt hàng ngày lúc 10:01 AM).

##### **🔹 Node 2 & 3: Fetch 10-Day Old Invoices & Retrieve Customer Contact - `odoo`**
- **Cấu hình Odoo Credentials**:
  - Trong **n8n Credentials** (đường dẫn: `https://your-n8n-instance/n8n/credentials`), tạo **một credential mới** với:
    - **Type**: `Odoo`.
    - **URL**: `https://your-odoo-domain.com`.
    - **Database**: `your_database_name`.
    - **Module**: `your_module_name` (ví dụ: `sale`).
    - **User**: `your_username`.
    - **Password**: `your_api_password_or_token`.
  - **Node "Fetch 10-Day Old Invoices"**:
    - **Resource**: `custom` (để lấy hóa đơn).
    - **Query**: `{"state": "paid", "date_invoice": {"$gte": "10 days ago"}}` (lấy hóa đơn đã thanh toán trong 10 ngày).
  - **Node "Retrieve Customer Contact"**:
    - **Resource**: `custom` (để lấy thông tin khách hàng).
    - **Query**: `{"id": "$$.json[0].partner_id"}` (lấy ID khách hàng từ hóa đơn).

##### **🔹 Node 4: Send WhatsApp Discount - `httpRequest`**
- **Cấu hình Evolution API**:
  - Trong **n8n Credentials**, tạo **một credential mới** với:
    - **Type**: `HTTP Request`.
    - **URL**: `https://graph.api.evolutionapi.com/v2/messages`.
    - **Headers**:
      ```
      Authorization: Bearer YOUR_EVOLUTION_API_KEY
      Content-Type: application/json
      ```
    - **Body**:
      ```json
      {
        "to": "$$.json[0].phone_number",
        "from": "YOUR_WHATSAPP_NUMBER",
        "text": "$$.json[0].ai_message"
      }
      ```
  - **Lưu ý**:
    - Thay `YOUR_EVOLUTION_API_KEY` bằng **API Key** của Evolution.
    - Thay `YOUR_WHATSAPP_NUMBER` bằng **số điện thoại WhatsApp** của doanh nghiệp (dạng `whatsapp:+841234567890`).

##### **🔹 Node 5: Process Customers (One by One) - `splitInBatches`**
- **Không cần chỉnh sửa** (n8n sẽ xử lý từng khách hàng một cách tự động).

##### **🔹 Node 6: Generate AI Message - `openAi`**
- **Cấu hình OpenAI**:
  - Trong **n8n Credentials**, tạo **một credential mới** với:
    - **Type**: `OpenAI`.
    - **API Key**: `your_openai_api_key`.
  - **Prompt Template** (cần chỉnh sửa để phù hợp với ngôn ngữ và giọng điệu):
    ```plaintext
    Tôi là một chuyên gia marketing. Hãy viết một tin nhắn WhatsApp **cá nhân hóa**, **thân mật** và **tự nhiên** (tiếng Ả Rập) cho khách hàng sau khi họ mua hàng 10 ngày trước.
    - Tên khách hàng: $$.json[0].name
    - Đối tượng: Khuyến mãi 10% cho sản phẩm đã mua.
    - Giọng điệu: **Thân mật, như bạn bè** (ví dụ: "Hey [Tên], bạn đã mua hàng rồi đấy! Bây giờ là lúc chúng ta có một cơ hội đặc biệt...").
    - Nội dung:
      1. Xưng hô thân mật.
      2. Nhắc lại sản phẩm đã mua.
      3. Giới thiệu khuyến mãi 10%.
      4. Kêu gọi hành động (ví dụ: "Nhấn vào đây để sử dụng mã giảm giá ngay!").
    ```
  - **Model**: `gpt-3.5-turbo` (hoặc `gpt-4` nếu muốn chất lượng cao hơn).

##### **🔹 Node 7: Wait 1 Mins (Anti-Ban) - `wait`**
- **Không cần chỉnh sửa** (n8n sẽ tự động chờ **1 phút** giữa mỗi tin nhắn để tránh bị chặn).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với **dữ liệu mẫu**:
   - Chạy workflow với **1-2 khách hàng mẫu** để kiểm tra:
     - AI có tạo tin nhắn cá nhân hóa không?
     - WhatsApp có gửi được không?
     - Có bị lỗi nào không?
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật Active** workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[MỞ RỘNG THÊM]
1. **Kết nối với Slack/Telegram**:
   - Thêm **node Slack/Telegram** để báo cáo **số tin nhắn đã gửi thành công/hỏng**.
   - Ví dụ: Khi workflow hoàn thành, gửi tin nhắn báo cáo lên **Slack** hoặc **Telegram**.

2. **Lưu Log & Báo Cáo Định Kỳ**:
   - Sử dụng **node Google Sheets** hoặc **node Airtable** để lưu **lịch sử gửi tin nhắn**.
   - Tạo **báo cáo hàng tháng** về tỷ lệ mở tin nhắn và chuyển đổi.

3. **Tùy Chỉnh Khuyến Mãi**:
   - Thay đổi **mức giảm giá** (ví dụ: 15% thay vì 10%) bằng cách chỉnh sửa **prompt AI**.
   - Thêm **mã giảm giá độc quyền** cho từng khách hàng.

4. **Kết Hợp với CRM Khác**:
   - Nếu sử dụng **HubSpot, Zoho CRM** thay vì Odoo, có thể thay thế **node Odoo** bằng **node HubSpot** hoặc **Zoho CRM**.

5. **Dùng AI Tạo Tin Nhắn Ngôn Ngữ Khác**:
   - Nếu doanh nghiệp phục vụ **khách hàng quốc tế**, có thể thay đổi **prompt AI** để tạo tin nhắn bằng **Tiếng Việt, Tiếng Anh, Tiếng Trung...**.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để các sếp:
✔ **Tự động hóa** quá trình gửi tin nhắn khuyến mãi sau mua hàng.
✔ **Tiết kiệm thời gian** và **tăng tỷ lệ chuyển đổi** với tin nhắn cá nhân hóa.
✔ **Tránh bị chặn** nhờ **thời gian chờ an toàn**.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**Hãy áp dụng ngay workflow này và xem doanh thu của bạn tăng lên như thế nào!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/14829)**
**💡 Cần hỗ trợ? Đăng ký VPS n8n tại [TinoHost](https://tino.vn/vps-n8n?affid=388) để chạy workflow ổn định!**