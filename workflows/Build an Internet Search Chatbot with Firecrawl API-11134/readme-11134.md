---
title: "🔍 **Tự Động Hóa Chatbot Tìm Kiếm Trang Web Siêu Nhanh Với Firecrawl API (N8n) - Không Cần Code!**"
description: "Xây dựng một chatbot tìm kiếm internet thông minh, trả kết quả chính xác từ Firecrawl API và trả lời tự động cho người dùng qua chatbot. Giúp tiết kiệm thời gian lên tới 80% so với cách tìm kiếm thủ công."
slug: "tay-dong-hoa-chatbot-tim-kiem-firecrawl-n8n"
tags: [n8n, automation, ai-chatbot, firecrawl-api, no-code, chatbot-internet]
keywords: [n8n workflow tìm kiếm web, tự động hóa chatbot, Firecrawl API, chatbot không code, tự động trả lời tìm kiếm internet]
---

# 🚀 **Chatbot Tìm Kiếm Internet Tự Động Hóa Với Firecrawl API (N8n)**

### **Giải pháp cho ai?**
Các sếp và doanh nghiệp đang mệt mỏi với việc phải **tìm kiếm thủ công trên Google, Bing hay các trang web chuyên ngành** để tổng hợp thông tin? Hay bạn muốn **cung cấp một công cụ tìm kiếm thông minh** cho khách hàng, nhân viên, hoặc nội bộ công ty mà **không cần viết một dòng code nào**?

**Workflow này sẽ giúp bạn:**
- **Tạo một chatbot tìm kiếm internet** trả lời tức thì với kết quả từ Firecrawl API (dữ liệu chính xác hơn Google, không bị ảnh hưởng bởi SEO).
- **Tự động hóa quá trình tìm kiếm** và trả lời người dùng qua **Slack, Telegram, Discord, hoặc chatbot riêng**.
- **Monitor số dư API Firecrawl** để tránh bị cắt nguồn do hết tín dụng.
- **Cài đặt và chạy 24/7** trên máy chủ riêng (Self-hosted) để đảm bảo **tính riêng tư và ổn định**.

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm thời gian lên tới 80%** so với cách tìm kiếm thủ công.
✅ **Kết quả tìm kiếm chính xác** từ Firecrawl (không bị lọc bởi Google).
✅ **Trả lời tự động** cho người dùng qua chatbot (Slack, Telegram, Discord…).
✅ **Monitor số dư API** để tránh tình trạng hết tín dụng bất ngờ.
✅ **Không cần viết code** – chỉ cần cấu hình và chạy.
✅ **Hoạt động liên tục 24/7** trên máy chủ riêng (Self-hosted).
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Firecrawl API**
   - Đăng ký tại [Firecrawl](https://www.firecrawl.co/) và lấy **API Key**.
   - **Lưu ý:** Firecrawl cung cấp **miễn phí 1000 credit/month** cho tài khoản mới (đủ để test).
   - [Hướng dẫn đăng ký Firecrawl](https://www.firecrawl.co/docs/getting-started).

2. **Máy chủ n8n (Self-hosted)**
   - **Khuyến nghị:** Cài n8n trên **VPS** để workflow hoạt động 24/7.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

3. **Các node cần thiết**
   - **n8n-nodes-firecrawl** (để kết nối với Firecrawl API).
   - **n8n-nodes-base** (webhook, HTTP Request, Code, Chat Trigger).
   - **n8n-nodes-langchain** (nếu muốn nâng cao tính năng chatbot AI).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/11134](https://n8n.io/workflows/11134) (chọn **Export as JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. **Hoặc** copy toàn bộ JSON từ [đây](https://n8n.io/workflows/11134) và paste vào **Import Workflow** trên n8n.

#### **Phương pháp 2: Copy từ GitHub (nếu có)**
Nếu workflow được host trên GitHub, các sếp có thể clone và import trực tiếp.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Cấu hình Firecrawl API**
1. **Tạo credentials Firecrawl**
   - Trong **n8n Editor**, nhấn **Credentials** → **Add Credentials** → **Firecrawl API**.
   - Điền:
     - **Name:** `firecrawlApi` (phải trùng với workflow).
     - **API Key:** Lấy từ Firecrawl (đã đăng ký trước).
     - **Base URL:** `https://api.firecrawl.co`.

2. **Kiểm tra số dư API**
   - Node **"Verify Firecrawl Account Credit Balance"** sẽ tự động check số dư khi **Manual Trigger** được kích hoạt.

#### **🔹 Cấu hình Webhook (Backend Service)**
1. **Node "Define constants"**
   - Cần cập nhật **URL Webhook** để chatbot gọi đến.
   - **Cú pháp:**
     ```json
     {
       "webhookUrl": "https://[TÊN_DOMAIN_CỦA_BẠN].n8n.cloud/[PATH_WEBHOOK]"
     }
     ```
   - Ví dụ:
     ```json
     {
       "webhookUrl": "https://chatbot.n8n.cloud/620a78d5-00a6-4a05-9587-837a8d23ef7c"
     }
     ```
   - **Lưu ý:**
     - **PATH_WEBHOOK** phải trùng với `620a78d5-00a6-4a05-9587-837a8d23ef7c` trong node **"Receive search query"**.
     - Nếu dùng **Self-hosted**, URL sẽ là `http://[IP_VPS]:5678/[PATH_WEBHOOK]`.

2. **Node "Receive search query"**
   - Đảm bảo **HTTP Method = POST**.
   - **Path** phải trùng với giá trị trong `Define constants`.

#### **🔹 Cấu hình Chatbot (Interface)**
1. **Node "Receive chat message" (Chat Trigger)**
   - Cần **cấu hình Chat Trigger** để nhận tin nhắn từ người dùng.
   - **Cách thiết lập:**
     - Nhấn **Configure** → Chọn **Public** (nếu muốn chatbot mở cho tất cả).
     - **Initial Messages:** Có thể thêm một tin nhắn chào mừng như:
       ```json
       {
         "content": "🔍 **Chatbot Tìm Kiếm Internet** của tôi đã sẵn sàng! Gửi cho tôi một câu hỏi tìm kiếm và tôi sẽ trả lời ngay. 🚀"
       }
       ```
     - **Lưu ý:** Nếu dùng **Slack/Telegram**, cần cài thêm **n8n-nodes-slack** hoặc **n8n-nodes-telegram**.

2. **Node "Query search server (HTTP)"**
   - Đây là node **gửi yêu cầu tìm kiếm** đến backend (webhook).
   - **Cần kiểm tra:**
     - **Method:** POST.
     - **URL:** Phải trùng với `webhookUrl` trong `Define constants`.
     - **Headers:** `Content-Type: application/json`.

3. **Node "Format search response (Python)"**
   - Node này **chuyển đổi kết quả thô** từ Firecrawl thành **Markdown** dễ đọc.
   - **Lưu ý:**
     - Nếu không quen với Python, có thể **bỏ qua** và dùng **n8n-nodes-base.code** với JavaScript thay thế.
     - **Mẫu code Python:**
       ```python
       import json

       def format_results(data):
           results = []
           for item in data.get("results", []):
               results.append(f"📌 **Tên trang:** {item.get('title', 'N/A')}")
               results.append(f"🔗 **Link:** {item.get('url', 'N/A')}")
               results.append(f"📝 **Tóm tắt:** {item.get('snippet', 'Không có tóm tắt')}\n\n")
           return "\n".join(results)

       json_data = json.loads($input.all()["json"])
       return format_results(json_data)
       ```

4. **Node "Reply to the user in the chat"**
   - Đây là node **trả lời người dùng** qua chatbot.
   - **Cần kiểm tra:**
     - **Message:** Phải là kết quả đã được format từ node trước.
     - **Nếu dùng Slack/Telegram**, cần cấu hình thêm **credentials** cho node này.

---

### **3. Kích hoạt ⚡️**
1. **Test Run với dữ liệu mẫu**
   - Nhấn **Run Workflow** và gửi một **câu hỏi tìm kiếm** (ví dụ: *"Tính năng mới nhất của n8n 1.0"*).
   - Kiểm tra kết quả trả về có đúng không.

2. **Bật Active Workflow**
   - Sau khi test thành công, chuyển **Active** sang **ON**.

3. **Kiểm tra số dư API (Optional)**
   - Nhấn **Manual Trigger** trên node **"Verify Firecrawl Account Credit Balance"** để xem số dư còn lại.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Kết hợp với Slack/Telegram**
- **Nếu muốn chatbot hoạt động trên Slack:**
  - Cài **n8n-nodes-slack**.
  - Thay thế node **"Receive chat message"** bằng **Slack Incoming Webhook**.
  - Cấu hình **credentials Slack** và **URL Webhook** từ Slack.

- **Nếu muốn chatbot hoạt động trên Telegram:**
  - Cài **n8n-nodes-telegram**.
  - Thay thế node **"Receive chat message"** bằng **Telegram Bot**.
  - Lấy **API Token** từ [@BotFather](https://t.me/BotFather) và cấu hình.

### **2. Lưu log tìm kiếm**
- Thêm node **n8n-nodes-base.file** để lưu **tất cả lịch sử tìm kiếm** vào Google Sheets hoặc cơ sở dữ liệu.
- **Cách làm:**
  1. Thêm node **Google Sheets** (nếu dùng Google Drive).
  2. Cấu hình **credentials Google** và **Sheet Name**.
  3. Kết nối node **"Format search response"** với node **Google Sheets**.

### **3. Gửi báo cáo định kỳ**
- Sử dụng **n8n-nodes-base.schedule** để **gửi báo cáo sử dụng API** hàng tuần.
- **Cách làm:**
  1. Thêm node **Schedule**.
  2. Cấu hình **thời gian chạy** (ví dụ: 09:00 hàng tuần).
  3. Kết nối với node **"Verify Firecrawl Account Credit Balance"**.
  4. Thêm node **Email** (n8n-nodes-base.email) để gửi báo cáo cho admin.

### **4. Cải thiện tính năng AI với LangChain**
- Nếu muốn **chatbot trả lời tự động** thay vì chỉ tìm kiếm, có thể kết hợp với **LangChain**.
- **Cách làm:**
  1. Cài **n8n-nodes-langchain**.
  2. Thêm node **Chat (LangChain)** sau khi lấy kết quả từ Firecrawl.
  3. Cấu hình **model AI** (ví dụ: GPT-4, Llama 2).
  4. **Prompt mẫu:**
     ```json
     {
       "prompt": "Tóm tắt lại kết quả tìm kiếm này cho người dùng một cách dễ hiểu và ngắn gọn. Nếu có thông tin quan trọng, hãy nhấn mạnh. Kết quả: {{$json.results}}"
     }
     ```

---

## 📌 **Kết luận**
### **Bây giờ các sếp đã có:**
✅ **Một chatbot tìm kiếm internet tự động hóa 100% không cần code.**
✅ **Kết quả chính xác từ Firecrawl (không bị lọc bởi Google).**
✅ **Monitor số dư API để tránh hết tín dụng.**
✅ **Hoạt động 24/7 trên máy chủ riêng (Self-hosted).**

### **Hành động tiếp theo:**
1. **Cài đặt n8n trên VPS** (nếu chưa có).
2. **Import workflow** và cấu hình **Firecrawl API**.
3. **Test với câu hỏi mẫu** và **bật Active**.
4. **Kết hợp với Slack/Telegram** nếu muốn mở rộng.

**🚀 Bắt đầu tự động hóa ngay hôm nay!** Nếu có vấn đề, các sếp có thể comment bên dưới hoặc liên hệ admin n8n cho hỗ trợ.

---
**🔗 [Tải workflow nguyên bản từ n8n.io](https://n8n.io/workflows/11134)**
**📌 [Hướng dẫn cài n8n trên VPS](https://docs.n8n.io/hosting/installation/installation-on-vps/)**