---
title: "🤖 Tạo Chatbot AI Tự Động Hóa Với Gemini AI, Dự Báo Thời Tiết & Trích Xuất Web (Starter Kit) - Tự Động Hóa 100% Không Code"
description: "Workflow này giúp các sếp xây dựng một chatbot AI thông minh tích hợp Gemini AI, dự báo thời tiết và trích xuất thông tin từ RSS, tự động hóa trả lời câu hỏi và thực hiện nhiệm vụ phức tạp chỉ bằng một giao diện chat. Giúp tiết kiệm thời gian lên đến 80% trong công việc hàng ngày."
slug: "tao-chatbot-ai-gemini-weather-web-scraping"
tags: [n8n, automation, ai-chatbot, gemini-ai, web-scraping, no-code]
keywords: [n8n workflow chatbot AI, tự động hóa với Gemini, dự báo thời tiết tự động, trích xuất tin tức từ RSS, AI agent n8n, tự động hóa công việc hàng ngày]
---

# 🚀 **Chatbot AI Tự Động Hóa: Gemini + Dự Báo Thời Tiết + Trích Xuất Web (Starter Kit)**

## **🔥 Giới Thiệu: Giải Pháp Tự Động Hóa AI Cho Các Sếp Bận Rộn**
Hãy tưởng tượng một chatbot AI không chỉ trả lời câu hỏi mà còn **tự động lấy dữ liệu thời tiết, trích xuất tin tức mới nhất từ RSS, hoặc thậm chí gửi email cho bạn** chỉ bằng một câu lệnh. **Không cần viết code, không cần kỹ sư phần mềm!** Workflow này là **Starter Kit hoàn hảo** để các sếp tự xây dựng một AI Agent thông minh, tích hợp với **Gemini AI (Google)**, dự báo thời tiết, và trích xuất thông tin từ web.

Với **9 node cốt lõi**, workflow này giúp bạn:
✅ **Tiết kiệm thời gian** lên đến **80%** trong công việc hàng ngày (không cần tra cứu thủ công).
✅ **Tự động hóa trả lời câu hỏi** phức tạp (ví dụ: *"Trời mưa ở Hà Nội tuần này?"* hoặc *"Lấy tin tức tech mới nhất"*).
✅ **Kết nối với Google Calendar & Gmail** để AI có thể **lấy lịch sự kiện hoặc gửi email tự động**.
✅ **Hoạt động 24/7** trên VPS riêng (self-hosted) để không phụ thuộc vào internet.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa trả lời câu hỏi phức tạp** (không cần tra cứu thủ công).
- **Dự báo thời tiết & tin tức mới nhất** chỉ bằng một câu lệnh.
- **Kết nối với Google Calendar & Gmail** để AI có thể **lấy lịch sự kiện hoặc gửi email tự động**.
- **Hoạt động liên tục 24/7** trên VPS riêng (không phụ thuộc vào máy tính cá nhân).
- **Tiết kiệm thời gian lên đến 80%** trong công việc hàng ngày.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Google** (để sử dụng **Gemini AI** và **Google Calendar**).
✔ **Tài khoản Gmail** (để gửi email tự động).
✔ **API Key của Google AI** (miễn phí, từ [Google AI Studio](https://aistudio.google.com/)).
✔ **Máy chủ VPS** (để chạy workflow 24/7, khuyến nghị **VPS TinoHost** hoặc **BNIX**).
:::

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
Các sếp có thể **import** workflow từ file JSON hoặc **copy/paste** JSON vào **n8n Editor**:
1. **Tải workflow** từ [n8n.io/workflows/6035](https://n8n.io/workflows/6035).
2. **Nhấn "Import"** trong n8n Editor.
3. **Chọn file JSON** và nhấn **"Import Workflow"**.

**Hoặc:**
1. **Copy toàn bộ JSON** từ file.
2. Trong n8n Editor, nhấn **"Import"** → **"Paste JSON"** → Dán và nhấn **"Import"**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
#### **🔑 Cấu Hình API Key cho Gemini & OpenAI**
Workflow này sử dụng **Gemini AI (Google)** làm mô hình mặc định, nhưng cũng hỗ trợ **OpenAI (GPT-4)** nếu các sếp muốn thay đổi.

##### **🔹 Cách Cấu Hình Gemini AI (Mặc Định)**
1. **Tìm node "Gemini"** (có biểu tượng **blue-purple swirl**).
2. **Double-click** vào node để mở cài đặt.
3. **Chọn "Credentials"** → **"Create New Credential"**.
4. **Nhập tên credential** (ví dụ: `"GoogleGeminiKey"`).
5. **Paste API Key** từ [Google AI Studio](https://aistudio.google.com/app/apikey) vào trường `API Key`.
6. **Lưu lại**.

##### **🔹 Cách Cấu Hình OpenAI (Tùy Chọn)**
1. **Tìm node "OpenAI"** (có biểu tượng **chatbot**).
2. **Double-click** vào node.
3. **Chọn "Credentials"** → **"Create New Credential"**.
4. **Nhập tên credential** (ví dụ: `"OpenAIKey"`).
5. **Paste API Key** từ [OpenAI Platform](https://platform.openai.com/api-keys) vào trường `API Key`.
6. **Lưu lại**.
7. **Bật node OpenAI** (nhấn `D` trên bàn phím khi chọn node để tắt/bật).

---
#### **🔹 Cấu Hình Google Calendar (Tùy Chọn)**
Nếu muốn AI **lấy lịch sự kiện từ Google Calendar**:
1. **Tìm node "Get Upcoming Events"** (Google Calendar Tool).
2. **Double-click** vào node.
3. **Chọn "Credentials"** → **"Create New Credential"**.
4. **Nhập tên credential** (ví dụ: `"GoogleCalendar"`).
5. **Cấu hình OAuth 2.0** (theo hướng dẫn của n8n).
6. **Lưu lại** và **connect** node này vào **Agent Tool**.

---
#### **🔹 Cấu Hình Gmail (Tùy Chọn)**
Nếu muốn AI **gửi email tự động**:
1. **Tìm node "Send Email"** (Gmail Tool).
2. **Double-click** vào node.
3. **Chọn "Credentials"** → **"Create New Credential"**.
4. **Nhập tên credential** (ví dụ: `"GmailAccount"`).
5. **Cấu hình OAuth 2.0** (theo hướng dẫn của n8n).
6. **Lưu lại** và **connect** node này vào **Agent Tool**.

---
#### **🔹 Cấu Hình RSS Feed (Tự Động Lấy Tin Tức)**
Workflow đã tích hợp **RSS Feed Reader** để lấy tin tức mới nhất:
1. **Tìm node "Get News"** (RSS Feed Read Tool).
2. **Double-click** vào node.
3. **Nhập URL RSS** (ví dụ: [RSS TechCrunch](https://techcrunch.com/feed/)).
4. **Lưu lại** và **connect** node này vào **Agent Tool**.

---
#### **🔹 Cấu Hình Dự Báo Thời Tiết (HTTP Request)**
Workflow sử dụng **OpenWeatherMap API** (miễn phí) để lấy thời tiết:
1. **Tìm node "Get Weather"** (HTTP Request Tool).
2. **Double-click** vào node.
3. **Nhập URL mẫu**:
   ```http
   https://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}&units=metric
   ```
4. **Thay thế `{city}` và `{api_key}`** bằng biến hoặc giá trị cố định.
5. **Lưu lại** và **connect** node này vào **Agent Tool**.

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Nhấn "Active"** ở góc trên bên phải (màu xanh).
2. **Test Run** với dữ liệu mẫu:
   - Mở **Chat Window** (node "Example Chat Window").
   - **Copy URL** từ node này.
   - **Dán vào trình duyệt** và thử chat với AI:
     - *"Trời mưa ở Hà Nội tuần này?"*
     - *"Lấy tin tức tech mới nhất."*
     - *"Lấy lịch sự kiện tuần này."*
3. **Nếu gặp lỗi**, kiểm tra lại **credentials** và **cấu hình node**.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **🔹 Thêm Tool Mới Cho AI Agent**
Các sếp có thể **thêm node mới** vào **Agent Tool** để AI có thêm khả năng:
- **Trích xuất dữ liệu từ website** (ví dụ: giá sản phẩm trên Shopee).
- **Kết nối với Trello/Notion** để AI quản lý công việc.
- **Gửi thông báo Slack/Telegram** khi có sự kiện mới.

**Cách thêm:**
1. **Kéo node mới** (ví dụ: **HTTP Request Tool**) vào **Agent Tool**.
2. **Cấu hình node** (ví dụ: lấy dữ liệu từ API).
3. **AI sẽ tự động sử dụng tool này** khi cần.

---
### **🔹 Lưu Log & Báo Cáo Tự Động**
Để theo dõi hoạt động của AI:
1. **Thêm node "Sticky Note"** (n8n-nodes-base.stickyNote) sau **Agent**.
2. **Lưu dữ liệu chat** vào **Google Sheets** hoặc **Notion**.
3. **Gửi báo cáo định kỳ** qua email (sử dụng **Gmail Tool**).

---
### **🔹 Tối Ưu Hóa Chat Interface**
Các sếp có thể **tùy chỉnh giao diện chat**:
- **Đổi màu nền, tiêu đề** trong **Options** của node "Example Chat Window".
- **Thêm CSS tùy chỉnh** trong **Custom CSS** để làm giao diện đẹp hơn.

---
## **📌 Kết Luận: Bắt Đầu Tự Động Hóa Ngay Hôm Nay!**
Workflow này là **công cụ hoàn hảo** để các sếp:
✔ **Tiết kiệm thời gian** trong công việc hàng ngày.
✔ **Tự động hóa trả lời câu hỏi phức tạp** chỉ bằng một chatbot AI.
✔ **Kết nối với nhiều dịch vụ** (Google Calendar, Gmail, RSS, thời tiết...).

**🎁 Khuyến nghị:**
- **Cài n8n trên VPS** để workflow hoạt động **24/7**.
- **Thử nghiệm với nhiều tool** để AI trở nên thông minh hơn.
- **Tùy chỉnh giao diện chat** để phù hợp với brand của doanh nghiệp.

**🚀 Hãy bắt đầu ngay!** Import workflow, cấu hình API, và **AI của bạn sẽ sẵn sàng trả lời mọi câu hỏi chỉ trong vài phút!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Happy Automating!** 🤖✨