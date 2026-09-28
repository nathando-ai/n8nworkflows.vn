---
title: "💰 Tự Động Gửi Link Thanh Toán MercadoPago Bulk qua Email, WhatsApp hoặc Telegram từ Google Sheets"
description: "Giải pháp tự động hóa hoàn toàn không cần code để gửi hàng loạt link thanh toán MercadoPago đến khách hàng qua 3 kênh liên lạc phổ biến: Email, WhatsApp Business hoặc Telegram. Tiết kiệm thời gian, giảm sai sót và tối ưu hóa quy trình bán hàng."
slug: "tieu-dong-gui-link-thanh-toan-mercadopago-bulk"
tags: [n8n, automation, crm, mercado-pago, google-sheets, whatsapp-business, telegram-bot, email-automation]
keywords: [n8n workflow mercado pago, tự động hóa thanh toán bulk, gửi link thanh toán qua email whatsapp telegram, tự động hóa bán hàng online]
---

# 🚀 **Tự Động Gửi Link Thanh Toán MercadoPago Bulk qua Email, WhatsApp hoặc Telegram**

### **Giải pháp cho ai?**
Các sếp kinh doanh, freelancer hoặc doanh nghiệp sử dụng **MercadoPago** để bán hàng online (khóa học, đăng ký, hóa đơn, sản phẩm cá nhân hóa) nhưng gặp khó khăn khi phải gửi **hàng loạt link thanh toán** một cách thủ công. Hãy tưởng tượng:
- **Tốn thời gian** phải copy-paste link cho từng khách hàng.
- **Rủi ro sai sót** khi gửi sai kênh hoặc quên gửi.
- **Không cá nhân hóa** được thông báo theo sở thích của khách hàng.

**Workflow này giúp các sếp:**
✅ **Tự động hóa hoàn toàn** việc tạo và gửi link thanh toán.
✅ **Chọn kênh liên lạc** (Email, WhatsApp, Telegram) theo lựa chọn của khách hàng.
✅ **Cập nhật trạng thái** trong Google Sheets để theo dõi hiệu quả.
✅ **Hoạt động 24/7** khi kết hợp với **Schedule Trigger** (không cần kích hoạt thủ công).

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này **chạy ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. Dưới đây là các gói VPS ưu đãi dành cho n8n:

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao, phù hợp cho workflow MercadoPago)

*Lưu ý:* Workflow này **không chạy trên n8n Cloud** do sử dụng node `@mercadopago/n8n-nodes-mercadopago` (cần tự cài đặt).
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Gửi hàng trăm link thanh toán chỉ với **1 lần kích hoạt**.
- **Chính xác 100%:** Không bị quên hoặc gửi sai kênh.
- **Cá nhân hóa:** Khách hàng nhận thông báo theo kênh ưa thích (Email, WhatsApp, Telegram).
- **Theo dõi dễ dàng:** Tất cả trạng thái (đã tạo link, đã gửi, kênh sử dụng) được cập nhật tự động trong Google Sheets.
- **Hoạt động liên tục:** Kết hợp với **Schedule Trigger** để chạy tự động hàng ngày/tuần.
- **Giảm chi phí:** Không cần thuê nhân viên hỗ trợ thanh toán.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản MercadoPago** với **Access Token** (đăng ký tại [đây](https://www.mercadopago.com.ar/developers/es/docs/credentials)).
2. **Google Sheets** với cấu trúc cột chuẩn (hướng dẫn chi tiết dưới phần **Cách chuẩn bị dữ liệu**).
3. **Một trong ba kênh liên lạc sau:**
   - **Gmail** (để gửi Email).
   - **WhatsApp Business Cloud API** (đăng ký tại [Meta for Developers](https://developers.facebook.com/docs/whatsapp/cloud-api/get-started)).
   - **Telegram Bot** (tạo bot tại [@BotFather](https://t.me/BotFather)).
4. **n8n Self-hosted** (không chạy được trên n8n Cloud).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/15719) và import vào n8n Editor.
- **Copy/paste JSON** từ file vào **Import Workflow** trong n8n.

*Lưu ý:* Đảm bảo **n8n đã cài đặt node `@mercadopago/n8n-nodes-mercadopago`** (nếu self-hosted).

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Chuẩn bị Google Sheets**
Trước khi chạy workflow, các sếp phải tạo **Google Sheet** với cấu trúc sau (điền vào **dòng 1**):

| **Cột bắt buộc (điền)**               | **Cột tự động cập nhật (không cần điền)**          |
|----------------------------------------|------------------------------------------------------|
| `customer_name`                        | `payment_link`                                      |
| `customer_email`                       | `preference_id`                                     |
| `customer_phone`                       | `link_created_at`                                   |
| `customer_telegram_chat_id`            | `status`                                            |
| `product_id`                           | `sent_at`                                           |
| `product_title`                        | `channel_used`                                      |
| `product_description`                  |                                                      |
| `quantity` (≥ 1)                       |                                                      |
| `unit_price` (> 0)                     |                                                      |
| `currency_id`                          |                                                      |
| `external_reference` (unique, ≤ 64 ký tự) |                                                      |
| `channel` (`email` / `whatsapp` / `telegram`) |                                                      |

*Ví dụ:*
| customer_name | customer_email       | customer_phone | customer_telegram_chat_id | product_title | quantity | unit_price | currency_id | external_reference | channel     |
|---------------|----------------------|----------------|---------------------------|----------------|-----------|-------------|--------------|----------------------|--------------|
| Nguyễn Văn A  | a@example.com        | 5491123456789  | 123456789                  | Khóa học SEO    | 1         | 500000      | ARS            | kh001                | email        |

---

#### **B. Cấu hình các node quan trọng**
##### **1. Node "Read Sheet" (googleSheets)**
- Chọn **Google Sheet** và **tab** đã tạo.
- Đảm bảo **OAuth đã được cấu hình** (n8n → Credentials → New → Google Sheets OAuth).

##### **2. Node "Create Payment Link" (mercadoPago)**
- **Chọn credential MercadoPago** (n8n → Credentials → New → MercadoPago API).
- Điền **Access Token** từ tài khoản MercadoPago.
- **Lưu ý:** Node này sẽ tự động tạo `payment_link` và `preference_id` cho mỗi hàng chưa có link.

##### **3. Node "Route by channel" (switch)**
- Node này **chia luồng** dựa trên cột `channel` trong Google Sheets:
  - `email` → Gửi qua Gmail.
  - `whatsapp` → Gửi qua WhatsApp Business.
  - `telegram` → Gửi qua Telegram.

##### **4. Cấu hình kênh liên lạc**
###### **Gmail (Email)**
- Tạo **credential Gmail OAuth2** (n8n → Credentials → New → Gmail OAuth2 API).
- Gắn credential vào node **Send Email**.
- **Điều kiện:** Cột `customer_email` phải có giá trị và `channel = email`.

###### **WhatsApp Business**
- Tạo **credential WhatsApp Business Cloud API** (n8n → Credentials → New → WhatsApp Business Cloud API).
- Điền:
  - **Permanent Access Token** (từ Meta Business App).
  - **Business Account ID**.
- Chọn **số điện thoại** từ dropdown.
- **Điều kiện:**
  - Cột `customer_phone` phải là **số điện thoại quốc tế (không dấu `+`)** (ví dụ: `5491123456789`).
  - `channel = whatsapp`.

###### **Telegram**
- Tạo **credential Telegram API** (n8n → Credentials → New → Telegram API).
- Điền **API Token** từ bot (tạo tại `@BotFather`).
- **Điều kiện:**
  - Cột `customer_telegram_chat_id` phải có giá trị (lấy từ `@userinfobot`).
  - `channel = telegram`.

##### **5. Cập nhật trạng thái trong Google Sheets**
- Các node **Mark Sent** (Email/WhatsApp/Telegram) sẽ tự động cập nhật:
  - `status = sent`.
  - `sent_at` (thời gian gửi).
  - `channel_used`.

---

### **3. Kích hoạt ⚡️**
1. **Test run** với **1-2 hàng mẫu** để kiểm tra:
   - Link thanh toán có được tạo không?
   - Kênh liên lạc có hoạt động không?
2. **Bật Active workflow** khi đã kiểm tra xong.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Chạy tự động với Schedule Trigger**
- **Xóa node Manual Trigger** và thay thế bằng **Schedule Trigger**.
- Cấu hình **thời gian chạy** (ví dụ: hàng ngày 8h sáng).
- *Lợi ích:* Không cần kích hoạt thủ công, workflow chạy tự động.

### **2. Gửi báo cáo định kỳ**
- Thêm **node Email (SMTP)** để gửi **báo cáo tổng hợp** hàng tuần:
  - Số lượng link đã tạo.
  - Số lượng đã gửi thành công.
  - Kênh phổ biến nhất.

### **3. Xử lý lỗi với Error Trigger**
- Thêm **node Error Trigger** để nhận thông báo khi workflow gặp lỗi (ví dụ: MercadoPago API lỗi, WhatsApp không gửi được).

### **4. Kết hợp với Zapier/Integromat**
- Nếu các sếp muốn **tích hợp thêm dữ liệu** từ CRM khác (HubSpot, Airtable), có thể sử dụng **Zapier** hoặc **Integromat** để tự động cập nhật Google Sheets.

### **5. Tối ưu hóa Google Sheets**
- **Sắp xếp dữ liệu** theo `status` để dễ theo dõi.
- **Sử dụng filter** để chỉ hiển thị hàng chưa gửi (`status = pending`).

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp bán hàng online muốn:
✔ **Tự động hóa gửi link thanh toán** một cách nhanh chóng và chính xác.
✔ **Cá nhân hóa trải nghiệm khách hàng** bằng cách chọn kênh liên lạc ưa thích.
✔ **Tiết kiệm thời gian** và giảm sai sót trong quy trình bán hàng.

**Hành động ngay hôm nay:**
1. **Chuẩn bị Google Sheets** theo cấu trúc trên.
2. **Cài đặt n8n trên VPS** (sử dụng mã giảm giá **VPSN8N**).
3. **Import workflow** và cấu hình các node.
4. **Kích hoạt và chạy thử** với dữ liệu mẫu!

*Cần hỗ trợ thêm? Đừng ngần ngại comment bên dưới hoặc liên hệ với cộng đồng n8n tại [n8n.io/community](https://n8n.io/community).* 🚀