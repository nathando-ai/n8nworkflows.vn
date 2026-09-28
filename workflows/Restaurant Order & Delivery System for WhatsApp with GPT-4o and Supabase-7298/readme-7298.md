---
title: "🍔 **Hệ Thống Đặt Hàng & Giao Hàng Tự Động WhatsApp với AI GPT-4o & Supabase - Giải Pháp 100% Không Code cho Quán Ẩm Thực**"
description: "Tự động hóa toàn bộ quy trình đặt hàng, xác nhận thanh toán và giao tiếp với khách hàng qua WhatsApp chỉ với 1 workflow n8n. Sử dụng AI GPT-4o phân tích hóa đơn, xử lý âm thanh, hình ảnh và văn bản, kết hợp với Supabase lưu trữ trí nhớ hội thoại. Giúp quán ăn tiết kiệm 80% thời gian quản lý đơn hàng và giảm sai sót trong xử lý."
slug: "he-thong-dat-hang-whatsapp-ai-gpt4o-supabase"
tags: [n8n, automation, no-code, whatsapp-business, ai-gpt-4o, supabase, restaurant-automation]
keywords: [tự động hóa đặt hàng whatsapp, ai xử lý hóa đơn, workflow n8n quán ăn, chatbot đặt hàng tự động, supabase lưu trữ hội thoại, gpt-4o phân tích hóa đơn]
---

# 🚀 **Hệ Thống Đặt Hàng & Giao Hàng Tự Động WhatsApp với AI GPT-4o & Supabase**

## **Giải pháp hoàn hảo cho quán ăn, nhà hàng, và cửa hàng ẩm thực**
Hãy tưởng tượng một ngày không cần phải lo lắng khi khách hàng gửi hóa đơn qua WhatsApp dạng ảnh, âm thanh, hoặc PDF để xác nhận thanh toán. Hoặc khi khách gọi đơn qua âm thanh, hệ thống tự động chuyển đổi thành văn bản và gửi cho nhân viên nấu ăn. **Workflow này làm tất cả những việc đó chỉ với 1 dòng code tự động hóa!**

Không cần viết một dòng code nào, bạn chỉ cần **cấu hình các API và kết nối các dịch vụ** như WhatsApp Business, OpenAI (GPT-4o), Supabase, và Google Drive. Workflow này sẽ:
- **Xử lý tất cả loại tin nhắn**: văn bản, hình ảnh, âm thanh, PDF, và vị trí.
- **Phân tích hóa đơn tự động** bằng AI để xác nhận thanh toán.
- **Gửi đơn hàng đến nhân viên** và quản lý.
- **Gửi menu và mã QR thanh toán** cho khách hàng.
- **Lưu trữ lịch sử hội thoại** để tiếp tục giao tiếp một cách tự nhiên.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian quản lý đơn hàng**: Không cần phải gọi điện hoặc chat thủ công với khách hàng.
- **Xác nhận thanh toán tự động**: AI phân tích hóa đơn (ảnh, âm thanh, PDF) để xác minh đơn hàng.
- **Giao tiếp tự động hóa**: Trả lời khách hàng 24/7 với AI GPT-4o, không cần nhân viên hỗ trợ.
- **Quản lý đơn hàng hiệu quả**: Gửi đơn hàng đến nhân viên nấu ăn và quản lý một cách tự động.
- **Tăng trải nghiệm khách hàng**: Gửi menu và mã QR thanh toán một cách nhanh chóng.
- **Lưu trữ trí nhớ hội thoại**: Supabase lưu trữ lịch sử chat để AI tiếp tục giao tiếp một cách tự nhiên.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị các tài khoản và API keys sau:
1. **WhatsApp Business API**:
   - Tài khoản WhatsApp Business Cloud (cần đăng ký trên [Meta Developer Portal](https://developers.facebook.com/)).
   - API Key và Phone Number ID.
2. **OpenAI API Key**:
   - API Key từ [OpenAI](https://platform.openai.com/) (để sử dụng GPT-4o và các mô hình khác).
3. **Supabase Account**:
   - Tài khoản [Supabase](https://supabase.com/) để lưu trữ trí nhớ hội thoại và vector database.
   - Database URL và API Key.
4. **Google Drive**:
   - Tài khoản Google với quyền truy cập vào folder chứa menu và QR code.
   - OAuth 2.0 API Key.
5. **Google Maps API Key** (nếu cần xác định vị trí khách hàng).
6. **Gemini API Key** (nếu muốn sử dụng Gemini Vision để phân tích PDF).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7298](https://n8n.io/workflows/7298) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  1. Mở n8n Workflow Editor.
  2. Nhấn **Import** và chọn file JSON.
  3. Hoặc nhấn **Create Workflow** → **Import from JSON** và dán nội dung JSON.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **42 node** và được cấu trúc theo logic sau. Các sếp cần chú ý đến các node quan trọng sau:

##### **A. Cấu hình Credentials (API Keys)**
- **WhatsApp Business Cloud**:
  - Tạo credential mới trong n8n với tên `whatsAppApi` và `whatsAppTriggerApi`.
  - Điền `Phone Number ID` và `API Key` từ WhatsApp Business Cloud.
- **OpenAI**:
  - Tạo credential `openAiApi` và điền `API Key` từ OpenAI.
- **Supabase**:
  - Tạo credential `postgres` với Database URL và API Key từ Supabase.
- **Google Drive**:
  - Tạo credential `googleDriveOAuth2Api` và kết nối với tài khoản Google.
- **Google Maps** (nếu cần):
  - Tạo credential `httpHeaderAuth` với API Key từ Google Maps.

##### **B. Cấu hình Node Quản Lý Hội Thoại (Chat Memory)**
- Node **`Postgres Chat Memory`** (tên: `Postgres Chat Memory`, `Postgres Chat Memory1`, `Postgres Chat Memory4`):
  - Đảm bảo kết nối với Supabase đúng.
  - Cấu hình `tableName` và `collectionName` phù hợp với schema của bạn.

##### **C. Cấu hình AI (GPT-4o và Gemini)**
- Node **`OpenAI Chat Model`** (gpt-4o, gpt-4o-mini, o3-mini):
  - Đảm bảo `model` được chọn là `gpt-4o` (hoặc mô hình khác nếu muốn thay đổi).
  - Cấu hình `prompt` trong node **`Agent`** (ví dụ: `Order Format`, `Receipt Analysis`) để phù hợp với quy trình của quán.
- Node **`Extract PDF Content Using Gemini Vision`**:
  - Nếu sử dụng Gemini, điền `API Key` vào credential `httpQueryAuth`.

##### **D. Cấu hình WhatsApp**
- Node **`WhatsAppTrigger`** (tên: `Message Received`):
  - Đảm bảo `Phone Number ID` và `Webhook URL` được cấu hình đúng.
- Node **`WhatsApp Business Cloud`** (gửi tin nhắn):
  - Chọn `recipient` là số điện thoại khách hàng.
  - Cấu hình `message` từ node **`Set`** (ví dụ: `Text`, `Image`, `Audio`).

##### **E. Cấu hình Menu và QR Code**
- Node **`Menu 1`** (Google Drive):
  - Chọn file menu từ Google Drive và cấu hình `operation: download`.
- Node **`Download file`** (QR code):
  - Tải file QR code từ Google Drive và gửi cho khách hàng.

##### **F. Cấu hình Logic Xử Lý Hóa Đơn**
- Node **`If`**, **`Switch`**, và **`Agent`**:
  - Cấu hình logic để phân loại tin nhắn (hóa đơn ảnh, âm thanh, PDF, văn bản).
  - Node **`Structured Output Parser`** giúp AI trả về định dạng đơn hàng chuẩn.

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi tin nhắn mẫu (ảnh hóa đơn, âm thanh, văn bản) từ WhatsApp Business đến số điện thoại được kết nối.
   - Kiểm tra workflow có xử lý đúng không (xem log trong n8n).
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp Slack/Telegram để báo cáo đơn hàng**:
   - Sử dụng node **`Slack`** hoặc **`Telegram`** để gửi thông báo đơn hàng mới đến quản lý.
2. **Lưu log tất cả giao dịch**:
   - Sử dụng node **`Set`** kết hợp với **`Google Sheets`** hoặc **`Airtable`** để lưu lịch sử đơn hàng.
3. **Gửi báo cáo hàng ngày**:
   - Sử dụng node **`Schedule`** (n8n Pro) để gửi báo cáo tổng hợp đơn hàng qua email.
4. **Cập nhật menu tự động**:
   - Sử dụng **Google Sheets** kết nối với **Google Drive** để cập nhật menu một cách tự động.
5. **Xử lý lỗi tự động**:
   - Sử dụng node **`Code`** để xử lý trường hợp AI không phân tích được hóa đơn.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa toàn bộ quy trình đặt hàng, xác nhận thanh toán, và giao tiếp với khách hàng qua WhatsApp. Bằng cách kết hợp **AI GPT-4o, Supabase, và các dịch vụ cloud**, quán ăn của các sếp sẽ **tiết kiệm thời gian, giảm sai sót, và nâng cao trải nghiệm khách hàng**.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Cấu hình các API keys** và import workflow.
3. **Test và bật Active** để bắt đầu tự động hóa ngay!

👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/7298) và bắt đầu!