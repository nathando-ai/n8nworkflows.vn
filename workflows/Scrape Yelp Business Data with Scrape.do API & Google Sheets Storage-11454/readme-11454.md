---
title: "🚀 Tự Động Hoàn Thành Scraping Dữ Liệu Doanh Nghiệp Yelp Và Lưu Trữ Trên Google Sheets"
description: "Workflow tự động hóa 100% không code giúp các sếp scrap dữ liệu chi tiết doanh nghiệp từ Yelp (tên, rating, địa chỉ, điện thoại...) và lưu trữ tự động vào Google Sheets. Giúp tiết kiệm thời gian nghiên cứu thị trường lên đến 80%."
slug: "tieu-dong-scrap-yelp-va-luu-googlesheets"
tags: [n8n, automation, market-research, scrape-do, google-sheets, no-code]
keywords: [scrap yelp dữ liệu doanh nghiệp, tự động hóa nghiên cứu thị trường, lưu dữ liệu google sheets, scrape.do api, n8n workflow market research]
---

# 🚀 **Tự Động Scrap Dữ Liệu Doanh Nghiệp Yelp & Lưu Trữ Trên Google Sheets**

### **Nỗi Đau Của Các Sếp Trong Nghiên Cứu Thị Trường**
Hàng ngày, các sếp phải tốn thời gian **quét thủ công** thông tin doanh nghiệp trên Yelp để phân tích:
- **Đánh giá trung bình** (rating) và số lượng đánh giá
- **Địa chỉ, điện thoại, website** chính thức
- **Dịch vụ cung cấp** (categories) và **độ phù hợp giá** (price range)
- **Giờ mở cửa** và **hình ảnh/video** giới thiệu

**Kết quả?** Thời gian mất **tối thiểu 30 phút/doanh nghiệp**, và dễ bị lỗi nhân thủ công. **Workflow này giải quyết hoàn toàn vấn đề đó bằng tự động hóa 100% không code!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Scrap **10+ doanh nghiệp/ngày** mà không cần làm thủ công.
✅ **Dữ liệu chính xác**: Không bị lỗi copy-paste, tự động cập nhật từ Yelp.
✅ **Lưu trữ tự động**: Tất cả dữ liệu được **append** vào Google Sheets theo định dạng chuẩn.
✅ **Hoạt động liên tục**: Chạy 24/7 trên VPS, không phụ thuộc vào máy tính cá nhân.
✅ **Dễ mở rộng**: Thêm các doanh nghiệp mới chỉ cần **copy URL** vào form.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Scrape.do**:
   - [Đăng ký miễn phí](https://scrape.do/?utm_source=n8n&utm_medium=yelp) và lấy **API Token**.
2. **Google Sheets**:
   - Tạo một **Google Sheet mới** với các cột sau (định dạng chính xác):
     ```
     name (Tên doanh nghiệp), overall_rating (Đánh giá trung bình), reviews_count (Số lượng đánh giá), url (Link Yelp), phone (Điện thoại), address (Địa chỉ), price_range (Phạm vi giá), categories (Dịch vụ), website (Website), hours (Giờ mở cửa), images_videos_urls (Link hình ảnh/video), scraped_at (Thời gian scrap)
     ```
   - **Cấp quyền OAuth2** cho n8n truy cập vào Google Sheets.
3. **Credentials cho n8n**:
   - **Scrape.do Token** (để thay thế `YOUR_SCRAPEDO_TOKEN` trong 3 node HTTP Request).
   - **Google Sheets OAuth2 Credentials** (để thay thế `YOUR_GOOGLE_SHEET_ID`).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/11454) và import vào **n8n Editor**.
- **Copy/Paste JSON** từ link trên vào **n8n Editor** (tab "Import").

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Sau khi import, các sếp **phải** thực hiện các bước sau để workflow hoạt động:

##### **A. Cấu Hình Scrape.do API**
Trong **3 node HTTP Request** (`🔍 Create Scrape.do Job`, `📡 Check Job Status`, `📥 Fetch Task Results`):
1. **Thay thế `YOUR_SCRAPEDO_TOKEN`** bằng **API Token** của bạn (đã lấy từ Scrape.do).
   - Ví dụ:
     ```json
     "headers": {
       "Authorization": "Bearer YOUR_SCRAPEDO_TOKEN"
     }
     ```
2. **Kiểm tra URL API**:
   - **Create Job**: `https://scrape.do/api/v1/jobs`
   - **Check Status**: `https://scrape.do/api/v1/jobs/{jobId}`
   - **Fetch Results**: `https://scrape.do/api/v1/jobs/{jobId}/results`

##### **B. Cấu Hình Google Sheets**
Trong node `📊 Store to Google Sheet`:
1. **Thay thế `YOUR_GOOGLE_SHEET_ID`** bằng **ID Sheet** của bạn (tìm trong URL Google Sheets).
   - Ví dụ: Nếu URL Sheet là `https://docs.google.com/spreadsheets/d/abc123xyz/edit`, thì `YOUR_GOOGLE_SHEET_ID = abc123xyz`.
2. **Chọn tab Sheet** (nếu Sheet có nhiều tab).
3. **Kiểm tra cấu trúc dữ liệu**:
   - Workflow **append** dữ liệu theo **trật tự cột** đã định nghĩa trước đó.

##### **C. Cấu Hình Form Trigger**
Node `📥 Form Trigger` sẽ **khởi động workflow** khi người dùng nhập URL Yelp:
1. **Cấu hình form** (nếu muốn sử dụng UI):
   - Thêm một **input text** với label `"Nhập URL Yelp"` và **mã field** là `url`.
   - **Optional**: Thêm các field khác như `businessName` (tên doanh nghiệp) để cá nhân hóa.

##### **D. Cấu Hình Parse HTML (Node Code)**
Node `🔧 Parse Yelp HTML` sử dụng **regex** và **JSON-LD** để trích xuất dữ liệu:
- **Không cần chỉnh sửa** nếu đã import file JSON chính xác.
- **Nếu cần tùy chỉnh**:
  - Mở node `Code` và xem **logic trích xuất** (sử dụng `cheerio` và `jsonld`).
  - Ví dụ:
    ```javascript
    // Trích xuất rating từ JSON-LD
    const rating = JSON.parse(data).@graph.find(item => item['@type'] === 'Rating').ratingValue;
    ```

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với một URL Yelp mẫu (ví dụ: `https://www.yelp.com/biz/example-restaurant-ho-chi-minh-city`).
2. **Kiểm tra Google Sheets**:
   - Dữ liệu mới sẽ được **append** vào Sheet sau khi scrap hoàn tất.
3. **Bật Active** workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động gửi báo cáo định kỳ**:
   - Sử dụng **node `n8n-nodes-base.email`** hoặc **Slack/Telegram** để gửi **tóm tắt dữ liệu mới** hàng tuần.
   - Ví dụ: "Đã scrap 50 doanh nghiệp mới, trung bình rating 4.2/5".

2. **Lưu log scrap**:
   - Thêm node `n8n-nodes-base.file` để **lưu file HTML raw** của mỗi scrap vào Google Drive hoặc Dropbox.

3. **Kết hợp với LLM (AI)**:
   - Sử dụng **node `n8n-nodes-base.llm`** (OpenAI, Mistral) để **tóm tắt phân tích** dữ liệu scrap (ví dụ: "Doanh nghiệp này có ưu điểm gì so với đối thủ?").

4. **Tự động cập nhật định kỳ**:
   - Sử dụng **node `n8n-nodes-base.cron`** để **scrap lại** các doanh nghiệp cũ sau 1 tháng.

5. **Tạo dashboard**:
   - Kết nối với **Google Data Studio** hoặc **Power BI** để **visualize** dữ liệu scrap.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào **strategy** thay vì làm thủ công. **Chỉ cần 10 phút setup**, bạn đã có một **công cụ tự động hóa scrap Yelp** chạy 24/7, lưu dữ liệu vào Google Sheets và sẵn sàng **phân tích thị trường** một cách chuyên nghiệp.

**Hành động ngay!**
1. **Import workflow** và **cấu hình** theo hướng dẫn.
2. **Test với 1-2 URL Yelp** để đảm bảo hoạt động.
3. **Bật Active** và **quên đi việc scrap thủ công**!

---
**💡 Cần hỗ trợ?** Liên hệ với tác giả [Onur](https://n8n.io/workflows/11454) qua email hoặc [GitHub](https://github.com/onurdev) để có thêm hướng dẫn chi tiết!