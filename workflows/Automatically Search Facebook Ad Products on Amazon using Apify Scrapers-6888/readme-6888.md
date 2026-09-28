---
title: "🚀 Tự Động Tìm Kiếm Sản Phẩm Quảng Cáo Facebook Trên Amazon Với Apify Scraper - Giải Pháp Market Research 100% Không Code"
description: "Workflow tự động hóa tìm kiếm sản phẩm từ quảng cáo Facebook (Ad Library) và so sánh trên Amazon, giúp các sếp tiết kiệm thời gian nghiên cứu thị trường, phát hiện cơ hội dropshipping/FBA mới chỉ trong vài giây. Hoạt động 24/7, không cần code."
slug: "tu-dong-tim-kiem-san-pham-facebook-amazon-apify"
tags: [n8n, automation, market-research, apify, dropshipping, amazon-fba, no-code]
keywords: [n8n workflow market research, tự động hóa tìm kiếm sản phẩm amazon, apify scraper facebook amazon, dropshipping tự động, nghiên cứu thị trường amazon]
---

# 🚀 **Tự Động Tìm Kiếm Sản Phẩm Quảng Cáo Facebook Trên Amazon - Giải Pháp Market Research Siêu Tốc**

### **Nỗi Đau Của Các Sếp Trong Nghiên Cứu Thị Trường**
Các sếp dropshipping, Amazon FBA hoặc kinh doanh online thường phải mất **giờ đồng hồ** để:
- **Tìm kiếm** sản phẩm đang quảng cáo hiệu quả trên Facebook Ads Library.
- **So sánh** sản phẩm đó trên Amazon để đánh giá cạnh tranh, giá cả, và tiềm năng bán hàng.
- **Lặp lại** quá trình này cho hàng trăm sản phẩm, dẫn đến **sai sót**, **thời gian chậm** và **cơ hội bỏ lỡ**.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động** lấy danh sách sản phẩm từ Facebook Ad Library.
✅ **So sánh** sản phẩm trên Amazon trong **vài giây** thay vì vài giờ.
✅ **Lưu trữ** kết quả vào Google Sheets để theo dõi và phân tích định kỳ.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ **giờ đồng hồ** xuống **phút giây** cho mỗi sản phẩm.
- **Độ chính xác cao**: Không bị lỗi nhân thủ công, kết quả đồng nhất.
- **Phân tích cạnh tranh**: So sánh giá, đánh giá, và xu hướng bán hàng trên Amazon.
- **Cơ hội dropshipping/FBA mới**: Dễ dàng phát hiện sản phẩm hot trên Facebook nhưng chưa được bán nhiều trên Amazon.
- **Lưu trữ dữ liệu**: Tất cả kết quả được ghi lại trong Google Sheets, dễ dàng chia sẻ và phân tích.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Apify** (đăng ký miễn phí tại [Apify](https://apify.com/)) và **API Token** của hai scraper sau:
   - **"Facebook Ad Library Scraper"** ([Tải tại đây](https://apify.com/richardbesier/facebook-ad-library-scraper))
   - **"Amazon Search Scraper"** ([Tải tại đây](https://apify.com/richardbesier/amazon-search-scraper))
2. **Google Sheets OAuth 2.0 API Key** (để lưu kết quả):
   - Tạo một Google Sheet mới.
   - Cài đặt **Google Sheets API** và tạo **credentials OAuth 2.0** (hướng dẫn tại [Google Cloud Console](https://developers.google.com/sheets/api/quickstart/python)).
3. **API Key OpenAI** (nếu sử dụng node **Product Name Finder** để xác định tên sản phẩm từ nội dung Facebook).
4. **URL Facebook Ad Library** (đường link đến danh sách quảng cáo bạn muốn phân tích).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/6888](https://n8n.io/workflows/6888) và import vào n8n Editor.
- **Copy/Paste** JSON từ file vào **Import Workflow** trong n8n Dashboard.

:::note[LƯU Ý]
- **Không** cần thay đổi cấu trúc workflow, chỉ cần **cấu hình các node quan trọng** như hướng dẫn dưới đây.
- Đảm bảo **n8n đang chạy trên VPS** (Self-hosted) để workflow hoạt động liên tục 24/7.
:::

---

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **17 node**, nhưng chỉ có **5 node quan trọng** cần cấu hình kỹ lưỡng:

##### **A. Cấu Hình Apify Scrapers (2 Node HTTP Request)**
Các sếp cần **thêm API Endpoint** của Apify vào hai node `httpRequest` sau:
1. **Node "Run FB Library Actor"**
   - **Method**: `POST`
   - **URL**: `https://api.apify.com/v2/act/{ACTOR_SLUG}/runs`
   - **Headers**:
     ```json
     {
       "Authorization": "Bearer {API_TOKEN}",
       "Content-Type": "application/json"
     }
     ```
   - **Body (JSON)**:
     ```json
     {
       "input": {
         "startUrls": ["{{ $input["url"] }}"]
       }
     }
     ```
   - **Tham số cần điền**:
     - `{ACTOR_SLUG}`: `facebook-ad-library-scraper` (hoặc slug của scraper Facebook).
     - `{API_TOKEN}`: Token Apify của bạn.
     - `{{ $input["url"] }}`: URL Facebook Ad Library (ví dụ: `https://www.facebook.com/ads/library/?ad_set_id=123456789`).

2. **Node "Get Actor's Scraped Content"**
   - **Method**: `GET`
   - **URL**: `https://api.apify.com/v2/act/{ACTOR_SLUG}/runs/{RUN_ID}/dataset/items`
   - **Headers**:
     ```json
     {
       "Authorization": "Bearer {API_TOKEN}"
     }
     ```
   - **Tham số cần điền**:
     - `{RUN_ID}`: ID của run từ node trước (sử dụng `{{ $node["Run FB Library Actor"].json()["default"].runId }}`).

   **Lặp lại** cho node `httpRequest` gọi Amazon Search Scraper:
   - Thay `{ACTOR_SLUG}` thành `amazon-search-scraper`.
   - Thay `input` thành:
     ```json
     {
       "input": {
         "query": "{{ $json.snapshot.caption }}",
         "limit": 1
       }
     }
     ```

##### **B. Cấu Hình Google Sheets (Node "Append row in sheet")**
- **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước khi import).
- **Sheet Name**: Điền tên sheet bạn muốn lưu kết quả (ví dụ: `FacebookToAmazon_Results`).
- **Range**: Điền `Sheet1!A1` (hoặc tên sheet cụ thể).
- **Data Format**: Đảm bảo các cột trong sheet phù hợp với output của workflow (ví dụ: `FB_Ad_URL`, `Amazon_URL`, `Product_Name`, `Price`).

##### **C. Cấu Hình OpenAI (Node "Product Name Finder")**
- **Credentials**: Chọn `openAiApi` (đã cấu hình API Key OpenAI).
- **Model**: Chọn `gpt-3.5-turbo` (hoặc model khác).
- **Prompt**: Sử dụng prompt mặc định hoặc tùy chỉnh:
  ```text
  Extract the product name from the following Facebook ad caption: "{{ $json.snapshot.caption }}".
  Return only the product name in Vietnamese, no extra words.
  ```

##### **D. Cấu Hình Node "Limit"**
- **Limit to**: `1` (để chỉ lấy kết quả Amazon đầu tiên).

##### **E. Cấu Hình Node "Filter"**
- **Condition**: Lọc bỏ các sản phẩm không có URL Amazon (nếu cần).

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với một URL Facebook Ad Library mẫu:
   - Nhấn **Run Workflow** và nhập URL vào node `Manual Trigger`.
   - Kiểm tra kết quả trong Google Sheets.
2. **Active Workflow**:
   - Sau khi kiểm tra thành công, chuyển workflow sang **Active**.
   - **Lưu ý**: Để workflow chạy liên tục, các sếp nên **cài đặt cron job** (ví dụ: chạy hàng ngày) hoặc sử dụng **webhook** để kích hoạt tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Slack/Telegram**:
   - Thêm node `slack` hoặc `telegram` để thông báo kết quả mới khi tìm thấy sản phẩm hot.
   - Ví dụ: `"Tìm thấy sản phẩm {{ $json.productName }} trên Amazon với giá {{ $json.price }}!"`.

2. **Lưu Log & Theo Dõi**:
   - Sử dụng node `set` để lưu log vào Google Sheets với thời gian, URL, và kết quả.
   - Cấu hình **alert** cho sản phẩm có giá giảm hoặc đánh giá cao.

3. **Tự Động Cập Nhật Định Kỳ**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow hàng ngày/tuần.
   - Ví dụ: `0 0 * * *` (chạy mỗi ngày lúc 00:00).

4. **Phân Tích Dữ Liệu**:
   - Kết hợp với **Google Data Studio** hoặc **Power BI** để tạo báo cáo thị trường tự động.
   - Sử dụng node `code` để tính toán chỉ số cạnh tranh (ví dụ: tỷ lệ sản phẩm Facebook vs. Amazon).

5. **Lọc Sản Phẩm Hot**:
   - Thêm điều kiện trong node `filter` để chỉ lấy sản phẩm có:
     - Giá trên Amazon < Giá trên Facebook.
     - Đánh giá > 4.5 sao.
     - Số lượng bán hàng > 1000 trong 30 ngày.
:::

---

### 📌 **Kết Luận**
Workflow **"Tự Động Tìm Kiếm Sản Phẩm Facebook Trên Amazon"** là **giải pháp hoàn hảo** cho các sếp dropshipping, Amazon FBA hoặc nghiên cứu thị trường muốn:
✔ **Tiết kiệm thời gian** từ hàng giờ xuống **phút giây**.
✔ **Phát hiện cơ hội bán hàng** mới chỉ trong vài click.
✔ **Hoạt động tự động** 24/7 mà không cần code.

**Hành động ngay hôm nay:**
1. **Cài đặt n8n trên VPS** (đăng ký [TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm **VPSN8N**).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Chạy thử** với một URL Facebook Ad Library và theo dõi kết quả!

**Nếu cần hỗ trợ thêm**, các sếp có thể liên hệ với tác giả Richard Besier tại **richard@advetica-systems.com**.

---
:::success[CHÚC MỪNG!]
Bây giờ các sếp đã có **công cụ tự động hóa market research mạnh mẽ**, giúp cạnh tranh hiệu quả trên Amazon và Facebook!
:::