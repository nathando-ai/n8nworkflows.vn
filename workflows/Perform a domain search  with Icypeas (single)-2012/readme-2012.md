---
title: "🔍 Tự Động Hoàn Thành Tra Cứu Domain Với Icypeas - Không Cần Code"
description: "Workflow tự động hóa tra cứu thông tin chi tiết về domain/company từ Icypeas chỉ với một cú nhấp chuột, tiết kiệm thời gian và nâng cao hiệu quả marketing/sales cho doanh nghiệp."
slug: "tieu-chu-domain-voi-icypeas"
tags: [n8n, automation, sales, marketing, tra-cuu-domain]
keywords: [tự động hóa tra cứu domain, icypeas api, n8n workflow domain scan, tra cứu thông tin công ty, tự động hóa marketing]
---

# 🚀 Tự Động Tra Cứu Domain Với Icypeas - Không Cần Code

### 📌 **Nỗi Đau Của Các Sếp**
Trong công việc marketing và sales, việc tra cứu thông tin chi tiết về một domain hoặc công ty là một công việc tốn thời gian và dễ gây nhầm lẫn. Các sếp thường phải:
- **Tìm kiếm thủ công** trên nhiều trang web khác nhau để thu thập thông tin về domain, lịch sử đăng ký, chủ sở hữu, và các chi tiết liên quan.
- **Mất nhiều thời gian** để so sánh và tổng hợp dữ liệu từ nhiều nguồn khác nhau.
- **Không đảm bảo tính chính xác** vì phải dựa vào khả năng tìm kiếm của con người.

Workflow này giúp **tự động hóa hoàn toàn** quá trình tra cứu thông tin domain/company từ Icypeas chỉ với một cú nhấp chuột, mang lại **tính chính xác cao, tiết kiệm thời gian và nâng cao hiệu quả công việc**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tra cứu thông tin domain chỉ trong vài giây thay vì mất nhiều giờ.
- **Tính chính xác cao**: Dữ liệu được lấy trực tiếp từ Icypeas, không bị sai sót.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công, hoạt động liên tục 24/7.
- **Nâng cao hiệu quả marketing/sales**: Có thể tra cứu nhanh chóng thông tin về đối thủ hoặc khách hàng tiềm năng.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để sử dụng workflow này, các sếp cần:
1. **Tài khoản Icypeas**: Đăng ký tại [icypeas.com](https://icypeas.com) để lấy **API Key, API Secret và User ID**.
2. **VPS hoặc máy chủ n8n**: Để chạy workflow 24/7 (nếu không muốn dùng phiên bản cloud).
3. **N8n Editor**: Cài đặt và truy cập vào [n8n.io](https://n8n.io/) để import workflow.
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON từ [link gốc](https://n8n.io/workflows/2012) vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm **3 node chính**, các sếp cần chú ý cấu hình như sau:

##### **Node 1: Manual Trigger (Bắt đầu workflow)**
- **Tên node**: "When clicking 'Execute Workflow'"
- **Lưu ý**: Node này chỉ là nút kích hoạt thủ công. Các sếp không cần chỉnh sửa gì.

##### **Node 2: Authenticates to your Icypeas account (Mã hóa và xác thực)**
- **Tên node**: "Authenticates to your Icypeas account"
- **Loại node**: `n8n-nodes-base.code`
- **Cách cấu hình**:
  - Mở node này và thay thế các giá trị sau trong mã code:
    ```javascript
    const API_KEY = "**PUT_API_KEY_HERE**";
    const API_SECRET = "**PUT_API_SECRET_HERE**";
    const USER_ID = "**PUT_USER_ID_HERE**";
    ```
  - **Lấy API Key, API Secret và User ID** từ [trang cá nhân Icypeas](https://app.icypeas.com/bo/profile).
  - **Không chỉnh sửa** bất kỳ dòng code nào khác ngoài 3 dòng trên.

  :::note[Lưu ý cho người dùng self-hosted]
  Nếu các sếp tự host n8n, cần **bật module Crypto** để mã hóa hoạt động:
  1. Truy cập **Settings** → **General**.
  2. Tìm phần **"Additional Node Packages"** và bật **crypto**.
  3. Lưu thay đổi và **restart n8n** để áp dụng.
  :::

##### **Node 3: Run domain scan (single) (Gửi yêu cầu HTTP)**
- **Tên node**: "Run domain scan (single)"
- **Loại node**: `n8n-nodes-base.httpRequest`
- **Cách cấu hình**:
  - **Credentials**:
    - Tạo **mới một credential** với tên **"Authorization"**.
    - Trong **Value**, chọn **expression** và nhập:
      ```javascript
      {{ $json.api.key + ':' + $json.api.signature }}
      ```
    - Lưu credential này.
  - **Body Parameters**:
    - Thêm một **parameter mới** với tên **"domainOrCompany"**.
    - Điền **domain/company** muốn tra cứu vào **Value**.

---

#### 3. Kích hoạt ⚡️
- **Test run**: Nhấp vào nút **"Execute Workflow"** để chạy thử với một domain mẫu (ví dụ: `google.com`).
- **Bật Active**: Sau khi kiểm tra thành công, bật **Active** để workflow hoạt động tự động.

---

### ✍️ Mẹo & gợi ý nâng cao
:::tip[CÁCH SỬ DỤNG HIỆU QUẢ]
1. **Tích hợp với Slack/Telegram**: Sau khi tra cứu xong, gửi kết quả về Slack/Telegram để các sếp theo dõi dễ dàng.
   - Sử dụng node **Slack** hoặc **Telegram Bot** để gửi thông báo tự động.
2. **Lưu log tra cứu**: Sử dụng node **Google Sheets** hoặc **Airtable** để lưu lịch sử tra cứu.
   - Cấu hình node **HTTP Request** để gửi kết quả vào bảng dữ liệu.
3. **Tra cứu định kỳ**: Sử dụng **n8n Cron Trigger** để tự động tra cứu domain theo lịch trình (ví dụ: hàng tuần).
4. **Tích hợp với CRM**: Gửi kết quả tra cứu vào **HubSpot** hoặc **Salesforce** để cập nhật thông tin khách hàng.
:::

---

### 📌 Kết luận
Workflow này giúp **tự động hóa hoàn toàn** quá trình tra cứu domain/company từ Icypeas, mang lại **tính chính xác, tiết kiệm thời gian và nâng cao hiệu quả công việc** cho các sếp marketing và sales. **Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất!**

👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/2012) và bắt đầu tự động hóa ngay hôm nay!