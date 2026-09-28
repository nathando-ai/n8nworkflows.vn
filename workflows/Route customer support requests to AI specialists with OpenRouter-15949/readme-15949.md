---
title: "🤖 **Tự Động Hướng Yêu Cầu Khách Hàng Đến Chuyên Gia AI Với OpenRouter (N8n) - Giải Pháp Chatbot Hỗ Trợ 24/7 Miễn Code**"
description: "Workflow này tự động phân loại và chuyển giao yêu cầu hỗ trợ khách hàng đến chuyên gia phù hợp (tài chính, kỹ thuật, tài khoản) thông qua AI Orchestrator và 3 Chatbot chuyên gia riêng biệt. Giảm thiểu thời gian phản hồi, tăng trải nghiệm khách hàng và tối ưu chi phí hỗ trợ."
slug: "tieu-dong-ho-trong-yeu-cau-khach-hang-den-chuyen-gia-ai"
tags: [n8n, automation, ai-chatbot, support-chatbot, openrouter, no-code, langchain]
keywords: [n8n tự động hóa hỗ trợ khách hàng, chatbot AI phân loại yêu cầu, OpenRouter trong n8n, tự động hóa chuyên gia AI, giải pháp hỗ trợ 24/7 không code]
---

# 🚀 **Tự Động Hướng Yêu Cầu Khách Hàng Đến Chuyên Gia AI Với OpenRouter (Multi-Agent Router)**

### **🔥 Nỗi Đau Của Các Sếp Hiện Nay**
Hỗ trợ khách hàng là một trong những công việc **tiêu tốn thời gian và nhân lực** nhất trong doanh nghiệp. Các yêu cầu hỗ trợ thường phải được chuyển giữa nhiều bộ phận (tài chính, kỹ thuật, tài khoản) gây **chậm trễ phản hồi**, **trải nghiệm khách hàng kém** và **chi phí cao** do phải thuê nhiều nhân viên.

**Giải pháp này giúp:**
- **Tự động phân loại** yêu cầu khách hàng và chuyển giao đến **chuyên gia AI phù hợp** (tài chính, kỹ thuật, tài khoản) **một cách tức thì**.
- **Giảm thiểu 90% công việc thủ công** của bộ phận hỗ trợ.
- **Tăng trải nghiệm khách hàng** với phản hồi nhanh chóng và chính xác.
- **Tối ưu chi phí** bằng cách sử dụng AI thay vì nhân viên toàn thời gian.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này **chạy 24/7 ổn định**, các sếp nên **self-host n8n** trên VPS riêng để đảm bảo **tính bảo mật và hiệu suất cao**.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Hỗ trợ tối đa cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Phản hồi tức thời** (không chờ chuyển giao giữa bộ phận).
✅ **Chính xác cao** (AI phân loại yêu cầu dựa trên ngữ cảnh).
✅ **Tiết kiệm chi phí** (giảm số lượng nhân viên hỗ trợ).
✅ **Hoạt động liên tục** (không cần nghỉ ngơi, 24/7).
✅ **Cá nhân hóa hỗ trợ** (mỗi chuyên gia AI có hệ thống prompt riêng).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản OpenRouter API** (để kết nối với mô hình AI).
✔ **Credentials cho n8n** (để kết nối với OpenRouter).
✔ **Webhook URL** (để nhận yêu cầu từ khách hàng).
✔ **Dữ liệu mẫu** (yêu cầu hỗ trợ từ khách hàng để test).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15949](https://n8n.io/workflows/15949) hoặc copy **JSON từ canvas**.
- Vào **n8n Editor** → Nhấn **Import Workflow** → Dán JSON và nhấn **Import**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này sử dụng **Multi-Agent System** (hệ thống AI nhiều chuyên gia). Các bước cấu hình quan trọng:

##### **A. Cấu Hình Webhook (Nhận Yêu Cầu Khách Hàng)**
- Node: **Webhook - Customer Request**
  - **Path:** `customer-request-aat` (không thay đổi).
  - **HTTP Method:** `POST`.
  - **Credentials:** Không cần (sử dụng mặc định).

##### **B. Kết Nối OpenRouter API**
- Node: **OpenRouter Chat Model** (4 node: Orchestrator + 3 Specialist)
  - **Credentials:** `openRouterApi` (cần tạo trên n8n).
    - Đi đến **Credentials** → **Add Credentials** → Chọn **OpenRouter API**.
    - Nhập **API Key** từ tài khoản OpenRouter.
  - **Model Configuration:**
    - Orchestrator (AI điều phối): Sử dụng mô hình **rationality** (để phân loại logic).
    - Specialist (AI chuyên gia):
      - **Billing_Specialist:** Mô hình **stronger** (ví dụ: `openrouter/mistral-7b`).
      - **Technical_Specialist:** Mô hình **tối ưu tính năng** (ví dụ: `openrouter/llama3-8b`).
      - **Account_Specialist:** Mô hình **chuyên sâu** (ví dụ: `openrouter/mistral-7b-instruct`).

##### **C. Cấu Hình Orchestrator Agent (AI Điều Phối)**
- Node: **Orchestrator Agent**
  - **Tool Descriptions:** Cần **định nghĩa rõ ràng** các chuyên gia:
    ```json
    {
      "Billing_Specialist": "Giải quyết vấn đề về thanh toán, hóa đơn, khuyến mãi.",
      "Technical_Specialist": "Giải quyết vấn đề kỹ thuật, API, tích hợp.",
      "Account_Specialist": "Giải quyết vấn đề tài khoản, quyền hạn, dữ liệu cá nhân."
    }
    ```
  - **System Prompt:** Cần **tối ưu** để AI phân loại chính xác:
    ```plaintext
    "Bạn là một AI điều phối hỗ trợ khách hàng. Phân loại yêu cầu dựa trên nội dung và chuyển đến chuyên gia phù hợp."
    ```

##### **D. Cấu Hình Specialist Tools (AI Chuyên Gia)**
- Node: **Billing_Specialist**, **Technical_Specialist**, **Account_Specialist**
  - **System Prompt:** Mỗi chuyên gia có **prompt riêng** để trả lời chuyên nghiệp:
    - **Billing_Specialist:**
      ```plaintext
      "Bạn là chuyên gia tài chính. Trả lời ngắn gọn, rõ ràng về vấn đề thanh toán."
      ```
    - **Technical_Specialist:**
      ```plaintext
      "Bạn là chuyên gia kỹ thuật. Giải thích kỹ thuật một cách dễ hiểu."
      ```
    - **Account_Specialist:**
      ```plaintext
      "Bạn là chuyên gia tài khoản. Bảo mật thông tin khách hàng."
      ```

##### **E. Cấu Hình Escalate to Human (Chuyển Giao Sang Nhân Viên)**
- Node: **Escalate to Human**
  - **Điều kiện:** Nếu AI không tự tin (confidence < 70%), yêu cầu chuyển giao sang nhân viên.
  - **Cách cấu hình:**
    - Sử dụng **Code Node** để kiểm tra `jsonPath("$.confidence") < 0.7`.
    - Gửi thông báo đến **Slack/Email** hoặc **CRM** (ví dụ: Zendesk).

##### **F. Cấu Hình Respond to Customer (Trả Lời Khách Hàng)**
- Node: **Respond to Webhook**
  - **Trả lời tự động** với kết quả từ AI.
  - **Cấu hình:**
    - **Headers:** `Content-Type: application/json`.
    - **Body:** `{"response": "$json.response"}`.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Gửi **yêu cầu mẫu** (ví dụ: *"Tôi bị lỗi thanh toán, không thể hoàn thành đơn hàng"*).
- **Kiểm tra:**
  - AI có phân loại đúng chuyên gia không?
  - Trả lời có logic không?
- **Bật Active:** Sau khi test thành công, **bật workflow**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Slack/Telegram** để **báo cáo lỗi** khi AI không phân loại chính xác.
2. **Lưu Log** để theo dõi hiệu suất của AI (sử dụng **Google Sheets** hoặc **Airtable**).
3. **Tối ưu mô hình AI** bằng cách:
   - Sử dụng **mô hình miễn phí** cho Orchestrator (ví dụ: `openrouter/mistral-7b`).
   - Sử dụng **mô hình mạnh** cho Specialist (ví dụ: `openrouter/llama3-8b`).
4. **Thêm chuyên gia mới** bằng cách:
   - Tạo **tool mới** trong Orchestrator.
   - Cấu hình **system prompt** riêng.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để **tự động hóa hỗ trợ khách hàng** một cách **chuyên nghiệp, tiết kiệm chi phí và hiệu quả**. Các sếp chỉ cần **cấu hình OpenRouter API** và **test với dữ liệu mẫu**, sau đó **bật workflow** và **nhận phản hồi tức thì** từ AI.

**🚀 Hãy áp dụng ngay và giảm thiểu công việc thủ công trong bộ phận hỗ trợ!**

---
**🔗 [Xem workflow gốc](https://n8n.io/workflows/15949) | [Tải file JSON](https://n8n.io/workflows/15949/download)**