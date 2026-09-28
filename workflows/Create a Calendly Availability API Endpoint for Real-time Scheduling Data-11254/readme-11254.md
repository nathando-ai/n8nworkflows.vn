---
title: "🚀 Tự Động Hóa API Kiểm Tra Sẵn Sàng Lịch Calendly - Giải Pháp Scheduling Thông Minh Cho Doanh Nghiệp"
description: "Workflow này tự động hóa việc kiểm tra sẵn sàng lịch thời gian thực với Calendly API, giúp doanh nghiệp tiết kiệm thời gian lên đến 80% khi xây dựng giao diện đặt lịch cá nhân hóa. Hỗ trợ tích hợp với website, chatbot và hệ thống CRM."
slug: "tieu-dong-hoa-api-kiem-tra-san-sang-calendly"
tags: [n8n, automation, calendly, api-integration, scheduling, no-code]
keywords: [tự động hóa calendly, api calendly, scheduling tự động, n8n workflow, tích hợp calendly với website]
---

# 🚀 **API Kiểm Tra Sẵn Sàng Lịch Calendly - Tự Động Hóa Scheduling Thông Minh**

### **Giải Pháp Cho Nỗi Đau Của Các Sếp**
Hiện nay, việc quản lý lịch hẹn thủ công không chỉ tốn thời gian mà còn dễ gây lỗi và mất tính cá nhân hóa. Các sếp thường phải:
- **Tra cứu sẵn sàng lịch** trên Calendly thủ công trước khi đề xuất thời gian cho khách hàng.
- **Tạo giao diện đặt lịch riêng** trên website, nhưng phải viết code hoặc phụ thuộc vào các plugin có hạn chế.
- **Mất thời gian phản hồi** khi khách hàng hỏi về sẵn sàng lịch, dẫn đến trải nghiệm khách hàng kém.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tạo API endpoint** để kiểm tra sẵn sàng lịch thời gian thực từ Calendly.
✅ **Tích hợp với website, chatbot hoặc CRM** để tự động hiển thị thời gian sẵn sàng.
✅ **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công.
✅ **Cá nhân hóa lịch hẹn** cho từng khách hàng dựa trên sự sẵn sàng thực tế.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tra cứu sẵn sàng lịch thủ công, tự động hóa toàn bộ quy trình.
- **Cải thiện trải nghiệm khách hàng**: Hiển thị thời gian sẵn sàng chính xác ngay trên website hoặc chatbot.
- **Tích hợp linh hoạt**: Sử dụng API endpoint để kết nối với bất kỳ hệ thống nào (WordPress, Shopify, Slack, Telegram...).
- **Dữ liệu thời gian thực**: Kiểm tra sẵn sàng lịch trong vòng vài giây, không cần cập nhật thủ công.
- **Cá nhân hóa**: Lọc theo loại sự kiện hoặc ngày cụ thể để phù hợp với từng khách hàng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Calendly** và quyền truy cập vào **API & Webhooks**.
2. **Token OAuth2** hoặc **Personal Access Token** từ Calendly (hướng dẫn tạo ở phần sau).
3. **n8n Self-hosted** (không dùng phiên bản miễn phí trên cloud).
4. **API Key** của n8n (để kết nối với Calendly).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/11254) hoặc copy toàn bộ JSON từ canvas.
- Mở **n8n Editor** → Nhấn **Import Workflow** → Dán JSON và nhấn **Import**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **9 node chính**, các sếp cần chú ý đến các bước sau:

##### **A. Cấu Hình Credentials Calendly**
- **Node "Get Current User"**, **"Get Event Types"**, **"Get Available Times"** đều sử dụng **credentials "calendlyOAuth2Api"**.
  - **Cách tạo credentials**:
    1. Vào [Calendly API & Webhooks](https://calendly.com/integrations/api).
    2. Tạo **Personal Access Token** hoặc **OAuth2 App** (nếu cần quyền cao).
    3. Trong n8n:
       - Tạo **new credential** → Chọn **Calendly OAuth2 API**.
       - Điền **Token** hoặc **Client ID/Secret** (nếu dùng OAuth2).
       - Lưu và chọn credential này trong các node HTTP Request.

##### **B. Cấu Hình Webhook Trigger**
- **Node "Webhook Trigger"**:
  - **Path**: `check-calendly-availability` (không thay đổi).
  - **HTTP Method**: `POST` (không thay đổi).
  - **Credentials**: Không cần (webhook tự động nhận request).

##### **C. Cấu Hình Request Body (Nếu Sử Dụng API)**
- Khi gọi API từ bên ngoài (ví dụ: từ website), gửi **body JSON** như sau:
  ```json
  {
    "event_type_uri": "string",  // (Optional) URI của loại sự kiện (vd: "https://api.calendly.com/event_types/123")
    "days_ahead": 7             // (Optional) Số ngày kiểm tra (mặc định: 7)
  }
  ```
  - Nếu không gửi `event_type_uri`, workflow sẽ sử dụng **loại sự kiện đầu tiên** trong danh sách.

##### **D. Cấu Hình Response Format**
- **Node "Respond with Availability"** sẽ trả về dữ liệu theo mẫu:
  ```json
  {
    "success": true,
    "user": { ... },          // Thông tin người dùng
    "event_type": { ... },    // Loại sự kiện được chọn
    "availability": {
      "has_slots": true,       // Có sẵn sàng không
      "total_slots": 45,       // Tổng số slot sẵn sàng
      "next_available": "Mon, Dec 2, 10:00 AM"  // Thời gian sẵn sàng đầu tiên
    },
    "slots": [...],           // Danh sách tất cả slot sẵn sàng
    "slots_by_day": {         // Slot phân theo ngày
      "Monday, Dec 2": [...],
      "Tuesday, Dec 3": [...]
    }
  }
  ```

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi một request POST đến `http://[your-n8n-domain]/webhook/check-calendly-availability` với body như trên.
  - Kiểm tra response trong **n8n Dashboard** → **Executions**.
- **Bật Active**:
  - Chuyển trạng thái workflow từ **Inactive** sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Với Website**
   - Sử dụng API endpoint này trong **JavaScript** để hiển thị sẵn sàng lịch trên trang web:
     ```javascript
     fetch('http://[your-n8n-domain]/webhook/check-calendly-availability', {
       method: 'POST',
       headers: { 'Content-Type': 'application/json' },
       body: JSON.stringify({ days_ahead: 7 })
     })
     .then(response => response.json())
     .then(data => {
       console.log(data.slots_by_day); // Hiển thị trên UI
     });
     ```

2. **Kết Nối Với Chatbot (Slack/Telegram)**
   - Thêm **node Slack/Telegram** sau "Respond with Availability" để gửi thông báo tự động khi có slot sẵn sàng mới.

3. **Lưu Log & Báo Cáo**
   - Thêm **node "Set"** sau "Respond with Availability" để lưu dữ liệu vào **Google Sheets** hoặc **Airtable** để theo dõi lịch sử.

4. **Tùy Chỉnh Ngày & Loại Sự Kiện**
   - Sử dụng **node "Set"** trước "Get Available Times" để lọc theo ngày cụ thể hoặc loại sự kiện (vd: chỉ hiển thị slot cho "Hội thảo 1:1").

5. **Sử Dụng Scheduled Trigger**
   - Thay vì gọi webhook thủ công, các sếp có thể **schedule** workflow chạy định kỳ (vd: mỗi ngày 8h) để cập nhật sẵn sàng lịch.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các doanh nghiệp muốn tự động hóa quy trình đặt lịch, tiết kiệm thời gian và cải thiện trải nghiệm khách hàng. Bằng cách tích hợp với **n8n**, các sếp có thể:
✔ **Xây dựng API endpoint** một cách dễ dàng, không cần viết code.
✔ **Tích hợp với bất kỳ hệ thống nào** (website, chatbot, CRM...).
✔ **Cập nhật sẵn sàng lịch thời gian thực** mà không cần can thiệp thủ công.

**Hãy áp dụng ngay workflow này và biến quy trình đặt lịch của doanh nghiệp trở nên thông minh hơn!** 🚀

---
:::note[Lưu Ý Cuối Cùng]
- **Không dùng phiên bản n8n cloud** vì không hỗ trợ webhook và credentials OAuth2.
- **Test cẩn thận** trước khi sử dụng với khách hàng thực tế.
- **Cập nhật credentials** nếu Calendly thay đổi API.
:::