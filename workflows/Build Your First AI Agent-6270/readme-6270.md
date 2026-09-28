---
title: "🤖 Tạo AI Agent Của Bạn: Chatbot Tự Động Hóa Thông Minh Với n8n & Google Gemini"
description: "Workflow này giúp các sếp xây dựng AI Agent đầu tiên, tự động trả lời câu hỏi, lấy tin tức thời sự, kiểm tra thời tiết và nhiều hơn nữa chỉ với một chatbot thông minh. Tiết kiệm thời gian, tăng hiệu suất và tự động hóa công việc hàng ngày."
slug: "tai-tao-ai-agent-voi-n8n-google-gemini"
tags: [n8n, automation, ai-agent, chatbot, google-gemini, langchain]
keywords: [n8n workflow ai agent, tự động hóa chatbot, google gemini api, xây dựng ai agent không code, tự động lấy tin tức thời sự, kiểm tra thời tiết tự động]
---

# 🚀 **Tạo AI Agent Của Bạn: Chatbot Tự Động Hóa Thông Minh Với n8n & Google Gemini**

---

### **🔥 Bạn đã bao giờ mệt mỏi vì phải tra cứu tin tức, kiểm tra thời tiết, hoặc trả lời những câu hỏi lặp đi lặp lại hàng ngày?**
Hãy tưởng tượng một AI Agent cá nhân hóa, hoạt động 24/7, giúp bạn:
- **Lấy tin tức thời sự** từ RSS Feed.
- **Kiểm tra thời tiết** ở bất kỳ địa điểm nào.
- **Trả lời câu hỏi** về n8n, công nghệ, hoặc bất kỳ chủ đề nào.
- **Tự động hóa công việc** như gửi email, quản lý lịch, hoặc tra cứu thông tin.

**Workflow này là giải pháp hoàn hảo!** Với **n8n + Google Gemini**, bạn có thể xây dựng một AI Agent thông minh, **không cần viết một dòng code nào!**

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản Cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** – AI Agent trả lời ngay lập tức thay vì bạn phải tra cứu thủ công.
✅ **Tính chính xác cao** – Lấy dữ liệu thời sự và thời tiết **thực thời**.
✅ **Cá nhân hóa** – Thay đổi **System Message** để AI Agent phù hợp với phong cách của bạn.
✅ **Hoạt động liên tục** – Chạy 24/7 trên VPS, không giới hạn phiên bản Cloud.
✅ **Mở rộng khả năng** – Thêm các công cụ như **Gmail, Google Calendar** để AI Agent tự động hóa nhiều hơn.
:::

---

### **🔧 Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Google AI Studio** (để lấy **API Key** của Google Gemini).
✔ **Tài khoản RSS Feed** (ví dụ: Feedly, NewsAPI, hoặc RSS Feed của blog cá nhân).
✔ **N8n Self-hosted** (để workflow hoạt động liên tục).
✔ **Mối liên kết với các dịch vụ mở rộng** (nếu muốn thêm Gmail, Calendar…).

---

### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào **n8n Editor**:
1. **Tải workflow** từ [đây](https://n8n.io/workflows/6270) (nếu có link JSON).
2. **Mở n8n Editor** → **Import Workflow** → **Paste JSON**.
3. **Hoặc** tải file `.json` và kéo thả vào Editor.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **6 node chính**, các sếp cần **cấu hình kỹ lưỡng** như sau:

##### **🔹 Node 1: "Get News" (RSS Feed Read Tool)**
- **Mục đích**: Lấy tin tức thời sự từ RSS Feed.
- **Cách cấu hình**:
  - **Credentials**: Tạo mới và điền **URL RSS Feed** (ví dụ: [TechCrunch RSS](https://techcrunch.com/feed/)).
  - **Lưu ý**: Nếu không có RSS Feed, các sếp có thể dùng **NewsAPI** hoặc **Feedly**.

##### **🔹 Node 2: "Get Weather" (HTTP Request Tool)**
- **Mục đích**: Lấy thông tin thời tiết từ API (ví dụ: OpenWeatherMap).
- **Cách cấu hình**:
  - **URL**: `https://api.openweathermap.org/data/2.5/weather?q={city}&appid={API_KEY}&units=metric`
  - **Thay thế `{city}`** bằng tên thành phố (ví dụ: `Hanoi`).
  - **Thay thế `{API_KEY}`** bằng API Key của OpenWeatherMap (nếu muốn sử dụng).
  - **Lưu ý**: Nếu không muốn dùng API, có thể **bỏ node này** và chỉ giữ **Google Gemini** trả lời.

##### **🔹 Node 3: "Connect your model" (LM Chat Google Gemini)**
- **Mục đích**: Kết nối với **Google Gemini** để AI Agent trả lời.
- **Cách cấu hình**:
  1. **Tạo API Key Google Gemini**:
     - Đăng nhập [Google AI Studio](https://aistudio.google.com/app/apikey).
     - Nhấn **"Create API key in new project"** → **Copy Key**.
  2. **Trong n8n**:
     - Mở node **LM Chat Google Gemini** → **Credentials** → **Create New**.
     - Dán **API Key** vào trường **API Key** → **Save**.
  3. **Thay đổi System Message** (nếu muốn AI Agent có phong cách riêng):
     ```json
     "You are a helpful AI assistant that can fetch real-time data using tools. Always provide accurate and up-to-date information."
     ```

##### **🔹 Node 4: "Example Chat" (Chat Trigger)**
- **Mục đích**: Khởi động giao diện chat cho AI Agent.
- **Cách cấu hình**:
  - **Credentials**: Tạo mới (nếu chưa có).
  - **Lưu ý**: Sau khi cấu hình xong, **không cần thay đổi gì** nữa.

##### **🔹 Node 5: "Your First AI Agent" (Agent)**
- **Mục đích**: **Cơ sở** của AI Agent, kết nối tất cả các node.
- **Cách cấu hình**:
  - **Tool Inputs**:
    - **Add Tool** → Chọn **RSS Feed Read Tool** (node "Get News").
    - **Add Tool** → Chọn **HTTP Request Tool** (node "Get Weather").
    - **Add Tool** → Chọn **LM Chat Google Gemini** (node "Connect your model").
  - **Lưu ý**: Nếu không muốn dùng **thời tiết**, có thể **bỏ node HTTP Request**.

##### **🔹 Node 6: "Conversation Memory" (Memory Buffer Window)**
- **Mục đích**: **Giữ nhớ** các câu hỏi trước đó để AI Agent trả lời liên tục.
- **Cách cấu hình**:
  - **Context Window Length**: Đặt **5-10** (số lượng câu hỏi lưu trữ).
  - **Lưu ý**: Nếu muốn AI Agent **quên** sau mỗi lần chat, đặt **0**.

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và thử các câu hỏi:
     - *"What’s the weather in Hanoi?"*
     - *"Get me the latest tech news."*
     - *"Give me ideas for n8n AI agents."*
2. **Bật Active Workflow**:
   - Nhấn **Active** → **Save**.

---

### **✍️ Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÂNG CAO]
🔹 **Thêm công cụ Gmail/Calendar**:
   - Mở node **Agent** → **Tool Inputs** → **Add Tool** → Chọn **Gmail** hoặc **Google Calendar**.
   - Cấu hình **Credentials** và **API Key** tương ứng.

🔹 **Lưu log chat**:
   - Thêm node **Google Sheets** hoặc **Slack** để ghi lại tất cả các cuộc chat.
   - Ví dụ: Sau khi AI Agent trả lời, gửi kết quả vào **Google Sheets** để theo dõi.

🔹 **Chia sẻ AI Agent với khách hàng**:
   - Sau khi **Active Workflow**, n8n sẽ tạo **URL công khai**.
   - Chia sẻ URL này cho khách hàng để họ **trả lời câu hỏi tự động** mà không cần hỗ trợ trực tiếp.

🔹 **Tweak System Message**:
   - Thay đổi **phong cách** của AI Agent bằng cách sửa **System Message** trong node **LM Chat Google Gemini**.
   - Ví dụ:
     ```json
     "You are a Vietnamese AI assistant, friendly and professional. Always use Vietnamese language."
     ```
:::

---

### **📌 Kết luận**
**Workflow này là cách đơn giản nhất để các sếp xây dựng một AI Agent thông minh, tự động hóa công việc hàng ngày, và tiết kiệm thời gian!**
🚀 **Bắt đầu ngay** bằng cách:
1. **Import workflow** vào n8n.
2. **Cấu hình API Key Google Gemini**.
3. **Thêm các công cụ** (nếu muốn).
4. **Kích hoạt và sử dụng!**

**Happy Automating!** 🤖✨
---
**Nếu gặp vấn đề, các sếp có thể:**
- **Đọc tài liệu chính thức** của n8n: [n8n.io](https://n8n.io/)
- **Đăng ký coaching** để nâng cao kỹ năng: [Book Coaching](https://api.ia2s.app/form/templates/coaching?template=Very%20First%20AI%20Agent)
- **Gửi feedback** để cải thiện template: [Submit Feedback](https://api.ia2s.app/form/templates/feedback?template=Very%20First%20AI%20Agent)