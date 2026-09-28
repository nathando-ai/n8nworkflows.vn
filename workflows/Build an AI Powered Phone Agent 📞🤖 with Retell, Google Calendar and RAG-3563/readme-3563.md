---
title: "🤖📞 Tự Động Hóa Agent AI Điện Thoại Học Hỏi & Đặt Lịch với RAG, Google Calendar & Retell AI - Cách Sử Dụng Chi Tiết"
description: "Workflow này tự động hóa một AI Phone Agent thông minh, kết hợp RAG (Retrieval-Augmented Generation) để trả lời câu hỏi chính xác từ dữ liệu nội bộ, đồng thời đặt lịch trực tiếp trên Google Calendar. Giúp doanh nghiệp tiết kiệm thời gian hỗ trợ khách hàng 24/7 mà không cần nhân viên."
slug: "ai-phone-agent-retell-google-calendar-rag"
tags: [n8n, automation, ai, no-code, google-calendar, rag, retell-ai, openai, self-hosted]
keywords: [n8n workflow ai điện thoại, tự động hóa hỗ trợ khách hàng, đặt lịch tự động google calendar, rag với n8n, retell ai với n8n, tự động hóa chatbot điện thoại]
---

# 🤖📞 **Tạo Agent AI Điện Thoại Học Hỏi & Đặt Lịch Tự Động với RAG, Google Calendar & Retell AI**

## **🔥 Bạn đang gặp vấn đề gì?**
Hỗ trợ khách hàng qua điện thoại là một trong những công việc tốn thời gian và tốn chi phí nhất của doanh nghiệp. Các sếp thường phải:
- **Phối hợp nhiều nhân viên** để đáp ứng lượng gọi điện cao.
- **Lo ngại sai sót** khi trả lời câu hỏi phức tạp (giá sản phẩm, chính sách hoàn trả, lịch mở cửa...).
- **Không thể hoạt động 24/7** vì giới hạn nhân sự.
- **Tốn kém** khi phải thuê nhân viên chuyên nghiệp.

**Workflow này giải quyết tất cả!** Một AI Phone Agent thông minh sẽ:
✅ **Trả lời mọi câu hỏi** dựa trên dữ liệu nội bộ (RAG) với độ chính xác cao.
✅ **Đặt lịch tự động** trên Google Calendar khi khách hàng yêu cầu.
✅ **Hoạt động 24/7** mà không cần nhân viên.
✅ **Tiết kiệm chi phí** với mô hình trả theo sử dụng (Retell AI cung cấp 10$ miễn phí).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và ổn định.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian hỗ trợ khách hàng** (AI xử lý 100% cuộc gọi).
- **Trả lời chính xác** dựa trên dữ liệu nội bộ (RAG) thay vì nhớ thủ công.
- **Đặt lịch tự động** trên Google Calendar khi khách hàng yêu cầu.
- **Hoạt động 24/7** mà không cần nhân viên.
- **Chi phí thấp** (Retell AI cung cấp 10$ miễn phí, sau đó trả theo sử dụng).
- **Dễ dàng mở rộng** (thêm chức năng mới như Slack, Telegram, email...).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Retell AI** ([Đăng ký miễn phí](https://retellai.com)) với **10$ credit** (đủ để test).
✔ **Tài khoản OpenAI** ([Đăng ký API Key](https://platform.openai.com/)) để sử dụng **GPT-4o-mini**.
✔ **Tài khoản Google Calendar** (để đặt lịch tự động).
✔ **Tài khoản Google Drive** (để lưu trữ dữ liệu cho RAG).
✔ **Tài khoản Qdrant** ([Đăng ký miễn phí](https://qdrant.tech/)) để lưu trữ vector embeddings.
✔ **Tài khoản Telegram** (để nhận transcript cuộc gọi).
✔ **Số điện thoại miễn phí** (Retell AI cung cấp qua Twilio).

---

## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Mở **n8n Workflow Editor**.
2. Nhấp vào **"Import"** và chọn file JSON (hoặc paste JSON từ [link gốc](https://n8n.io/workflows/3563)).
3. Chọn **"Import"** để tải workflow vào.

---

### **2. Các bước cấu hình BẮC BUỘC 📌**

#### **🔹 STEP 1: Thiết lập Qdrant Collection (Lưu trữ dữ liệu cho RAG)**
Workflow cần một **collection** trong Qdrant để lưu trữ embeddings (dữ liệu đã chuyển đổi thành vector).
**Cách làm:**
1. Trong node **"Create collection"** (HTTP Request), thay đổi:
   - `QDRANTURL` → URL của Qdrant (ví dụ: `http://localhost:6333`).
   - `COLLECTION` → Tên collection (ví dụ: `ai_phone_agent_data`).
2. Chạy node **"Refresh collection"** để cập nhật.

#### **🔹 STEP 2: Vectorize Documents từ Google Drive (Chuẩn bị dữ liệu cho RAG)**
Workflow sẽ tải **tất cả file từ Google Drive** và chuyển chúng thành **embeddings** để RAG sử dụng.
**Cách làm:**
1. Trong node **"Get folder"** (Google Drive), chọn **folder chứa dữ liệu** (ví dụ: "FAQs", "Product Info").
2. Trong node **"Download Files"**, đảm bảo **tất cả file** được tải xuống.
3. Trong node **"Embeddings OpenAI"**, kiểm tra **API Key OpenAI** đã điền đúng.
4. Trong node **"Token Splitter"**, điều chỉnh **chiều dài token** (ví dụ: `1000`) để phù hợp với dữ liệu.

#### **🔹 STEP 3: Kết nối với Retell AI (Agent AI Điện Thoại)**
Retell AI là nền tảng cho phép tạo **AI Phone Agent** với số điện thoại ảo.
**Cách làm:**
1. **Đăng ký Retell AI** và lấy **10$ credit miễn phí**.
2. **Tạo một Agent mới** và thiết lập:
   - **Voice & Language** (ví dụ: tiếng Việt, giọng nữ).
   - **System Prompt** (ví dụ: *"Bạn là AI hỗ trợ khách hàng của [Tên Doanh Nghiệp]. Hãy trả lời tất cả câu hỏi một cách thân thiện và chính xác."*).
3. **Thiết lập Webhook trong Retell AI**:
   - Trong **Webhook settings**, thêm **Agent Level Webhook URL** từ node **"n8n_call"** (path: `b352dd49-d3b3-4e0a-a781-17137f7199c8`).
   - Thêm **2 Webhook khác** cho:
     - **RAG Function** (`n8n_rag_function`).
     - **Booking Function** (`n8n_check_available`).
4. **Mua số điện thoại** (Retell AI hỗ trợ Twilio, số +1 miễn phí trong 10$ credit).

#### **🔹 STEP 4: Thiết lập Telegram (Nhận transcript cuộc gọi)**
Workflow sẽ gửi **transcript cuộc gọi** về Telegram để các sếp theo dõi.
**Cách làm:**
1. Trong node **"Telegram"**, điền **CHAT_ID** của Telegram (lấy từ `@username` hoặc `@id`).
2. Kiểm tra **API Key Telegram** đã điền đúng.

#### **🔹 STEP 5: Kết nối Google Calendar (Đặt lịch tự động)**
Khi khách hàng yêu cầu đặt lịch, AI sẽ tự động tạo **event** trên Google Calendar.
**Cách làm:**
1. Trong node **"Google Calendar"**, chọn **credentials OAuth2** đã thiết lập.
2. Kiểm tra **thời gian zone** (ví dụ: `Asia/Ho_Chi_Minh`).
3. Thiết lập **tiêu đề và mô tả event** (ví dụ: `Lịch hẹn với AI hỗ trợ - [Tên Khách Hàng]`).

#### **🔹 STEP 6: Cấu hình RAG (Trả lời câu hỏi từ dữ liệu nội bộ)**
Workflow sử dụng **Retrieval-Augmented Generation (RAG)** để trả lời câu hỏi dựa trên dữ liệu đã lưu.
**Cách làm:**
1. Trong node **"Retrive Qdrant Vector Store"**, kiểm tra **Qdrant API Key** đã điền.
2. Trong node **"OpenAI Chat Model"**, chọn **model `gpt-4o-mini`**.
3. Thiết lập **prompt** cho RAG (ví dụ: *"Trả lời câu hỏi của khách hàng dựa trên dữ liệu từ collection Qdrant. Nếu không tìm thấy, hãy nói 'Tôi không biết, xin liên hệ admin.'"*).

---

### **3. Kích hoạt Workflow ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấp vào **"Execute Workflow"** và kiểm tra từng node.
   - Đảm bảo **tất cả webhook** (`n8n_call`, `n8n_rag_function`, `n8n_check_available`) hoạt động.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

## ✍️ **Mẹo & Gợi ý Nâng Cao**

### **🔹 Thêm Slack/Email để báo cáo**
- Sử dụng node **Slack** hoặc **Email** để gửi **báo cáo cuộc gọi** (ví dụ: thời gian gọi, nội dung, kết quả).
- Ví dụ:
  ```json
  {
    "operation": "sendMessage",
    "text": "📞 Cuộc gọi mới: {{$node["Telegram"].json["text"]}} | Thời gian: {{$node["Google Calendar"].json["start"]}}"
  }
  ```

### **🔹 Lưu log cuộc gọi vào Google Drive**
- Sử dụng node **Google Drive (Create File)** để lưu **transcript** của mỗi cuộc gọi vào một folder riêng.

### **🔹 Tăng cường RAG với nhiều nguồn dữ liệu**
- Thêm **Google Sheets** hoặc **Notion** để lấy dữ liệu mới nhất cho RAG.
- Ví dụ: Tải **tất cả sheet từ Google Sheets** và chuyển thành embeddings.

### **🔹 Sử dụng AI Agent cho nhiều ngôn ngữ**
- Thay đổi **Voice & Language** trong Retell AI để hỗ trợ **tiếng Anh, tiếng Nhật, tiếng Pháp...**.

---

## 📌 **Kết Luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn** quá trình hỗ trợ khách hàng qua điện thoại với:
✔ **AI trả lời chính xác** (RAG).
✔ **Đặt lịch tự động** (Google Calendar).
✔ **Hoạt động 24/7** (không cần nhân viên).
✔ **Chi phí thấp** (Retell AI miễn phí 10$).

**Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao trải nghiệm khách hàng!** 🚀

---
**💡 Cần hỗ trợ thêm?**
- Liên hệ tác giả: [info@n3w.it](mailto:info@n3w.it) hoặc [LinkedIn](https://www.linkedin.com/in/davideboizza).
- Đăng ký VPS để self-host: [TinoHost](https://tino.vn/vps-n8n?affid=388).