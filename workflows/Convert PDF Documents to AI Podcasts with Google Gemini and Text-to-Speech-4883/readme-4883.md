---
title: "🎙️ Chuyển PDF thành Podcast AI Tự Động với Google Gemini & Text-to-Speech - Tiết Kiệm 100% Thời Gian Nội Dung"
description: "Workflow tự động hóa hoàn toàn không cần code chuyển đổi tài liệu PDF thành podcast AI chất lượng cao với giọng nói tự nhiên, giúp các sếp tiết kiệm thời gian và nâng cao hiệu quả nội dung marketing. Kết quả: Podcast WAV sẵn sàng phát sóng chỉ trong vài giây!"
slug: "chuyen-pdf-thanh-podcast-ai-voi-google-gemini"
tags: [n8n, automation, ai-marketing, google-gemini, text-to-speech, no-code]
keywords: [n8n workflow podcast, tự động hóa nội dung, convert pdf thành podcast, google gemini api, text to speech tự động]
---

# 🚀 **Chuyển PDF thành Podcast AI Tự Động với Google Gemini & Text-to-Speech**

### **Giải pháp hoàn hảo cho các sếp muốn:**
- **Tạo podcast từ tài liệu PDF** mà không cần ghi âm thủ công.
- **Tiết kiệm 10+ giờ/ngày** cho việc biên tập và ghi âm nội dung.
- **Nâng cao chất lượng giọng nói** với công nghệ AI hiện đại.
- **Phát sóng podcast 24/7** mà không cần can thiệp người dùng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động ổn định và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian:** Chuyển PDF thành podcast chỉ trong **vài giây** thay vì nhiều giờ ghi âm.
✅ **Giọng nói tự nhiên:** Sử dụng **Google Gemini** để tạo script và **Text-to-Speech** với giọng nói ấn tượng.
✅ **Chất lượng chuyên nghiệp:** Podcast được lưu dưới định dạng **WAV** sẵn sàng phát sóng.
✅ **Hoạt động liên tục:** Workflow tự động hóa, không cần can thiệp người dùng.
✅ **Tích hợp AI:** Sử dụng **Google Gemini** để tạo script podcast thông minh, phù hợp với nội dung PDF.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
- **API Key Google Gemini** (để sử dụng AI tạo script và Text-to-Speech).
- **Tài khoản n8n** (cài đặt trên máy chủ hoặc VPS).
- **File PDF** (cần upload thủ công qua node **Manual Trigger**).

:::info[Cách lấy API Key Google Gemini]
1. Đăng ký tài khoản tại: [Google AI Studio](https://aistudio.google.com/).
2. Tạo **API Key** và thêm vào **Credentials** của n8n với tên: **"Google Gemini(PaLM) Api account"**.
3. Cấu hình **httpCustomAuth** cho node **Text-to-Speech** (nếu cần).
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
```bash
# Nếu import từ file JSON:
- Tải file workflow từ [n8n.io/workflows/4883](https://n8n.io/workflows/4883).
- Vào **n8n Editor** → **Import Workflow** → Chọn file JSON.

# Nếu copy/paste JSON:
- Copy toàn bộ JSON từ [n8n.io/workflows/4883](https://n8n.io/workflows/4883).
- Vào **n8n Editor** → **Import Workflow** → Chọn **Paste JSON**.
```

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **📄 Node 1: 🎬 Start (Manual Trigger)**
- **Cách hoạt động:** Các sếp cần **upload PDF** thủ công qua node này.
- **Lưu ý:** Đảm bảo file PDF được chọn là **PDF chuẩn** (không bị lỗi format).

#### **🤖 Node 2: 📄 Extract Text from PDF**
- **Công việc:** Trích xuất toàn bộ văn bản từ PDF.
- **Lưu ý:** Node này tự động xử lý, không cần cấu hình thêm.

#### **🤖 Node 3: 🤖 Generate Podcast Script (ChainLlm)**
- **Công việc:** Sử dụng **Google Gemini** để tạo script podcast từ văn bản trích xuất.
- **Lưu ý:**
  - **Prompt mặc định:** `"Convert this PDF text into a conversational podcast script. Make it engaging and natural."`
  - **Nếu muốn thay đổi prompt:** Cập nhật trong **Configuration** của node này.

#### **🤖 Node 4: Google Gemini Flash 2.0**
- **Công việc:** Sử dụng API **Google Gemini** để tạo script podcast.
- **Lưu ý:**
  - **Credentials:** Đã cấu hình sẵn với tên **"googlePalmApi"**.
  - **Không cần thay đổi** nếu đã thêm API Key đúng cách.

#### **⚙️ Node 5: ⚙️ Prepare TTS Request (Code)**
- **Công việc:** Chuẩn bị dữ liệu để chuyển text thành giọng nói.
- **Lưu ý:**
  - Node này **không cần chỉnh sửa** nếu đã import workflow chính xác.
  - Nếu cần thay đổi, các sếp có thể mở **Code Editor** và cập nhật logic.

#### **🎙️ Node 6: 🎙️ Convert Text to Speech With Gemini (HTTP Request)**
- **Công việc:** Chuyển script podcast thành âm thanh.
- **Lưu ý:**
  - **Credentials:** Sử dụng **"googlePalmApi"** (API Key Gemini) và **"httpCustomAuth"** (nếu cần).
  - **URL API:** Đã cấu hình sẵn, không cần thay đổi.

#### **🔧 Node 7: 🔧 Process Audio Response (Code)**
- **Công việc:** Xử lý phản hồi âm thanh từ API.
- **Lưu ý:**
  - Node này **tự động xử lý**, không cần chỉnh sửa.

#### **💾 Node 8: 💾 Save Podcast Audio (Write Binary File)**
- **Công việc:** Lưu podcast dưới dạng **WAV file**.
- **Lưu ý:**
  - **Đường dẫn lưu:** Cần **cấu hình** trong **Configuration** (ví dụ: `/podcasts/`).
  - **Tên file:** Có thể tự động hóa bằng **{{ $node["Extract Text from PDF"].json["$response.body"].fileName }}**.

---

### **3. Kích hoạt ⚡️**
1. **Test Run:** Upload một file PDF mẫu (ví dụ: bài báo, tài liệu marketing).
2. **Kiểm tra kết quả:**
   - Script podcast được tạo từ AI.
   - Âm thanh được chuyển đổi thành giọng nói tự nhiên.
   - File WAV được lưu thành công.
3. **Bật Active:** Nếu test thành công, **bật workflow** để hoạt động liên tục.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tích hợp với Slack/Telegram để thông báo kết quả**
- Sử dụng **node Slack Webhook** hoặc **Telegram Bot** để gửi thông báo khi podcast hoàn thành.
- **Cách làm:**
  - Thêm node **Slack Webhook** sau **Save Podcast Audio**.
  - Cấu hình message: `"Podcast đã tạo thành công! Tải tại: [link]"`.
  - **Lợi ích:** Các sếp được thông báo ngay khi podcast sẵn sàng.

### **2. Lưu log hoạt động để theo dõi**
- Sử dụng **node Sticky Note** để ghi lại thông tin debug.
- **Cách làm:**
  - Thêm node **Sticky Note** sau **Process Audio Response**.
  - Ghi log: `"File: {{ $node["Extract Text from PDF"].json["$response.body"].fileName }} - Kích thước: {{ $node["Save Podcast Audio"].json["$response.body"].size }} bytes"`.

### **3. Tự động gửi podcast qua email định kỳ**
- Sử dụng **node Email** (ví dụ: Gmail) để gửi podcast cho khách hàng.
- **Cách làm:**
  - Thêm node **Gmail** sau **Save Podcast Audio**.
  - Cấu hình email: `"Chào [Tên Khách Hàng], Podcast mới đã sẵn sàng: [link]"`.
  - **Lợi ích:** Tự động hóa phân phối nội dung cho khách hàng.

### **4. Chuyển đổi nhiều file PDF cùng lúc**
- Sử dụng **node Loop** để xử lý nhiều file PDF trong một lần.
- **Cách làm:**
  - Thêm node **Loop** trước **Manual Trigger**.
  - Cấu hình: `"Loop through all files in a folder"`.
  - **Lợi ích:** Tiết kiệm thời gian khi xử lý nhiều tài liệu.

---

## 📌 **Kết luận**
Workflow **"Chuyển PDF thành Podcast AI"** là giải pháp **tự động hóa hoàn toàn** giúp các sếp:
✔ **Tiết kiệm thời gian** ghi âm và biên tập.
✔ **Nâng cao chất lượng nội dung** với giọng nói tự nhiên.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**Hãy áp dụng ngay workflow này và bắt đầu tạo podcast AI trong giây lát!** 🚀

---
**🔗 [Xem workflow gốc tại n8n.io](https://n8n.io/workflows/4883)**
**📌 [Hướng dẫn cài đặt n8n trên VPS](https://docs.n8n.io/hosting/installation/installation-on-a-vps/)**