---
title: "🤖 Tự Động Hóa Trả Lời WhatsApp Bằng AI: AI Agent Cho WhatsApp Với WOZTELL + Google Gemini"
description: "Workflow tự động hóa trả lời tin nhắn WhatsApp bằng AI thông minh, tích hợp WOZTELL và Google Gemini để cung cấp phản hồi cá nhân hóa 24/7, giảm thiểu công việc cho đội ngũ hỗ trợ. Giúp doanh nghiệp tiết kiệm thời gian và cải thiện trải nghiệm khách hàng."
slug: "tieu-dong-hoa-ai-agent-whatsapp-woztell-gemini"
tags: [n8n, automation, no-code, ai-chatbot, whatsapp-business, google-gemini, woztell]
keywords: [tự động hóa whatsapp bằng ai, chatbot whatsapp n8n, google gemini n8n, woztell n8n, tự động trả lời tin nhắn whatsapp]
---

# 🚀 **Tự Động Hóa Trả Lời WhatsApp Bằng AI: AI Agent Cho WhatsApp Với WOZTELL + Google Gemini**

## **Giới Thiệu**
Bạn đã bao giờ cảm thấy mệt mỏi khi phải trả lời hàng trăm tin nhắn WhatsApp hàng ngày từ khách hàng? Hay phải lo lắng về việc phản hồi chậm khiến khách hàng mất niềm tin? **Workflow này sẽ giải quyết tất cả những vấn đề đó!**

Với **AI Agent tự động hóa trên WhatsApp**, doanh nghiệp của các sếp có thể:
- **Trả lời tự động** mọi tin nhắn WhatsApp bằng AI thông minh (Google Gemini).
- **Hiểu ngữ cảnh** từ lịch sử cuộc trò chuyện trước đó để trả lời chính xác và chuyên nghiệp.
- **Giảm thiểu công việc** cho đội ngũ hỗ trợ, tiết kiệm thời gian và chi phí.
- **Hoạt động 24/7** mà không cần nhân viên trực ca.

Không cần viết một dòng code nào! Chỉ cần **cài đặt và chạy**, AI sẽ tự động xử lý mọi tin nhắn!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7**, các sếp nên **self-host n8n** trên VPS riêng để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (Đảm bảo tốc độ cao, phù hợp với AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** – AI tự động trả lời thay vì các sếp phải làm thủ công.
✅ **Trả lời chính xác** – Hiểu ngữ cảnh từ lịch sử cuộc trò chuyện.
✅ **Cá nhân hóa phản hồi** – AI điều chỉnh giọng điệu phù hợp với từng khách hàng.
✅ **Hoạt động liên tục** – Không cần nhân viên trực ca, giảm chi phí nhân sự.
✅ **Tăng trải nghiệm khách hàng** – Phản hồi nhanh chóng, chuyên nghiệp.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản n8n** (self-hosted hoặc cloud).
✔ **Tài khoản WOZTELL** (đã kết nối với WhatsApp Business API).
✔ **API Key Google Gemini** (để sử dụng mô hình AI).
✔ **Tài khoản WhatsApp Business** (đã đăng ký và xác thực).

---
:::info[CHUẨN BỊ WOZTELL]
1. **Đăng ký tài khoản WOZTELL** tại: [https://platform.woztell.com/signup](https://platform.woztell.com/signup)
2. **Xác thực email** và hoàn thành thiết lập tài khoản.
3. **Cài đặt WhatsApp Business API** theo hướng dẫn: [https://doc.woztell.com/docs/procedures/basic-whatsapp-chatbot-setup/standard-procedures-wa-connect-waba/](https://doc.woztell.com/docs/procedures/basic-whatsapp-chatbot-setup/standard-procedures-wa-connect-waba/)
4. **Tạo Access Token** với quyền:
   - `channel:list`
   - `channel:getBasicInfo`
   - `member:getConversations`
   - `bot:sendResponses`
   (Hướng dẫn: [https://support.woztell.com/portal/en/kb/articles/access-token](https://support.woztell.com/portal/en/kb/articles/access-token))
:::

---
:::info[CHUẨN BỊ Google Gemini]
1. **Tạo API Key Google Gemini** theo hướng dẫn: [https://docs.n8n.io/integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.lmchatgooglegemini/](https://docs.n8n.io/integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.lmchatgooglegemini/)
2. **Thêm credentials** trong n8n với tên `googlePalmApi`.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import từ file JSON** hoặc **copy/paste JSON** vào n8n Editor:
```bash
# Nếu import từ file:
1. Tải workflow từ [n8n.io/workflows/13641](https://n8n.io/workflows/13641)
2. Vào n8n Dashboard → **Import** → Chọn file JSON.
3. Hoặc copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.
```

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **7 node chính**, các sếp cần **cấu hình kỹ lưỡng** như sau:

##### **🔹 Node 1: Webhook (Nhận tin nhắn WhatsApp)**
- **Cấu hình**:
  - **Path**: `inbound/message` (không thay đổi).
  - **HTTP Method**: `POST`.
  - **Credentials**: Không cần (sử dụng mặc định).
- **Lưu ý**:
  - Sau khi import, **copy URL Production** từ node này và **dán vào WOZTELL Webhook Settings**.
  - Hướng dẫn cấu hình Webhook WOZTELL: [https://support.woztell.com/portal/en/kb/articles/web#Create_Webhooks](https://support.woztell.com/portal/en/kb/articles/web#Create_Webhooks)

##### **🔹 Node 2: Filter (Lọc tin nhắn hợp lệ)**
- **Cấu hình**:
  - **Conditions**:
    - `event.type === "inbound"` (chỉ nhận tin nhắn vào).
    - `message.type === "text"` (chỉ xử lý tin nhắn văn bản).
    - `liveChat.active === false` (bỏ qua cuộc trò chuyện đang diễn ra với nhân viên).
- **Lưu ý**:
  - Nếu không lọc kỹ, AI sẽ trả lời sai cho tin nhắn không phù hợp (ví dụ: tin nhắn hình ảnh, cuộc trò chuyện trực tiếp).

##### **🔹 Node 3: Edit Fields (Định dạng dữ liệu)**
- **Cấu hình**:
  - **Thêm trường `conversationHistory`** (sẽ được lấy từ node sau).
  - **Định dạng tin nhắn**:
    ```json
    {
      "customerMessage": "$json.message.text",
      "agentMessage": "$json.message.text" // (nếu cần phân biệt)
    }
    ```
- **Lưu ý**:
  - Node này chuẩn bị dữ liệu cho AI để hiểu ngữ cảnh.

##### **🔹 Node 4: Get conversation history by id (Lấy lịch sử cuộc trò chuyện)**
- **Cấu hình**:
  - **Credentials**: `woztellCredentialApi` (đã tạo trước).
  - **Operation**: `getConversationHistory`.
  - **Resource**: `memberAPI`.
  - **Tham số**:
    - `conversationId`: `$json.conversationId` (lấy từ tin nhắn vào).
    - `limit`: `100` (lấy tối đa 100 tin nhắn trước đó).
- **Lưu ý**:
  - **Không quên thêm `woztellCredentialApi`** vào n8n Credentials trước khi chạy.

##### **🔹 Node 5: AI Agent (Google Gemini)**
- **Cấu hình**:
  - **Credentials**: `googlePalmApi` (API Key Google Gemini).
  - **System Prompt (gợi ý)**:
    ```plaintext
    You are a professional customer support assistant. Always respond politely and professionally.
    Use the conversation history to provide accurate and helpful answers.
    If you don't know the answer, say: "I'm sorry, I don't have that information. Let me check and get back to you."
    ```
  - **Lưu ý**:
    - **Thay đổi System Prompt** để phù hợp với giọng điệu của doanh nghiệp.
    - **Kiểm tra token limit** để tránh lỗi quá dài.

##### **🔹 Node 6: Send responses (Gửi trả lời về WhatsApp)**
- **Cấu hình**:
  - **Credentials**: `woztellCredentialApi`.
  - **Tham số**:
    - `conversationId`: `$json.conversationId` (lấy từ tin nhắn vào).
    - `message`: `$json.aiResponse` (trả lời từ AI).
- **Lưu ý**:
  - **Không quên chọn `bot:sendResponses`** trong quyền WOZTELL.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với một tin nhắn mẫu:
   - Gửi tin nhắn WhatsApp đến số liên hệ của WOZTELL.
   - Kiểm tra AI trả lời có hợp lý không.
2. **Bật Active workflow** nếu test thành công.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh System Prompt** để phù hợp với **giọng điệu thương hiệu**:
   - Ví dụ: Nếu doanh nghiệp là **cửa hàng điện thoại**, có thể thêm:
     ```plaintext
     Always mention our latest promotions and discounts when possible.
     ```
2. **Lưu lịch sử cuộc trò chuyện** vào Google Sheets/Database để **analyze hiệu suất**:
   - Sử dụng node **Google Sheets** hoặc **Database** sau node `Send responses`.
3. **Kết hợp với Slack/Telegram** để **monitor hoạt động**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo khi AI trả lời.
4. **Thêm logic lọc từ khóa** để **chuyển tiếp tin nhắn phức tạp** cho nhân viên:
   - Ví dụ: Nếu tin nhắn chứa từ khóa `"hủy đơn"`, chuyển cho nhân viên xử lý.

---

### 📌 **Kết luận**
**Workflow này là giải pháp hoàn hảo** để tự động hóa trả lời WhatsApp bằng AI, giúp doanh nghiệp:
✔ **Tiết kiệm thời gian** và **giảm chi phí nhân sự**.
✔ **Cải thiện trải nghiệm khách hàng** với phản hồi nhanh chóng.
✔ **Hoạt động 24/7** mà không cần nhân viên trực ca.

**Hãy áp dụng ngay và trải nghiệm sự khác biệt!**
👉 **Bắt đầu từ [n8n.io/workflows/13641](https://n8n.io/workflows/13641)** và **cài đặt trên VPS** để đảm bảo hiệu suất tối ưu.

---
**Có thắc mắc? Hãy để lại comment bên dưới!** 🚀