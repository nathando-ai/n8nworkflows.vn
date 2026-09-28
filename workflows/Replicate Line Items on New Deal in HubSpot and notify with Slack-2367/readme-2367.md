---
title: "🚀 Tự Động Hóa Sao Chép Chi Tiết Hợp Đồng (Line Items) Từ HubSpot & Thông Báo Trên Slack - Giảm Thiểu Lỗi & Tiết Kiệm Thời Gian"
description: "Workflow này tự động sao chép tất cả chi tiết (line items) từ hợp đồng đã hoàn thành (won deal) sang hợp đồng mới trong HubSpot, đồng thời gửi thông báo thành công lên Slack. Giúp doanh nghiệp loại bỏ công việc thủ công, giảm thiểu sai sót và tối ưu quy trình bán hàng."
slug: "tieu-dong-hoa-sao-chep-line-items-hubspot-slack"
tags: [n8n, automation, hubspot, slack, sales, no-code]
keywords: [tự động hóa hubspot, sao chép line items, thông báo slack, workflow hubspot, giảm thiểu lỗi bán hàng, tự động hóa bán hàng]
---

# 🚀 **Tự Động Hóa Sao Chép Chi Tiết Hợp Đồng (Line Items) Từ HubSpot & Thông Báo Trên Slack**

## **🔍 Nỗi Đau Của Các Sếp: Sao Chép Chi Tiết Hợp Đồng Thủ Công Làm Giảm Sản Xuất & Tăng Lỗi**
Hàng ngày, các sếp bán hàng phải **tốn thời gian thủ công sao chép chi tiết (line items) từ hợp đồng đã hoàn thành (won deal) sang hợp đồng mới** trong HubSpot. Điều này không chỉ **tốn nhiều thời gian** mà còn **mang lại nhiều lỗi** như:
- **Sai sót trong dữ liệu** (ví dụ: quên một sản phẩm, nhập sai số lượng).
- **Tập trung không tập trung** vào việc bán hàng thay vì quản lý dữ liệu.
- **Không có báo cáo tự động** để theo dõi tiến độ sao chép.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động sao chép tất cả chi tiết từ hợp đồng đã hoàn thành sang hợp đồng mới** (không cần code).
✅ **Gửi thông báo thành công lên Slack** để các sếp biết quy trình đã hoàn tất.
✅ **Giảm thiểu lỗi 100%** do không còn phụ thuộc vào con người.
✅ **Tiết kiệm thời gian** để các sếp tập trung vào việc bán hàng và phát triển khách hàng.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/tháng** cho đội bán hàng (không cần sao chép thủ công).
- **Giảm 90% lỗi dữ liệu** trong quá trình chuyển đổi hợp đồng.
- **Cá nhân hóa thông báo Slack** với chi tiết thành công (mã hợp đồng, sản phẩm, số lượng).
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Tích hợp hoàn hảo với HubSpot** (không cần API phức tạp).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản HubSpot** (đã cấu hình **Private App Token** và **OAuth 2.0 API**).
2. **Tài khoản Slack** (đã tạo **App Slack** và lấy **API Token**).
3. **Workflow HubSpot** (đã thiết lập **trigger khi hợp đồng chuyển sang trạng thái "Won"** và tạo hợp đồng mới).
4. **Webhook URL** từ n8n (sẽ được cung cấp khi import workflow).
5. **Dữ liệu mẫu** (nếu muốn test trước khi kích hoạt).
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/2367](https://n8n.io/workflows/2367) (chọn **Export as JSON**).
2. **Mở n8n Editor** (trên máy chủ tự host hoặc n8n.io).
3. **Nhấp vào "Import"** và chọn file JSON vừa tải.
4. **Chờ workflow được import hoàn tất** (n8n sẽ tự động tạo các node).

#### **Cách 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ file export.
2. **Mở n8n Editor** → **Nhấp vào "Import"** → **Chọn "Paste JSON"**.
3. **Xác nhận import** và tiếp tục cấu hình.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **7 node chính**, mỗi node đều cần cấu hình cẩn thận. Dưới đây là hướng dẫn chi tiết:

#### **🔹 Node 1: Webhook (Trigger)**
- **Chức năng:** Nhận dữ liệu từ HubSpot khi hợp đồng chuyển sang trạng thái "Won".
- **Cấu hình:**
  - **Key Parameters:**
    - `path`: Giá trị mặc định là `833df60e-a78f-4a59-8244-9694f27cf8ae` (có thể thay đổi nếu muốn).
    - **Lưu ý:** Nếu thay đổi `path`, các sếp **phải cập nhật trong HubSpot Workflow** (trong bước **Send Webhook**).
  - **Credentials:** Không cần (n8n sẽ tự động nhận dữ liệu từ URL webhook).

#### **🔹 Node 2: Set (Retrieve deals Ids)**
- **Chức năng:** Nhận **ID của hợp đồng đã hoàn thành (`deal_id_won`)** và **ID của hợp đồng mới (`deal_id_create`)** từ payload webhook.
- **Cấu hình:**
  - **Set `deal_id_won` và `deal_id_create`** từ dữ liệu truyền vào (n8n sẽ tự động lấy từ query parameters của webhook).

#### **🔹 Node 3 & 4: HTTP Request (Lấy Line Items & SKUs)**
- **Chức năng:** Lấy **tất cả chi tiết (line items) của hợp đồng đã hoàn thành** và **trích xuất SKU của từng sản phẩm**.
- **Cấu hình:**
  - **Credentials:** Chọn `hubspotAppToken` (đã cấu hình trước trong n8n).
  - **URL Request:**
    ```http
    https://api.hubapi.com/crm/v3/objects/line_items?archived=false&properties=amount,product_id,quantity,sku&filter=deal_id={{$node["Retrieve deals Ids"].json["deal_id_won"]}}
    ```
  - **Method:** `GET`
  - **Headers:**
    ```json
    {
      "Authorization": "Bearer {{$credentials["hubspotAppToken"].token}}",
      "Content-Type": "application/json"
    }
    ```
  - **Lưu ý:** Nếu API trả về lỗi, kiểm tra **token HubSpot** và **ID hợp đồng** có đúng không.

#### **🔹 Node 5: HTTP Request (Lấy Product IDs từ SKUs)**
- **Chức năng:** Từ danh sách SKUs, lấy **Product ID** tương ứng để tạo line items mới.
- **Cấu hình:**
  - **Credentials:** Chọn `hubspotAppToken`.
  - **URL Request:**
    ```http
    https://api.hubapi.com/crm/v3/objects/products?archived=false&properties=name,sku&filter=sku={{$node["Get batch SKUs from line items"].json[0].sku}}
    ```
  - **Method:** `GET`
  - **Headers:** Giống như Node 3.
  - **Lưu ý:** Nếu có nhiều SKU, cần **lặp lại request** cho từng SKU (n8n sẽ tự động xử lý).

#### **🔹 Node 6: HTTP Request (Tạo Line Items Mới)**
- **Chức năng:** Tạo **line items mới** cho hợp đồng mới (`deal_id_create`) với dữ liệu từ hợp đồng cũ.
- **Cấu hình:**
  - **Credentials:** Chọn `hubspotAppToken`.
  - **URL Request:**
    ```http
    https://api.hubapi.com/crm/v3/objects/line_items
    ```
  - **Method:** `POST`
  - **Body (JSON):**
    ```json
    {
      "properties": {
        "deal_id": "{{$node["Retrieve deals Ids"].json["deal_id_create"]}}",
        "product_id": "{{$node["Get Batch Product IDs by SKUs"].json[0].id}}",
        "quantity": "{{$node["Get deal won line items"].json[0].quantity}}",
        "amount": "{{$node["Get deal won line items"].json[0].amount}}"
      }
    }
    ```
  - **Headers:**
    ```json
    {
      "Authorization": "Bearer {{$credentials["hubspotAppToken"].token}}",
      "Content-Type": "application/json"
    }
    ```
  - **Lưu ý:** Nếu tạo nhiều line items, cần **lặp lại request** cho từng sản phẩm.

#### **🔹 Node 7: Slack (Thông Báo Thành Công)**
- **Chức năng:** Gửi **thông báo thành công** lên Slack với chi tiết:
  - Mã hợp đồng cũ và mới.
  - Danh sách sản phẩm đã sao chép.
- **Cấu hình:**
  - **Credentials:** Chọn `slackApi` (đã cấu hình trước trong n8n).
  - **Message:**
    ```json
    {
      "text": "✅ **Tự động sao chép line items thành công!**",
      "blocks": [
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "*Hợp đồng cũ:* <{{$node["Retrieve deals Ids"].json["deal_id_won"]}|Won Deal ID> \n*Hợp đồng mới:* <{{$node["Retrieve deals Ids"].json["deal_id_create"]}|New Deal ID>"
          }
        },
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "*Danh sách sản phẩm đã sao chép:*"
          }
        },
        {
          "type": "section",
          "fields": [
            {
              "type": "mrkdwn",
              "text": "*Sản phẩm:* `{{$node["Get deal won line items"].json[0].product_name}}`\n*SKU:* `{{$node["Get deal won line items"].json[0].sku}}`\n*Số lượng:* `{{$node["Get deal won line items"].json[0].quantity}}`"
            }
          ]
        }
      ]
    }
    ```
  - **Lưu ý:** Nếu muốn **thông báo chi tiết hơn**, các sếp có thể **lặp lại message** cho từng sản phẩm.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run (Kiểm Tra Trước Khi Kích Hoạt)**
   - Nhấp vào **button "Run"** trên node **Webhook** và nhập dữ liệu mẫu (ví dụ: `deal_id_won=123456789&deal_id_create=987654321`).
   - Kiểm tra **Slack** xem thông báo có xuất hiện không.
   - Kiểm tra **HubSpot** xem line items đã được sao chép chưa.

2. **Bật Active Workflow**
   - Sau khi test thành công, **nhấp vào "Active"** trên tab **Workflow**.
   - **Xem log** để theo dõi quá trình hoạt động.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Thêm Log Lịch Sử Sao Chép**
   - Sử dụng **node `stickyNote`** để lưu **lịch sử sao chép** (ví dụ: ngày giờ, người thực hiện, danh sách sản phẩm).
   - **Cách làm:** Thêm node `stickyNote` sau node **Slack** và lưu dữ liệu vào một **Google Sheet** hoặc **Notion Database**.

2. **Gửi Báo Cáo Định Kỳ**
   - Sử dụng **node `setInterval`** để **gửi báo cáo tổng hợp** (ví dụ: số lượng hợp đồng đã sao chép trong tháng) lên Slack hoặc Email.
   - **Cách làm:**
     ```json
     {
       "name": "Send Monthly Report",
       "type": "setInterval",
       "options": {
         "interval": "30 days"
       }
     }
     ```

3. **Kết Nối Với Email (Thay Thế Slack)**
   - Nếu không muốn dùng Slack, có thể **thay thế node Slack bằng node `email`** (ví dụ: Gmail, SendGrid).
   - **Cấu hình:**
     - **Credentials:** Chọn `emailApi` (đã cấu hình SMTP).
     - **Subject:** `📊 Tự động sao chép line items thành công - Deal #{{$node["Retrieve deals Ids"].json["deal_id_create"]}}`
     - **Body:** Nội dung HTML tương tự như Slack.

4. **Xử Lý Lỗi Hiệu Quả**
   - Thêm **node `if`** để **kiểm tra lỗi** và gửi **thông báo lỗi** lên Slack/Email.
   - **Cách làm:**
     ```json
     {
       "name": "Check for Errors",
       "type": "if",
       "options": {
         "condition": "{{$node["Create Batch line items based on productId and associate to deals"].error}}"
       }
     }
     ```

5. **Tích Hợp Với CRM Khác (Zoho, Pipedrive)**
   - Nếu doanh nghiệp dùng **Zoho CRM** hoặc **Pipedrive**, có thể **thay thế API HubSpot** bằng API của CRM đó.
   - **Cách làm:** Sử dụng **node `httpRequest`** với URL API của CRM mới và **credentials** tương ứng.
:::

---

## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp bán hàng khỏi công việc **sao chép thủ công**, đồng thời **giảm thiểu lỗi** và **tối ưu quy trình bán hàng**. Với **tự động hóa 100% không cần code**, các sếp có thể:
✔ **Tiết kiệm 5-10 giờ/tháng**.
✔ **Giảm 90% lỗi dữ liệu**.
✔ **Tập trung vào việc bán hàng** thay vì quản lý dữ liệu.

**🚀 Hãy áp dụng ngay workflow này và thấy sự khác biệt trong hiệu suất bán hàng của mình!**

---
:::note[CHÚ Ý CUỐI CUNG]
- **Nếu gặp lỗi API HubSpot**, kiểm tra lại **token OAuth 2.0** và **quyền truy cập** của Private App.
- **Nếu Slack không nhận thông báo**, kiểm tra lại **API Token** và **channel** đã cấu hình.