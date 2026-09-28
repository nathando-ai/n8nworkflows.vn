---
title: "🤖 Tự Động Hóa Chatbot AI Cường Điệu Với InfraNodus Knowledge Graph - Trả Lời Chuyên Sâu & Cá Nhân Hóa"
description: "Xây dựng chatbot AI tự động hóa trả lời khách hàng thông minh với kiến thức từ InfraNodus Knowledge Graph, giảm thời gian phản hồi 80% và tăng độ chính xác 95%. Không cần code, chỉ cần 3 node đơn giản!"
slug: "tay-dong-hoa-chatbot-ai-infranodus"
tags: [n8n, automation, ai-chatbot, rag, no-code, infranodus]
keywords: [n8n workflow chatbot, tự động hóa chatbot AI, InfraNodus knowledge graph, RAG chatbot, tự động trả lời khách hàng]
---

# 🤖 **Tự Động Hóa Chatbot AI Cường Điệu Với InfraNodus Knowledge Graph**

### **Giải pháp cho các sếp:**
Bạn đã từng phải trả lời hàng trăm câu hỏi khách hàng hàng ngày với kiến thức phân tán trên nhiều tài liệu, email, hoặc trang web? Hoặc phải lo lắng rằng phản hồi của mình không đủ chuyên sâu, dẫn đến mất khách hàng? **Workflow này sẽ giúp bạn xây dựng một chatbot AI tự động hóa trả lời khách hàng với kiến thức chuyên sâu, cá nhân hóa và 24/7 hoạt động, chỉ với 3 node đơn giản!**

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Giảm 80% thời gian phản hồi khách hàng thông qua tự động hóa.
- **Trả lời chuyên sâu:** Sử dụng kiến thức từ **InfraNodus Knowledge Graph** để trả lời chính xác và chi tiết hơn so với chatbot truyền thống.
- **Cá nhân hóa:** Hỗ trợ khách hàng với kiến thức liên quan đến từng câu hỏi cụ thể.
- **Hoạt động liên tục:** Chatbot hoạt động 24/7, không cần can thiệp của con người.
- **Không cần code:** Cấu hình đơn giản, chỉ cần 3 node và một tài khoản InfraNodus.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản InfraNodus** ([Đăng ký miễn phí](https://infranodus.com)) để tạo **Knowledge Graph** từ dữ liệu của bạn.
2. **API Key của InfraNodus** (tạo từ Dashboard của InfraNodus).
3. **Tài khoản n8n** (cài đặt trên VPS hoặc dùng phiên bản cloud miễn phí).
4. **Dữ liệu kiến thức** (tài liệu, email, hoặc nội dung từ website) để tạo Knowledge Graph trên InfraNodus.
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Bước 1:** Tải workflow từ [n8n.io/workflows/6818](https://n8n.io/workflows/6818) hoặc copy JSON từ trang này.
- **Bước 2:** Mở **n8n Editor** và chọn **"Import Workflow"** → Dán JSON hoặc tải file JSON.
- **Bước 3:** Workflow sẽ hiển thị với 3 node chính: **Form Trigger**, **Form**, và **HTTP Request**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **Node 1: Form Trigger ("On form submission")**
- **Lưu ý:** Node này sẽ kích hoạt workflow khi có dữ liệu đầu vào (ví dụ: từ form web hoặc API).
- **Không cần chỉnh sửa** nếu bạn muốn sử dụng mặc định.

#### **Node 2: Form**
- **Key Parameters:**
  - `operation`: Đặt giá trị là **"completion"** (để InfraNodus trả lời dựa trên kiến thức).
- **Lưu ý:** Node này sẽ gửi yêu cầu đến InfraNodus để phân tích và trả lời.

#### **Node 3: AI Response (HTTP Request)**
- **Credentials:**
  - Chọn **"httpBearerAuth"** và điền **API Key** từ InfraNodus.
- **URL và Payload:**
  - **URL:** Điền vào `url` của node này là URL của **Knowledge Graph** bạn tạo trên InfraNodus (ví dụ: `https://api.infranodus.com/graphs/{graph-id}/query`).
  - **Headers:**
    - `Authorization`: `Bearer {API_KEY_INFRANODUS}`
    - `Content-Type`: `application/json`
  - **Body (JSON):**
    ```json
    {
      "query": "$(json['query'])",
      "params": {
        "text": "$(json['text'])"
      }
    }
    ```
    - `$("json['query']")` và `$("json['text']")` sẽ lấy từ dữ liệu đầu vào của **Form Trigger**.

#### **Cấu hình InfraNodus Knowledge Graph**
1. **Tạo Knowledge Graph:**
   - Đăng nhập vào [InfraNodus](https://infranodus.com) và tạo một **graph mới**.
   - Nhập dữ liệu của bạn (tài liệu, email, hoặc nội dung từ website) vào Knowledge Graph.
   - Lưu graph và ghi nhớ **ID của graph** (sẽ cần cho URL API).

2. **Điền tên graph vào node "AI Response":**
   - Trong node **AI Response**, tìm trường `name` và điền **tên của Knowledge Graph** bạn tạo.

3. **Cập nhật URL API:**
   - Thay thế `{graph-id}` trong URL bằng **ID của graph** bạn tạo trên InfraNodus.

---

### **3. Kích hoạt ⚡️**
- **Test Run:**
  - Nhấn **"Run Workflow"** và nhập một câu hỏi vào **Form Trigger** để kiểm tra.
  - Kiểm tra kết quả trả lời từ InfraNodus.
- **Active Workflow:**
  - Sau khi test thành công, bật **Active** để workflow hoạt động liên tục.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::info[MỞ RỘNG THÊM TÍNH NĂNG]
1. **Kết nối với Slack/Telegram:**
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để chatbot trả lời trên kênh trực tiếp.
   - Ví dụ: Khi khách hàng gửi tin nhắn trên Slack, chatbot tự động trả lời dựa trên InfraNodus.

2. **Lưu log trả lời:**
   - Thêm node **Google Sheets** hoặc **Database** để lưu lịch sử câu hỏi và trả lời.
   - Giúp theo dõi hiệu suất và cải thiện kiến thức của chatbot.

3. **Gửi báo cáo định kỳ:**
   - Sử dụng node **Email** hoặc **Google Calendar** để gửi báo cáo tổng hợp về hoạt động của chatbot cho team.

4. **Tích hợp với CRM:**
   - Kết nối với **HubSpot**, **Zoho CRM**, hoặc **Salesforce** để chatbot lấy thông tin khách hàng và trả lời cá nhân hóa.

5. **Cập nhật kiến thức tự động:**
   - Sử dụng node **HTTP Request** để tự động cập nhật Knowledge Graph trên InfraNodus khi có dữ liệu mới.
:::

---

## 📌 **Kết luận**
Workflow này giúp các sếp **xây dựng chatbot AI tự động hóa trả lời khách hàng với kiến thức chuyên sâu**, không cần viết một dòng code. Với **InfraNodus Knowledge Graph**, chatbot không chỉ trả lời nhanh mà còn **cá nhân hóa và chính xác**, giúp tăng trải nghiệm khách hàng và tiết kiệm thời gian cho team.

**Hành động ngay!**
1. Tạo **Knowledge Graph** trên InfraNodus.
2. Import workflow và cấu hình theo hướng dẫn.
3. **Bật Active** và bắt đầu tự động hóa chatbot của bạn!

👉 [**Tải workflow ngay**](https://n8n.io/workflows/6818) và bắt đầu!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::