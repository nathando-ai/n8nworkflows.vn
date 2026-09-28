---
title: "📈 **Tự Động Hóa Phân Tích Cổ Phiếu Mỹ (US Stock) + Báo Cáo PDF + Telegram AI – Không Cần Code!**"
description: "Workflow tự động phân tích danh mục cổ phiếu Mỹ hàng ngày bằng AI (Perplexity + OpenAI), tạo báo cáo PDF chuyên nghiệp và gửi thông báo trực tiếp qua Telegram. Giúp các nhà đầu tư tiết kiệm thời gian, tối ưu hóa quyết định đầu tư với dữ liệu phân tích tự động hóa 24/7."
slug: "tu-dong-hoa-phan-tich-co-phieu-my-ai-telegram-pdf"
tags: [n8n, automation, ai-chatbot, stock-analysis, telegram-bot, pdf-automation, no-code]
keywords: [n8n workflow phân tích cổ phiếu, tự động hóa đầu tư chứng khoán, AI phân tích stock, báo cáo PDF tự động, Telegram bot đầu tư, Perplexity AI + OpenAI]
---

# 🚀 **Tự Động Hóa Phân Tích Cổ Phiếu Mỹ (US Stock) Với AI + Telegram + PDF – Không Cần Code!**

### **🔍 Nỗi Đau Của Các Nhà Đầu Tư Chứng Khoán**
Các sếp đang phải:
- **Tốn thời gian** để theo dõi và phân tích hàng chục cổ phiếu Mỹ hàng ngày.
- **Khó khăn trong việc tổng hợp dữ liệu** từ nhiều nguồn khác nhau (API, báo cáo tài chính, tin tức thị trường).
- **Không có báo cáo định kỳ** để đánh giá hiệu suất danh mục đầu tư.
- **Phải làm thủ công** việc tạo báo cáo PDF và gửi thông báo qua Telegram, mất nhiều công sức.

**Workflow này giải quyết tất cả!** Với sự kết hợp giữa **AI (Perplexity + OpenAI)**, **tự động hóa n8n** và **Telegram**, các sếp có thể:
✅ **Phân tích tự động** danh mục cổ phiếu Mỹ hàng ngày.
✅ **Tạo báo cáo PDF chuyên nghiệp** với dữ liệu phân tích chi tiết.
✅ **Nhận thông báo trực tiếp** qua Telegram khi có kết quả mới.
✅ **Tối ưu hóa quyết định đầu tư** dựa trên phân tích AI.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phân tích thủ công hàng ngày.
- **Dữ liệu chính xác**: AI phân tích từ nhiều nguồn (Perplexity + OpenAI).
- **Báo cáo PDF tự động**: Tạo và gửi báo cáo định kỳ một cách chuyên nghiệp.
- **Thông báo tức thời**: Nhận kết quả phân tích qua Telegram ngay khi có.
- **Tối ưu hóa đầu tư**: Đánh giá hiệu suất danh mục một cách khoa học.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram**:
   - Bot Telegram (đăng ký tại [@BotFather](https://t.me/BotFather)).
   - Chat ID của cá nhân hoặc nhóm để nhận báo cáo.
2. **API Keys**:
   - **Perplexity API Key** (đăng ký tại [Perplexity](https://www.perplexity.ai/)).
   - **OpenAI API Key** (đăng ký tại [OpenAI](https://platform.openai.com/)).
   - **PDFco API Key** (đăng ký tại [PDFco](https://pdfco.io/)).
3. **Database**:
   - **Supabase** hoặc **PostgreSQL** để lưu trữ dữ liệu người dùng và danh mục cổ phiếu.
4. **Danh sách cổ phiếu**:
   - Danh sách mã cổ phiếu Mỹ (ví dụ: AAPL, MSFT, GOOGL) để phân tích.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [link gốc](https://n8n.io/workflows/5687).
2. Mở **n8n Editor** và chọn **Import Workflow**.
3. Chọn file JSON và nhấn **Import**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này sử dụng nhiều node quan trọng. Dưới đây là hướng dẫn chi tiết:

##### **A. Cấu Hình Telegram**
- **Telegram Trigger** và **Telegram** nodes:
  - Đăng ký **Bot Telegram** và lấy **Token Bot**.
  - Thêm **Chat ID** của cá nhân hoặc nhóm vào các node liên quan.
  - Cấu hình **Update Sent** và **Download PDF Telegram** để gửi báo cáo.

##### **B. Cấu Hình AI (Perplexity + OpenAI)**
- **Perplexity Node**:
  - Điền **Perplexity API Key** vào node **"Message a model"** và **"Message a model1"**.
  - Cấu hình **Prompt** để phân tích cổ phiếu (ví dụ: *"Analyze the performance of AAPL stock in the last 30 days"*).
- **OpenAI Chat Model Nodes**:
  - Điền **OpenAI API Key** vào các node như **"OpenAI Chat Model1"**, **"OpenAI Chat Model"**, **"OpenAI Analysis"**, v.v.
  - Cấu hình **Model** (ví dụ: `gpt-4` hoặc `gpt-3.5-turbo`).
  - Đặt **Prompt** phù hợp cho từng node (ví dụ: phân tích, tổng hợp, tạo báo cáo).

##### **C. Cấu Hình Database (Supabase/PostgreSQL)**
- **Supabase Nodes**:
  - Đăng ký tài khoản **Supabase** và lấy **API URL** và **Service Role Key**.
  - Cấu hình **Search Clients**, **GET Supabase User**, **Update Sent**, **Created Supabase Wallet**, và các node liên quan.
  - Tạo bảng **users** và **wallets** để lưu trữ thông tin người dùng và danh mục cổ phiếu.
- **PostgreSQL Nodes**:
  - Nếu sử dụng PostgreSQL, cấu hình **Host**, **Port**, **Database**, **User**, và **Password**.
  - Cấu hình **Postgres Chat Memory** để lưu trữ lịch sử phân tích.

##### **D. Cấu Hình PDF Generator**
- **PDFco API Node**:
  - Điền **PDFco API Key** vào node **"PDF Generator"** và **"PDF Generator1"**.
  - Cấu hình **Template HTML** (sử dụng node **"HTML"** và **"HTML1"** để định dạng báo cáo).
  - Đảm bảo **HTML Report Generator** và **HTML FORMATTER AGENT** tạo ra nội dung PDF chính xác.

##### **E. Cấu Hình Schedule Trigger**
- **Schedule Trigger Node**:
  - Cấu hình **Lịch trình** (ví dụ: chạy hàng ngày lúc 9h sáng) để tự động phân tích và gửi báo cáo.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn **Test Run** với dữ liệu mẫu (ví dụ: danh sách cổ phiếu AAPL, MSFT).
   - Kiểm tra các node quan trọng như **Perplexity**, **OpenAI**, **PDF Generator**, và **Telegram**.
2. **Active Workflow**:
   - Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack**:
   - Thêm node **Slack** để gửi báo cáo đến nhóm làm việc.
2. **Lưu Log**:
   - Sử dụng node **StickyNote** để lưu trữ log phân tích cho việc theo dõi sau này.
3. **Báo Cáo Định Kỳ**:
   - Cấu hình **Schedule Trigger** để gửi báo cáo hàng tuần hoặc hàng tháng.
4. **Tối Ưu Hóa Prompt**:
   - Cập nhật **Prompt** trong các node AI để phân tích sâu hơn (ví dụ: phân tích rủi ro, cơ hội đầu tư).

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các nhà đầu tư chứng khoán muốn tự động hóa phân tích cổ phiếu Mỹ, tạo báo cáo PDF và nhận thông báo qua Telegram **không cần code**. Với sự hỗ trợ của **AI (Perplexity + OpenAI)**, các sếp có thể **tiết kiệm thời gian**, **tối ưu hóa quyết định đầu tư** và **nhận báo cáo chuyên nghiệp** hàng ngày.

**Hãy áp dụng ngay và bắt đầu tự động hóa đầu tư của mình!** 🚀