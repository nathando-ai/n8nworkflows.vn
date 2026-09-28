---
title: "🛍️ Tự Động Lấy Toàn Bộ Sản Phẩm Shopify Với GraphQL Cursor (Không Cần Code)"
description: "Giải pháp tự động hóa lấy tất cả sản phẩm từ Shopify bằng GraphQL cursor, phù hợp cho các sếp muốn tránh thủ công và tránh giới hạn page size mặc định. Workflow này giúp lấy toàn bộ danh sách sản phẩm một cách hiệu quả và không giới hạn."
slug: "tay-toan-bo-san-pham-shopify-graphql-cursor"
tags: [n8n, automation, shopify, graphql, ecommerce]
keywords: [n8n shopify, lấy sản phẩm shopify, graphql cursor, tự động hóa shopify, lấy toàn bộ sản phẩm shopify]
---

# 🚀 Lấy Toàn Bộ Sản Phẩm Shopify Với GraphQL Cursor (Không Cần Code)

### **Nỗi Đau Của Các Sếp**
Lấy toàn bộ danh sách sản phẩm từ Shopify bằng API truyền thống thường gặp 2 vấn đề lớn:
1. **Giới hạn page size**: API mặc định chỉ trả về tối đa 250 sản phẩm/lần gọi (hoặc 50 sản phẩm nếu không cấu hình).
2. **Thủ công tốn thời gian**: Các sếp phải viết code hoặc sử dụng các công cụ khác để loop qua từng trang, dẫn đến rủi ro lỗi và tốn nhiều thời gian.

**Giải pháp này** giúp các sếp tự động hóa việc lấy **toàn bộ sản phẩm** từ Shopify bằng cách sử dụng **GraphQL cursor-based pagination**, không cần viết một dòng code nào cả!

---

### 🎯 Kết Quả Các Sếp Nhận Được
:::tip[LỢI ÍCH CỐT LÕI]
- **Lấy toàn bộ sản phẩm** một cách tự động, không giới hạn số lượng.
- **Tiết kiệm thời gian** so với cách thủ công hoặc sử dụng API REST truyền thống.
- **Không cần code**: Sử dụng n8n để tự động hóa quy trình.
- **Hiệu quả cao**: Dùng GraphQL cursor để duyệt qua tất cả trang sản phẩm một cách liền mạch.
:::

---

### 🔧 Yêu Cầu Cần Thiết
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow này, các sếp cần:
- **Tài khoản Shopify** và **API Key** (có thể lấy từ **Shopify Admin → Apps and Sales Channels → Develop Apps → API Credentials**).
- **N8n Self-hosted** (không dùng phiên bản miễn phí trên cloud vì cần chạy liên tục).
- **Node GraphQL** được cấu hình sẵn trong n8n (nếu chưa có, cài đặt từ **n8n Marketplace**).
:::

---

### 🚀 Cách Import & Lưu Ý Khi "Lên Đồ"

#### 1. **Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
```json
[
  {
    "name": "Start Workflow",
    "type": "manualTrigger"
  },
  {
    "name": "Shopify, products",
    "type": "graphql",
    "credentials": ["httpHeaderAuth"]
  },
  {
    "name": "hasMoreProducts",
    "type": "if"
  },
  {
    "name": "Wait 1s",
    "type": "wait"
  }
]
```
**Cách import:**
1. Mở **n8n Editor** → Nhấn **Import Workflow** → Chọn file JSON hoặc paste JSON vào.
2. Sau khi import, workflow sẽ hiển thị trên canvas.

#### 2. **Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
##### **a. Cấu Hình Node "Shopify, products" (GraphQL)**
- **Endpoint**: Điền vào **Shopify GraphQL API URL** của mình (ví dụ: `https://{store-name}.myshopify.com/admin/api/{version}/graphql.json`).
- **Query**:
  ```graphql
  query {
    products(first: 5, after: $cursor) {
      edges {
        node {
          id
          title
          description
          # Thêm các trường khác cần lấy
        }
      }
      pageInfo {
        hasNextPage
        endCursor
      }
    }
  }
  ```
  - **Lưu ý**:
    - `first: 5` chỉ để minh họa (các sếp nên tăng lên **250** để tối ưu).
    - `$cursor` là biến để duyệt qua các trang.
- **Headers**:
  - `X-Shopify-Access-Token`: Điền **API Key** của Shopify.
  - `Content-Type`: `application/json`.

##### **b. Cấu Hình Node "hasMoreProducts" (If)**
- **Condition**: Kiểm tra `$.json.pageInfo.hasNextPage` (nếu `true`, có sản phẩm tiếp theo).
- **True Branch**: Chỉnh để gọi lại node GraphQL với `after: $$.json.pageInfo.endCursor`.

##### **c. Node "Wait 1s" (Wait)**
- **Thời gian chờ**: 1 giây (có thể điều chỉnh tùy theo tốc độ API của Shopify).

#### 3. **Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** để kiểm tra.
   - Kiểm tra kết quả trong **Execution History**.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ Mẹo & Gợi Ý Nâng Cao
:::info[TIẾP CẬN HƠN]
- **Lưu kết quả vào Google Sheets/Excel**:
  - Thêm node **Google Sheets** sau node GraphQL để tự động ghi sản phẩm vào bảng tính.
- **Gửi thông báo Slack/Email khi hoàn thành**:
  - Thêm node **Slack** hoặc **Email** để báo cáo khi workflow lấy xong tất cả sản phẩm.
- **Lưu log vào file JSON**:
  - Sử dụng node **File** để lưu lịch sử lấy dữ liệu.
- **Chạy định kỳ**:
  - Sử dụng **n8n Cron Trigger** để tự động chạy workflow hàng ngày/tuần.
:::

---

### 📌 Kết Luận
Workflow này giúp các sếp **tự động hóa việc lấy toàn bộ sản phẩm Shopify một cách hiệu quả**, không cần viết code và tránh giới hạn của API REST truyền thống. **Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất kinh doanh!**

:::tip[LƯU Ý CUỐI CÙNG]
- **N8n Self-hosted** là giải pháp tối ưu để workflow chạy 24/7.
- **Cập nhật API Key** nếu Shopify thay đổi.
- **Monitor Execution History** để phát hiện lỗi nếu có.
:::

---
👉 **Bắt đầu tự động hóa ngay hôm nay!** [Tải n8n Self-hosted](https://n8n.io/) hoặc [đăng ký VPS](https://tino.vn/vps-n8n?affid=388) để chạy workflow ổn định. 🚀