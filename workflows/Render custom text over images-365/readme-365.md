---
title: "🎨 Tự Động Hoàn Thành Thiết Kế Banner Cá Nhân Hóa Trên Hình Ảnh - Không Cần Code!"
description: "Workflow tự động hóa tạo banner cá nhân hóa từ template trên Bannerbear và gửi kết quả ngay đến Slack/Rocket.Chat, tiết kiệm thời gian thiết kế lên đến 90% cho các sếp marketing!"
slug: "tu-dong-hoan-thanh-thiet-ke-banner-cach-nhan-hoa"
tags: [n8n, automation, bannerbear, rocketchat, slack, no-code, thiết kế tự động]
keywords: [n8n workflow banner, tự động hóa thiết kế banner, banner cá nhân hóa, rocketchat api, bannerbear tự động]
---

# 🎨 **Tự Động Hoàn Thành Thiết Kế Banner Cá Nhân Hóa Trên Hình Ảnh - Không Cần Code!**

### **Nỗi Đau Của Các Sếp Marketing**
Các sếp marketing thường phải mất **giờ đồng hồ** để thiết kế banner cá nhân hóa cho từng khách hàng, sự kiện hoặc chiến dịch. Thậm chí, khi cần gửi banner đến nhiều kênh (Slack, Rocket.Chat, email) thì công việc trở nên **phức tạp và tốn thời gian hơn bao giờ hết**. Với **n8n**, các sếp có thể **tự động hóa toàn bộ quy trình** chỉ trong vài phút, **không cần viết một dòng code nào!**

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Thiết kế và gửi banner chỉ trong **vài giây** thay vì nhiều giờ.
✅ **Cá nhân hóa hoàn toàn**: Thay đổi văn bản, logo, màu sắc theo từng khách hàng hoặc chiến dịch.
✅ **Gửi tự động đến nhiều kênh**: Banner được gửi ngay đến **Slack, Rocket.Chat, hoặc email** một cách đồng bộ.
✅ **Hoạt động 24/7**: Dùng **Cron Job** để chạy tự động theo lịch trình (ngày, giờ cụ thể).
✅ **Giảm thiểu lỗi**: Không cần copy-paste thủ công, tránh sai sót trong nội dung.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Bannerbear** (để tạo template banner):
   - [Đăng ký Bannerbear miễn phí](https://bannerbear.com/) (nếu chưa có).
   - **API Key** của Bannerbear (tìm trong **Settings > API**).
2. **Tài khoản Rocket.Chat** (hoặc Slack, nếu muốn thay thế):
   - **API Key** và **Webhook URL** của Rocket.Chat (tìm trong **Admin > API**).
   - **Credentials** cho n8n (cấu hình trong **n8n Credentials Manager**).
3. **Lịch trình chạy tự động (Cron)**:
   - Ví dụ: `0 0 * * *` (chạy hàng ngày lúc 00:00).
4. **(Tùy chọn) API Key cho HTTP Request** (nếu muốn gọi API bên thứ ba).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow bằng **2 cách**:
- **Tải file JSON** từ [n8n.io/workflows/365](https://n8n.io/workflows/365) và import vào **n8n Editor**.
- **Copy JSON** và dán vào **n8n Editor** (tab **Import/Export**).

:::note[Lưu ý]
- Nếu các sếp **self-host n8n**, hãy đảm bảo **cài đặt các node cần thiết**:
  - `n8n-nodes-base.cron`
  - `n8n-nodes-base.bannerbear`
  - `n8n-nodes-base.rocketchat`
  - `n8n-nodes-base.httpRequest`
:::

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow có **4 node chính**, các sếp cần cấu hình kỹ lưỡng:

##### **A. Node "Cron" (Đặt lịch chạy tự động)**
- **Expression**: Đặt lịch chạy theo nhu cầu (ví dụ: `0 0 * * *` = hàng ngày 00:00).
- **Time Zone**: Chọn múi giờ phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).
- **Active**: Bật để workflow chạy theo lịch.

##### **B. Node "HTTP Request" (Gọi API để lấy dữ liệu)**
- **Method**: `GET` hoặc `POST` (tùy thuộc vào API bạn muốn gọi).
- **URL**: Điền URL API của **Bannerbear** hoặc API bên thứ ba.
- **Headers**:
  - `Authorization: Bearer {bannerbearApiKey}` (điền từ **Credentials**).
  - `Content-Type: application/json`.
- **Body (nếu POST)**: JSON chứa tham số cần gửi (ví dụ: `{"text": "Hello {{customerName}}!"}`).

##### **C. Node "Bannerbear" (Tạo banner từ template)**
- **Credentials**: Chọn `bannerbearApi` (đã cấu hình trước).
- **Template ID**: ID của template banner bạn đã tạo trên Bannerbear.
- **Variables**:
  - Thay thế **{{customerName}}**, **{{logo}}**, **{{message}}** bằng dữ liệu từ **HTTP Request** (hoặc từ **Rocket.Chat**).
  - Ví dụ:
    ```json
    {
      "text": "Chào mừng {{customerName}}!",
      "logo": "https://example.com/logo.png",
      "backgroundColor": "#FF5733"
    }
    ```
- **Output**: Banner sẽ được tạo và trả về **URL download**.

##### **D. Node "Rocketchat" (Gửi banner đến Rocket.Chat)**
- **Credentials**: Chọn `rocketchatApi` (đã cấu hình trước).
- **Room ID**: ID của phòng chat (tìm trong **Admin > Rooms**).
- **Message**: Nội dung gửi kèm banner (ví dụ: `Xin chào {{customerName}}, đây là banner cá nhân hóa của bạn!`).
- **File**: Chọn **URL banner** từ **Bannerbear** (trong **Data** của node trước).
- **Attachments**: Bật để gửi banner như **file đính kèm**.

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Chạy **Manual Execution** với dữ liệu mẫu để kiểm tra.
- **Active Workflow**: Bật **Active** để workflow chạy tự động theo lịch.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM NÀY ĐỂ TIẾT KIỆM THÊM THỜI GIAN]
1. **Kết hợp với Slack**:
   - Thay thế node **Rocketchat** bằng **Slack Webhook** để gửi banner đến Slack.
   - Cấu hình trong **n8n Credentials** với **Slack Webhook URL**.

2. **Lưu log hoạt động**:
   - Thêm node **n8n-nodes-base.set** để lưu dữ liệu vào **Google Sheets** hoặc **Airtable** để theo dõi lịch sử.

3. **Tự động gửi email kèm banner**:
   - Sử dụng node **n8n-nodes-base.email** để gửi email tự động với banner đính kèm.

4. **Cá nhân hóa theo dữ liệu khách hàng**:
   - Nếu dữ liệu khách hàng từ **CRM** (HubSpot, Salesforce), sử dụng node **HTTP Request** để gọi API CRM và truyền vào **Bannerbear**.

5. **Chạy theo sự kiện (Webhook)**:
   - Thay thế **Cron** bằng **Webhook** để workflow chạy khi có yêu cầu (ví dụ: khi khách hàng đăng ký).
:::

---

### 📌 **Kết Luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn quy trình thiết kế và gửi banner cá nhân hóa**, **giảm thiểu công việc thủ công** và **tăng hiệu suất marketing**. **Không cần code**, chỉ cần **cấu hình vài bước**, các sếp đã có thể **tiết kiệm hàng giờ mỗi tuần**!

:::success[HÀNH ĐỘNG NGÀY HÔM NAY]
1. **Đăng ký Bannerbear** và **Rocket.Chat** (nếu chưa có).
2. **Import workflow** và cấu hình **Credentials**.
3. **Test Run** và **Active** để bắt đầu tự động hóa!
4. **Mở rộng** bằng cách kết hợp với Slack, email hoặc CRM.
:::

**Các sếp đã sẵn sàng tự động hóa không?** 🚀 **Hãy bắt đầu ngay!**