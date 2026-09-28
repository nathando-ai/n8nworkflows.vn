---
title: "🚀 Tự Động Hóa Scrape & Phân Tích Quảng Cáo Google Ads Với AI – Báo Cáo Email Tự Động (Bright Data + LangChain)"
description: "Workflow này tự động scrape top ads từ Google Search Results, phân tích giá trị truyền thông và site links bằng AI, sau đó tổng hợp báo cáo chi tiết gửi qua email – tiết kiệm 10+ giờ công/tháng cho đội marketing."
slug: "tieu-dong-hoa-scrape-phan-tich-google-ads-ai-email"
tags: [n8n, automation, market-research, ai-summarization, google-ads, bright-data, langchain, gmail]
keywords: [n8n workflow google ads, tự động hóa phân tích quảng cáo google, scrape top ads google, báo cáo marketing tự động, ai phân tích quảng cáo, langchain n8n]
---

# 🚀 **Tự Động Hóa Scrape & Phân Tích Quảng Cáo Google Ads Với AI – Báo Cáo Email Tự Động**

### **🔍 Nỗi Đau Của Các Sếp Marketing**
Làm thủ công phân tích quảng cáo Google Ads của đối thủ là một công việc **mệt mỏi, tốn thời gian và dễ sai sót**:
- **Scrape top ads** từ hàng chục keyword mỗi ngày?
- **Phân tích giá trị truyền thông** của từng quảng cáo thủ công?
- **Tổng hợp báo cáo** và gửi cho team?
- **Cần 10+ giờ công/tháng** chỉ để cập nhật thông tin cơ bản!

Workflow này **giải quyết tất cả** bằng cách tự động hóa **100% quy trình** từ scrape đến phân tích AI và gửi báo cáo email.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10+ giờ/tháng** – Không cần scrape thủ công.
✅ **Phân tích AI chính xác** – Trích xuất giá trị truyền thông, site links, và keyword mapping.
✅ **Báo cáo tự động** – Email chi tiết gửi hàng ngày/tuần.
✅ **Cập nhật liên tục** – Workflow hoạt động 24/7, không cần can thiệp.
✅ **Dễ mở rộng** – Thêm keyword mới chỉ cần cập nhật Google Sheet.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Bright Data** (để scrape Google Search Results):
   - Tạo **1 zone SERP API** (hướng dẫn chi tiết trong phần **Cách cấu hình**).
   - Lưu **API Key** của Bright Data.
2. **Google Sheet mẫu** (để lưu keyword và cấu hình):
   - [Lấy bản sao Google Sheet](https://docs.google.com/spreadsheets/d/1QU9rwawCZLiYW8nlYYRMj-9OvAUNZoe2gP49KbozQqw/edit?usp=sharing).
   - Cập nhật **keyword** và **mã quốc gia** (country code) cho từng zone Bright Data.
3. **Tài khoản Gmail** (để gửi báo cáo):
   - Cấu hình **OAuth2** trong n8n (hướng dẫn trong phần **Cách cấu hình**).
4. **API Key cho OpenRouter & Google Gemini** (để phân tích AI):
   - [Đăng ký OpenRouter](https://openrouter.ai/) (miễn phí).
   - [Đăng ký Google Vertex AI (Gemini)](https://ai.google.dev/) (miễn phí 1 triệu token/tháng).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/6256](https://n8n.io/workflows/6256).
- **Import vào n8n Editor**:
  - Trên trang **Workflows**, nhấn **Import** → Chọn file JSON.
  - Hoặc **copy/paste** JSON vào **Import Workflow** (tab bên phải).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow có **36 node**, nhưng các bước quan trọng nhất cần chú ý:

##### **A. Cấu Hình Bright Data (Scrape Google Ads)**
1. **Node `Fetch Google Search Results JSON`**:
   - **Credentials**: Chọn `httpHeaderAuth` (đã cấu hình sẵn trong workflow).
   - **URL**: Điền vào `Request URL`:
     ```
     https://api.brightdata.com/serp/v1/search
     ```
   - **Headers**:
     - `Authorization`: `Bearer {API_KEY_BRIGHT_DATA}`
     - `Content-Type`: `application/json`
   - **Body (JSON)**:
     ```json
     {
       "search": "$$.json["search"]",
       "country": "$$.json["country"]",
       "language": "en",
       "device": "desktop"
     }
     ```
   - **Lưu ý**:
     - `$$.json["search"]` và `$$.json["country"]` sẽ được lấy từ **Google Sheet** (node `Get Keywords`).

2. **Node `Get Keywords` (Google Sheets)**:
   - **Credentials**: Chọn `googleSheetsOAuth2Api` (cấu hình OAuth2 từ Google Cloud).
   - **Sheet Name**: Điền tên sheet trong Google Sheet mẫu (ví dụ: `Sheet1`).
   - **Range**: Điền `A2:B` (cột keyword và country code).

##### **B. Cấu Hình AI (Phân Tích Quảng Cáo)**
Workflow sử dụng **2 mô hình AI**:
1. **OpenRouter (Chat Model)**:
   - **Node `OpenRouter Chat Model`** và các biến thể (`OpenRouter Chat Model1`, `OpenRouter Chat Model2`, `OpenRouter Chat Model3`).
   - **Credentials**: Chọn `openRouterApi` (đã cấu hình API Key).
   - **Prompt**: Workflow đã định sẵn, nhưng các sếp có thể **cập nhật** trong node `chainLlm` (ví dụ: `Value Proposition & Messaging Analysis`).

2. **Google Gemini (Chat Model)**:
   - **Node `Google Gemini Chat Model`** và các biến thể.
   - **Credentials**: Chọn `googlePalmApi` (cấu hình API Key từ Google Vertex AI).
   - **Prompt**: Tương tự OpenRouter, nhưng sử dụng mô hình Gemini.

##### **C. Cấu Hình Gmail (Gửi Báo Cáo)**
1. **Node `Send a message`**:
   - **Credentials**: Chọn `gmailOAuth2` (cấu hình OAuth2 từ Google Cloud).
   - **To**: Điền email nhận báo cáo (ví dụ: `marketing@doanhnghiep.com`).
   - **Subject**: Điền tiêu đề email (ví dụ: `Báo cáo Top Ads Google Ads - {DATE}`).
   - **Body**: Workflow tự động generate HTML từ node `Generate HTML`.

##### **D. Các Node Quan Trọng Khác**
- **Node `filter ads`**: Lọc kết quả scrape để chỉ giữ top ads.
- **Node `extract ads` (Code)**: Trích xuất dữ liệu từ JSON Bright Data.
- **Node `Generate HTML` (Agent)**: Tạo báo cáo HTML từ kết quả phân tích AI.

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Execute Workflow** (node `manualTrigger`).
   - Kiểm tra **log** để đảm bảo:
     - Bright Data scrape thành công.
     - AI phân tích đúng dữ liệu.
     - Email gửi đi đúng.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động hóa hàng tuần**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow vào mỗi thứ 2 sáng 8h.
2. **Lưu log vào Google Sheets**:
   - Thêm node `googleSheets` sau `Send a message` để lưu lịch sử báo cáo.
3. **Kết hợp với Slack/Telegram**:
   - Thêm node `webhook` để gửi thông báo khi workflow hoàn thành.
4. **Cập nhật keyword tự động**:
   - Sử dụng **Google Sheets API** để tự động thêm keyword mới từ một sheet khác.
5. **Phân tích cạnh tranh sâu hơn**:
   - Thêm node `chainLlm` để AI so sánh giá trị truyền thông giữa các đối thủ.

---

### 📌 **Kết Luận**
Workflow này **giải phóng đội marketing** khỏi công việc scrape và phân tích thủ công, đồng thời cung cấp **báo cáo AI chi tiết** hàng ngày. Các sếp chỉ cần:
1. **Cấu hình Bright Data & Google Sheet** (1 lần).
2. **Chạy workflow** và **quên đi** – nó sẽ tự động hoạt động.

**🚀 Hãy áp dụng ngay và tiết kiệm 10+ giờ/tháng!**
Nếu có vấn đề, hãy comment bên dưới hoặc liên hệ với **Zacharia Kimotho** (tác giả workflow) qua [n8n Community](https://community.n8n.io/).

---
**💡 Lưu ý cuối cùng**:
- **Bright Data có giới hạn scrape** – đảm bảo tài khoản đủ capacity.
- **API OpenRouter/Gemini có hạn mức** – theo dõi sử dụng để tránh bị cut.
- **Google Sheets không quá 1000 hàng** – nếu nhiều keyword, chia sheet thành nhiều tab.