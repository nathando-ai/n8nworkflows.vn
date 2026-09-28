---
title: "🚀 Tự Động Hóa Email Tin Tức Tuần Kể AI: RSS + Vector DB + GPT-4o (Không Cần Code)"
description: "Workflow tự động hóa gửi email tổng hợp tin tức hàng tuần theo chủ đề yêu thích, sử dụng AI GPT-4o để phân tích và tổng hợp tin tức từ RSS feeds, lưu trữ trong Vector DB, và gửi email cá nhân hóa hàng tuần - tiết kiệm thời gian lên tới 20h/tháng cho các sếp."
slug: "tieu-dong-hoa-email-tin-tuc-tuan-ke-ai-rss-vector-db-gpt-4o"
tags: [n8n, automation, ai-rag, email-marketing, vector-database, gpt-4o, rss-feed]
keywords: [n8n workflow tự động hóa email tin tức, AI tổng hợp tin tức hàng tuần, vector database n8n, GPT-4o tự động hóa, RSS feed + AI, tự động hóa email cá nhân hóa]
---

# 🚀 **Tự Động Hóa Email Tin Tức Tuần Kể AI: RSS + Vector DB + GPT-4o**

### **Giải pháp cho các sếp bị "ngập" trong luồng tin tức không cần thiết**
Hàng ngày, các sếp phải mất **30-60 phút** để tìm kiếm, lọc và tổng hợp tin tức từ nhiều nguồn khác nhau (TechCrunch, Bloomberg, Reuters,...) chỉ để gửi cho đồng nghiệp hoặc bản thân. Kết quả? **Thời gian quý giá bị "chôn vùi" trong công việc thủ công**, trong khi tin tức quan trọng lại bị bỏ qua do không thể theo dõi kịp thời.

**Workflow này tự động hóa toàn bộ quy trình:**
✅ **Tự động thu thập** tin tức từ RSS feeds hàng ngày
✅ **Lưu trữ thông minh** trong Vector Database (OpenAI Embeddings) để tìm kiếm nhanh
✅ **Tổng hợp AI** bằng GPT-4o, lọc tin tức theo chủ đề và số lượng yêu cầu
✅ **Gửi email tự động** hàng tuần với nội dung cá nhân hóa, sạch sẽ và chuyên nghiệp
✅ **Tiết kiệm thời gian** lên tới **20h/tháng** cho các sếp

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thủ công lọc tin tức hàng ngày (giảm 30-60 phút/ngày).
- **Tin tức chính xác và cá nhân hóa**: AI tự động lọc tin tức theo chủ đề và số lượng yêu cầu.
- **Hệ thống thông minh**: Vector DB cho phép tìm kiếm nhanh và cập nhật liên tục.
- **Email chuyên nghiệp**: Nội dung được chuyển đổi từ Markdown sang email-friendly tự động.
- **Hoạt động liên tục**: Khả năng chạy 24/7 trên VPS, không phụ thuộc vào máy tính cá nhân.
- **Mở rộng dễ dàng**: Thêm/loại bỏ RSS feeds hoặc chủ đề theo nhu cầu.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI**:
   - API Key cho **Embeddings OpenAI** và **Chat Model (GPT-4o)**.
   - [Tạo API Key tại đây](https://platform.openai.com/account/api-keys).
2. **Tài khoản Gmail**:
   - OAuth 2.0 credentials cho gửi email tự động.
   - [Cài đặt OAuth 2.0 tại đây](https://developers.google.com/gmail/api/quickstart/nodejs).
3. **RSS Feeds**:
   - Danh sách URL RSS feeds của các nguồn tin tức muốn theo dõi (ví dụ: TechCrunch, Bloomberg, Reuters,...).
4. **Thông tin cá nhân hóa**:
   - Email nhận tin tức (được cấu hình trong node **Send Newsletter**).
   - Chủ đề quan tâm (ví dụ: "Tech", "Finance", "Startup").

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/11951](https://n8n.io/workflows/11951) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/11951) và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **17 node** với các bước chính sau. Dưới đây là hướng dẫn chi tiết:

##### **A. Cấu hình RSS Feeds (Thu thập tin tức hàng ngày)**
1. **Node "Set Tech News RSS Feeds"**:
   - **Thao tác**: Chỉnh sửa giá trị trong `json` để thêm URL RSS feeds.
   - **Ví dụ**:
     ```json
     {
       "json": {
         "feeds": [
           "https://techcrunch.com/feed/",
           "https://www.bloomberg.com/rss/technology",
           "https://www.reuters.com/rss/topnews"
         ]
       }
     }
     ```
   - **Lưu ý**: Thêm/loại bỏ URL theo nhu cầu.

2. **Node "Read RSS News Feeds"**:
   - **Không cần chỉnh**: Node này tự động đọc RSS feeds từ danh sách trên.

##### **B. Cấu hình Vector Database (Lưu trữ tin tức)**
1. **Node "Embeddings OpenAI"**:
   - **Không cần chỉnh**: Sử dụng API Key đã cấu hình trong `openAiApi` (đã được setup trong n8n).

2. **Node "Store News Articles"**:
   - **Không cần chỉnh**: Lưu tin tức vào Vector Store với embeddings OpenAI.

##### **C. Cấu hình AI Agent (Tổng hợp tin tức)**
1. **Node "OpenAI Chat Model"**:
   - **Model**: Đã cấu hình sẵn là **GPT-4o** (không cần chỉnh).
   - **API Key**: Đã sử dụng `openAiApi` (cần đảm bảo đã setup trong n8n).

2. **Node "News reader AI" (Agent)**:
   - **Prompt mặc định**: AI sẽ tự động tổng hợp tin tức theo chủ đề và số lượng yêu cầu.
   - **Lưu ý**: Nếu muốn thay đổi logic, chỉnh sửa trong **Sticky Note** hoặc **Set** node liên quan.

##### **D. Cấu hình Email (Gửi hàng tuần)**
1. **Node "Send Newsletter"**:
   - **Credentials**: Chọn `gmailOAuth2` (cần đã setup trong n8n).
   - **Email nhận**: Điền địa chỉ email muốn nhận tin tức (ví dụ: `sếp@example.com`).

2. **Node "Convert Response to an Email-Friendly Format"**:
   - **Không cần chỉnh**: Node này tự động chuyển đổi nội dung từ Markdown sang email-friendly.

##### **E. Cấu hình Lịch trình (Daily & Weekly)**
1. **Node "Get Articles Daily"**:
   - **Schedule**: Mặc định là **hàng ngày** (không cần chỉnh).
   - **Lưu ý**: Nếu muốn thay đổi, chỉnh sửa trong **Schedule Trigger**.

2. **Node "Send Weekly Summary"**:
   - **Schedule**: Mặc định là **hàng tuần** (ví dụ: Chủ Nhật 8h sáng).
   - **Lưu ý**: Thay đổi ngày giờ theo nhu cầu.

##### **F. Cấu hình Chủ đề quan tâm**
1. **Node "Your topics of interest"**:
   - **Thao tác**: Chỉnh sửa giá trị trong `json` để thêm chủ đề muốn theo dõi.
   - **Ví dụ**:
     ```json
     {
       "json": {
         "topics": ["Tech", "Startup", "Finance"],
         "numberOfArticles": 5
       }
     }
     ```
   - **Lưu ý**: Thay đổi số lượng tin tức (`numberOfArticles`) theo yêu cầu.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chạy **manual** để kiểm tra workflow với dữ liệu mẫu.
   - Kiểm tra email đã nhận được tin tức chưa.

2. **Bật Active**:
   - Sau khi test thành công, bật **Active** cho cả hai schedule:
     - `Get Articles Daily`
     - `Send Weekly Summary`

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Slack/Telegram Notifications**:
   - Kết nối với **Slack** hoặc **Telegram** để thông báo khi email được gửi thành công.
   - Sử dụng node **Slack** hoặc **Telegram Bot** sau node **Send Newsletter**.

2. **Lưu Log cho Debugging**:
   - Thêm node **Sticky Note** hoặc **Set** để lưu log tin tức đã xử lý.
   - Có thể kết nối với **Google Sheets** để theo dõi lịch sử.

3. **Tùy chỉnh Email Format**:
   - Chỉnh sửa **Markdown template** trong node **"Convert Response to an Email-Friendly Format"** để thay đổi bố cục email.

4. **Mở rộng với API khác**:
   - Thêm RSS feeds từ **NewsAPI**, **Google News RSS**, hoặc **Feedly** bằng cách kết nối với node **HTTP Request**.

5. **Báo cáo định kỳ**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu trữ tin tức theo tháng và tạo báo cáo.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc thủ công lọc tin tức hàng ngày, đồng thời **cung cấp tin tức cá nhân hóa** dựa trên sở thích và nhu cầu thực tế. Với **Vector DB + GPT-4o**, hệ thống không chỉ nhanh chóng mà còn thông minh, tự động cập nhật và tổng hợp tin tức một cách hiệu quả.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn trên.
2. **Bật Active** để bắt đầu nhận email tin tức hàng tuần.
3. **Tùy chỉnh** RSS feeds và chủ đề theo nhu cầu cá nhân.

**🚀 Còn chần chừ gì nữa? Hãy tự động hóa ngay và dành thời gian cho những việc quan trọng hơn!**