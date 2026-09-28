---
title: "🚀 Tự Động Hoàn Thành Báo Cáo Market Research Shopify: Scrape Dữ Liệu Cửa Hàng & Sản Phẩm Sang Google Sheets"
description: "Workflow tự động hóa 100% không code giúp các sếp nhanh chóng lấy dữ liệu cửa hàng Shopify (thông tin cơ bản, danh sách sản phẩm) và lưu vào Google Sheets để phân tích thị trường. Giúp tiết kiệm thời gian lên đến 80% so với cách làm thủ công."
slug: "tieu-dung-danh-sach-san-pham-shopify-vao-google-sheets"
tags: [n8n, automation, market-research, shopify-scraper, google-sheets]
keywords: [tự động hóa scrape shopify, lấy dữ liệu cửa hàng shopify, lưu sản phẩm shopify vào google sheets, market research tự động, n8n workflow shopify]
---

# 🚀 **Tự Động Hoàn Thành Báo Cáo Market Research Shopify: Scrape Dữ Liệu Cửa Hàng & Sản Phẩm Sang Google Sheets**

## **💡 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Các sếp thường phải:
- **Tốn thời gian** (từ 2-5 tiếng/lần) để copy-paste dữ liệu cửa hàng Shopify từ trang web sang Google Sheets.
- **Mất chính xác** khi dữ liệu không được cập nhật kịp thời hoặc bị lỗi khi nhập thủ công.
- **Khó so sánh** giữa nhiều cửa hàng vì thiếu hệ thống dữ liệu thống nhất.
- **Không có báo cáo tự động** để theo dõi xu hướng thị trường.

**Workflow này giải quyết tất cả đó bằng cách:**
✅ **Lấy dữ liệu tự động** từ Shopify (thông tin cửa hàng + danh sách sản phẩm) chỉ bằng một cú nhấn.
✅ **Lưu vào Google Sheets** với định dạng sẵn sàng phân tích.
✅ **Hoạt động 24/7** khi tự động hóa trên VPS (không cần mở máy tính).
✅ **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần copy-paste dữ liệu thủ công.
- **Dữ liệu chính xác**: Lấy trực tiếp từ API Shopify Scraper.
- **Báo cáo tự động**: Dữ liệu cập nhật ngay khi có yêu cầu.
- **Phân tích thị trường**: So sánh nhiều cửa hàng trong cùng một bảng Google Sheets.
- **Hoạt động liên tục**: Chạy 24/7 trên VPS, không phụ thuộc vào máy tính cá nhân.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối với Google Sheets).
2. **API Key của RapidAPI** (để gọi API Shopify Scraper):
   - Đăng ký tại [RapidAPI](https://rapidapi.com/apidojo/api/shopify-scraper4/) và lấy `x-rapidapi-key`.
   - **Lưu ý**: API này có giới hạn request (miễn phí 1000 request/tháng).
3. **Google Sheets** đã tạo sẵn với **2 sheet**:
   - `Shop Info` (để lưu thông tin cửa hàng).
   - `Products` (để lưu danh sách sản phẩm).
   - **Link mẫu**: [Google Sheets mẫu](https://docs.google.com/spreadsheets/d/1mVC_2w7vHsKtcxUGkLWvzWSUqpzCoUWtWkLy3CPnfa4) (sao chép và chỉnh sửa).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/8049](https://n8n.io/workflows/8049) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/8049) và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp cần **cấu hình lại các node quan trọng**:

##### **🔹 Node 1: On form submission (formTrigger)**
- **Không cần chỉnh gì** (n8n sẽ tự tạo form nhập URL cửa hàng Shopify).
- **Lưu ý**: Nếu muốn thay đổi form, các sếp có thể chỉnh sửa ở **Properties > Form**.

##### **🔹 Node 2 & 3: Store Info Scrap Request & Products Scrap Request (httpRequest)**
- **URL API**:
  - `https://shopify-scraper4.p.rapidapi.com/shopinfo.php` (thông tin cửa hàng).
  - `https://shopify-scraper4.p.rapidapi.com/products.php` (danh sách sản phẩm).
- **Headers**:
  - `x-rapidapi-host`: `shopify-scraper4.p.rapidapi.com`
  - `x-rapidapi-key`: **Điền API Key của bạn** (đã lấy từ RapidAPI).
- **Body (JSON)**:
  ```json
  {
    "url": "{{ $node["On form submission"].json["website"] }}"
  }
  ```
  *(Đây là URL cửa hàng Shopify mà người dùng nhập vào form.)*

##### **🔹 Node 4 & 5: Append Store Info & Products Data (googleSheets)**
- **Credentials**:
  - Chọn `googleApi` (đã cấu hình trước khi import).
- **Sheet Name**:
  - **Node 4**: `Shop Info` (để lưu thông tin cửa hàng).
  - **Node 5**: `Products` (để lưu danh sách sản phẩm).
- **Range**:
  - **Node 4**: `Shop Info!A1` (n8n sẽ tự động append xuống dòng mới).
  - **Node 5**: `Products!A1` (tương tự).
- **Headers**:
  - **Node 4 (Store Info)**:
    ```
    Name,Domain,Location,Description,Tags,Products Count
    ```
  - **Node 5 (Products)**:
    ```
    Title,Price,Tags,Description,Images,Variants
    ```
  *(Nếu sheet của các sếp khác, cần chỉnh sửa theo cấu trúc dữ liệu thực tế.)*

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhập URL của một cửa hàng Shopify vào form (ví dụ: `https://example.shopify.com`).
  - Chạy workflow và kiểm tra **Google Sheets** xem dữ liệu có được append không.
- **Bật Active**:
  - Sau khi test thành công, **bật workflow** để hoạt động tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động hóa theo lịch**:
   - Sử dụng **n8n Cron Trigger** để scrape dữ liệu định kỳ (ví dụ: hàng tuần).
   - Ví dụ: `0 0 * * 1` (chạy vào thứ Hai hàng tuần).

2. **Gửi báo cáo tự động qua Email/Slack**:
   - Kết nối với **n8n-nodes-base.email** hoặc **n8n-nodes-base.slack** để thông báo khi có dữ liệu mới.

3. **Lọc dữ liệu theo điều kiện**:
   - Sử dụng **n8n-nodes-base.if** để chỉ scrape cửa hàng có giá trị nhất định (ví dụ: chỉ lấy cửa hàng có `Products Count > 50`).

4. **Lưu log hoạt động**:
   - Kết nối với **Google Drive** hoặc **Notion** để ghi lại lịch sử scrape.

5. **Tối ưu API Key**:
   - Nếu dùng API miễn phí, các sếp nên **lưu trữ dữ liệu đã scrape** trong Google Sheets và **không gọi API liên tục** vào cùng một cửa hàng.

---

### 📌 **Kết Luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn quá trình lấy dữ liệu Shopify** và lưu vào Google Sheets, tiết kiệm thời gian và tăng hiệu suất phân tích thị trường. **Chỉ cần một cú nhấn**, dữ liệu cửa hàng và sản phẩm đã sẵn sàng để so sánh, báo cáo và đưa ra quyết định kinh doanh chính xác.

**🚀 Hãy áp dụng ngay và bắt đầu tự động hóa market research của mình!**

---
**💡 Cần hỗ trợ thêm?**
- **Hỏi đáp trên cộng đồng n8n**: [n8n Community](https://community.n8n.io/)
- **Đăng ký VPS n8n**: [TinoHost](https://tino.vn/vps-n8n?affid=388) (mã giảm giá **VPSN8N**)