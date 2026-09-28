---
title: "🚀 Tự Động Hóa Tìm Kiếm Khách Hàng HubSpot Trên Slack – Giúp Đội Ngũ Sales & Support Tiết Kiệm 30% Thời Gian"
description: "Workflow này tự động tra cứu thông tin khách hàng từ HubSpot qua Slack chỉ bằng một lệnh `/hubspot-contact-lookup`. Giúp đội ngũ Sales & Support nhanh chóng tìm kiếm thông tin chi tiết (email, ID, công ty, deal stage) mà không cần chuyển đổi giữa các tab, tiết kiệm thời gian và giảm sai sót."
slug: "tieu-dong-hoa-tim-kiem-khach-hang-hubspot-tren-slack"
tags: [n8n, automation, HubSpot, Slack, CRM, no-code, sales-automation, support-automation]
keywords: [n8n workflow HubSpot Slack, tự động hóa tìm kiếm khách hàng, tra cứu thông tin khách hàng nhanh chóng, tự động hóa sales support, n8n tự động hóa CRM]
---

# 🚀 **Tự Động Hóa Tìm Kiếm Khách Hàng HubSpot Trên Slack – Giải Pháp "1 Lệnh, Thông Tin Ngay"**

### **Nỗi Đau Của Đội Ngũ Sales & Support**
Hàng ngày, các sếp phải:
- **Chuyển đổi liên tục** giữa Slack và HubSpot để tra cứu thông tin khách hàng.
- **Nhập sai thông tin** do phải copy-paste nhiều lần giữa các hệ thống.
- **Mất thời gian** tìm kiếm thông tin chi tiết (email, ID, công ty, deal stage) khi khách hàng gọi hoặc gửi tin nhắn.
- **Không cập nhật kịp thời** khi thông tin khách hàng thay đổi trên HubSpot.

**Workflow này giải quyết tất cả đó!** Chỉ cần gõ một lệnh Slack (`/hubspot-contact-lookup`), hệ thống sẽ tự động tra cứu và trả về thông tin khách hàng **trong vòng 2 giây**, giúp các sếp **tiết kiệm 30% thời gian** và **giảm sai sót**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng. Dưới đây là 2 lựa chọn tối ưu:
👉 **[VPS TinoHost – Giảm 39% với mã VPSN8N](https://tino.vn/vps-n8n?affid=388)**
   - **Tính năng**: 2 CPU, 2GB RAM, SSD 50GB, IP riêng, hỗ trợ Docker.
   - **Giá**: ~150k/tháng (giảm từ 250k).
   - **Ưu điểm**: Hỗ trợ kỹ thuật 24/7, tốc độ cao, phù hợp cho workflow CRM.

👉 **[VPS Xeon 4GB – Chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
   - **Tính năng**: Xeon, 4GB RAM, 100GB SSD, IP riêng.
   - **Ưu điểm**: Tốc độ xử lý nhanh, phù hợp cho workflow AI + CRM.
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 30% thời gian** tra cứu khách hàng (không cần chuyển đổi giữa Slack và HubSpot).
✅ **Giảm sai sót** do tự động hóa tra cứu thông tin chính xác từ HubSpot.
✅ **Cung cấp thông tin toàn diện** (tên, email, số điện thoại, công ty, deal stage, lịch sử tương tác).
✅ **Hoạt động liên tục 24/7** (không phụ thuộc vào giờ làm việc của nhân viên).
✅ **Tích hợp Slack** – thông tin khách hàng được gửi ngay vào channel hoặc DM, không cần mở HubSpot.
✅ **Dễ dàng mở rộng** – có thể kết nối với nhiều hệ thống khác (Zapier, Google Sheets, Notion...).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản HubSpot** (cần **API Token** để kết nối).
   - **Cách lấy API Token**:
     - Đăng nhập HubSpot → **Settings (Cài đặt)** → **Integrations (Tích hợp)** → **API Keys**.
     - Sao chép **Private App Token** và đặt tên là `hubspotAppToken` trong n8n.
2. **Tài khoản Slack** (cần **API Token** để gửi thông báo).
   - **Cách lấy API Token**:
     - Đăng nhập Slack → **Settings (Cài đặt)** → **Apps & Integrations** → **Basic Information** → **Install App** (cho app n8n).
     - Sao chép **Bot User OAuth Token** và đặt tên là `slackApi` trong n8n.
3. **Slash Command trên Slack** (để người dùng gõ lệnh `/hubspot-contact-lookup`).
   - **Cách thiết lập**:
     - Trên Slack, gõ `/slash-commands create` → Nhập:
       - **Command**: `/hubspot-contact-lookup`
       - **Request URL**: `https://[your-n8n-domain]/hubspot-contact-lookup` (địa chỉ Webhook của workflow).
       - **Description**: "Tra cứu thông tin khách hàng HubSpot."
       - **Short description**: "Nhập email hoặc ID khách hàng."
     - Chọn **Save Changes**.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
**Cách 1: Import từ file JSON**
- Tải workflow từ [đây](https://n8n.io/workflows/8108) (n8n.io) hoặc [link gốc](https://n8n.io/workflows/8108).
- Trên **n8n Editor**, nhấn **Import** → Chọn file JSON → Nhấn **Import**.

**Cách 2: Copy/Paste JSON**
- Trên trang workflow [n8n.io/workflows/8108](https://n8n.io/workflows/8108), nhấn **Export** → Copy toàn bộ JSON.
- Trên **n8n Editor**, nhấn **Import** → Chọn **Paste JSON** → Nhấn **Import**.

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp **phải cấu hình** các node quan trọng sau:

##### **🌐 Node: Incoming Slash Command (Webhook)**
- **Không cần chỉnh sửa** nếu đã thiết lập Slash Command trên Slack như hướng dẫn trên.
- **Path**: `hubspot-contact-lookup` (đã được cấu hình sẵn).
- **HTTP Method**: `POST` (không thay đổi).

##### **✂️ Node: Parse Search Input (Code)**
- **Không cần chỉnh sửa** vì đã sử dụng regex để phân biệt email và ID.
- **Nếu muốn mở rộng**:
  - Thêm logic kiểm tra thêm trường hợp (ví dụ: tra cứu theo tên).
  - Ví dụ mã JavaScript:
    ```javascript
    // Thêm vào nếu cần tra cứu theo tên
    if (!isEmail && !isHubSpotId && message.includes("tên")) {
      return { searchType: "name", value: message.trim() };
    }
    ```

##### **📧 Node: Search Contact by Email (HubSpot)**
- **Credentials**: Chọn `hubspotAppToken` (đã đặt trước).
- **Operation**: `search` (không thay đổi).
- **Filter**: `{ email: "$input" }` (đã tự động hóa từ node Code).

##### **🆔 Node: Get Contact by ID (HubSpot)**
- **Credentials**: Chọn `hubspotAppToken`.
- **Operation**: `get` (không thay đổi).
- **ID**: `$node["Parse Search Input"].json["value"]` (đã tự động lấy từ input).

##### **📝 Node: Format Contact Info (ID Search) & Format Contact Info (Email Search)**
- **Không cần chỉnh sửa** vì đã định dạng thông tin theo mẫu Slack.
- **Nếu muốn thay đổi định dạng**:
  - Mở node **Code** → Sửa phần `return` để thay đổi cách hiển thị.
  - Ví dụ:
    ```javascript
    // Thay đổi cách hiển thị deal stage
    const dealStage = contact.properties.deal_stage || "Không có";
    return {
      text: `*Khách hàng:* ${contact.properties.first_name} ${contact.properties.last_name}\n` +
            `*Email:* ${contact.properties.email}\n` +
            `*Công ty:* ${contact.properties.company || "Không có"}\n` +
            `*Trạng thái giao dịch:* ${dealStage}\n` +
            `*Số điện thoại:* ${contact.properties.phone || "Không có"}`,
      attachments: [
        {
          text: `Thông tin chi tiết:\n` +
                `ID HubSpot: ${contact.id}\n` +
                `Lịch sử tương tác: ${contact.properties._last_activity_date || "Không có"}`
        }
      ]
    };
    ```

##### **💬 Node: Send Contact Info to Slack**
- **Credentials**: Chọn `slackApi`.
- **Channel**: Nhập `#general` (hoặc channel cụ thể của team).
- **Text**: `$node["Format Contact Info (ID Search)"].json.text` (hoặc `$node["Format Contact Info (Email Search)"].json.text`).
- **Attachments**: `$node["Format Contact Info (ID Search)"].json.attachments` (hoặc tương ứng với email).

---

#### **3. Kích Hoạt ⚡️**
Sau khi cấu hình xong:
1. **Test Run** với dữ liệu mẫu:
   - Gõ lệnh Slack: `/hubspot-contact-lookup email@example.com` (thay bằng email thật).
   - Kiểm tra kết quả trên Slack.
2. **Bật Active**:
   - Nhấn **Active** trên workflow.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Google Sheets/Notion để lưu lịch sử tra cứu**
   - Thêm node **Google Sheets** hoặc **Notion** sau node **Send to Slack** để ghi lại tất cả các lần tra cứu.
   - Ví dụ:
     ```json
     {
       "name": "📊 Log Search to Google Sheets",
       "type": "googleSheets",
       "credentials": ["googleSheetsApi"],
       "keyParameters": {
         "sheetName": "HubSpot Search Log",
         "values": [
           {
             "email": "$node["Parse Search Input"].json.value",
             "timestamp": "$node["Parse Search Input"].json.timestamp",
             "contactId": "$node["Get Contact by ID"].json.json.id"
           }
         ]
       }
     }
     ```

2. **Gửi thông báo báo cáo định kỳ cho team**
   - Thêm node **Set Interval** (n8n) để gửi báo cáo hàng ngày về:
     - Số lượng tra cứu.
     - Khách hàng được tra cứu nhiều nhất.
     - Thông tin khách hàng mới nhất.
   - Ví dụ:
     ```json
     {
       "name": "📅 Send Daily Report",
       "type": "setInterval",
       "keyParameters": {
         "interval": "1d"
       }
     }
     ```

3. **Tích hợp với Zapier để mở rộng chức năng**
   - Nếu cần tra cứu khách hàng từ **email khác** (ví dụ: Gmail, Outlook), có thể kết nối với **Zapier** và gọi Webhook của n8n.
   - Cách làm:
     - Tạo **Zapier Trigger** (ví dụ: khi có email mới).
     - Gửi **Webhook** đến `https://[your-n8n-domain]/hubspot-contact-lookup` với payload:
       ```json
       {
         "text": "email@example.com"
       }
       ```

4. **Tự động tra cứu khi có tin nhắn mới trên Slack**
   - Thêm node **Slack Incoming Webhook** để lắng nghe tin nhắn chứa từ khóa (ví dụ: "khách hàng", "deal").
   - Ví dụ:
     ```json
     {
       "name": "🔍 Listen for Keywords in Slack",
       "type": "slack",
       "credentials": ["slackApi"],
       "keyParameters": {
         "operation": "listen",
         "keyword": "khách hàng"
       }
     }
     ```

---

### 📌 **Kết Luận**
Workflow **Tự Động Hóa Tìm Kiếm Khách Hàng HubSpot Trên Slack** là **giải pháp hoàn hảo** để đội ngũ Sales & Support **tiết kiệm thời gian, giảm sai sót và tăng hiệu suất**. Với chỉ **một lệnh Slack**, các sếp có thể tra cứu thông tin khách hàng **ngay lập tức**, không cần chuyển đổi giữa các hệ thống.

**Hành động ngay hôm nay!**
1. **Cài đặt VPS** (nếu chưa có) và **self-host n8n**.
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test Run** và **bật Active** để bắt đầu tự động hóa!

**Nếu có vấn đề**, các sếp có thể:
- **Trả lời comment** dưới bài viết này.
- **Gửi tin nhắn** cho tôi trên Slack/Discord để hỗ trợ kỹ thuật.

**Chúc các sếp thành công với tự động hóa!** 🚀