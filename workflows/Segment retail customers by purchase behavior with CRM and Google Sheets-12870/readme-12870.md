---
title: "🚀 **Tự Động Phân Loại Khách Hàng Sỉ Theo Hành Vi Mua Hàng - CRM + Google Sheets (N8n)**
description: "Workflow tự động phân loại khách hàng sỉ thành VIP, mới, tái mua hoặc không hoạt động dựa trên hành vi mua hàng, đồng bộ với CRM và Google Sheets. Giúp doanh nghiệp tiết kiệm thời gian, tối ưu chiến dịch marketing và tăng doanh thu từ khách hàng trung thành."
slug: "tu-dong-phan-loai-khach-hang-si-theo-hanh-vi-mua-hang"
tags: [n8n, automation, CRM, Google Sheets, phân loại khách hàng, AI, no-code]
keywords: [n8n workflow phân loại khách hàng, tự động hóa CRM, phân khúc khách hàng sỉ, Google Sheets + CRM, tối ưu marketing]
---

# 🚀 **Tự Động Phân Loại Khách Hàng Sỉ Theo Hành Vi Mua Hàng - CRM + Google Sheets**

## **🔍 Nỗi Đau Của Các Sếp: Phân Loại Khách Hàng Thủ Công Làm Giảm Doanh Thu**
Hàng ngày, các sếp phải **quét thủ công** danh sách khách hàng, tính toán số lần mua, tổng giá trị giao dịch, và phân loại họ thành các nhóm như *khách hàng mới*, *khách hàng tái mua*, *VIP*, hoặc *khách hàng không hoạt động*. Đây là công việc **tốn thời gian, dễ sai sót**, và **không thể thực hiện 24/7** như một hệ thống tự động.

Kết quả?
- **Không biết ai là khách hàng VIP** nên bỏ qua cơ hội bán thêm.
- **Không theo dõi khách hàng không hoạt động** dẫn đến mất doanh thu từ họ.
- **Không cá nhân hóa marketing**, khiến chiến dịch trở nên **rất tốn kém và hiệu quả thấp**.

**Workflow này giải quyết tất cả!** Nó **tự động phân loại khách hàng** dựa trên hành vi mua hàng, đồng bộ với **CRM** và **Google Sheets**, giúp các sếp **tiết kiệm thời gian, tối ưu chiến dịch marketing**, và **tăng doanh thu từ khách hàng trung thành**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
✅ **Tự động phân loại khách hàng** trong giây lát (không cần code).
✅ **Đồng bộ dữ liệu CRM** (HubSpot, Salesforce, Zoho…) để marketing tự động hóa.
✅ **Lưu lịch sử phân loại** trên Google Sheets để báo cáo và phân tích.
✅ **Tối ưu chiến dịch marketing** bằng cách biết chính xác khách hàng nào là VIP, mới, tái mua, hoặc không hoạt động.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản CRM** (HubSpot, Salesforce, Zoho CRM…) với **API Key** hoặc **URL API endpoint**.
✔ **Tài khoản Google Sheets** và **API Key OAuth2** của Google.
✔ **Webhook URL** từ hệ thống bán hàng (WooCommerce, Shopify, ERP…) để gửi dữ liệu khách hàng.
✔ **Dữ liệu mẫu** (JSON) của một đơn hàng hoặc sự kiện khách hàng để test.

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON** từ [n8n.io/workflows/12870](https://n8n.io/workflows/12870) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và **paste** vào **n8n Editor** (tab `Import`).

:::note[**Lưu ý quan trọng**]
- **Không sao chép toàn bộ JSON** từ link (n8n sẽ không nhận dạng được).
- **Chỉ copy phần JSON của workflow** (không bao gồm phần `output` hoặc metadata).
:::

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **11 node**, nhưng **các node quan trọng nhất** cần cấu hình kỹ là:

#### **🔹 Node Webhook: "Receive Customer Order or Update Event"**
- **Cấu hình**:
  - **Method**: `POST`
  - **Path**: `customer-segmentation` (không đổi)
  - **Credentials**: Không cần (sử dụng URL mặc định của n8n).
- **Lưu ý**:
  - **Cấu hình webhook trong hệ thống bán hàng** (WooCommerce, Shopify…) để gửi dữ liệu khách hàng đến URL này.
  - **Dữ liệu đầu vào phải có các trường**: `customerId`, `email`, `orderCount`, `lifetimeSpend`, `lastOrderDate`, `sourceSystem`.

#### **🔹 Node Google Sheets: "Append or update row in sheet"**
- **Cấu hình**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).
  - **Sheet Name**: Đặt tên sheet (ví dụ: `Customer_Segmentation_Log`).
  - **Columns**: Cần có các cột: `CustomerID`, `Email`, `Segment`, `OrderCount`, `LifetimeSpend`, `LastOrderDate`.
- **Lưu ý**:
  - **Tạo sheet mới** trong Google Drive trước khi chạy workflow.
  - **Không xóa cột** sau khi cấu hình, workflow sẽ tự động append/update dữ liệu.

#### **🔹 Node HTTP Request: "Sync Customer Segment to CRM"**
- **Cấu hình**:
  - **URL**: Điền **API endpoint** của CRM (ví dụ: `https://api.hubspot.com/crm/v3/objects/contacts`).
  - **Method**: `POST` (hoặc `PATCH` nếu cập nhật).
  - **Headers**:
    - `Content-Type`: `application/json`
    - `Authorization`: `Bearer {API_KEY_CRM}`
  - **Body**:
    ```json
    {
      "properties": {
        "email": "{{$node["Normalize Customer Segment Output"].json["email"]}}",
        "custom_properties": {
          "customer_segment": "{{$node["Normalize Customer Segment Output"].json["segment"]}}"
        }
      }
    }
    ```
- **Lưu ý**:
  - **Test API CRM** trước để đảm bảo dữ liệu đồng bộ đúng.
  - **Nếu CRM không hỗ trợ API**, có thể thay thế bằng **Slack/Email Notification** (xem phần **Mẹo & Gợi Ý Nâng Cao**).

#### **🔹 Node Switch: "Determine Customer Segment"**
- **Cấu hình**:
  - **Rule-based logic** đã được định sẵn:
    - **VIP**: `lifetimeSpend > 1000000` (1 triệu VNĐ) **và** `orderCount > 5`.
    - **Repeat Customer**: `orderCount > 1` **và** `lastOrderDate > 30 days ago`.
    - **New Customer**: `orderCount = 1`.
    - **Inactive Customer**: `lastOrderDate > 90 days ago`.
  - **Lưu ý**:
    - **Cập nhật ngưỡng** (`1000000`, `30 days`, `90 days`) theo chiến lược kinh doanh của các sếp.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run với dữ liệu mẫu**:
   - Gửi **payload JSON** mẫu từ Postman hoặc hệ thống bán hàng đến webhook.
   - Kiểm tra **Google Sheets** và **CRM** xem dữ liệu đã đồng bộ chưa.
   - **Dữ liệu mẫu**:
     ```json
     {
       "customerId": "CUST_123",
       "email": "khachhang@example.com",
       "orderCount": 3,
       "lifetimeSpend": 1500000,
       "lastOrderDate": "2024-05-10",
       "sourceSystem": "Shopify"
     }
     ```
2. **Bật Active workflow**:
   - Chuyển trạng thái từ `Inactive` sang `Active` trong n8n Editor.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Kết Nối với Slack/Telegram để Thông Báo**
- Thêm **node Slack/Telegram** sau node `Sync Customer Segment to CRM` để **thông báo khi phân loại thành công**.
- **Cấu hình**:
  - **Webhook URL** từ Slack/Telegram.
  - **Message template**:
    ```json
    {
      "text": "🚀 Khách hàng {{$node["Normalize Customer Segment Output"].json["email"]}} đã được phân loại thành: **{{$node["Normalize Customer Segment Output"].json["segment"]}}**"
    }
    ```

### **2. Lưu Log Chi Tiết vào Google Sheets**
- Thêm **node Google Sheets** mới để lưu **lịch sử phân loại chi tiết** (thời gian, người phân loại, lý do).
- **Cấu hình cột**:
  - `CustomerID`, `Email`, `Segment`, `Reason`, `Timestamp`, `ActionBy`.

### **3. Gửi Báo Cáo Định Kỳ qua Email**
- Sử dụng **node Email (SMTP)** hoặc **node Google Sheets + Zapier** để gửi **báo cáo tuần/month** về phân loại khách hàng.
- **Dữ liệu báo cáo**:
  - Số lượng VIP, Repeat, New, Inactive.
  - Tổng doanh thu từ mỗi nhóm.
  - Khách hàng không hoạt động trong 90 ngày.

### **4. Tích Hợp với AI để Tự Động Gợi Ý Chiến Dịch**
- Sử dụng **node LLM (n8n-nodes-ai)** để **tự động gợi ý chiến dịch marketing** cho từng nhóm khách hàng.
- **Ví dụ**:
  - **VIP**: "Gửi voucher 20% cho VIP".
  - **Repeat Customer**: "Gửi email khuyến mãi sản phẩm mới".
  - **Inactive Customer**: "Gửi email kích hoạt lại với ưu đãi đặc biệt".

---

## 📌 **Kết Luận: Áp Dụng Ngay & Tăng Doanh Thu!**
Workflow này **giải phóng thời gian** của các sếp khỏi công việc **phân loại khách hàng thủ công**, đồng thời **tối ưu hóa chiến dịch marketing** bằng cách biết chính xác **ai là khách hàng VIP**, **ai cần kích hoạt lại**, và **ai là khách hàng tái mua tiềm năng**.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với dữ liệu mẫu** để đảm bảo hoạt động.
3. **Bật Active** và **theo dõi kết quả** trên Google Sheets & CRM.
4. **Nâng cao** bằng cách kết nối Slack, Email, hoặc AI.

**Kết quả?** **Khách hàng được phân loại chính xác, marketing hiệu quả hơn, và doanh thu tăng lên!** 🚀

---
**💡 Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) và liên hệ **WeblineIndia** qua [website](https://www.weblineindia.com/) để hỗ trợ cấu hình chi tiết!