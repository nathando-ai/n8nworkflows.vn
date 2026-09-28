---
title: "🚀 Tự Động Tạo Contact Mautic Từ Khách Hàng Mới Shopify - Không Cần Code!"
description: "Hiểu bao giờ các sếp phải nhập thủ công thông tin khách hàng mới từ Shopify sang Mautic? Workflow này tự động hóa hoàn toàn quá trình, tiết kiệm thời gian và giảm sai sót. Kết quả: Dữ liệu khách hàng đồng bộ 100%, hoạt động 24/7."
slug: "tu-dong-tao-contact-mautic-tu-khach-hang-moi-shopify"
tags: [n8n, automation, marketing, shopify, mautic, no-code, ecommerce]
keywords: [tự động hóa shopify mautic, workflow mautic shopify, tự động tạo contact mautic, tự động hóa marketing, n8n workflow shopify]
---

# 🚀 Tự Động Tạo Contact Mautic Từ Khách Hàng Mới Shopify - Không Cần Code!

### **📌 Nỗi Đau Của Các Sếp**
Các sếp có biết rằng mỗi khi khách hàng mới mua hàng trên Shopify, thông tin của họ phải được nhập thủ công vào Mautic để tiếp thị sau này? Quá trình này không chỉ tốn thời gian mà còn dễ gây sai sót, đặc biệt khi số lượng khách hàng tăng cao. **Với workflow này, các sếp sẽ tự động hóa hoàn toàn quá trình, đồng bộ thông tin khách hàng mới từ Shopify sang Mautic ngay lập tức!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted) để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhập thủ công thông tin khách hàng mới.
- **Dữ liệu chính xác**: Tránh sai sót khi đồng bộ thông tin từ Shopify sang Mautic.
- **Hoạt động liên tục**: Workflow chạy tự động 24/7, không phụ thuộc vào giờ làm việc.
- **Tiếp thị hiệu quả**: Khách hàng mới được thêm vào Mautic ngay lập tức để tiếp thị theo dõi.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Shopify**:
   - API Access Token (Shopify Access Token API) để n8n có thể truy cập dữ liệu khách hàng mới.
   - [Hướng dẫn tạo API Token trên Shopify](https://help.shopify.com/en/manual/apps/develop-api-key).
2. **Tài khoản Mautic**:
   - API Key (Mautic API) để n8n có thể tạo contact mới.
   - [Hướng dẫn tạo API Key trên Mautic](https://docs.mautic.org/en/latest/integrations/api.html).
3. **Cài đặt n8n**:
   - N8n phiên bản mới nhất (Self-hosted hoặc Cloud).
   - Nodes cần thiết: `n8n-nodes-base.mautic`, `n8n-nodes-base.shopifyTrigger`.
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n Editor](https://n8n.io/editor/) và chọn **Import Workflow**.
2. Chọn file JSON hoặc copy toàn bộ mã JSON dưới đây và dán vào ô **Import Workflow**:
   ```json
   {
     "nodes": [
       {
         "parameters": {},
         "name": "On new customer",
         "type": "shopifyTrigger",
         "typeVersion": 1,
         "position": [
           250,
           300
         ],
         "credentials": {
           "shopifyAccessTokenApi": "shopifyAccessTokenApi"
         }
       },
       {
         "parameters": {},
         "name": "Create contact",
         "type": "mautic",
         "typeVersion": 1,
         "position": [
           450,
           300
         ],
         "credentials": {
           "mauticApi": "mauticApi"
         }
       }
     ],
     "connections": {
       "On new customer": {
         "main": [
           {
             "to": "Create contact",
             "connectionType": "direct"
           }
         ]
       }
     }
   }
   ```
3. Nhấn **Import** để hoàn tất.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các node quan trọng như sau:

##### **Node 1: On new customer (Shopify Trigger)**
- **Tên node**: "On new customer"
- **Loại node**: `shopifyTrigger`
- **Tham số cần thiết**:
  - **Credentials**: Chọn `shopifyAccessTokenApi` (đã tạo trước đó).
  - **Trigger Type**: Chọn `Customer Created` (hoặc tùy chỉnh theo yêu cầu).
  - **Fields to Watch**: Chọn các trường cần theo dõi (ví dụ: `firstName`, `lastName`, `email`, `createdAt`).

##### **Node 2: Create contact (Mautic)**
- **Tên node**: "Create contact"
- **Loại node**: `mautic`
- **Tham số cần thiết**:
  - **Credentials**: Chọn `mauticApi` (đã tạo trước đó).
  - **Action**: Chọn `Create Contact`.
  - **Fields to Map**:
    - **Email**: `$json["email"]` (đồng bộ từ Shopify).
    - **First Name**: `$json["firstName"]` (đồng bộ từ Shopify).
    - **Last Name**: `$json["lastName"]` (đồng bộ từ Shopify).
    - **Custom Fields (nếu cần)**: Thêm các trường tùy chỉnh như `phone`, `address`, `createdAt` từ Shopify vào Mautic. Ví dụ:
      ```
      Phone: $json["phone"]
      Address: $json["address1"]
      ```
    - **Lưu ý**: Nếu Mautic có các trường tùy chỉnh (Custom Fields), các sếp cần thêm chúng vào phần `Create contact` để đồng bộ đầy đủ thông tin.

#### 3. Kích hoạt ⚡️
1. **Test Run**: Chọn **Run Once** để kiểm tra workflow với dữ liệu mẫu.
2. **Active Workflow**: Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động khi có khách hàng mới trên Shopify.

---

### ✍️ Mẹo & gợi ý nâng cao
:::tip[CÁCH LÀM NÂNG CAO]
1. **Thêm thông tin thêm từ Shopify**:
   - Nếu khách hàng có thông tin như `phone`, `address`, `order history`, các sếp có thể thêm các trường này vào node `Create contact` bằng cách sử dụng `$json["fieldName"]`.

2. **Gửi thông báo Slack/Email khi tạo contact mới**:
   - Thêm node `slack` hoặc `email` sau node `Create contact` để thông báo cho team khi có khách hàng mới được tạo trong Mautic.

3. **Lưu log hoạt động**:
   - Thêm node `stickyNote` để ghi lại thông tin khách hàng mới (ví dụ: `Customer ID: $json["id"]`, `Email: $json["email"]`).

4. **Tùy chỉnh thông tin contact**:
   - Nếu Mautic có các nhóm (Groups) hoặc tags, các sếp có thể thêm chúng vào node `Create contact` để phân loại khách hàng (ví dụ: `Group: New Customers`).

5. **Sử dụng Webhook để kiểm tra hoạt động**:
   - Thêm node `webhook` để nhận thông báo khi workflow gặp lỗi hoặc hoạt động không như mong đợi.
:::

---

### 📌 Kết luận
Với workflow này, các sếp sẽ **tự động đồng bộ thông tin khách hàng mới từ Shopify sang Mautic một cách hoàn toàn tự động**, tiết kiệm thời gian và giảm thiểu sai sót. **Không cần viết một dòng code nào!** Hãy áp dụng ngay để tối ưu hóa quy trình tiếp thị của mình.

👉 **Bắt đầu tự động hóa ngay hôm nay!** [Tải workflow JSON](https://n8n.io/workflows/1829) và cài đặt trên n8n của mình. 🚀