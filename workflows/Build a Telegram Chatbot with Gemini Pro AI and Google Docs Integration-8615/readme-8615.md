---
title: "🤖 Tự Động Hóa Chatbot Telegram Siêu Nhanh với Gemini Pro AI + Google Docs - Không Cần Code!"
description: "Cài đặt workflow tự động hóa chatbot Telegram sử dụng trí tuệ nhân tạo Gemini Pro của Google và tích hợp Google Docs để trả lời tự động, trả lời FAQ, hoặc hỗ trợ khách hàng 24/7. Tiết kiệm thời gian lên tới 80% cho các sếp và nhân viên hỗ trợ!"
slug: "tay-dong-hoa-chatbot-telegram-gemini-pro-google-docs"
tags: [n8n, automation, ai-chatbot, telegram-bot, google-gemini, google-docs, no-code]
keywords: [n8n workflow telegram chatbot, tự động hóa chatbot Telegram, Gemini Pro AI, tích hợp Google Docs, tự động trả lời FAQ, hỗ trợ khách hàng AI]
---

# 🚀 **Tự Động Hóa Chatbot Telegram Siêu Nhanh với Gemini Pro AI + Google Docs**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Các sếp và nhân viên hỗ trợ khách hàng thường phải mất **giờ đồng hồ** để trả lời các câu hỏi lặp đi lặp lại, kiểm tra tài liệu trên Google Docs, hoặc xử lý yêu cầu đơn giản. Với **workflow này**, các sếp có thể:
✅ **Tự động hóa hoàn toàn** quá trình trả lời trên Telegram bằng trí tuệ nhân tạo **Gemini Pro** (mô hình AI tiên tiến nhất của Google).
✅ **Tích hợp Google Docs** để trả lời FAQ, cung cấp thông tin từ tài liệu, hoặc even tự động tạo phản hồi cá nhân hóa.
✅ **Loại bỏ hoàn toàn công việc thủ công**, tiết kiệm **tối thiểu 80% thời gian** cho đội ngũ hỗ trợ.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải trả lời lại các câu hỏi lặp đi lặp lại.
- **Trả lời chính xác & tự động**: Gemini Pro hiểu ngữ cảnh và trả lời như người chuyên nghiệp.
- **Tích hợp Google Docs**: Trả lời từ tài liệu chính thức, giảm thiểu sai sót.
- **Hoạt động liên tục**: Chatbot hoạt động 24/7, không cần nghỉ ngơi.
- **Dễ dàng mở rộng**: Thêm logic mới chỉ với vài click mà không cần viết code.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo bot trên [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Cài đặt bot vào nhóm hoặc chat cá nhân để test.
2. **Google Gemini API Key**:
   - Đăng ký tại [Google AI Studio](https://aistudio.google.com/) và lấy **API Key**.
   - Chọn mô hình **Gemini Pro** (`models/gemini-pro`) hoặc **Gemini Flash** (`models/gemini-2.0-flash-exp`).
3. **Google Docs OAuth 2.0**:
   - Tạo **Service Account** trong [Google Cloud Console](https://console.cloud.google.com/) và cấp quyền truy cập vào Google Drive.
   - Lấy **Client ID** và **Client Secret** để kết nối với n8n.
4. **File JSON Workflow**:
   - Tải workflow từ [n8n.io/workflows/8615](https://n8n.io/workflows/8615) hoặc copy JSON từ trang này.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
#### **Cách 1: Import từ file JSON**
1. Tải file JSON từ [n8n.io/workflows/8615](https://n8n.io/workflows/8615).
2. Trên **n8n Editor**, click vào **Import** (icon hình mũi tên vòng tròn).
3. Chọn file JSON và click **Import**.

#### **Cách 2: Copy/Paste JSON**
1. Copy toàn bộ JSON từ trang này (hoặc từ link trên).
2. Trên **n8n Editor**, click **Import** → **Paste JSON**.
3. Chọn **Import**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp **phải cấu hình** các node quan trọng sau:

#### **🔹 Node 1: Telegram Trigger (`telegramTrigger`)**
- **Credentials**: Chọn **Telegram Bot Token** đã tạo từ `@BotFather`.
- **Chat ID**: Lấy từ [@userinfobot](https://t.me/userinfobot) và nhập vào.
- **Message Type**: Chọn **Text** (hoặc **Any** nếu muốn hỗ trợ nhiều loại tin nhắn).

#### **🔹 Node 2: Loop Over Items (`splitInBatches`)**
- **Batch Size**: Đặt **1** (mặc định) để xử lý từng tin nhắn một.
- **Delay Between Batches**: Đặt **1 giây** (đã có sẵn trong node `Wait 1s`).

#### **🔹 Node 3: Message a model (`langchain.googleGemini`)**
- **API Key**: Nhập **Google Gemini API Key** từ Google AI Studio.
- **Model**: Chọn **`models/gemini-pro`** (hoặc `gemini-2.0-flash-exp` nếu muốn tốc độ nhanh hơn).
- **Prompt Template**:
  ```plaintext
  You are a helpful assistant. Reply to the user's message in a friendly and professional tone.
  If the message contains a question, provide a detailed answer.
  If the user asks for information from Google Docs, fetch it and include in the response.
  ```
  *(Các sếp có thể tùy chỉnh prompt theo nhu cầu.)*

#### **🔹 Node 4: Get a document in Google Docs (`googleDocsTool`)**
- **Credentials**: Chọn **Google OAuth 2.0** đã cấu hình.
- **Document ID**: Lấy từ URL của Google Docs (ví dụ: `https://docs.google.com/document/d/1ABC123...` → **1ABC123** là Document ID).
- **Operation**: Đặt **`get`** (lấy nội dung tài liệu).

#### **🔹 Node 5: HTTP Request (`httpRequestTool`)**
- **URL**: Đặt **`https://devcodejourney.com/`** (hoặc thay thế bằng API của các sếp).
- **Method**: Chọn **GET** (hoặc **POST** nếu cần gửi dữ liệu).
- **Headers**: Thêm `Content-Type: application/json` nếu cần.

#### **🔹 Node 6: Send a text message (`telegram`)**
- **Credentials**: Chọn **Telegram Bot Token** cùng với node `Telegram Trigger`.
- **Chat ID**: Sử dụng cùng **Chat ID** đã nhập ở node `Telegram Trigger`.
- **Message**: Sử dụng **output từ node Gemini** để trả lời tự động.

#### **🔹 Node 7: Wait 1s (`wait`)**
- **Time**: Đặt **1000ms** (1 giây) để tránh bị Telegram rate limit.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với tin nhắn mẫu:
   - Gửi tin nhắn từ Telegram đến bot (ví dụ: *"Chào bot, tôi muốn biết về dịch vụ của công ty"*).
   - Kiểm tra nếu bot trả lời chính xác.
2. **Bật Active**:
   - Click vào **Active** ở góc trên bên phải của n8n Editor.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
Các sếp có thể **mở rộng** workflow này để phù hợp hơn với nhu cầu:
1. **Thêm Logic Lọc Tin Nhắn**:
   - Sử dụng **`Set` node** để kiểm tra nếu tin nhắn chứa từ khóa như *"FAQ"*, *"giá cả"*, *"hỗ trợ"* → chuyển sang node Gemini.
   - Nếu không, bot có thể trả lời tự động: *"Xin lỗi, tôi chưa hỗ trợ được yêu cầu này. Hãy liên hệ với admin!"*

2. **Lưu Log Tất Cả Các Tin Nhắn**:
   - Thêm **`Set` node** sau `Telegram Trigger` để lưu tin nhắn vào **Google Sheets** hoặc **Database**.
   - Cài đặt **`n8n-nodes-base.googleSheets`** để tự động ghi lại lịch sử.

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **`Set` node** kết hợp với **`Schedule` node** để gửi báo cáo tổng hợp về hoạt động của bot qua **Email** hoặc **Slack**.

4. **Tích Hợp Slack/Telegram**:
   - Thay vì chỉ Telegram, các sếp có thể thêm **`Slack` node** để bot hoạt động trên cả 2 nền tảng.

5. **Cải Thiện Prompt cho Gemini**:
   - Nếu bot trả lời không chính xác, các sếp có thể **tùy chỉnh prompt** để Gemini hiểu rõ hơn ngữ cảnh:
     ```plaintext
     You are a customer support assistant for [Tên Công Ty]. Always:
     1. Use a polite and professional tone.
     2. If the user asks about pricing, fetch the latest info from Google Docs.
     3. If the user asks about a specific product, provide detailed features.
     4. If you don't know the answer, say: "I'm sorry, I can't find that information. Please contact our admin at [email]".
     ```

---

## 📌 **Kết Luận**
Với **workflow này**, các sếp đã có một **chatbot Telegram tự động hóa hoàn toàn**, tích hợp trí tuệ nhân tạo **Gemini Pro** và **Google Docs**, giúp tiết kiệm **thời gian, giảm sai sót**, và **hỗ trợ khách hàng 24/7** mà không cần can thiệp của con người.

👉 **Hãy áp dụng ngay** và tự động hóa đội ngũ hỗ trợ của mình!
👉 **Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để workflow chạy ổn định!

---
**#TựĐộngHóa #AIChatbot #GeminiPro #GoogleDocs #n8n**