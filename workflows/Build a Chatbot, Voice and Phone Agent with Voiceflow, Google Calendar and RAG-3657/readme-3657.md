---
title: "🤖 Tự Động Hóa Agent Chat, Gọi Điện & Lịch Trình AI với Voiceflow + Google Calendar + RAG (N8N)"
description: "Workflow tự động hóa hoàn toàn không code giúp các sếp xây dựng một agent AI đa kênh (chatbot, gọi điện, lịch trình) với khả năng truy vấn thông tin từ Google Drive, Google Calendar và hệ thống RAG (Retrieval-Augmented Generation) để trả lời chính xác và cá nhân hóa. Giảm thiểu thời gian phản hồi từ 30 phút xuống dưới 5 giây!"
slug: "tieu-dong-hoa-agent-chat-goi-dien-voi-voiceflow-google-calendar-rag"
tags: [n8n, automation, ai, voiceflow, google-calendar, rag, no-code, chatbot, phone-agent]
keywords: [n8n workflow chatbot, tự động hóa gọi điện AI, agent voiceflow n8n, google calendar automation, rag với n8n, tự động hóa không code]
---

# 🚀 **Xây Dựng Agent AI Đa Kênh: Chatbot + Gọi Điện + Lịch Trình với Voiceflow, Google Calendar & RAG**

### **🔥 Nỗi Đau Của Các Sếp Hiện Nay**
Hiện tại, khi khách hàng liên hệ qua:
- **Chatbot** (trả lời chậm, thiếu thông tin chính xác),
- **Gọi điện** (đội ngũ phải phản hồi thủ công, mất thời gian),
- **Lịch trình** (quên lịch hẹn, không tự động cập nhật),

**Kết quả?** Khách hàng mất niềm tin, doanh nghiệp mất thời gian và tiền bạc.

**Giải pháp?** Một **agent AI tự động hóa hoàn toàn** (không cần code) kết hợp:
✅ **Voiceflow** (chatbot + gọi điện + số điện thoại Twilio)
✅ **Google Calendar** (tự động tạo/quên lịch hẹn)
✅ **RAG (Retrieval-Augmented Generation)** (trả lời chính xác từ dữ liệu trong Google Drive)
✅ **N8N** (tự động hóa logic giữa các hệ thống)

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 10+ giờ/ngày** cho đội ngũ hỗ trợ khách hàng.
- **Trả lời khách hàng trong 5 giây** (thay vì 30 phút thủ công).
- **Tự động tạo lịch hẹn** trên Google Calendar khi khách hàng yêu cầu.
- **Trả lời chính xác** từ dữ liệu trong Google Drive (không sai sót).
- **Hoạt động 24/7** mà không cần nhân viên.
- **Kết hợp gọi điện thực tế** (nếu sử dụng Twilio).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản & API Keys:**
   - [Voiceflow](https://www.voiceflow.com/) (đăng ký miễn phí).
   - [OpenAI API](https://platform.openai.com/) (API Key).
   - [Qdrant](https://qdrant.tech/) (URL và Collection Name).
   - [Google Drive](https://drive.google.com/) (OAuth2 API).
   - [Google Calendar](https://calendar.google.com/) (OAuth2 API).
   - [Twilio](https://www.twilio.com/) (nếu muốn gọi điện, số điện thoại Twilio).

2. **Dữ liệu đầu vào:**
   - Tệp tin trong Google Drive (sẽ được vector hóa và lưu vào Qdrant).
   - Dữ liệu lịch hẹn (Google Calendar sẽ tự động đồng bộ).

3. **Cấu hình n8n:**
   - Cài đặt **n8n Self-hosted** (khuyến nghị trên VPS để hoạt động 24/7).
   :::info[Gợi ý hạ tầng cho n8n]
   Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
   :::
---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/3657) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import:**
  1. Mở n8n Editor → Nhấn **"Import"** → Chọn file JSON.
  2. Hoặc copy toàn bộ JSON và nhấn **"Import from JSON"**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **28 node**, các sếp cần chú ý cấu hình **các node quan trọng sau**:

##### **🔹 Step 1: Cấu Hình Qdrant Vector Store**
- **Node:** `Qdrant Vector Store` và `Retrive Qdrant Vector Store`
  - **Tham số cần thay đổi:**
    - `QDRANTURL`: URL của Qdrant (vd: `https://your-qdrant-url:6333`).
    - `COLLECTION`: Tên collection (vd: `my_collection`).
  - **Cách tạo collection:**
    - Sử dụng node `Create collection` (HTTP Request) với header:
      ```json
      {
        "Authorization": "Bearer YOUR_API_KEY"
      }
      ```
    - Gửi request POST đến:
      ```
      http://{QDRANTURL}/collections/{COLLECTION}
      ```

##### **🔹 Step 2: Cấu Hình Google Drive & Vectorization**
- **Node:** `Get folder`, `Download Files`, `Embeddings OpenAI`, `Token Splitter`
  - **Tham số cần thay đổi:**
    - `Google Drive OAuth2Api`: Thiết lập trong **Credentials** của n8n.
    - **Folder ID** trong `Get folder` (lấy từ liên kết Google Drive).
  - **Quá trình:**
    1. Lấy danh sách file từ folder.
    2. Tải xuống và vector hóa bằng OpenAI Embeddings.
    3. Lưu vào Qdrant.

##### **🔹 Step 3: Cấu Hình Voiceflow Webhooks**
- **Node:** `n8n_order`, `n8n_appointment`, `n8n_rag` (Webhook)
  - **Tham số cần thay đổi:**
    - **URL Webhook** trong Voiceflow phải trùng với `path` trong node:
      - `n8n_order`: `https://your-n8n-url/webhook/9ff7a394-5b4b-4790-a96b-c41c4ba27fa5`
      - `n8n_appointment`: `https://your-n8n-url/webhook/f5edfe92-649b-40da-ab35-f818ccb55ad4`
      - `n8n_rag`: `https://your-n8n-url/webhook/edb1e894-1210-4902-a34f-a014bbdad8d8`
  - **Cách thiết lập trong Voiceflow:**
    1. Đăng ký [Voiceflow](https://www.voiceflow.com/).
    2. Tạo **3 Capture** với tên tương ứng (`n8n_order`, `n8n_appointment`, `n8n_rag`).
    3. Điền URL Webhook vào mỗi Capture.
    4. Test agent và lấy **Project ID**.

##### **🔹 Step 4: Cấu Hình OpenAI & RAG**
- **Node:** `OpenAI Chat Model1/2/3`, `RAG`, `Structured Output Parser`
  - **Tham số cần thay đổi:**
    - `openAiApi`: Thiết lập trong **Credentials** của n8n (API Key OpenAI).
    - **Model:** Đặt là `gpt-4o-mini` (hoặc model khác).
  - **Cách hoạt động:**
    - Khi khách hàng gửi yêu cầu, hệ thống sẽ:
      1. Truy vấn Qdrant để lấy thông tin liên quan (RAG).
      2. Sử dụng OpenAI Chat Model để trả lời.
      3. Trả kết quả qua Voiceflow (chatbot/gọi điện).

##### **🔹 Step 5: Cấu Hình Google Calendar**
- **Node:** `Google Calendar`
  - **Tham số cần thay đổi:**
    - `googleCalendarOAuth2Api`: Thiết lập trong **Credentials** của n8n.
  - **Cách hoạt động:**
    - Khi khách hàng yêu cầu lịch hẹn, hệ thống sẽ tự động tạo sự kiện trên Google Calendar.

##### **🔹 Step 6: Kích Hoạt Workflow**
1. **Test Run:**
   - Nhấn **"Execute"** trên node `When clicking ‘Test workflow’` để kiểm tra logic.
   - Gửi yêu cầu mẫu qua Voiceflow để đảm bảo agent trả lời chính xác.
2. **Bật Active:**
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**TIPS THỰC TẾ**]
1. **Kết hợp với Slack/Telegram:**
   - Sử dụng node `Slack` hoặc `Telegram Bot` để gửi báo cáo hoạt động của agent.
2. **Lưu Log & Monitoring:**
   - Thêm node `Set` để lưu lịch sử giao tiếp vào Google Sheets.
3. **Báo Cáo Định Kỳ:**
   - Sử dụng node `Google Calendar` + `Email` để gửi báo cáo tổng hợp hàng tuần.
4. **Cải Thiện RAG:**
   - Tăng kích thước collection Qdrant nếu dữ liệu lớn.
5. **Sử Dụng Twilio (Gọi Điện):**
   - Nếu muốn agent gọi điện, cài đặt Twilio Number trong Voiceflow.
:::

---

### 📌 **Kết Luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn** quá trình hỗ trợ khách hàng qua **chatbot, gọi điện và lịch trình**, với khả năng **trả lời chính xác và cá nhân hóa** nhờ RAG. **Không cần code**, chỉ cần cấu hình các API và webhook.

**Hành động ngay!**
1. **Import workflow** vào n8n.
2. **Cấu hình các node quan trọng** theo hướng dẫn.
3. **Test và bật Active** để bắt đầu tự động hóa!

**🚀 Cần hỗ trợ?** Liên hệ với tác giả Davide qua [LinkedIn](https://www.linkedin.com/in/davideboizza/) hoặc email: **info@n3w.it**.

---
**Chúc các sếp thành công với agent AI của mình!** 🤖✨