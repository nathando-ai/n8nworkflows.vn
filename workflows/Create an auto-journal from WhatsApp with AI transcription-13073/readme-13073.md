---
title: "📱 Tự Động Hóa Sổ Nhật Ký WhatsApp Với AI Phiên Âm - Không Cần Code!"
description: "Tự động lưu tất cả tin nhắn, ghi âm và ảnh từ WhatsApp vào Google Docs với phiên âm AI, đồng thời gửi xác nhận tự động - giải phóng thời gian cho các sếp trong công việc hàng ngày."
slug: "tự-dộng-hoa-so-nhat-ky-whatsapp-voi-ai-phien-am"
tags: [n8n, automation, no-code, google-docs, ai-transcription, whatsapp-business-api]
keywords: [n8n workflow whatsapp, tự động hóa nhật ký, phiên âm giọng nói, google gemini ai, lưu tin nhắn whatsapp, google drive tự động]
---

# 🚀 **Tự Động Hóa Sổ Nhật Ký WhatsApp Với AI Phiên Âm - Không Cần Code!**

### **Giải pháp hoàn hảo cho các sếp muốn:**
- **Lưu trữ tất cả cuộc trò chuyện** (tin nhắn, ghi âm, ảnh) từ WhatsApp vào một **Google Doc** duy nhất.
- **Phiên âm tự động** tất cả ghi âm bằng **Google Gemini AI** (chất lượng cao, không cần code).
- **Xác nhận tự động** trên WhatsApp khi lưu thành công.
- **Tiết kiệm thời gian** lên đến **90%** so với việc ghi chép thủ công.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động hóa hoàn toàn** - Không cần nhớ ghi chép, tất cả cuộc trò chuyện được lưu tự động.
✅ **Phiên âm AI chính xác** - Ghi âm được chuyển thành văn bản bằng Google Gemini (chất lượng cao).
✅ **Lưu trữ an toàn** - Tất cả tin nhắn, ghi âm và ảnh được lưu vào **Google Drive** và **Google Docs**.
✅ **Xác nhận tức thời** - WhatsApp tự động gửi thông báo khi lưu thành công.
✅ **Dễ dàng truy cập** - Tất cả dữ liệu tập trung ở một **Google Doc** duy nhất, có thể chia sẻ hoặc xuất PDF.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
✔ **Tài khoản WhatsApp Business API** (đăng ký tại [Meta Business](https://developers.facebook.com/docs/whatsapp/cloud-api/get-started)).
✔ **Google Service Account** (để truy cập Google Drive & Docs).
✔ **API Key Google Gemini** (để phiên âm ghi âm).
✔ **Google Drive** (đã tạo 2 folder riêng cho **audio** và **image**).
✔ **Google Doc** (đã tạo sẵn để lưu nhật ký).
✔ **Số điện thoại được ủy quyền** (để kiểm tra tin nhắn).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Bước 1:** Tải file JSON từ [n8n.io/workflows/13073](https://n8n.io/workflows/13073) hoặc copy toàn bộ JSON từ link trên.
- **Bước 2:** Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON hoặc chọn file JSON.
- **Bước 3:** Chọn **"Import"** để tạo workflow.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **17 node** và cần cấu hình kỹ lưỡng. Dưới đây là hướng dẫn chi tiết:

#### **🔹 Node 1: WhatsApp Trigger (`whatsappTrigger`)**
- **Không cần chỉnh gì**, chỉ cần **bật Active** sau khi cấu hình xong.

#### **🔹 Node 2: Authorized Numbers Check (`if`)**
- **Cấu hình điều kiện:**
  - Thay `YOURNUMBERPHONE(1/2/3)` bằng **số điện thoại được ủy quyền** (định dạng quốc tế, **không dấu +**).
  - Ví dụ: `843212345678` (Việt Nam) hoặc `14155552671` (Mỹ).
  - Nếu muốn thêm nhiều số, dùng **OR** (`||`) trong điều kiện:
    ```json
    $json["from"].includes("843212345678") || $json["from"].includes("14155552671")
    ```

#### **🔹 Node 3-4: Get Audio/Image URL (`whatsapp`)**
- **Không cần chỉnh**, node này tự động lấy URL của file từ tin nhắn.

#### **🔹 Node 5-6: Download Audio/Image (`httpRequest`)**
- **Không cần chỉnh**, node này tự động tải file từ URL.

#### **🔹 Node 7-8-10-12: Google Docs (`googleDocs`)**
- **Cấu hình:**
  - Thay `YOUR_GOOGLE_DOC_URL` bằng **URL của Google Doc** bạn muốn lưu nhật ký.
  - Ví dụ: `https://docs.google.com/document/d/1AbCdEfGhIjKlMnOpQrStUvWxYz/`.
  - **Chú ý:** Đảm bảo tài khoản n8n có quyền **sửa** Google Doc này.

#### **🔹 Node 9: Transcribe Audio with AI (`googleGemini`)**
- **Cấu hình:**
  - **API Key:** Điền **API Key của Google Gemini** (tạo tại [Google AI Studio](https://aistudio.google.com/)).
  - **Model:** Chọn `gemini-pro` (hoặc `gemini-1.5-flash` nếu muốn tiết kiệm chi phí).
  - **Prompt:** Sử dụng mặc định (n8n sẽ tự động chuyển đổi âm thanh thành văn bản).

#### **🔹 Node 11: Upload Audio/Image to Drive (`googleDrive`)**
- **Cấu hình:**
  - **Folder ID Audio:** Thay `YOUR_AUDIO_FOLDER_ID` bằng **ID folder** của folder lưu âm thanh (lấy từ URL Google Drive).
    - Ví dụ: Nếu URL là `https://drive.google.com/drive/folders/1AbCdEfGhIjKlMnOpQrStUvWxYz`, thì **Folder ID = `1AbCdEfGhIjKlMnOpQrStUvWxYz`**.
  - **Folder ID Image:** Thay `YOUR_IMAGE_FOLDER_ID` bằng **ID folder** của folder lưu ảnh.

#### **🔹 Node 13-15: Send Confirmation (`whatsapp`)**
- **Cấu hình:**
  - Thay `YOUR_WHATSAPP_PHONE_NUMBER_ID` bằng **ID của số điện thoại WhatsApp Business** (lấy từ Meta Business API).
  - **Lưu ý:** Nếu muốn gửi xác nhận cho nhiều người, thêm nhiều node `whatsapp` với điều kiện khác nhau.

---
### **3. Kích hoạt ⚡️**
- **Bước 1:** Nhấn **"Run"** để test với một tin nhắn mẫu.
- **Bước 2:** Kiểm tra **Google Doc** và **Google Drive** để xác nhận dữ liệu đã lưu.
- **Bước 3:** Nếu test thành công, **bật Active** workflow.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
🔹 **Gửi báo cáo định kỳ:** Sử dụng **n8n + Google Sheets** để tự động tạo báo cáo tổng hợp hàng tuần.
🔹 **Kết hợp Slack/Telegram:** Thêm node `slack` hoặc `telegram` để thông báo khi lưu thành công.
🔹 **Lưu log:** Sử dụng **Google Sheets** hoặc **Google Docs** để ghi lại lịch sử hoạt động.
🔹 **Tự động chia sẻ:** Khi lưu xong, tự động chia sẻ Google Doc với người liên quan bằng node `googleDrive`.
🔹 **Phân loại tin nhắn:** Sử dụng **Google Docs Table** để phân loại tin nhắn theo chủ đề (VD: "Hợp đồng", "Yêu cầu", "Ghi chú").
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng hoàn toàn thời gian** của các sếp khỏi việc ghi chép nhật ký WhatsApp thủ công. Với **AI phiên âm Google Gemini**, tất cả ghi âm đều được chuyển thành văn bản chính xác, trong khi **Google Drive** lưu trữ an toàn tất cả dữ liệu.

**🚀 Hãy áp dụng ngay và bắt đầu tự động hóa nhật ký của mình!**
Nếu có vấn đề, hãy để lại comment bên dưới hoặc liên hệ với **Diego Alejandro Parrás** (tác giả) qua [n8n Community](https://community.n8n.io/).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Lưu ý:** Nếu gặp lỗi **CORS** hoặc **API rate limit**, hãy kiểm tra lại **API Key** và **credentials** của Google Gemini.