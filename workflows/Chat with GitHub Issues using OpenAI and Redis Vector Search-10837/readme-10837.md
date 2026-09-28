---
title: "🤖 Tự Động Hóa Trợ Lý AI Chat Trực Tuyến Cho GitHub Issues Với OpenAI & Redis Vector Search"
description: "Workflow này tự động hóa hệ thống Trí tuệ Nhân tạo tăng cường bằng dữ liệu (RAG) để các sếp có thể tương tác với các issue của GitHub thông qua chatbot AI, tiết kiệm thời gian tìm kiếm và giải quyết vấn đề hiệu quả. Dữ liệu được lưu trữ trên Redis Vector Store cho phép tra cứu nhanh chóng và chính xác."
slug: "tự-dộng-hoa-trợ-ly-ai-chat-github-issues"
tags: [n8n, automation, ai-rag, github-api, redis-vector-search, openai]
keywords: [n8n workflow github issues, tự động hóa chatbot AI, RAG với OpenAI, lưu trữ vector Redis, tra cứu issue GitHub]
---

# 🚀 **Tự Động Hóa Trợ Lý AI Chat Trực Tuyến Cho GitHub Issues**

## **Giới Thiệu**
Các sếp có biết rằng việc tìm kiếm và giải quyết các **issue** trong dự án GitHub thủ công có thể tốn thời gian và dễ gây nhầm lẫn? Với **workflow này**, các sếp có thể **tạo một chatbot AI thông minh** để tương tác với tất cả các **issue** của dự án thông qua **OpenAI (GPT-4.1-mini)** và **Redis Vector Search**, giúp tra cứu và phân tích nhanh chóng mà không cần code!

Workflow này sử dụng **Retrieval-Augmented Generation (RAG)** – một kỹ thuật AI hiện đại giúp kết hợp **tìm kiếm vector** (Redis) với **trí tuệ nhân tạo** (OpenAI) để trả lời các câu hỏi về **issue** GitHub một cách **chính xác và tự động hóa**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài **n8n trên VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** – Không cần tìm kiếm thủ công trên GitHub API.
✅ **Trả lời chính xác** – AI sử dụng **RAG** để tra cứu và trả lời dựa trên dữ liệu thực tế.
✅ **Hoạt động liên tục** – Chatbot hoạt động 24/7, không cần can thiệp người dùng.
✅ **Lưu trữ thông minh** – Dữ liệu **issue** được vector hóa và lưu trên **Redis**, cho phép tra cứu nhanh chóng.
✅ **Cá nhân hóa** – Hệ thống nhớ lịch sử chat (Redis Chat Memory) để hỗ trợ các cuộc trò chuyện dài.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Các sếp cần chuẩn bị:
✔ **Tài khoản OpenAI** (để sử dụng GPT-4.1-mini và Embeddings).
✔ **Redis Server 8.x** (hoặc phiên bản cũ cần cài **Redis Query Engine**).
✔ **GitHub Personal Access Token** (để tránh giới hạn rate limit khi fetch issue).
✔ **URL của repository GitHub** (để workflow fetch dữ liệu).
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào **n8n Editor**:
1. Mở **n8n Editor** trên trang web hoặc VPS.
2. Nhấn **Import Workflow** và chọn file JSON hoặc **paste JSON** từ [link gốc](https://n8n.io/workflows/10837).
3. Sau khi import, workflow sẽ hiển thị trên **canvas**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này được chia thành **2 phần chính**:
- **Phần 1: Data Ingestion (Lấy dữ liệu từ GitHub)**
- **Phần 2: Chat Interface (Chat với AI)**

#### **🔹 Phần 1: Data Ingestion (Top Flow)**
1. **Node `Manual Trigger`** → Khởi động thủ công khi cần lấy dữ liệu mới.
2. **Node `Fetch issues from GitHub` (HTTP Request)**
   - **Cần thay đổi URL** thành:
     ```
     https://api.github.com/repos/{owner}/{repository}/issues
     ```
     (Thay `{owner}/{repository}` bằng tên repository của các sếp).
   - **Thêm Personal Access Token** vào header:
     ```
     Authorization: token {YOUR_GITHUB_TOKEN}
     ```
   - **Lưu ý:** Nếu không thêm token, GitHub sẽ **limit request** (60 request/giây).

3. **Node `Embeddings OpenAI`**
   - Điền **API Key OpenAI** vào **Credentials**.
   - Chọn model **text-embedding-ada-002** (mặc định).

4. **Node `Vectorize and store in Redis` (Redis Vector Store)**
   - **Thiết lập Redis Connection**:
     - Host: `localhost` (nếu Redis cài trên cùng máy)
     - Port: `6379` (mặc định)
     - Username/Password: (nếu có)
   - **Index Name**: `github_issues_v1` (không thay đổi).

#### **🔹 Phần 2: Chat Interface (Bottom Flow)**
1. **Node `When chat message received` (Chat Trigger)**
   - Đây là **gateway** để nhận tin nhắn từ người dùng.
   - Các sếp có thể **kết nối với Slack/Telegram** sau này (xem phần **Mẹo nâng cao**).

2. **Node `OpenAI Chat Model` (lmChatOpenAi)**
   - Chọn model: `gpt-4.1-mini` (mặc định).
   - Điền **API Key OpenAI** vào **Credentials**.

3. **Node `Redis Chat Memory`**
   - **Thiết lập Redis Connection** tương tự như phần **Data Ingestion**.
   - **Index Name**: `github_issues_v1` (phải khớp với phần 1).

4. **Node `AI Agent using RAG` (Agent)**
   - Đây là **trí tuệ nhân tạo** thực hiện logic chat.
   - Các sếp **không cần chỉnh sửa** trừ khi muốn thay đổi logic.

5. **Node `Augment with results from Redis` (Vector Store Redis)**
   - **Không cần chỉnh sửa**, nó tự động lấy dữ liệu từ Redis.

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Execute Workflow** (phần **Data Ingestion**) để lấy dữ liệu từ GitHub.
   - Sau đó, **gửi tin nhắn** vào **Chat Trigger** và kiểm tra AI trả lời có chính xác không.
2. **Bật Active Workflow**:
   - Đảm bảo **tất cả node** đều hoạt động và **không có lỗi**.
   - Nhấn **Active** để workflow chạy tự động.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
🔹 **Kết nối với Slack/Telegram**:
   - Sử dụng **node `webhook`** để nhận tin nhắn từ Slack/Telegram và chuyển vào **Chat Trigger**.
   - Cài đặt **webhook URL** trong Slack/Telegram và kết nối với n8n.

🔹 **Lưu log hoạt động**:
   - Thêm **node `Set`** sau **Chat Trigger** để lưu tin nhắn và phản hồi vào **Google Sheets** hoặc **Firebase**.

🔹 **Gửi báo cáo định kỳ**:
   - Sử dụng **node `Schedule`** để tự động gửi **tóm tắt các issue mới** qua email (với **node `Email`**).

🔹 **Cập nhật dữ liệu tự động**:
   - Thay vì **Manual Trigger**, sử dụng **node `Schedule`** để tự động lấy dữ liệu từ GitHub mỗi ngày.
:::

---

## 📌 **Kết luận**
Workflow này giúp các sếp **tự động hóa việc tương tác với GitHub Issues** thông qua **AI RAG**, tiết kiệm thời gian và tăng hiệu suất làm việc. **Không cần code**, chỉ cần **cấu hình Redis và OpenAI**, các sếp đã có một **trợ lý AI thông minh** hoạt động 24/7!

**Hãy áp dụng ngay và trải nghiệm sự thuận tiện của tự động hóa!** 🚀

---
**Cần hỗ trợ?** Hãy tham gia **Discord Redis** để được hỗ trợ kỹ thuật: [https://discord.com/invite/redis](https://discord.com/invite/redis)