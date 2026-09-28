---
title: "🚀 Tự Động Hoá Nghiên Cứu Doanh Nghiệp & Tăng Cường Dữ Liệu Lead với GPT-4o và Google Sheets"
description: "Workflow tự động hóa hoàn toàn không cần code giúp các sếp tự động tra cứu thông tin chi tiết về doanh nghiệp từ tên công ty, bao gồm domain, LinkedIn, định hướng thị trường, giá cả, tích hợp API và nhiều thông tin quý giá khác. Giúp tiết kiệm thời gian lên đến 90% so với cách làm thủ công."
slug: "tự-dộng-hoá-nghiên-cứu-doanh-nghiệp-gpt-4o-google-sheets"
tags: [n8n, automation, lead-generation, ai-chatbot, google-sheets, openai, serpapi]
keywords: [n8n workflow tự động hóa, nghiên cứu doanh nghiệp, tăng cường dữ liệu lead, GPT-4o, Google Sheets tự động, tự động hóa không code]
---

# 🚀 **Tự Động Hoá Nghiên Cứu Doanh Nghiệp & Tăng Cường Dữ Liệu Lead với GPT-4o và Google Sheets**

Hãy tưởng tượng một tình huống: Các sếp phải tra cứu thông tin về hàng trăm doanh nghiệp để xây dựng danh sách lead chất lượng, nhưng phải mất hàng giờ để tìm kiếm domain, LinkedIn, định hướng thị trường (B2B/B2C), thông tin giá cả, hoặc các tính năng tích hợp. **Công việc này không chỉ tốn thời gian mà còn dễ mắc sai sót** khi phải copy-paste thông tin từ nhiều trang web khác nhau.

Workflow này **giải quyết hoàn toàn vấn đề đó** bằng cách sử dụng **AI Agent (GPT-4o) kết hợp với công cụ tìm kiếm Google** để tự động tra cứu và tổng hợp thông tin chi tiết về doanh nghiệp từ **chỉ một tên công ty**. Kết quả sẽ được lưu vào **Google Sheets** với định dạng sẵn sàng sử dụng cho marketing, sales hoặc phân tích thị trường.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 mà không gặp lỗi, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) để đảm bảo tính ổn định và bảo mật cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 90%** so với cách làm thủ công (không cần copy-paste từ nhiều trang web).
- **Dữ liệu chính xác và toàn diện**: AI tự động tra cứu domain, LinkedIn, định hướng thị trường, giá cả, tích hợp API, và nhiều thông tin khác.
- **Hoạt động liên tục**: Cấu hình chạy tự động hàng ngày hoặc theo lịch trình (Schedule Trigger).
- **Cá nhân hóa và mở rộng**: Thay đổi prompt AI để tra cứu thông tin khác (ví dụ: tìm kiếm case study mới nhất).
- **Tích hợp với Google Sheets**: Dữ liệu tự động cập nhật vào bảng tính, sẵn sàng export hoặc phân tích.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối với Google Sheets).
2. **API Key OpenAI** (để sử dụng GPT-4o).
3. **API Key SerpAPI hoặc ScrapingBee** (để tìm kiếm Google tự động).
4. **Bảng Google Sheets** (sử dụng template đã cung cấp).

---
:::info[CHUẨN BỊ]
- **OpenAI API Key**: [Đăng ký miễn phí tại OpenAI](https://platform.openai.com/account/api-keys).
- **SerpAPI API Key** (gợi ý): [Đăng ký tại SerpAPI](https://serpapi.com/) (miễn phí 5000 request/tháng).
- **ScrapingBee API Key** (lựa chọn rẻ hơn): [Đăng ký tại ScrapingBee](https://www.scrapingbee.com/) (miễn phí 1000 request/tháng).
- **Google Sheets**: [Tải template mẫu](https://docs.google.com/spreadsheets/d/1_F_An3yLSCsjgLN5w9RcJN-lJj_6mUT1nngMJPYws2Y/edit?usp=sharing) và sao chép vào Google Drive cá nhân.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/6776) (nút "Export Workflow").
- Mở **n8n Editor** → Nhấn **"Import"** → Chọn file JSON vừa tải.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần cấu hình các node quan trọng như sau:

##### **A. Cấu hình Google Sheets**
1. **Node "Get rows to enrich"**:
   - Chọn **credentials**: `googleSheetsOAuth2Api`.
   - Chọn **Google Sheet** đã sao chép từ template.
   - Chọn **Sheet Name**: `Sheet1` (hoặc tên sheet đã đặt).
   - Chọn **Range**: `A2:B` (cột `input` chứa tên công ty).

2. **Node "Google Sheets - Update Row with data"**:
   - Chọn cùng **credentials** và **Google Sheet** như trên.
   - Chọn **operation**: `update`.
   - Cấu hình **range**: `A2:Z` (để cập nhật toàn bộ dữ liệu tra cứu).

##### **B. Cấu hình OpenAI (GPT-4o)**
- **Node "OpenAI Chat Model"**:
  - Chọn **credentials**: `openAiApi`.
  - Đảm bảo **model** được đặt là `gpt-4o`.
  - **Prompt mặc định** đã được tối ưu để tra cứu thông tin doanh nghiệp. Các sếp có thể **tùy chỉnh** ở node **"AI company researcher"** (xem phần nâng cao).

##### **C. Cấu hình SerpAPI / ScrapingBee**
- **Node "SerpAPI - Search Google"**:
  - Chọn **credentials**: `serpApi`.
  - Điền **API Key** đã đăng ký từ SerpAPI.

- **Node "Search Google with ScrapingBee"**:
  - Chọn **credentials**: `scrapingBeeApi` (nếu sử dụng ScrapingBee).
  - Điền **API Key** từ ScrapingBee.
  - **Lưu ý**: Nếu chọn ScrapingBee, cần **điều hướng node này đến "AI company researcher"** thay vì SerpAPI.

##### **D. Cấu hình AI Agent**
- **Node "AI company researcher"**:
  - Đây là **cốt lõi** của workflow. AI sẽ sử dụng **prompt** để tra cứu thông tin.
  - Các sếp có thể **tùy chỉnh prompt** để tra cứu thông tin khác (ví dụ: tìm kiếm "case study mới nhất" thay vì "giá cả").
  - **Structured Output Parser**: Đảm bảo **JSON schema** phù hợp với dữ liệu tra cứu (ví dụ: `{ "domain": "string", "linkedin": "string", "marketFocus": "string", ... }`).

##### **E. Cấu hình Schedule Trigger (nếu muốn chạy tự động)**
- **Node "Schedule Trigger"**:
  - Chọn **cron expression** phù hợp (ví dụ: `0 0 * * *` để chạy hàng ngày lúc 00:00).

#### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Nhập **tên công ty** vào cột `input` của Google Sheets.
   - Chọn **node "Manual Trigger"** → Nhấn **"Execute"** để test.
   - Kiểm tra **Google Sheets** để xem dữ liệu đã được cập nhật chưa.

2. **Bật Active workflow**:
   - Nhấn **"Active"** ở góc trên bên phải của n8n Editor.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh prompt AI để tra cứu thông tin khác**:
   - Ví dụ: Thay vì tra cứu "giá cả", các sếp có thể yêu cầu AI tra cứu **"tính năng mới nhất"**, **"đối tác tích hợp"**, hoặc **"lịch sử phát triển"**.
   - **Cách làm**: Mở node **"AI company researcher"** → Chỉnh sửa **prompt** trong phần `tools` hoặc `input`.

2. **Lưu log hoạt động**:
   - Sử dụng **node "Sticky Note"** để ghi chú hoặc lưu log mỗi khi workflow chạy.
   - Ví dụ: Ghi ngày giờ tra cứu và tên công ty đã xử lý.

3. **Gửi báo cáo định kỳ qua Email/Slack**:
   - Kết hợp với **node "Email"** hoặc **"Slack"** để gửi báo cáo tổng hợp hàng tuần.
   - Ví dụ: "Workflow đã tra cứu 50 công ty mới, kết quả chi tiết ở đây: [link Google Sheets]".

4. **Kết hợp với CRM (HubSpot, Salesforce)**:
   - Sử dụng **node "HTTP Request"** để đẩy dữ liệu lead đã enrich vào CRM tự động.

5. **Optimize chi phí**:
   - Nếu budget hạn chế, **chỉ sử dụng ScrapingBee** thay vì SerpAPI (rẻ hơn).
   - **Limit số lượng request** trong ngày để tránh vượt quá free tier.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc tra cứu lead thủ công, đồng thời **cung cấp dữ liệu chính xác và chi tiết** để hỗ trợ quyết định marketing và sales. **Chỉ cần nhập tên công ty vào Google Sheets, AI sẽ tự động làm tất cả!**

🚀 **Hành động ngay**:
1. **Sao chép Google Sheet template** và cấu hình API.
2. **Import workflow** và điều chỉnh các node quan trọng.
3. **Chạy test** với 1-2 công ty mẫu.
4. **Bật Schedule Trigger** để tự động hóa hàng ngày.

**Nếu có thắc mắc**, các sếp có thể tham khảo [hướng dẫn chi tiết của tác giả](https://n8n.io/workflows/6776) hoặc liên hệ cộng đồng n8n tại [Discord](https://discord.gg/n8n). **Hãy bắt đầu tự động hóa ngay hôm nay!** 💪