---
title: "🚀 Tự Động Hóa Tạo Nhiều Sản Phẩm Shopify + Quản Lý Kho Từ Google Sheets (Không Cần Code)"
description: "Workflow này tự động tạo hàng loạt sản phẩm Shopify từ Google Sheets, đồng thời kích hoạt quản lý tồn kho và cập nhật số lượng hàng tồn kho theo mặc định. Giúp các sếp tiết kiệm thời gian lên tới 80% so với cách làm thủ công, đồng thời đảm bảo dữ liệu chính xác và đồng bộ hóa liên tục."
slug: "tay-dong-hoa-tao-san-pham-shopify-tu-google-sheets"
tags: [n8n, automation, shopify, google-sheets, inventory-management, no-code]
keywords: [tự động hóa shopify, tạo sản phẩm bulk shopify, quản lý tồn kho shopify, google sheets shopify, n8n workflow shopify]
---

# 🚀 **Tự Động Hóa Tạo Nhiều Sản Phẩm Shopify + Quản Lý Kho Từ Google Sheets (Không Cần Code)**

### **🔥 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
- **Tốn thời gian**: Tạo từng sản phẩm trên Shopify thủ công mất hàng giờ, thậm chí hàng ngày khi có nhiều sản phẩm mới.
- **Rủi ro sai sót**: Nhập sai thông tin như giá, SKU, hoặc tồn kho dẫn đến mất doanh thu hoặc trải nghiệm khách hàng tệ.
- **Không đồng bộ hóa**: Dữ liệu trên Google Sheets và Shopify không tự động cập nhật, gây ra tình trạng "thông tin cũ" và khó quản lý.
- **Khó mở rộng**: Khi số lượng sản phẩm tăng, việc quản lý thủ công trở nên không thể khả thi, đặc biệt là với các shop bán hàng bulk.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tạo sản phẩm bulk tự động** từ Google Sheets (một hàng = một sản phẩm).
✅ **Kích hoạt quản lý tồn kho** và cập nhật số lượng hàng tồn kho theo mặc định.
✅ **Bỏ qua sản phẩm đã tồn tại** (tránh trùng lặp và lỗi).
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này chạy ổn định và không ngừng nghỉ, các sếp nên **self-host n8n** trên VPS riêng để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tạo hàng trăm sản phẩm chỉ trong vài phút thay vì mất cả ngày.
- **Dữ liệu chính xác**: Không còn lo lắng về sai sót khi nhập thông tin thủ công.
- **Quản lý kho tự động**: Tồn kho được cập nhật ngay khi có thay đổi trên Google Sheets.
- **Hoạt động liên tục**: Workflow chạy tự động mỗi khi có dữ liệu mới trên Sheets.
- **Dễ dàng mở rộng**: Thêm sản phẩm mới chỉ cần cập nhật trên Google Sheets.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Shopify** với quyền **Admin** (để có API Access Token).
2. **Google Sheets** với cấu trúc cột chuẩn (xem chi tiết dưới đây).
3. **API Access Token của Shopify** (tạo từ [Shopify Admin](https://shopify.com/admin/apps)).
4. **Credentials OAuth 2.0 cho Google Sheets** (cài đặt trong n8n).

#### **Cấu trúc Google Sheets bắt buộc**
| Column Name  | Kiểu Dữ liệu | Ghi Chú |
|--------------|-------------|----------|
| `title`      | Text        | Tên sản phẩm |
| `description`| Text        | Mô tả sản phẩm |
| `company`    | Text        | Thương hiệu (nếu có) |
| `category`   | Text        | Danh mục sản phẩm |
| `status`     | Text        | `ACTIVE`, `DRAFT`, hoặc `ARCHIVE` |
| `slug`       | Text        | URL của sản phẩm (không dấu, dùng `-` thay thế) |
| `price`      | Number      | Giá bán |
| `compare_at_price` | Number | Giá so sánh (nếu có) |
| `sku`        | Text        | Mã SKU duy nhất |
| `stock_on_hand` | Number | Số lượng tồn kho |

**Lưu ý:** Dòng đầu tiên của Sheets **phải** là tiêu đề cột (n8n sẽ tự động đọc cấu trúc này).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [link gốc](https://n8n.io/workflows/5664) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/5664) và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **10 node**, nhưng các bước quan trọng nhất cần chú ý như sau:

##### **A. Cấu Hình Google Sheets**
- **Node:** `Google Sheet, Fetch Products`
  - **Credentials:** Chọn `googleSheetsOAuth2Api` (đã cài đặt trước).
  - **Sheet Name:** Điền tên Sheet của bạn.
  - **Range:** Điền `Sheet1!A1:Z` (hoặc thay đổi theo cấu trúc của bạn).
  - **Test Run:** Chạy thử để đảm bảo n8n đọc được dữ liệu.

##### **B. Cấu Hình Shopify (GraphQL API)**
- **Node:** `Shopify, ProductQuery`, `Shopify, CreateProduct`, `Shopify, GetLocations`, `Shopify, Enable InventoryTracking`, `Shopify, Set InventoryLevel`
  - **Credentials:** Chọn `httpHeaderAuth` (đã cài đặt trước).
  - **URL:** Thay thế tất cả URL trong các node bằng **URL Shopify của bạn** (ví dụ: `https://[your-store].myshopify.com/admin/api/2025-04/graphql.json`).
  - **Headers:**
    - `X-Shopify-Access-Token`: Điền **API Access Token** của Shopify.
    - `Content-Type`: `application/json`.
  - **Query/Variables:**
    - Các query đã được cấu hình sẵn, **không cần chỉnh sửa** trừ khi có yêu cầu đặc biệt.

##### **C. Logic "If Product Exists"**
- **Node:** `If product exists`
  - N8n sẽ **bỏ qua sản phẩm đã tồn tại** nếu `slug` trùng với một sản phẩm hiện có trên Shopify.
  - **Không cần chỉnh sửa** nếu muốn giữ logic mặc định.

##### **D. Loop Over Items & Inventory Management**
- **Node:** `Loop Over Items` (splitInBatches)
  - N8n sẽ **chia dữ liệu thành batch** để tránh quá tải API.
  - **Không cần chỉnh sửa** (n8n tự động điều chỉnh).
- **Node:** `Shopify, Enable InventoryTracking` và `Shopify, Set InventoryLevel`
  - Cập nhật **tồn kho mặc định** cho sản phẩm mới.
  - **Lưu ý:** Đảm bảo `stock_on_hand` trong Google Sheets là số dương.

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Chạy thử với **1-2 sản phẩm** để kiểm tra logic.
- **Active Workflow:** Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động khi có dữ liệu mới trên Google Sheets.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Telegram để báo cáo**
   - Thêm node `webhook` hoặc `slack` sau `Finished` để nhận thông báo khi workflow hoàn thành.
   - Ví dụ: Gửi tin nhắn "X sản phẩm đã tạo thành công trên Shopify!"

2. **Lưu log hoạt động**
   - Thêm node `googleSheets` sau `Finished` để ghi lại lịch sử tạo sản phẩm (cột mới: `created_at`, `status`).

3. **Cập nhật giá và tồn kho tự động**
   - Nếu muốn **cập nhật tồn kho theo thời gian thực**, thêm node `googleSheets` để đọc dữ liệu mới và chạy workflow định kỳ (ví dụ: hàng ngày).

4. **Tạo sản phẩm theo danh mục**
   - Nếu có nhiều danh mục, chia Google Sheets thành nhiều Sheet riêng và chạy workflow riêng cho mỗi Sheet.

5. **Sử dụng n8n Cloud (nếu không self-host)**
   - Nếu không muốn tự host, có thể dùng **n8n Cloud** (miễn phí cho 1000 execution/tháng), nhưng **self-host vẫn ổn định hơn**.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tạo sản phẩm bulk trên Shopify một cách tự động**.
✔ **Quản lý tồn kho hiệu quả** mà không cần can thiệp thủ công.
✔ **Tiết kiệm thời gian và giảm thiểu lỗi**.

**Hành động ngay hôm nay:**
1. **Chuẩn bị Google Sheets** với cấu trúc đúng.
2. **Import workflow** và cấu hình Shopify.
3. **Test Run** và bật **Active** để workflow chạy tự động!

**Nếu có vấn đề gì, hãy để lại comment dưới đây hoặc liên hệ với team n8n Việt Nam!** 🚀

---
**#TựĐộngHóaShopify #N8NVietnam #QuảnLýKhoTựĐộng**