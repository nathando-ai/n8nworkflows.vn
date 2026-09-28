---
title: "🚀 Tự Động Hóa Báo Cáo Khách Hàng Tiềm Năng Hàng Ngày: Theo Dõi Website Visitor với ProspectPro & Gmail"
description: "Workflow tự động hóa gửi báo cáo hàng ngày về khách hàng tiềm năng đã ghé thăm website trong 24h qua, giúp doanh nghiệp tiết kiệm thời gian và tối ưu hóa chiến dịch marketing. Kết nối ProspectPro với Gmail để nhận email thông báo chi tiết, cá nhân hóa."
slug: "tieu-dong-hoa-bao-cao-khach-hang-tiem-nen-hang-ngay"
tags: [n8n, automation, lead-generation, prospectpro, gmail, no-code, marketing-automation]
keywords: [tự động hóa n8n, theo dõi khách hàng tiềm năng, ProspectPro API, báo cáo hàng ngày, email tự động, marketing automation]
---

# 🚀 **Tự Động Hóa Báo Cáo Khách Hàng Tiềm Năng Hàng Ngày: Theo Dõi Website Visitor với ProspectPro & Gmail**

## **🔍 Nỗi Đau Của Doanh Nghiệp**
Các sếp đang mất nhiều thời gian quét thủ công danh sách khách hàng đã ghé thăm website, phân tích hành vi, và gửi báo cáo hàng ngày cho đội ngũ marketing hoặc bán hàng. Điều này không chỉ tốn thời gian mà còn dễ gây lỗi nhân sự và thiếu chính xác. **Workflow này giải quyết vấn đề này bằng cách tự động hóa toàn bộ quy trình:**
- **Lấy dữ liệu** khách hàng tiềm năng từ ProspectPro trong 24h qua.
- **Lọc và chọn** những lead phù hợp (không bị loại bỏ, đã tương tác).
- **Gửi email tự động** hàng ngày (lúc 07:50) với danh sách chi tiết, giúp đội ngũ marketing hành động nhanh chóng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần quét thủ công danh sách lead hàng ngày.
✅ **Chính xác 100%**: Dữ liệu lấy từ API ProspectPro, không sai sót.
✅ **Cá nhân hóa báo cáo**: Chỉ bao gồm lead phù hợp, không có thông tin thừa.
✅ **Hoạt động liên tục**: Workflow chạy tự động hàng ngày, không phụ thuộc vào nhân viên.
✅ **Tối ưu hóa marketing**: Đội ngũ bán hàng nhận được thông tin kịp thời để liên hệ.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản ProspectPro**:
   - Đăng ký tại [ProspectPro](https://mijn.prospectpro.nl) và lấy **API Key**.
   - Cài đặt **credentials** trong n8n với tên `prospectproApi` (điền `apiKey` và `baseUrl`).
2. **Tài khoản Gmail**:
   - Cấu hình **OAuth2** trong n8n với tên `gmailOAuth2` (sử dụng email chính thức của doanh nghiệp).
3. **Dữ liệu mẫu (nếu test)**:
   - Một số lead đã tương tác trong 24h qua để test workflow.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/8689) hoặc copy toàn bộ JSON từ canvas.
- Trong **n8n Editor**, nhấn **Import** → Chọn file JSON hoặc dán JSON vào ô `Import Workflow`.
- Workflow sẽ tự động tạo 11 node như mô tả.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
##### **A. Cấu Hình Credentials**
- **Node "Get Prospects"**:
  - Chọn `prospectproApi` trong `Credentials`.
  - Điền `apiKey` và `baseUrl` (mặc định là `https://api.prospectpro.nl`).
- **Node "Send Notification"**:
  - Chọn `gmailOAuth2` trong `Credentials`.
  - Chọn **Gmail Account** để gửi email (cần cấp quyền cho n8n).

##### **B. Cấu Hình Lọc Lead (Node "Select Prospects")**
- Mở node **"Select Prospects"** (type: `code`).
- **Sửa code** để lọc lead phù hợp (ví dụ: loại bỏ lead đã bị loại bỏ hoặc chưa tương tác trong 24h).
  ```javascript
  // Ví dụ: Chỉ giữ lead có `status: "active"` và `lastVisit > 24h`
  return $input.all().filter(prospect =>
    prospect.status === "active" &&
    new Date(prospect.lastVisit) > new Date(Date.now() - 24 * 60 * 60 * 1000)
  );
  ```
- **Lưu ý**: Thay đổi logic lọc nếu cần phù hợp với chiến lược marketing của doanh nghiệp.

##### **C. Thiết Lập Email Template (Node "Send Notification")**
- Mở node **"Send Notification"** (type: `gmail`).
- **Cấu hình email**:
  - **Subject**: `"Báo cáo Lead Tiềm Năng Hôm Nay - [Ngày]"` (có thể tự động hóa bằng `$node["Daily, 07:50"].json()["date"]`).
  - **Body**: Sử dụng **HTML template** để hiển thị danh sách lead (ví dụ:
    ```html
    <h2>Danh sách Lead Tiềm Năng (${$node["Daily, 07:50"].json()["date"]})</h2>
    <ul>
      {% for prospect in $input.all() %}
        <li>
          <strong>Tên:</strong> {{ prospect.name }}<br>
          <strong>Email:</strong> {{ prospect.email }}<br>
          <strong>Trang Web Ghé:</strong> {{ prospect.website }}<br>
          <strong>Thời Gian Ghé:</strong> {{ prospect.lastVisit }}
        </li>
      {% endfor %}
    </ul>
    ```
  - **Thêm link hành động**: Ví dụ, link liên hệ qua Slack/Telegram hoặc trang CRM.

##### **D. Thiết Lập Lịch Trình Chạy (Node "Daily, 07:50")**
- Node này đã được cấu hình chạy **mỗi ngày lúc 07:50**.
- **Không cần chỉnh** trừ khi muốn thay đổi giờ (ví dụ: 08:00).

##### **E. Xử Lý Lỗi (Error Handling)**
- Workflow có **3 node noOp** để xử lý lỗi:
  - **"Error: ProspectPro"**: Hiển thị lỗi khi lấy dữ liệu thất bại.
  - **"Error: Gmail"**: Hiển thị lỗi khi gửi email thất bại.
  - **"No Prospects, No Email"**: Dừng workflow nếu không có lead nào.
- **Mẹo nâng cao**:
  - Thêm **node Google Sheets** để log lỗi vào bảng tính.
  - Thêm **node Slack/Telegram** để thông báo lỗi ngay khi xảy ra.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** với dữ liệu mẫu (nếu có lead trong 24h qua).
   - Kiểm tra email nhận được có đúng format không.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo ngay khi có lead mới.
   - Ví dụ:
     ```json
     {
       "name": "Notify Slack",
       "type": "slack",
       "credentials": ["slackApi"],
       "options": {
         "channel": "#marketing-leads",
         "text": "🚨 Có lead mới: {{ $inputItem.name }} (Email: {{ $inputItem.email }})"
       }
     }
     ```

2. **Lưu Log vào Google Sheets**:
   - Thêm node **Google Sheets** sau node **"Send Notification"** để ghi lại lịch sử lead.
   - Cấu hình:
     - **Sheet Name**: `Báo cáo Lead Tiềm Năng`
     - **Range**: `A1` (để ghi dữ liệu mới vào hàng mới).

3. **Tự động Gửi Báo Cáo Định Kỳ**:
   - Nếu muốn gửi báo cáo **tuần/Tháng**, thay đổi node `scheduleTrigger` thành:
     - **Tuần**: `cron(0 0 * * 1)` (mỗi thứ 2 lúc 00:00).
     - **Tháng**: `cron(0 0 1 * *)` (ngày 1 hàng tháng lúc 00:00).

4. **Cá nhân hóa Email**:
   - Sử dụng **node `code`** trước node `gmail` để thêm thông tin cá nhân hóa như:
     ```javascript
     // Thêm tên người nhận vào email
     $input.all().forEach(item => {
       item.emailBody = item.emailBody.replace(
         "{{NAME}}",
         item.name || "Khách Hàng"
       );
     });
     ```

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa báo cáo lead hàng ngày mà không cần viết code. Với sự kết hợp giữa **ProspectPro** (theo dõi website visitor) và **Gmail** (gửi email tự động), doanh nghiệp sẽ tiết kiệm thời gian, tăng hiệu quả marketing, và có dữ liệu chính xác để ra quyết định.

**Hành động ngay!**
1. Import workflow vào n8n của mình.
2. Cấu hình credentials và email template.
3. Bật **Active** và chờ email báo cáo hàng ngày!

Nếu có vấn đề, hãy **comment bên dưới** hoặc liên hệ với cộng đồng n8n tại [n8n.io/community](https://n8n.io/community). 🚀