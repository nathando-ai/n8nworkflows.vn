---
title: "🌐 Tự Động Scrape Dữ Liệu Doanh Nghiệp Từ Google Maps Và Xuất Ra Excel/Sheets - Không Cần Code!"
description: "Workflow này tự động scrape thông tin doanh nghiệp từ Google Maps qua SerpAPI, xử lý dữ liệu và xuất ra Google Sheets/Excel, giúp các sếp tiết kiệm thời gian và tối ưu hóa quy trình lead generation."
slug: "tieu-dong-scrape-google-maps-va-xuat-ra-excel-sheets"
tags: [n8n, automation, lead-generation, serpapi, google-sheets, excel, no-code]
keywords: [n8n workflow scrape google maps, tự động hóa scrape dữ liệu doanh nghiệp, export google maps data to excel, lead generation automation, serpapi n8n]
---

# 🚀 **Tự Động Scrape Dữ Liệu Doanh Nghiệp Từ Google Maps & Xuất Ra Excel/Sheets**

### **Giải pháp hoàn hảo cho các sếp muốn tự động hóa việc thu thập thông tin doanh nghiệp từ Google Maps mà không cần viết một dòng code nào!**

---

### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần scrape thủ công hàng trăm doanh nghiệp.
- **Dữ liệu chính xác**: Lấy thông tin từ Google Maps chính thức qua SerpAPI.
- **Xuất ra nhiều định dạng**: Dữ liệu được xuất ra **Google Sheets** (để theo dõi trực tiếp) và **Excel** (để phân tích sâu).
- **Hoạt động 24/7**: Workflow chạy tự động khi có yêu cầu (ví dụ: qua Slack, Telegram hoặc chatbot).
- **Tối ưu lead generation**: Dữ liệu sẵn sàng để phân tích, marketing hoặc CRM.
:::

---

### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản SerpAPI** (để scrape Google Maps):
   - [Đăng ký SerpAPI miễn phí](https://serpapi.com/) (có phiên bản free với giới hạn request).
   - Lưu **API Key** của SerpAPI vào n8n (cấu hình ở node `Extract SerpAPI Map`).
2. **Tài khoản Google Cloud Platform (GCP)** (để kết nối với Google Sheets):
   - [Cài đặt OAuth 2.0 Client ID](https://developers.google.com/sheets/api/quickstart/python) và lưu **Client Email** và **Private Key** vào n8n.
3. **Google Sheet đã tạo sẵn** (để lưu dữ liệu):
   - Chọn **Sheet Name** trong node `Upsert Data in Sheets`.
4. **(Tùy chọn)**: Nếu muốn kích hoạt qua chatbot (Slack/Telegram), cần:
   - **API Key của LangChain** (nếu sử dụng node `chatTrigger`).
   - **Credentials của Slack/Telegram** (để nhận yêu cầu scrape).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/7541) hoặc copy toàn bộ JSON từ trang này.
- Vào **n8n Editor** → **Import Workflow** → Dán JSON và nhấn **Import**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này có **9 node chính**, nhưng các sếp chỉ cần chú ý đến **5 node quan trọng** sau:

##### **A. Node `Extract SerpAPI Map` (SerpAPI)**
- **Cấu hình**:
  - **API Key**: Điền **API Key** từ SerpAPI (đã đăng ký trước).
  - **Location**: Nhập **tên địa điểm** (ví dụ: "Cà Mau") hoặc **tọa độ** (ví dụ: `10.3536° N, 105.7146° E`).
  - **Query**: Nhập **từ khóa** (ví dụ: "cửa hàng điện thoại").
  - **Limit**: Đặt số lượng kết quả scrape (ví dụ: `20`).
- **Lưu ý**:
  - SerpAPI có **giới hạn free** (500 request/tháng). Nếu cần scrape nhiều, nâng cấp plan.
  - Nếu scrape nhiều địa điểm, có thể **loop qua node `Set`** để thay đổi `Location` và `Query`.

##### **B. Node `Upsert Data in Sheets` (Google Sheets)**
- **Cấu hình**:
  - **Credentials**: Chọn **OAuth 2.0 Client ID** đã cấu hình trước.
  - **Spreadsheet ID**: Tìm trong URL của Google Sheet (ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
  - **Sheet Name**: Chọn **tên tab** trong Google Sheet (ví dụ: `Doanh Nghiệp`).
  - **Range**: Đặt `A1` (nếu muốn ghi từ ô A1).
- **Lưu ý**:
  - Nếu Sheet chưa có header, **node này sẽ tự động tạo** (cột `Name`, `Address`, `Phone`, `Rating`, `Review`, ...).
  - Nếu muốn **xóa dữ liệu cũ trước khi ghi**, thêm node `deleteRows` từ **Google Sheets**.

##### **C. Node `Get Data in XLSX` (ConvertToFile)**
- **Cấu hình**:
  - **File Format**: Chọn `Excel (XLSX)`.
  - **File Name**: Đặt tên file (ví dụ: `DoanhNghiep_CaMau_$(DateTime.Now)`).
- **Lưu ý**:
  - File Excel sẽ được **tải xuống tự động** khi workflow chạy.
  - Nếu muốn **gửi file qua Email/Slack**, thêm node `Email` hoặc `Slack Webhook`.

##### **D. Node `When chat message received` (LangChain ChatTrigger)**
- **(Tùy chọn)**: Nếu muốn kích hoạt scrape qua **chatbot** (Slack/Telegram):
  - **Cấu hình**:
    - **API Key**: Điền **API Key của LangChain**.
    - **Prompt**: Cấu hình câu lệnh (ví dụ: `Scrape doanh nghiệp ở [tên địa điểm]`).
  - **Lưu ý**:
    - Node này **không bắt buộc** nếu các sếp muốn chạy workflow **tự động định kỳ** (sử dụng **n8n Cron Trigger**).

##### **E. Node `Set` (Prepare Data & Extract Data)**
- **Cấu hình**:
  - **Prepare Data**: Đặt `jsonPath("$.organic_results[*].name")` (lấy tên doanh nghiệp).
  - **Extract Data**: Đặt `jsonPath("$.organic_results[*].snippet_local")` (lấy địa chỉ).
  - **Lưu ý**:
    - Các sếp có thể **thêm/bỏ cột** tùy ý bằng cách chỉnh `jsonPath` (xem [tài liệu n8n về JSONPath](https://docs.n8n.io/code-examples/working-with-data/working-with-json/)).

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Chạy **manual test** với dữ liệu mẫu (ví dụ: scrape "cửa hàng điện thoại" ở "Cà Mau").
  - Kiểm tra **Google Sheet** và **file Excel** có xuất dữ liệu không.
- **Bật Active**:
  - Sau khi test thành công, **bật workflow** và **lưu lại**.

---

### **✍️ Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÂNG CAO]
1. **Scrape nhiều địa điểm cùng lúc**:
   - Sử dụng **node `Set`** để loop qua danh sách địa điểm (ví dụ: `["Hà Nội", "TP.HCM", "Đà Nẵng"]`).
   - Thêm **node `Loop`** (n8n-nodes-base.loop) để chạy scrape cho từng địa điểm.

2. **Gửi báo cáo định kỳ qua Email**:
   - Thêm **node `Email`** (n8n-nodes-base.email) để gửi file Excel cho team hàng tuần.
   - Sử dụng **node `Cron`** (n8n-nodes-base.cron) để chạy workflow tự động vào mỗi thứ 7.

3. **Lưu log scrape vào Google Drive**:
   - Thêm **node `Google Drive`** (n8n-nodes-base.googleDrive) để lưu file Excel vào Drive.
   - Cấu hình **credentials** và **folder ID** tương tự như Google Sheets.

4. **Lọc dữ liệu theo rating**:
   - Sử dụng **node `Function`** (n8n-nodes-base.function) để lọc chỉ doanh nghiệp có `Rating >= 4`.
   - Ví dụ:
     ```javascript
     return $input.all().filter(item => item.rating >= 4);
     ```

5. **Kết hợp với AI để phân tích**:
   - Sử dụng **node `LangChain`** để phân tích review của doanh nghiệp (ví dụ: tìm từ khóa tích cực/tiêu cực).
   - Ví dụ prompt:
     ```
     Analyze the following Google Maps reviews and summarize the sentiment:
     [List of reviews]
     ```
:::

---

### **📌 Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✅ **Tự động scrape dữ liệu doanh nghiệp** từ Google Maps **không cần code**.
✅ **Xuất dữ liệu ra Google Sheets** (để theo dõi) và **Excel** (để phân tích).
✅ **Kích hoạt scrape qua chatbot** (Slack/Telegram) hoặc **tự động định kỳ**.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với dữ liệu mẫu** và kiểm tra kết quả.
3. **Bật workflow** và **tích hợp vào quy trình lead generation** của doanh nghiệp!

---
**💡 Cần hỗ trợ thêm?**
- Trả lời câu hỏi trong [community n8n](https://community.n8n.io/).
- Liên hệ **Andrew (tác giả)** qua [GitHub](https://github.com/AndrewN8N) để cải tiến workflow.

**🚀 Hãy tự động hóa ngay hôm nay!** 🚀