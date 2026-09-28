---
title: "🤖 **Tự Động Hóa Chatbot WhatsApp AI - Hướng Dẫn Xây Dựng Bot Sales Chuyên Nghiệp Miễn Code**"
description: "Workflow này giúp các sếp xây dựng một chatbot WhatsApp thông minh, tích hợp trí tuệ nhân tạo (AI) để tự động trả lời khách hàng về sản phẩm, tiết kiệm thời gian hỗ trợ lên đến 80%. Dùng vector store để tra cứu thông tin chính xác từ tài liệu PDF, kết hợp với GPT-4o để trả lời tự nhiên như con người."
slug: "tay-dong-hoa-chatbot-whatsapp-ai-sales"
tags: [n8n, automation, no-code, ai-chatbot, whatsapp-bot, sales-automation, vector-database]
keywords: [chatbot whatsapp tự động hóa, bot sales ai, n8n workflow whatsapp, tự động trả lời khách hàng, vector store n8n, gpt-4o chatbot]
---

# **🚀 Chatbot WhatsApp AI - Hỗ Trợ Khách Hàng Tự Động Hóa 100% Miễn Code**

## **💡 Giới Thiệu: Khắc Phục Nỗi Đau Hỗ Trợ Khách Hàng Thời Gian Thực**
Các sếp đang gặp phải những vấn đề sau khi hỗ trợ khách hàng qua WhatsApp:
- **Tốn thời gian**: Phải trả lời hàng chục tin nhắn mỗi ngày về sản phẩm, giá cả, hoặc đặc tính kỹ thuật.
- **Chính xác thấp**: Thông tin trả lời không đồng nhất, dễ gây nhầm lẫn cho khách.
- **Không hoạt động 24/7**: Đội ngũ phải trực ca để không bỏ lỡ tin nhắn.
- **Khó tra cứu**: Phải tìm kiếm thủ công trong tài liệu PDF để trả lời chính xác.

**Workflow này giải quyết tất cả!** Với một bot WhatsApp AI tích hợp:
✅ **Trả lời tự động** dựa trên trí tuệ nhân tạo (GPT-4o).
✅ **Tra cứu thông tin chính xác** từ tài liệu PDF (ví dụ: brochure sản phẩm Yamaha).
✅ **Học hỏi từ lịch sử** (chat memory) để trả lời cá nhân hóa.
✅ **Hoạt động 24/7** mà không cần người trực.

---

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm 80% thời gian hỗ trợ thủ công.
- **Trả lời chính xác**: Dựa trên kiến thức từ tài liệu PDF (không sai lệch).
- **Trải nghiệm khách hàng tốt hơn**: Trả lời tự nhiên như con người.
- **Hoạt động liên tục**: Bot hoạt động 24/7, không cần trực ca.
- **Dễ mở rộng**: Thêm sản phẩm mới chỉ cần cập nhật tài liệu PDF.
:::

---

### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần:
1. **Tài khoản WhatsApp Business API**:
   - Đăng ký trên [Meta Business Suite](https://business.facebook.com/) và lấy **API Key**.
   - **Lưu ý**: WhatsApp Business API yêu cầu xác thực qua số điện thoại hoặc tài khoản Meta.
   - **Gợi ý**: Sử dụng dịch vụ [Twilio](https://www.twilio.com/) hoặc [360dialog](https://360dialog.com/) để dễ dàng kết nối.

2. **Tài khoản OpenAI API**:
   - Đăng ký miễn phí trên [OpenAI](https://platform.openai.com/) và lấy **API Key**.
   - Workflow sử dụng mô hình **GPT-4o** và **text-embedding-3-small**.

3. **Tài liệu PDF sản phẩm**:
   - Ví dụ: Brochure sản phẩm Yamaha (được cung cấp trong workflow).
   - **Lưu ý**: Nếu muốn sử dụng tài liệu riêng, thay thế URL trong node **HTTP Request**.

4. **VPS cho n8n (Self-hosted)**:
   :::info[Gợi ý hạ tầng cho n8n]
   Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
   :::
---

---

## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/2465](https://n8n.io/workflows/2465) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import** → Dán JSON và nhấn **Import**.

### **2. Các Bước Cấu Hình BẮT BUỘC**
Workflow gồm **2 phần chính**:
- **Phần 1**: Tạo vector store từ tài liệu PDF (chỉ cần chạy 1 lần).
- **Phần 2**: Xây dựng bot WhatsApp AI (hoạt động liên tục).

#### **📌 Phần 1: Tạo Vector Store từ PDF**
1. **Node "Extract from File"**:
   - Đảm bảo **operation = "pdf"** (đã mặc định).
   - **Lưu ý**: Nếu muốn sử dụng PDF riêng, thay đổi URL trong node **"get Product Brochure"** (HTTP Request).

2. **Node "Create Product Catalogue"**:
   - Chọn **Vector Store Type = "In-Memory"** (đã mặc định).
   - **Lưu ý**: Đối với sản xuất, thay thế bằng **Qdrant** hoặc **Pinecone**.

#### **📌 Phần 2: Cấu Hình WhatsApp & AI Agent**
1. **Node "WhatsApp Trigger"**:
   - Chọn **credentials = "whatsAppTriggerApi"** (đã tạo khi đăng ký WhatsApp Business API).
   - **Lưu ý**: Cần cấu hình **Phone Number** và **Verification Token** trong credentials.

2. **Node "OpenAI Chat Model"**:
   - Chọn **credentials = "openAiApi"** (API Key OpenAI).
   - **Model**: Đã mặc định là **gpt-4o-2024-08-06** (mới nhất).

3. **Node "Reply To User"**:
   - Chọn **credentials = "whatsAppApi"** (API Key WhatsApp).
   - **Operation = "send"** (đã mặc định).

4. **Node "Handle Message Types" (Switch)**:
   - Cấu hình để **chỉ xử lý tin nhắn text** (loại bỏ audio/video).
   - **Lưu ý**: Nếu muốn hỗ trợ tất cả loại tin nhắn, tham khảo workflow khác của tác giả [đây](https://n8n.io/creators/jimleuk/).

5. **Node "AI Sales Agent"**:
   - **Tool Vector Store**: Kết nối với vector store đã tạo ở phần 1.
   - **Chat Memory**: Để bot nhớ lịch sử trò chuyện với từng khách hàng.

#### **🔄 Test Run & Kích Hoạt**
- Nhấn **Test Run** với tin nhắn mẫu (ví dụ: *"Giá của loa Yamaha mới nhất là bao nhiêu?"*).
- Nếu trả lời đúng, **bật Active workflow** để bot hoạt động 24/7.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Cập Nhật Tài Liệu PDF**:
   - Khi có brochure mới, chạy lại phần **Extract from File** và **Create Product Catalogue** để cập nhật vector store.

2. **Thêm Hỗ Trợ Slack/Telegram**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để gửi báo cáo lỗi hoặc tin nhắn quan trọng.

3. **Lưu Log Hỗ Trợ**:
   - Thêm node **Google Sheets** hoặc **Airtable** để ghi lại lịch sử trò chuyện với khách hàng.

4. **Tối Ưu Hóa Trả Lời**:
   - Cập nhật **prompt** trong node AI Agent để bot trả lời chuyên nghiệp hơn (ví dụ: thêm tone "chuyên nghiệp" hoặc "hữu nghị").

5. **Xử Lý Tin Nhắn Khác Loại**:
   - Thêm logic trong **Switch Node** để bot trả lời tin nhắn hình ảnh/video bằng cách gửi lại tin nhắn mẫu.

---

### **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa hỗ trợ khách hàng qua WhatsApp **miễn code**, tiết kiệm thời gian và nâng cao trải nghiệm khách hàng. **Bắt đầu ngay** bằng cách import và cấu hình theo hướng dẫn trên!

**🚀 Cần hỗ trợ thêm?**
- **Join Discord n8n**: [https://discord.com/invite/XPKeKXeB7d](https://discord.com/invite/XPKeKXeB7d)
- **Hỏi trên Forum**: [https://community.n8n.io/](https://community.n8n.io/)

---
**💡 Lưu ý cuối cùng**: Đối với sản xuất, thay thế **In-Memory Vector Store** bằng **Qdrant** hoặc **Pinecone** để lưu trữ vector store lâu dài.