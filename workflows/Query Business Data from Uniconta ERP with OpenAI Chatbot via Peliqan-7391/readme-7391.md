---
title: "🤖 Tự Động Hóa Trả Lời Câu Hỏi ERP Uniconta Bằng Chatbot AI (Không Cần Code)"
description: "Workflow này giúp các sếp tự động hóa việc trả lời các câu hỏi liên quan đến dữ liệu ERP Uniconta (sản phẩm, tồn kho, tài chính...) thông qua chatbot AI tích hợp với OpenAI và Peliqan - giải pháp 'cache' dữ liệu nhanh chóng và chính xác."
slug: "tự-dộng-hoa-chatbot-ai-erp-uniconta"
tags: [n8n, automation, no-code, ai-chatbot, uniconta-erp, peliqan, openai]
keywords: [n8n workflow uniconta, chatbot ai tự động hóa erp, peliqan n8n, query sql từ erp, tự động hóa câu hỏi tài chính, ai agent erp]
---

# 🚀 Chatbot AI Trả Lời Câu Hỏi ERP Uniconta (Không Cần Code)

### 🔍 Giải quyết vấn đề gì?
Các sếp thường phải mất thời gian **tìm kiếm thủ công** trên hệ thống ERP Uniconta để trả lời các câu hỏi như:
- *"Tồn kho sản phẩm ABC hiện tại là bao nhiêu?"*
- *"Doanh thu tháng 12/2023 của khách hàng XYZ là bao nhiêu?"*
- *"Số lượng đơn hàng chờ xử lý trong tháng này là bao nhiêu?"*

Workflow này **tự động hóa hoàn toàn** quá trình này bằng cách:
✅ **Chuyển câu hỏi tự nhiên (natural language) thành SQL** và truy vấn dữ liệu từ Uniconta.
✅ **Trả lời chính xác và nhanh chóng** thông qua chatbot AI tích hợp với OpenAI.
✅ **Không cần viết code** - chỉ cần cấu hình và chạy.

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Trả lời câu hỏi ERP chỉ trong vài giây thay vì phút/giây.
- **Chính xác 100%**: Dữ liệu lấy trực tiếp từ Uniconta, không sai sót.
- **Hoạt động 24/7**: Chatbot AI có thể trả lời bất kỳ lúc nào, kể cả ngoài giờ làm việc.
- **Cá nhân hóa**: Hỗ trợ nhiều loại câu hỏi (tồn kho, tài chính, sản phẩm, đơn hàng...).
- **Mở rộng dễ dàng**: Thêm dữ liệu từ các hệ thống khác (CRM, HRM...) vào Peliqan.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Uniconta ERP** (để lấy API key).
2. **Tài khoản Peliqan.io** (đăng ký [tại đây](https://peliqan.io)).
3. **API Key OpenAI** (để kết nối với mô hình AI).
4. **VPS hoặc máy chủ** để chạy n8n (self-hosted) để workflow hoạt động liên tục.
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

**Các bước thiết lập Peliqan:**
- Đăng ký tài khoản trên [Peliqan.io](https://peliqan.io).
- Thêm **Uniconta** làm kết nối trong Peliqan (sử dụng API key từ Uniconta).
- Sao chép **Peliqan API Key** (tìm ở Settings > API key) để dùng trong n8n.
- Chọn **Data Warehouse** trong node Peliqan (trong workflow).
- *(Tùy chọn)* Chạy [script mẫu](https://help.peliqan.io/build-ai-agents-with-n8n-and-peliqan#block-2401aa9b387980cf8b2ff069588dd3dc) để lấy **datamodel** của Uniconta và dán vào **System Message** của AI Agent (thay thế mô hình mặc định).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- **Tải file JSON** của workflow từ [đây](https://n8n.io/workflows/7391).
- Mở **n8n Editor** và nhấn **Import** > Chọn file JSON vừa tải.
- Hoặc **copy/paste** JSON từ file vào ô **Import Workflow** trong Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm **5 node chính**, các sếp cần cấu hình như sau:

##### **Node 1: When chat message received (chatTrigger)**
- **Không cần cấu hình** (node này tự động kích hoạt khi có tin nhắn).

##### **Node 2: AI Agent (agent)**
- **System Message**: Dán **datamodel** của Uniconta (nếu đã chạy script tùy chọn trên).
  *Ví dụ:*
  ```json
  {
    "description": "You are an AI assistant that can query Uniconta ERP data. Available tables: Products, Stock, Customers, Invoices, Orders."
  }
  ```
- **Tools**: Chọn **SQL** (đã được thêm tự động từ node Peliqan).

##### **Node 3: OpenAI Chat Model (lmChatOpenAi)**
- **Credentials**: Chọn `openAiApi` (đã cấu hình trước).
- **Model**: Chọn mô hình OpenAI (ví dụ: `gpt-4` hoặc `gpt-3.5-turbo`).
- **Temperature**: Đặt giá trị từ `0.3` đến `0.7` (để kết quả logic hơn).

##### **Node 4: Simple Memory (memoryBufferWindow)**
- **Không cần cấu hình** (node này lưu lịch sử chat để AI nhớ trải nghiệm trước).

##### **Node 5: Execute an SQL query via Peliqan (peliqanTool)**
- **Credentials**: Chọn `peliqanApi` (API key đã sao chép từ Peliqan).
- **Operation**: Đặt `exec`.
- **Resource**: Đặt `query`.
- **Data warehouse name**: Chọn **Data Warehouse** đã tạo trong Peliqan.
- **SQL Query**: Node này sẽ tự động nhận **SQL từ AI Agent** và thực thi.

##### **Bước quan trọng: Cấu hình môi trường**
Trước khi chạy, các sếp cần chạy lệnh sau trên **VPS** để cho phép sử dụng Peliqan như một tool:
```bash
export N8N_COMMUNITY_PACKAGES_ALLOW_TOOL_USAGE=True
```
*(Lưu ý: Lệnh này chỉ cần chạy 1 lần, sau đó lưu vào `.bashrc` hoặc `.zshrc` để tự động chạy khi khởi động máy.)*

#### 3. Kích hoạt ⚡️
- **Test run**: Nhấn **Run Workflow** và gửi một câu hỏi mẫu như:
  *"Hiện tại tồn kho sản phẩm 'ABC123' là bao nhiêu?"*
- **Kiểm tra kết quả**: Nếu trả lời chính xác, **bật Active** để workflow hoạt động liên tục.

---

### ✍️ Mẹo & gợi ý nâng cao
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** để chatbot AI trả lời trên kênh công việc.
   - *Cách làm*: Sau node `chatTrigger`, thêm node **Slack Incoming Webhook** để nhận tin nhắn từ kênh.

2. **Lưu lịch sử câu hỏi**:
   - Thêm node **Google Sheets** hoặc **Notion** để lưu tất cả câu hỏi và trả lời.
   - *Cách làm*: Sau node `OpenAI Chat Model`, thêm node **Google Sheets** với action `Create Row`.

3. **Báo cáo định kỳ**:
   - Tạo một workflow riêng để **tổng hợp thống kê** về câu hỏi thường gặp và gửi báo cáo hàng tuần qua email.
   - *Cách làm*: Sử dụng node **Schedule** + **Google Sheets** + **Email**.

4. **Cải thiện mô hình AI**:
   - Thêm **các ví dụ cụ thể** về câu hỏi ERP vào `System Message` của AI Agent để tăng độ chính xác.
   - *Ví dụ*:
     ```json
     "examples": [
       {
         "question": "Tồn kho sản phẩm 'ABC123' hiện tại là bao nhiêu?",
         "sql": "SELECT stock_quantity FROM Products WHERE product_code = 'ABC123'"
       }
     ]
     ```
:::

---

### 📌 Kết luận
Workflow này là **giải pháp hoàn hảo** để tự động hóa việc trả lời câu hỏi ERP Uniconta mà **không cần viết một dòng code**. Với sự hỗ trợ của **Peliqan** (cache dữ liệu nhanh) và **OpenAI** (AI trả lời logic), các sếp có thể:
✔ **Tiết kiệm thời gian** cho đội ngũ tài chính/kinh doanh.
✔ **Giảm sai sót** do tìm kiếm thủ công.
✔ **Mở rộng khả năng** với nhiều hệ thống khác (CRM, HRM...).

**Hành động ngay!**
1. Đăng ký **Peliqan** và **Uniconta API Key**.
2. Cài đặt **n8n trên VPS** (sử dụng mã giảm giá **VPSN8N**).
3. Import workflow và **bắt đầu tự động hóa**!

---
**Cần hỗ trợ?**
- Liên hệ **Peliqan** tại [support@peliqan.io](mailto:support@peliqan.io).
- Đăng ký **VPS** tại [TinoHost](https://tino.vn/vps-n8n?affid=388) hoặc [BNIX](https://my.bnix.one/aff.php?aff=172).