---
title: "🤖 **Tự Động Hóa Trợ Lý WhatsApp AI Đa Phương Tiện (Text, Audio, Image) Với GPT-4o & Evolution API - Không Cần Code**"
description: "Workflow này tự động hóa hoàn toàn trợ lý WhatsApp AI xử lý tin nhắn văn bản, âm thanh, hình ảnh và tài liệu với trí tuệ nhân tạo GPT-4o, nhớ đối thoại qua PostgreSQL và quản lý hàng đợi tin nhắn bằng Redis. Giúp doanh nghiệp tiết kiệm 80% thời gian hỗ trợ khách hàng 24/7."
slug: "tay-dong-hoa-tro-ly-whatsapp-ai-da-phuong-tien"
tags: [n8n, automation, ai-chatbot, evolution-api, gpt-4o, no-code, chatbot-whatsapp]
keywords: [tự động hóa trợ lý WhatsApp AI, GPT-4o tự động hóa, Evolution API n8n, xử lý âm thanh hình ảnh WhatsApp, chatbot AI không code, tự động hóa hỗ trợ khách hàng]
---

# 🚀 **Tự Động Hóa Trợ Lý WhatsApp AI Đa Phương Tiện (Text, Audio, Image) Với GPT-4o & Evolution API**

## **🔥 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Hiện nay, các doanh nghiệp phải mất **giờ đồng hồ** mỗi ngày để:
- **Trả lời tin nhắn WhatsApp** của khách hàng (văn bản, âm thanh, hình ảnh, tài liệu).
- **Nhớ lịch sử đối thoại** giữa các cuộc trò chuyện.
- **Quản lý hàng đợi** khi khách hàng gửi nhiều tin nhắn liên tiếp.
- **Xử lý tin nhắn không hỗ trợ** (ví dụ: file PDF, âm thanh dài) một cách thủ công.

**Workflow này tự động hóa hoàn toàn** tất cả các công việc trên bằng trí tuệ nhân tạo **GPT-4o**, kết hợp với:
✅ **Xử lý đa phương tiện** (text, audio, image, document)
✅ **Nhớ đối thoại** (PostgreSQL)
✅ **Hàng đợi tin nhắn** (Redis)
✅ **Trả lời tự động với hiệu suất cao**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** hỗ trợ khách hàng (tự động trả lời text, audio, image).
- **Hỗ trợ khách hàng 24/7** mà không cần nhân viên trực.
- **Nhớ lịch sử trò chuyện** (không mất thời gian nhắc lại thông tin).
- **Xử lý tin nhắn đa phương tiện** (âm thanh → văn bản, hình ảnh → mô tả).
- **Trả lời tự động với giọng điệu tự nhiên** (giống người).
- **Quản lý hàng đợi tin nhắn** (không bị mất tin nhắn giữa chừng).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng, các sếp cần chuẩn bị:
✔ **Tài khoản Evolution API** (để kết nối WhatsApp)
✔ **API Key OpenAI** (để sử dụng GPT-4o)
✔ **Redis** (để quản lý hàng đợi tin nhắn)
✔ **PostgreSQL** (để lưu nhớ đối thoại)
✔ **VPS n8n** (để chạy workflow 24/7)
✔ **Node Evolution API** (cài đặt từ [n8n Community](https://github.com/n8n-community/n8n-nodes-evolution-api))
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/11754) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Workflow Editor**.
  2. Nhấn **Import** → **Paste JSON**.
  3. Chọn **Import Workflow**.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này **phức tạp** vì xử lý **4 loại tin nhắn khác nhau** (text, audio, image, document). Các bước **cần chỉnh sửa bắt buộc**:

#### **A. Cấu Hình Webhook (Receive WhatsApp)**
- Node: **"Receive WhatsApp" (webhook)**
- **Cấu hình**:
  - **Path**: `whatsapp-multimodal` (không đổi)
  - **HTTP Method**: `POST` (không đổi)
  - **Credentials**: Tạo mới **Evolution API** với:
    - **Server URL**: `https://api.evolution-api.com`
    - **API Key**: Đăng ký tại [Evolution API](https://evolution-api.com/)

#### **B. Lọc Số Điện Thoại Cho Phep (Filter Allowed Numbers)**
- Node: **"Filter Allowed Numbers" (filter)**
- **Cấu hình**:
  - Thêm **điều kiện** để chỉ cho phép số điện thoại của khách hàng hợp lệ.
  - Ví dụ: `jsonpath("$.from") == "YOUR_ALLOWED_NUMBER"`

#### **C. Xử Lý Tin Nhắn Âm Thanh (Audio)**
- **Node "Transcribe Audio" (openAi)**
  - **API Key**: Điền **OpenAI API Key**.
  - **Model**: `whisper-1` (mặc định).
  - **File Input**: Sử dụng **Base64** từ node **"Convert to Audio"**.

- **Node "Format Audio Input" (set)**
  - **Cấu hình**:
    ```json
    {
      "jsonpath": "$",
      "value": {
        "model": "gpt-4o-mini",
        "messages": [
          {
            "role": "user",
            "content": "Transcribe this audio: {{$json["transcription"]}}"
          }
        ]
      }
    }
    ```

#### **D. Xử Lý Tin Nhắn Hình Ảnh (Image)**
- **Node "Analyze Image" (openAi)**
  - **API Key**: Điền **OpenAI API Key**.
  - **Model**: `gpt-4o` (mặc định).
  - **File Input**: Sử dụng **Base64** từ node **"Convert to Image"**.

- **Node "Format Image Input" (set)**
  - **Cấu hình**:
    ```json
    {
      "jsonpath": "$",
      "value": {
        "model": "gpt-4o-mini",
        "messages": [
          {
            "role": "user",
            "content": "Describe this image: {{$json["description"]}}"
          }
        ]
      }
    }
    ```

#### **E. Cấu Hình Redis (Queue Tin Nhắn)**
- **Node "Queue Message" (redis)**
  - **Host**: `localhost` (hoặc IP VPS của bạn).
  - **Port**: `6379` (mặc định).
  - **Password**: (Nếu có).

- **Node "Get Queued Messages" (redis)**
  - **Key**: `whatsapp_messages` (không đổi).

#### **F. Cấu Hình PostgreSQL (Nhớ Đối Thoại)**
- **Node "Postgres Chat Memory" (memoryPostgresChat)**
  - **Host**: `localhost` (hoặc IP VPS).
  - **Port**: `5432` (mặc định).
  - **Database**: `n8n_chat_memory`.
  - **User**: `postgres`.
  - **Password**: (Đặt mật khẩu khi cài đặt).

#### **G. Cấu Hình AI Agent (GPT-4o)**
- **Node "OpenAI Chat Model" (lmChatOpenAi)**
  - **Model**: `gpt-4o-mini` (mặc định).
  - **API Key**: Điền **OpenAI API Key**.

- **Node "AI Agent" (agent)**
  - **System Prompt**: Tùy chỉnh theo nhu cầu (ví dụ: "Bạn là trợ lý hỗ trợ khách hàng của công ty XYZ").

#### **H. Cấu Hình Trả Lời Tin Nhắn**
- **Node "Send Text" / "Send Image" (evolutionApi)**
  - **Credentials**: Sử dụng **Evolution API** đã cấu hình trước.
  - **Message**: Sử dụng kết quả từ **Structured Output Parser**.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi tin nhắn **text, audio, image** từ WhatsApp đến webhook.
   - Kiểm tra **log** trong n8n để đảm bảo workflow chạy đúng.
2. **Bật Active workflow**:
   - Nhấn **Active** trên tab **Workflow**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tùy Chỉnh AI Agent**
- **Thay đổi System Prompt** để AI trả lời phù hợp với **ngành nghề** của bạn.
- **Ví dụ**:
  ```json
  {
    "role": "system",
    "content": "Bạn là trợ lý hỗ trợ khách hàng của công ty bán hàng điện thoại. Hãy trả lời thân thiện và chuyên nghiệp."
  }
  ```

### **2. Thêm Log Lịch Sử Trò Chuyện**
- Sử dụng **n8n-nodes-base.set** để lưu **tất cả tin nhắn** vào **Google Sheets** hoặc **Notion**.
- **Cách làm**:
  - Thêm node **Google Sheets** sau **"Postgres Chat Memory"**.
  - Cấu hình **Sheet Name** và **Credentials**.

### **3. Gửi Báo Cáo Định Kỳ**
- Sử dụng **n8n-nodes-base.aggregate** để **tổng hợp thống kê** tin nhắn trong ngày.
- **Ví dụ**:
  - Đếm số tin nhắn **text, audio, image**.
  - Gửi báo cáo qua **Email** hoặc **Slack**.

### **4. Thêm Hỗ Trợ Telegram**
- Sử dụng **n8n-nodes-telegram** để **chuyển tiếp tin nhắn** từ WhatsApp sang Telegram.
- **Cách làm**:
  - Thêm node **Telegram Bot** sau **"Send Text"**.
  - Cấu hình **Chat ID** và **API Token**.

### **5. Tăng Thời Gian Chờ (Wait Between Messages)**
- **Node "Wait Between Messages" (wait)**
  - **Thời gian mặc định**: `10s` (có thể tăng lên `15s` để tránh bị WhatsApp flag).

---

## 📌 **Kết Luận**
Workflow này **giải phóng hoàn toàn** thời gian của các sếp để tập trung vào **kinh doanh** thay vì hỗ trợ khách hàng. Với **GPT-4o + Evolution API**, trợ lý WhatsApp AI của bạn sẽ:
✅ **Hiểu và trả lời** tất cả loại tin nhắn (text, audio, image).
✅ **Nhớ lịch sử trò chuyện** để không bị lặp lại.
✅ **Hỗ trợ 24/7** mà không cần nhân viên trực.
✅ **Tự động hóa hoàn toàn** (không cần code).

**🚀 Hãy áp dụng ngay hôm nay!**
- **Import workflow** từ [đây](https://n8n.io/workflows/11754).
- **Cấu hình Evolution API, Redis, PostgreSQL, OpenAI**.
- **Bật Active** và bắt đầu tự động hóa!

---
**💡 Lưu ý cuối cùng**:
- Nếu gặp **lỗi API**, kiểm tra **log** trong n8n và **cấu hình lại credentials**.
- Nếu **Redis/PostgreSQL không hoạt động**, đảm bảo **VPS có kết nối mạng ổn định**.
- **Tùy chỉnh System Prompt** để AI phù hợp với **ngành nghề** của bạn.

**Chúc các sếp thành công!** 🚀