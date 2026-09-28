---
title: "🚀 Tự Động Hóa Tin Nhắn Chào Mừng WhatsApp Cho Lead Bán Hàng Với Google Sheets & Rapiwa - Không Cần Code!"
description: "Workflow này tự động gửi tin nhắn chào mừng cá nhân hóa đến lead bán hàng qua WhatsApp từ Google Sheets, kiểm tra số điện thoại, cập nhật trạng thái và hoạt động liên tục mỗi 5 phút. Giúp tiết kiệm thời gian, tăng tỷ lệ chuyển đổi và tối ưu hóa quy trình lead nurturing."
slug: "tieu-dong-hoa-tin-nhan-chao-mung-whatsapp-google-sheets-rapiwa"
tags: [n8n, automation, no-code, lead-nurturing, whatsapp-marketing, google-sheets, rapiwa, ai-multimodal]
keywords: [tự động hóa whatsapp, n8n workflow, gửi tin nhắn tự động, google sheets api, rapiwa api, lead nurturing, marketing automation, không cần code]
---

# 🚀 **Tự Động Hóa Tin Nhắn WhatsApp Chào Mừng Lead Bán Hàng Với Google Sheets & Rapiwa**

### **Giải pháp hoàn hảo cho các sếp bán hàng muốn tự động hóa tương tác với lead mà không cần viết một dòng code nào!**

---

### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần gửi tin nhắn thủ công, tự động hóa 100% quy trình.
- **Tăng tỷ lệ chuyển đổi**: Tin nhắn cá nhân hóa (chào tên lead) giúp tăng sự chú ý và tương tác.
- **Quản lý lead hiệu quả**: Cập nhật trạng thái (đã gửi, chưa gửi, số điện thoại không hợp lệ) trên Google Sheets.
- **Hoạt động liên tục**: Workflow chạy tự động mỗi 5 phút, không bỏ lỡ lead nào.
- **Tránh bị chặn**: Thiết kế với thời gian chờ giữa các tin nhắn để tránh bị WhatsApp hoặc Rapiwa cấm.
:::

---

### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Google Sheets**:
   - Tạo một bảng theo mẫu [đây](https://docs.google.com/spreadsheets/d/1amkVSIXrhOkf86YDYaddOcAamhUC4DlvFiSg3cpAH78/edit?usp=sharing) (chú ý cột `name` phải có **khoảng trắng ở cuối**).
   - Các cột bắt buộc:
     - `WhatsApp No` (số điện thoại lead).
     - `name` (tên lead, **có khoảng trắng ở cuối**).
     - `row_number` (số thứ tự hàng, có thể tự động sinh).
     - `status`, `check`, `validity` (để lưu trạng thái).
   - **Lưu ý**: Cột `check` phải được điền để workflow biết lead đó cần gửi tin nhắn.

2. **Credentials cho n8n**:
   - **Google Sheets OAuth2**: Cấu hình kết nối với tài khoản Google Sheets của bạn.
   - **Rapiwa Bearer Token**: Nhận từ [Rapiwa](https://rapiwa.com/) để gửi tin nhắn WhatsApp.

3. **WhatsApp Account**:
   - Tài khoản cá nhân hoặc doanh nghiệp (không phải là tài khoản chính thức của Meta).

4. **n8n Self-hosted**:
   - Để workflow chạy 24/7 ổn định, các sếp nên cài n8n trên **VPS riêng** (self-hosted).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---

### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/8572) hoặc copy toàn bộ JSON từ canvas.
- Mở **n8n Editor**, nhấn **Import Workflow** và dán JSON vào.
- **Lưu workflow** với tên mới (ví dụ: `WhatsApp Welcome Messages`).

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **11 node**, các sếp cần chú ý cấu hình các node sau:

##### **A. Node `Trigger Every 5 Minute` (scheduleTrigger)**
- **Thời gian chạy**: Mặc định là 5 phút. Các sếp có thể điều chỉnh để phù hợp (ví dụ: 10 phút nếu muốn giảm tải API).
- **Lưu ý**: Không nên chạy quá nhanh (dưới 1 phút) để tránh bị Rapiwa hoặc WhatsApp chặn.

##### **B. Node `Fetch All Pending Queries for Messaging` (googleSheets)**
- **Credentials**: Chọn `googleSheetsOAuth2Api` đã cấu hình trước.
- **Query**:
  ```json
  {
    "query": "SELECT * WHERE check IS NOT NULL AND status = 'pending'",
    "sheetName": "Sheet1" // Thay bằng tên sheet của bạn
  }
  ```
- **Lưu ý**:
  - Đảm bảo **Document ID** và **Sheet GID** trong credentials là chính xác.
  - Cột `check` phải có giá trị (không để trống) để workflow biết lead đó cần gửi tin nhắn.

##### **C. Node `Clean WhatsApp Number` (code)**
- **Mã JavaScript**:
  ```javascript
  // Loại bỏ khoảng trắng và ký tự đặc biệt khỏi số điện thoại
  return {
    whatsappNumber: item.whatsappNumber.replace(/\s+/g, '').replace(/[^0-9]/g, ''),
    name: item.name.trim() // Loại bỏ khoảng trắng thừa ở tên
  };
  ```
- **Lưu ý**:
  - Số điện thoại phải ở **định dạng quốc tế** (ví dụ: `841234567890` thay vì `0123456789`).

##### **D. Node `Check valid whatsapp number Using Rapiwa` (httpRequest)**
- **Credentials**: Chọn `httpBearerAuth` với **Bearer Token** từ Rapiwa.
- **URL**:
  ```
  https://api.rapiwa.com/v1/verify
  ```
- **Headers**:
  ```json
  {
    "Content-Type": "application/json"
  }
  ```
- **Body**:
  ```json
  {
    "phone": "{{$node["Clean WhatsApp Number"].json["whatsappNumber"]}}"
  }
  ```
- **Lưu ý**:
  - API này trả về trạng thái của số điện thoại (valid/unvalid). Workflow sẽ sử dụng kết quả này để quyết định gửi tin nhắn hay không.

##### **E. Node `Send Message Using Rapiwa` (httpRequest)**
- **Credentials**: Chọn `httpBearerAuth`.
- **URL**:
  ```
  https://api.rapiwa.com/v1/send
  ```
- **Headers**:
  ```json
  {
    "Content-Type": "application/json"
  }
  ```
- **Body**:
  ```json
  {
    "phone": "{{$node["Clean WhatsApp Number"].json["whatsappNumber"]}}",
    "message": "Xin chào {{$node["Clean WhatsApp Number"].json["name"]}}! Cảm ơn bạn đã liên hệ với chúng tôi. Chúng tôi sẽ liên hệ lại trong vòng 24 giờ để hỗ trợ. Chúc bạn một ngày tốt lành!"
  }
  ```
- **Lưu ý**:
  - **Thay đổi nội dung tin nhắn** theo nhu cầu marketing của doanh nghiệp.
  - **Thời gian chờ 5 giây** giữa các tin nhắn (node `Wait`) để tránh bị chặn.

##### **F. Node `Update rows: sent & verified` & `Update rows: not sent & unverified` (googleSheets)**
- **Credentials**: Chọn `googleSheetsOAuth2Api`.
- **Query**:
  - **Đã gửi thành công**:
    ```json
    {
      "query": "UPDATE Sheet1 SET status = 'sent', validity = 'verified' WHERE row_number = {{$node["Loop Over Items"].currentItem.row_number}}"
    }
    ```
  - **Không gửi được**:
    ```json
    {
      "query": "UPDATE Sheet1 SET status = 'not sent', validity = 'unverified' WHERE row_number = {{$node["Loop Over Items"].currentItem.row_number}}"
    }
    ```
- **Lưu ý**:
  - Đảm bảo **cột `row_number`** được điền chính xác để cập nhật hàng đúng.

##### **G. Node `Limit` (limit)**
- **Số lượng tối đa**: Mặc định là **60 lead/luật**. Các sếp có thể điều chỉnh nếu cần (ví dụ: 30 lead/luật để giảm tải API).
- **Lưu ý**: Nếu quá nhiều lead, Rapiwa có thể cấm tài khoản.

---

#### **3. Kích hoạt ⚡️**
1. **Test run** với dữ liệu mẫu:
   - Chọn **Test tab** trong n8n Editor và nhấn **Execute Workflow**.
   - Kiểm tra các node quan trọng (đặc biệt là `Check valid whatsapp number` và `Send Message Using Rapiwa`) để đảm bảo không có lỗi.
2. **Bật Active workflow**:
   - Sau khi test thành công, chuyển trạng thái workflow từ **Inactive** sang **Active**.

---

### **✍️ Mẹo & gợi ý nâng cao**
:::tip[NÂNG CAO HỆ THỐNG]
1. **Gửi tin nhắn đa phương tiện**:
   - Kết hợp với node **Rapiwa Media** để gửi ảnh, video hoặc PDF cùng tin nhắn.
   - Ví dụ: Gửi **báo giá sản phẩm** hoặc **hướng dẫn sử dụng** qua WhatsApp.

2. **Lưu log lỗi**:
   - Thêm node **Google Sheets** hoặc **Slack** để ghi lại các lead không gửi được tin nhắn.
   - Cấu hình node `Update rows: not sent` để gửi thông báo lỗi đến Slack:
     ```json
     {
       "text": "Lead không gửi được tin nhắn: {{$node["Clean WhatsApp Number"].json["name"]}} (Số: {{$node["Clean WhatsApp Number"].json["whatsappNumber"]}})"
     }
     ```

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node **Google Sheets** hoặc **Email** để gửi báo cáo tổng hợp số lead đã gửi/tổng số lead trong ngày.
   - Ví dụ: Gửi báo cáo qua **Gmail** mỗi tối 8h.

4. **Tích hợp với CRM**:
   - Nếu sử dụng **HubSpot**, **Zoho CRM** hoặc **Salesforce**, các sếp có thể kết nối workflow này với CRM để cập nhật trạng thái lead tự động.

5. **Tự động hóa tin nhắn nhắc nhở**:
   - Thêm logic để gửi tin nhắn nhắc nhở sau 3 ngày nếu lead chưa phản hồi.
   - Ví dụ:
     ```json
     {
       "message": "Xin chào {{$node["Clean WhatsApp Number"].json["name"]}}! Chúng tôi vẫn chờ phản hồi của bạn. Hãy liên hệ với chúng tôi qua số này nếu cần hỗ trợ!"
     }
     ```
     (Sử dụng node `Wait` và `If` để kiểm tra trạng thái `status = 'pending'`).
:::

---

### **📌 Kết luận**
Workflow này là **giải pháp hoàn hảo** để các sếp tự động hóa quy trình gửi tin nhắn chào mừng WhatsApp cho lead bán hàng, **không cần viết một dòng code nào**. Với tính năng:
✅ **Tự động hóa 100%** (không cần can thiệp thủ công).
✅ **Cá nhân hóa tin nhắn** (chào tên lead).
✅ **Quản lý lead hiệu quả** (cập nhật trạng thái trên Google Sheets).
✅ **Tránh bị chặn** (thời gian chờ giữa các tin nhắn).

**Hãy áp dụng ngay workflow này và tiết kiệm thời gian cho đội ngũ marketing của mình!**
👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/8572) và bắt đầu tự động hóa hôm nay!