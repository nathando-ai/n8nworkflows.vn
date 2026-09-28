---
title: "🚀 Tự Động Hóa Gửi Lại Thông Báo Giữa Kỳ Hợp Đồng từ HubSpot qua Gmail & Slack (Không Cần Code)"
description: "Giải pháp tự động hóa hoàn toàn để theo dõi và nhắc nhở khách hàng về thời hạn kết thúc hợp đồng (30/60/90 ngày) qua email cá nhân hóa và cảnh báo Slack, đồng thời tạo nhiệm vụ theo dõi trong ClickUp. Tiết kiệm 10+ giờ/tháng cho bộ phận CRM và giảm thiểu rủi ro hợp đồng hết hạn."
slug: "tu-dong-hoa-gui-lai-thong-bao-gia-ky-hop-dong-hubspot"
tags: [n8n, automation, crm, hubspot, gmail, slack, clickup, no-code, sales]
keywords: [tự động hóa hợp đồng hết hạn, nhắc nhở giữa kỳ hợp đồng, workflow n8n hubspot, gửi email tự động từ hubspot, cảnh báo slack hợp đồng, tự động hóa crm không code]
---

# 🚀 **Tự Động Hóa Gửi Lại Thông Báo Giữa Kỳ Hợp Đồng: Từ HubSpot → Gmail + Slack (Không Cần Code)**

### **Nỗi Đau Của Các Sếp CRM**
Hàng ngày, bộ phận CRM phải:
- **Quét thủ công** danh sách hợp đồng sắp hết hạn trong HubSpot.
- **Gửi email nhắc nhở** một cách rời rạc, dễ bỏ quên hoặc không đồng bộ.
- **Phản hồi chậm** khi hợp đồng hết hạn vì thiếu cảnh báo kịp thời.
- **Tốn thời gian** để tạo nhiệm vụ theo dõi trong ClickUp hoặc Trello.

**Kết quả?** Hợp đồng hết hạn không được xử lý kịp thời, mất khách hàng, và doanh thu bị ảnh hưởng. **Công việc này hoàn toàn có thể tự động hóa!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao, không lag)
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10+ giờ/tháng** cho bộ phận CRM (không cần quét danh sách thủ công).
✅ **Nhắc nhở chính xác** khách hàng về thời hạn hợp đồng (30/60/90 ngày) qua email cá nhân hóa.
✅ **Cảnh báo kịp thời** cho team nội bộ qua Slack (không bỏ lỡ hợp đồng nào).
✅ **Tạo nhiệm vụ tự động** trong ClickUp để theo dõi hành động tiếp theo.
✅ **Giảm rủi ro hợp đồng hết hạn** và tăng tỷ lệ tái ký hợp đồng.
✅ **Hoạt động liên tục** (không phụ thuộc vào giờ làm việc của nhân viên).
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| Dịch vụ          | Thông Tin Cần Thiết                                                                 | Làm Thế Nào Để Lấy?                                                                 |
|-------------------|------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| **HubSpot**       | API Key + Access Token (Deals & Contacts)                                          | [Tạo API Key HubSpot](https://developers.hubspot.com/docs/api/private-apps)            |
| **Gmail**         | Email & Password (hoặc App Password nếu 2FA bật)                                   | [Cài đặt App Password](https://myaccount.google.com/apppasswords)                     |
| **Slack**         | Token OAuth (Bot User) + Channel ID                                                | [Tạo Bot Slack](https://api.slack.com/apps) + [Tìm Channel ID](https://api.slack.com/docs/message-formatting) |
| **ClickUp**       | API Key + Workspace ID + Space ID                                                   | [Tạo API Key ClickUp](https://clickup.com/api)                                       |

### **2. Thiết Lập Trước**
- **HubSpot**: Chắc chắn các hợp đồng có trường `expiration_date` được cập nhật chính xác.
- **Gmail**: Đảm bảo email gửi không bị đánh dấu là spam (thiết lập SPF/DKIM nếu cần).
- **Slack**: Chọn **channel** phù hợp để gửi cảnh báo (ví dụ: `#contract-renewals`).
- **ClickUp**: Chọn **list/task template** để tạo nhiệm vụ theo dõi (ví dụ: "Follow-up Contract Renewal").

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương Pháp 1: Từ File JSON**
1. **Tải workflow** từ [n8n.io/workflows/14155](https://n8n.io/workflows/14155) (chọn **Export JSON**).
2. **Trên n8n Editor**:
   - Nhấn **Import** (icon mũi tên vòng tròn ở góc trên bên phải).
   - Chọn file JSON vừa tải và nhấn **Import**.
3. **Kích hoạt workflow** bằng cách bật **Active** (switch ở góc trên bên phải).

#### **Phương Pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n.io/workflows/14155](https://n8n.io/workflows/14155).
2. **Trên n8n Editor**:
   - Nhấn **Import** → **Paste JSON**.
   - Dán và nhấn **Import**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này có **13 node**, nhưng **các bước quan trọng nhất** cần cấu hình kỹ lưỡng:

#### **🔹 Node 1: Schedule Trigger (Đặt Lịch Trình Chạy)**
- **Cấu hình**:
  - **Cron Expression**: `0 0 1,11,21 * *` (chạy hàng tháng vào ngày 1, 11, 21 để bắt đầu quá trình lọc hợp đồng).
  - **Timezone**: Chọn timezone phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).
- **Lưu ý**:
  - Nếu muốn chạy **hàng ngày**, thay đổi thành `0 0 * * *`.
  - **Không chạy quá thường** để tránh tải quá nhiều dữ liệu từ HubSpot.

#### **🔹 Node 2: Get All Deals (Lấy Tất Cả Hợp Đồng)**
- **Cấu hình**:
  - **Operation**: `getAll`
  - **Resource**: `deal`
  - **Credentials**: Chọn **HubSpot** đã cấu hình trước.
- **Lưu ý**:
  - HubSpot có **limit API calls**, nên **không lọc quá nhiều dữ liệu** trong một lần chạy.
  - Nếu có nhiều hợp đồng, **sử dụng pagination** (nếu cần, thêm node `httpRequest` để phân trang).

#### **🔹 Node 3: Filter Deals (Lọc Hợp Đồng Sắp Hết Hạn)**
- **Cấu hình trong Code Node**:
  ```javascript
  // Lọc hợp đồng hết hạn trong 30, 60, 90 ngày
  const today = new Date();
  const deals = $input.all();

  const filteredDeals = deals.filter(deal => {
    const expiryDate = new Date(deal.properties.expiration_date);
    const daysLeft = Math.ceil((expiryDate - today) / (1000 * 60 * 60 * 24));

    return (
      (daysLeft <= 30 && daysLeft > 0) ||
      (daysLeft <= 60 && daysLeft > 30) ||
      (daysLeft <= 90 && daysLeft > 60)
    );
  });

  return { json: filteredDeals };
  ```
- **Lưu ý**:
  - **Trường `expiration_date`** trong HubSpot phải là **date format ISO** (ví dụ: `2024-12-31`).
  - Nếu dữ liệu không đúng định dạng, **cần chỉnh sửa trong Code Node**.

#### **🔹 Node 4: Loop Over Deals (Lặp Qua Mỗi Hợp Đồng)**
- **Cấu hình**:
  - **Batch Size**: 5-10 (tránh quá tải API).
  - **Merge Node**: Đảm bảo dữ liệu được **gộp từ các batch** trước khi xử lý tiếp.

#### **🔹 Node 5: Fetch Associated Contact (Lấy Thông Tin Khách Hàng)**
- **Cấu hình trong HTTP Request**:
  - **Method**: `GET`
  - **URL**: `https://api.hubapi.com/crm/v3/objects/contacts/{contactId}`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer {{$credentials.hubspot_api_key}}",
      "Content-Type": "application/json"
    }
    ```
  - **Query Parameters**:
    ```json
    {
      "properties": ["email", "firstName", "lastName"]
    }
    ```
- **Lưu ý**:
  - **Trường `contactId`** được lấy từ **hợp đồng** trong HubSpot (thường là `hs_object_id`).
  - Nếu **không có contactId**, **cần thêm node `httpRequest`** để tìm kiếm contact từ email.

#### **🔹 Node 6: Switch (Phân Luồng Theo Thời Gian Hết Hạn)**
- **Cấu hình**:
  - **Condition 1**: `daysLeft <= 30` → Gửi email **30 ngày trước**.
  - **Condition 2**: `daysLeft <= 60 && daysLeft > 30` → Gửi email **60 ngày trước**.
  - **Condition 3**: `daysLeft <= 90 && daysLeft > 60` → Gửi email **90 ngày trước**.
- **Lưu ý**:
  - **Thêm trường `daysLeft`** vào dữ liệu trước khi vào Switch Node (sử dụng **Code Node** nếu cần).

#### **🔹 Node 7-9: 30 Day Mail / 60 Day Mail / 90 Day Mail (Gửi Email)**
- **Cấu hình chung**:
  - **Credentials**: Chọn **Gmail** đã cấu hình.
  - **Subject**:
    - **30 ngày trước**: `📅 Thông Báo: Hợp Đồng Sắp Hết Hạn (30 Ngày) - {{deal.name}}`
    - **60 ngày trước**: `📅 Thông Báo: Hợp Đồng Sắp Hết Hạn (60 Ngày) - {{deal.name}}`
    - **90 ngày trước**: `📅 Thông Báo: Hợp Đồng Sắp Hết Hạn (90 Ngày) - {{deal.name}}`
  - **Body (HTML)**:
    ```html
    <p>Chào {{contact.firstName}},</p>
    <p>Hợp đồng của bạn với {{deal.name}} sẽ hết hạn vào ngày <strong>{{deal.properties.expiration_date}}</strong>.</p>
    <p>Vui lòng liên hệ với chúng tôi để tái ký hợp đồng trước khi hết hạn.</p>
    <p>Trân trọng,</p>
    <p>Team {{deal.properties.company}}</p>
    ```
- **Lưu ý**:
  - **Thêm biến `{{deal.name}}` và `{{contact.firstName}}`** từ dữ liệu trước đó.
  - **Kiểm tra email mẫu** trước khi gửi thật.

#### **🔹 Node 10: Notify Account Manager (Cảnh Báo Slack)**
- **Cấu hình**:
  - **Channel**: Chọn **#contract-renewals** (hoặc channel tương tự).
  - **Message**:
    ```json
    {
      "text": `:bell: Hợp Đồng Sắp Hết Hạn - {{deal.name}} ({{daysLeft}} ngày trước)`,
      "attachments": [
        {
          "title": "Chi Tiết Hợp Đồng",
          "title_link": "https://app.hubspot.com/deals/{{deal.id}}",
          "fields": [
            { "title": "Khách Hàng", "value": "{{contact.firstName}} {{contact.lastName}}", "short": true },
            { "title": "Ngày Hết Hạn", "value": "{{deal.properties.expiration_date}}", "short": true },
            { "title": "Ngày Gửi Email", "value": "{{$node["30 day mail"].timestamp}}", "short": true }
          ]
        }
      ]
    }
    ```
- **Lưu ý**:
  - **Thêm `daysLeft`** vào dữ liệu trước khi vào Slack Node (sử dụng **Code Node**).
  - **Link HubSpot** phải đúng định dạng (thường là `https://app.hubspot.com/deals/{{deal.id}}`).

#### **🔹 Node 11: Create Follow-up Task (Tạo Nhiệm Vụ ClickUp)**
- **Cấu hình**:
  - **API Key**: Chọn **ClickUp** đã cấu hình.
  - **Endpoint**: `https://api.clickup.com/api/v2/list/{listId}/task`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer {{$credentials.clickup_api_key}}",
      "Content-Type": "application/json"
    }
    ```
  - **Body**:
    ```json
    {
      "name": "Follow-up: Renewal - {{deal.name}} ({{contact.firstName}})",
      "content": "Hợp đồng sắp hết hạn vào {{deal.properties.expiration_date}}. Liên hệ khách hàng để tái ký.",
      "assignee": "{{account_manager_id}}", // Thay bằng ID người quản lý
      "list": "{{listId}}", // Thay bằng ID list trong ClickUp
      "due_date": "{{due_date}}" // Ngày hết hạn hợp đồng
    }
    ```
- **Lưu ý**:
  - **Thêm `account_manager_id`** (ID người quản lý trong ClickUp).
  - **`listId`** là ID của **list** trong ClickUp (ví dụ: `123456789`).
  - **`due_date`** phải là định dạng `YYYY-MM-DD`.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** (kiểm tra trước khi chạy thật):
   - Chọn **Run Once** (icon play ở góc trên bên phải).
   - Kiểm tra **email mẫu**, **cảnh báo Slack**, và **nhiệm vụ ClickUp**.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật switch Active** ở góc trên bên phải.

---

## ✍