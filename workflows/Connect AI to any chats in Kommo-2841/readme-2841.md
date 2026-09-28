---
title: "🤖 **Tự Động Hóa Trả Lời Chat AI Tự Động Trên Kommo - Không Cần Code!**"
description: "Workflow này kết nối AI với tất cả các cuộc trò chuyện trên Kommo để tự động trả lời, xử lý yêu cầu khách hàng và tối ưu hóa dịch vụ hỗ trợ 24/7. Giảm thiểu thời gian phản hồi, tăng trải nghiệm khách hàng và tiết kiệm chi phí nhân sự."
slug: "tieu-dong-hoa-chat-ai-tren-kommo"
tags: [n8n, automation, ai-chatbot, kommo, no-code, openai, langchain]
keywords: [n8n workflow kommo, tự động hóa hỗ trợ khách hàng, chatbot ai tự động, xử lý chat trên kommo, n8n ai agent]
---

# 🚀 **Tự Động Hóa Trả Lời Chat AI Tự Động Trên Kommo - Không Cần Code!**

### **Giải pháp cho các sếp đang mệt mỏi với công việc hỗ trợ khách hàng thủ công**
Các sếp có biết rằng **80% các câu hỏi trên chat hỗ trợ** đều có thể được tự động trả lời bằng AI? Thay vì phải ngồi chờ khách hàng gọi điện hoặc gửi tin nhắn, **Workflow này sẽ tự động phân tích và trả lời tất cả các cuộc trò chuyện trên Kommo** bằng AI, giúp tiết kiệm **tối thiểu 10-15 giờ/ngày** cho đội ngũ hỗ trợ.

Với **n8n + OpenAI + LangChain**, workflow này không chỉ **hiểu được ngữ cảnh** của khách hàng mà còn **tự động trả lời chính xác**, **cập nhật lịch sử trò chuyện** và **ngừng khi khách hàng không muốn tiếp tục**. Đây là **công cụ tự động hóa hỗ trợ khách hàng hoàn hảo** cho doanh nghiệp nhỏ và vừa.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động trả lời tất cả các cuộc trò chuyện** trên Kommo (không cần nhân viên ngồi chờ).
✅ **Hiểu ngữ cảnh và trả lời chính xác** nhờ AI (OpenAI + LangChain).
✅ **Tiết kiệm thời gian** (giảm **10-15 giờ/ngày** cho đội ngũ hỗ trợ).
✅ **Cập nhật lịch sử trò chuyện** để AI nhớ được các cuộc trò chuyện trước đó.
✅ **Ngừng tự động khi khách hàng không muốn tiếp tục** (tránh phản hồi không cần thiết).
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Kommo** (API Key hoặc Webhook URL của Kommo).
✔ **API Key OpenAI** (để AI trả lời).
✔ **N8n self-hosted** (trên VPS để workflow hoạt động liên tục).
✔ **N8n Node LangChain** (đã cài đặt trong n8n Community Edition).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow từ file JSON** hoặc **copy/paste JSON** vào n8n Editor.

🔹 **Bước 1:** Tải workflow từ [n8n.io/workflows/2841](https://n8n.io/workflows/2841).
🔹 **Bước 2:** Mở **n8n Editor** → Nhấn **"Import"** → Chọn file JSON hoặc **paste JSON** vào.
🔹 **Bước 3:** Chọn **"Import"** để hoàn tất.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

Workflow này sử dụng **12 node** chính, và **các bước quan trọng cần cấu hình** như sau:

#### **🔹 Node "new_message" (Webhook)**
- **Chức năng:** Nhận tất cả các tin nhắn mới từ Kommo.
- **Cấu hình:**
  - **URL Webhook:** Điền **URL Webhook của Kommo** (cần lấy từ Kommo API).
  - **Method:** POST.
  - **Headers:** `Content-Type: application/json`.

#### **🔹 Node "Get token" (HTTP Request)**
- **Chức năng:** Lấy token để xác thực với Kommo.
- **Cấu hình:**
  - **URL:** `https://api.kommo.com/oauth/token` (hoặc URL API của Kommo).
  - **Headers:**
    ```json
    {
      "Authorization": "Basic {BASE64_ENCODED_CLIENT_ID:CLIENT_SECRET}",
      "Content-Type": "application/x-www-form-urlencoded"
    }
    ```
  - **Body:**
    ```json
    {
      "grant_type": "client_credentials"
    }
    ```

#### **🔹 Node "Recieve message" (HTTP Request)**
- **Chức năng:** Lấy tin nhắn mới từ Kommo.
- **Cấu hình:**
  - **URL:** `https://api.kommo.com/api/v1/messages` (hoặc URL API của Kommo).
  - **Headers:**
    ```json
    {
      "Authorization": "Bearer {TOKEN_FROM_GET_TOKEN_NODE}",
      "Content-Type": "application/json"
    }
    ```

#### **🔹 Node "isVoice" (If)**
- **Chức năng:** Kiểm tra tin nhắn có phải là **gọi thoại (voice)** hay không.
- **Cấu hình:**
  - **Condition:** `$.type === "voice"` (hoặc điều kiện tương tự của Kommo).

#### **🔹 Node "transcribe voice" (OpenAI)**
- **Chức năng:** Chuyển **gọi thoại thành văn bản** bằng AI.
- **Cấu hình:**
  - **API Key:** Điền **API Key OpenAI**.
  - **Model:** `whisper-1` (hoặc model transcribe khác).
  - **Audio File:** Lấy từ node **"get voice"**.

#### **🔹 Node "ai" (Agent - LangChain)**
- **Chức năng:** **Trả lời tự động** bằng AI.
- **Cấu hình:**
  - **Model:** `gpt-4` hoặc `gpt-3.5-turbo`.
  - **Prompt:** Cần **cấu hình cụ thể** để AI trả lời phù hợp với doanh nghiệp.
    ```json
    {
      "role": "system",
      "content": "Bạn là trợ lý hỗ trợ khách hàng của {TÊN DOANH NGHIỆP}. Hãy trả lời khách hàng một cách thân thiện và chuyên nghiệp."
    }
    ```
  - **Memory:** Kết nối với node **"memory"** để AI nhớ lịch sử trò chuyện.

#### **🔹 Node "memory" (MemoryBufferWindow)**
- **Chức năng:** **Giữ lịch sử trò chuyện** để AI nhớ được các cuộc trò chuyện trước đó.
- **Cấu hình:**
  - **Window Size:** 5 (hoặc số lượng tin nhắn muốn lưu).
  - **Key:** `chat_history`.

#### **🔹 Node "hasStopTag" (Switch)**
- **Chức năng:** **Dừng tự động trả lời** nếu khách hàng không muốn tiếp tục.
- **Cấu hình:**
  - **Condition:** Kiểm tra nếu tin nhắn có từ khóa **"dừng"**, **"không"**, **"tạm biệt"**, **"bye"**, **"stop"**.

#### **🔹 Node "setText" (Set)**
- **Chức năng:** **Chuyển tin nhắn thành văn bản** (nếu cần).
- **Cấu hình:**
  - **Expression:** `$.text` (hoặc `$.transcription` nếu là voice).

#### **🔹 Node "model" (lmChatOpenAi)**
- **Chức năng:** **Gửi tin nhắn AI trả lời** về Kommo.
- **Cấu hình:**
  - **API Key:** Điền **API Key OpenAI**.
  - **Model:** `gpt-4` hoặc `gpt-3.5-turbo`.
  - **Message:** Lấy từ node **"ai"**.

---

### **3. Kích hoạt ⚡️**
- **Test Run:** Chạy **dữ liệu mẫu** để kiểm tra workflow.
- **Bật Active:** Sau khi cấu hình xong, **bật workflow** để nó hoạt động tự động.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết nối với Slack/Telegram** để **báo cáo lỗi** nếu AI trả lời sai.
2. **Lưu log tất cả cuộc trò chuyện** vào **Google Sheets** hoặc **Notion** để theo dõi.
3. **Tự động gửi báo cáo hàng ngày** về **số lượng tin nhắn được tự động trả lời**.
4. **Cập nhật Prompt AI** để phù hợp với **ngôn ngữ và văn hóa** của doanh nghiệp.
5. **Sử dụng Node "stickyNote"** để ghi chú các **câu hỏi thường gặp** để AI trả lời nhanh hơn.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để **tự động hóa hỗ trợ khách hàng** trên Kommo **không cần code**. Với **AI + LangChain**, các sếp sẽ **giảm thiểu thời gian phản hồi**, **tăng trải nghiệm khách hàng** và **tiết kiệm chi phí nhân sự**.

**Hãy thử ngay và tự động hóa đội ngũ hỗ trợ của mình!** 🚀

---
**🔗 [Tải workflow từ n8n.io](https://n8n.io/workflows/2841)**
**💡 Cần hỗ trợ cấu hình?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) và liên hệ chúng tôi!