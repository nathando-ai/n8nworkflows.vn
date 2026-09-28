---
title: "🚀 Tự Động Hoá Scrape & Nhập Sản Phẩm Giày Vào Shopify Với BrowserAct (Kèm Variant & Hình Ảnh)"
description: "Workflow này tự động scrape dữ liệu sản phẩm giày từ bất kỳ URL nào, xử lý biến thể (size, màu) và hình ảnh, sau đó nhập hoàn chỉnh vào Shopify chỉ với một nhấp chuột. Giúp các sếp tiết kiệm 10-15 giờ/lần so với thủ công."
slug: "tự-dộng-hoa-scrape-nhap-san-pham-giay-vao-shopify"
tags: [n8n, automation, ecommerce, browseract, shopify, no-code, scraping]
keywords: [n8n workflow scrape shopify, tự động hóa nhập hàng shopify, browseract n8n, scrape sản phẩm giày, biến thể shopify, tự động hóa ecommerce]
---

# 🚀 **Tự Động Hoá Scrape & Nhập Sản Phẩm Giày Vào Shopify Với BrowserAct (Kèm Variant & Hình Ảnh)**

## **🔥 Giải Pháp Cho Nỗi Đau Của Các Sếp Ecommerce**
Hàng ngày, các sếp phải:
- **Tốn thời gian** thủ công nhập sản phẩm từ website đối thủ, Amazon, hoặc các trang bán lẻ vào Shopify (thường mất **10-15 giờ/lần**).
- **Lo lắng về chính xác** dữ liệu: Thông tin size, màu sắc, hoặc hình ảnh bị sai lệch → ảnh hưởng đến trải nghiệm khách hàng.
- **Khó quản lý biến thể**: Nhập size, màu, hoặc kích thước khác nhau một cách thủ công → dễ bị lỗi hoặc bỏ sót.
- **Không tự động hóa được**: Các công cụ scrape đơn giản chỉ lấy được dữ liệu thô, còn việc xử lý biến thể và upload hình ảnh vẫn phải làm thủ công.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Scrape** tất cả thông tin sản phẩm (tên, mô tả, giá, size, hình ảnh) từ bất kỳ URL nào.
✅ **Xử lý biến thể** (size, màu) thành định dạng chuẩn Shopify.
✅ **Upload hình ảnh** một cách tự động.
✅ **Nhập sản phẩm hoàn chỉnh** vào Shopify chỉ với một nhấp chuột.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Nhập **100 sản phẩm** chỉ trong **5 phút** thay vì 10-15 giờ thủ công.
- **Chính xác 100%**: Dữ liệu size, màu, hình ảnh được scrape và xử lý tự động, không sai sót.
- **Biến thể hoàn chỉnh**: Tự động tạo variant cho size, màu, kích thước khác nhau.
- **Hoạt động liên tục**: Chạy 24/7 trên VPS, không cần can thiệp thủ công.
- **Gửi báo cáo Slack**: Biết ngay khi workflow hoàn thành hoặc gặp lỗi.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản BrowserAct**:
   - [Đăng ký miễn phí](https://www.browseract.com/) và tạo **Workflow Template** có tên:
     *"Bulk Product Scraping From (URLs) and uploading to Shopify (Optimised for shoe - NIKE -> Shopify)"*.
   - **API Key** của BrowserAct (cần để kết nối với n8n).

2. **Tài khoản Shopify**:
   - **API Key** và **Shopify Access Token** (có quyền `write_products`).
   - **Storefront Access Token** (nếu muốn preview sản phẩm trước khi publish).

3. **Google Sheets**:
   - Một bảng Google Sheets chứa **cột `Product Link`** (đường dẫn sản phẩm cần scrape).
   - **Credentials OAuth2** để n8n đọc dữ liệu.

4. **Tài khoản Slack (tùy chọn)**:
   - **OAuth2 Token** để gửi thông báo khi workflow hoàn thành.

5. **Node BrowserAct cho n8n**:
   - Cài đặt node từ [n8n Nodes BrowserAct](https://www.npmjs.com/package/n8n-nodes-browseract-workflows).
   - **Cách cài đặt**:
     ```bash
     cd ~/.n8n/nodes
     npm install n8n-nodes-browseract-workflows
     ```
     Sau đó **restart n8n**.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/9946) hoặc copy toàn bộ JSON từ trang này.
- Trong **n8n Editor**, nhấn **Import Workflow** và dán JSON vào.
- **Lưu workflow** với tên mới (ví dụ: *"Scrape Giày Shopify - [Tên Shop]"*).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow có **16 node**, nhưng các bước quan trọng nhất cần điều chỉnh:

##### **A. Cấu Hình Credentials**
| Node | Tham Số Cần Điền | Ghi Chú |
|------|------------------|---------|
| **BrowserAct** | `browserActApi` | Điền **API Key** và **Workflow ID** từ BrowserAct. |
| **Shopify** | `shopifyAccessTokenApi` | Điền **Access Token** từ Shopify (có quyền `write_products`). |
| **Google Sheets** | `googleSheetsOAuth2Api` | Điền **Credentials OAuth2** của Google Sheets. |
| **Slack (nếu dùng)** | `slackOAuth2Api` | Điền **Token OAuth2** từ Slack. |

##### **B. Cấu Hình Google Sheets**
- Node **"Get List"** (Google Sheets) phải chỉ đến **cột `Product Link`** trong bảng.
- **Kiểm tra dữ liệu mẫu**: Nếu bảng có nhiều cột, chỉ chọn **cột `Product Link`** để workflow scrape chính xác.

##### **C. Cấu Hình BrowserAct**
- **Node "Run a workflow"** (BrowserAct):
  - **Tham số `operation`** phải là `"getTask"` (đã mặc định).
  - **Tham số `workflowId`** phải trùng với **Workflow ID** của template BrowserAct đã tạo.
- **Node "Parse Data"** (Code):
  - **Mã JavaScript** trong node này **không thể thay đổi** (do template BrowserAct đã định sẵn).
  - Nếu scrape sản phẩm khác giày (ví dụ: áo, quần), **cần chỉnh sửa mã** để phù hợp.

##### **D. Cấu Hình Shopify**
- **Node "Create a product"**:
  - **Tham số `title`**, `description`, `vendor` phải trùng với dữ liệu scrape.
  - **Tham số `tags`** có thể thêm `scraped`, `automated` để phân loại.
- **Node "Add Variant"** (HTTP Request):
  - **Tham số `option[0].name`** phải là `"Size"` (hoặc tên biến thể khác).
  - **Tham số `option[0].values`** sẽ tự động lấy từ dữ liệu scrape (ví dụ: `["36", "37", "38"]`).

##### **E. Cấu Hình Slack (nếu dùng)**
- Node **"Send a message"** (Slack) sẽ gửi thông báo khi workflow hoàn thành.
- **Tham số `text`** có thể tùy chỉnh:
  ```json
  {
    "type": "mrkdwn",
    "text": "🚀 Workflow Scrape Giày Shopify hoàn tất!\n*Số sản phẩm nhập:* {{ $json["items"].length }}"
  }
  ```

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Chọn **1 sản phẩm mẫu** trong Google Sheets (ví dụ: URL của một đôi giày Nike).
  - Nhấn **Execute Workflow** để kiểm tra:
    - Dữ liệu scrape có chính xác không?
    - Variant và hình ảnh có upload vào Shopify không?
- **Bật Active**:
  - Sau khi test thành công, **bật Active** và **lưu workflow**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Chạy tự động hàng ngày**:
   - Thay thế **Manual Trigger** bằng **Schedule Trigger** (ví dụ: chạy lúc 2 giờ sáng hàng ngày).
   - Cách thiết lập:
     - Thêm node **`n8n-nodes-base.schedule`**.
     - Chọn **cron job** như `0 2 * * *` (lúc 2 giờ sáng hàng ngày).

2. **Lưu log hoạt động**:
   - Thêm node **`n8n-nodes-base.httpRequest`** để gửi dữ liệu scrape vào **Google Sheets Log** hoặc **Database**.
   - Ví dụ: Lưu `product_id`, `url`, `status` (thành công/thất bại).

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **Slack** hoặc **Email** để báo cáo số lượng sản phẩm nhập thành công.
   - Ví dụ:
     ```json
     {
       "blocks": [
         {
           "type": "section",
           "text": {
             "type": "mrkdwn",
             "text": "*Báo cáo tự động hóa nhập hàng Shopify*\n*Ngày:* {{ $json["date"] }}\n*Số sản phẩm:* {{ $json["items"].length }}"
           }
         }
       ]
     }
     ```

4. **Scrape nhiều loại sản phẩm**:
   - Nếu muốn scrape **áo, quần, túi** thay vì giày, cần:
     - **Chỉnh sửa template BrowserAct** để phù hợp với cấu trúc trang mới.
     - **Cập nhật node `Parse Data`** (Code) để xử lý dữ liệu biến thể mới.

5. **Xử lý lỗi tự động**:
   - Thêm node **`n8n-nodes-base.if`** để kiểm tra lỗi:
     - Nếu `statusCode` của Shopify API là `422` (Unprocessable Entity), gửi thông báo Slack và **dừng workflow**.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp ecommerce muốn:
✔ **Tiết kiệm thời gian** nhập hàng thủ công.
✔ **Nhập sản phẩm chính xác** với biến thể và hình ảnh hoàn chỉnh.
✔ **Hoạt động tự động** 24/7 mà không cần can thiệp.

**Hành động ngay!**
1. **Chuẩn bị tài khoản** (BrowserAct, Shopify, Google Sheets).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test với 1-2 sản phẩm** trước khi chạy toàn bộ.

**Nếu gặp khó khăn**, tham khảo:
- [Hướng dẫn kết nối n8n với BrowserAct](https://www.youtube.com/watch?v=RoYMdJaRdcQ)
- [Cách sử dụng template BrowserAct](https://www.youtube.com/watch?v=CPZHFUASncY)

**Chúc các sếp thành công!** 🚀🛍️