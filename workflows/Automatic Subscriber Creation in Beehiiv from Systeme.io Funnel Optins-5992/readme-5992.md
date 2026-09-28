---
title: "🚀 Tự Động Tạo Khách Hàng Beehiiv Từ Opt-in Systeme.io (Không Cần Code)"
description: "Workflow tự động hóa hoàn toàn chuyển đổi khách hàng từ Systeme.io sang Beehiiv, tiết kiệm thời gian quản lý danh sách email và tối ưu hóa chiến dịch marketing. Hỗ trợ theo dõi UTM tags và cảnh báo lỗi API."
slug: "tu-dong-tao-khach-hang-beehiiv-tu-systemeio"
tags: [n8n, automation, email-marketing, beehiiv, systemeio, no-code]
keywords: [n8n workflow beehiiv, tự động hóa danh sách email, hệ thống marketing tự động, Systeme.io Beehiiv integration, tự động tạo subscriber]
---

# 🚀 **Tự Động Tạo Khách Hàng Beehiiv Từ Opt-in Systeme.io (Không Cần Code)**

## **🔥 Bạn đang gặp phải vấn đề gì?**
Hiện nay, khi bạn chạy **chiến dịch marketing** trên Systeme.io và thu thập thông tin khách hàng qua opt-in, việc **chuyển dữ liệu sang Beehiiv** để quản lý danh sách email vẫn còn là công việc **thủ công, tốn thời gian và dễ sai sót**. Kết quả là:
- **Danh sách email không đồng bộ**, dẫn đến mất khách hàng tiềm năng.
- **Không theo dõi được nguồn gốc** (UTM tags) của khách hàng, khiến phân tích hiệu quả chiến dịch trở nên khó khăn.
- **Phải làm lại thủ công** mỗi khi có opt-in mới, làm giảm hiệu suất làm việc.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động tạo subscriber Beehiiv** ngay khi khách hàng opt-in trên Systeme.io.
✅ **Chuyển dữ liệu tên, email, UTM tags** một cách chính xác, không cần code.
✅ **Gửi cảnh báo lỗi** nếu API Beehiiv gặp sự cố, giúp bạn không bỏ lỡ bất kỳ khách hàng nào.
✅ **Hoạt động 24/7**, không phụ thuộc vào thời gian làm việc của bạn.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Không cần nhập liệu thủ công, tự động hóa toàn bộ quy trình.
- **Danh sách email luôn đồng bộ**: Khách hàng mới được thêm vào Beehiiv ngay lập tức.
- **Theo dõi nguồn gốc khách hàng**: UTM tags (utm_source, utm_medium, utm_campaign) được chuyển tự động, giúp phân tích hiệu quả chiến dịch chính xác.
- **Cảnh báo lỗi API**: Nếu Beehiiv gặp sự cố, hệ thống sẽ gửi email cảnh báo ngay.
- **Không giới hạn số lượng opt-in**: Workflow hoạt động với mọi opt-in mới, giúp bạn **văn hóa hóa** quy trình marketing.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow hoạt động, các sếp cần chuẩn bị:
✔ **Tài khoản Systeme.io** (đã cấu hình webhook cho opt-in).
✔ **Tài khoản Beehiiv** (có **publication ID** và **API key**).
✔ **Tài khoản Gmail** (để gửi cảnh báo lỗi).
✔ **Dữ liệu tùy chọn** (nếu muốn chuyển **tên đầu, tên cuối** của khách hàng sang Beehiiv).
:::

---

## **🚀 Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Workflow này đã được **tạo sẵn trên n8n.io** với ID **5992**. Các sếp có thể:
- **Tải xuống file JSON** từ [đây](https://n8n.io/workflows/5992) và import vào n8n Editor.
- **Copy JSON** từ trang workflow và dán vào **Import Workflow** trong n8n.

:::note[**Lưu ý quan trọng**]
- **Không sử dụng phiên bản n8n Community** (n8n.io) để chạy 24/7, vì nó có giới hạn tài nguyên.
- **Cài đặt n8n trên VPS** để workflow hoạt động liên tục.
:::

---

### **2. Các bước cấu hình BẮT BUỘC phải chỉnh 📌**

#### **🔹 Bước 1: Cấu hình Webhook Systeme.io**
1. Mở node **"On New Systeme.io Optin"** (loại `webhook`).
2. **Không cần thay đổi gì** trong node này, vì nó sẽ tự động nhận dữ liệu từ Systeme.io.
3. **Tạo webhook trên Systeme.io**:
   - Đi đến **Funnel Settings** > **Webhooks**.
   - Chọn **Trigger: "New Opt-in"** và **HTTP Method: POST**.
   - Dán **URL webhook** từ node n8n vào Systeme.io.
   - **Lưu ý**: Systeme.io sẽ gửi yêu cầu từ **IP cố định**, nên các sếp nên **bỏ qua yêu cầu xác thực IP** (nếu muốn đơn giản).

#### **🔹 Bước 2: Cấu hình "Configure Workflow" (node `set`)**
Mở node **"Configure Workflow"** và điền các thông tin sau vào **Environment Variables**:
| **Biến môi trường**          | **Giá trị cần điền**                                                                 | **Ghi chú**                                                                 |
|--------------------------------|--------------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| `beehiiv_publication_id`      | ID của **publication Beehiiv** của bạn (tìm ở [đây](https://www.beehiiv.com/support/article/13091918395799-how-to-access-your-publication-id-or-api-keys)). | **Bắt buộc**. Nếu không điền, API sẽ không hoạt động.                     |
| `beehiiv_firstname_field_name` | Tên trường **tên đầu** trong Systeme.io (ví dụ: `first_name`, `given_name`).         | **Không bắt buộc**, chỉ cần điền nếu muốn chuyển tên đầu sang Beehiiv. |
| `beehiiv_lastname_field_name`  | Tên trường **tên cuối** trong Systeme.io (ví dụ: `last_name`, `family_name`).        | **Không bắt buộc**, chỉ cần điền nếu muốn chuyển tên cuối sang Beehiiv. |
| `email_alert_recipients`       | Danh sách email (cách nhau bởi dấu `,`) để nhận cảnh báo lỗi (ví dụ: `sop@gmail.com, sop2@gmail.com`). | **Bắt buộc** để nhận thông báo khi API Beehiiv lỗi.                     |

#### **🔹 Bước 3: Kết nối Beehiiv (node `httpRequest`)**
Mở node **"Create New Beehiiv Subscriber"** (loại `httpRequest`):
1. **Chọn phương thức HTTP**: `POST`.
2. **URL API**: `https://api.beehiiv.com/v1/publications/{beehiiv_publication_id}/subscribers`.
   - Thay `{beehiiv_publication_id}` bằng giá trị từ **Environment Variables** trên.
3. **Headers**:
   - `Authorization`: `Bearer {beehiiv_api_key}` (tìm API key ở [đây](https://www.beehiiv.com/support/article/13091918395799-how-to-access-your-publication-id-or-api-keys)).
   - `Content-Type`: `application/json`.
4. **Body (JSON)**:
   ```json
   {
     "email": "{{$node["On New Systeme.io Optin"].json["email"]}}",
     "first_name": "{{$node["On New Systeme.io Optin"].json[beehiiv_firstname_field_name]}}",
     "last_name": "{{$node["On New Systeme.io Optin"].json[beehiiv_lastname_field_name]}}",
     "utm_source": "{{$node["On New Systeme.io Optin"].json["utm_source"]}}",
     "utm_medium": "{{$node["On New Systeme.io Optin"].json["utm_medium"]}}",
     "utm_campaign": "{{$node["On New Systeme.io Optin"].json["utm_campaign"]}}"
   }
   ```
   - **Lưu ý**:
     - Nếu không muốn chuyển **tên đầu/tên cuối**, xóa `first_name` và `last_name` trong body.
     - UTM tags (`utm_source`, `utm_medium`, `utm_campaign`) sẽ tự động chuyển từ Systeme.io sang Beehiiv.

#### **🔹 Bước 4: Cấu hình cảnh báo lỗi (node `gmail`)**
Mở node **"Send Email Alert (Beehiiv API error)"** (loại `gmail`):
1. **Kết nối tài khoản Gmail**:
   - Nhấn **Connect Account** và đăng nhập vào Gmail.
2. **Cấu hình email cảnh báo**:
   - **Subject**: `⚠️ Beehiiv API Error: Failed to create subscriber for {{$node["On New Systeme.io Optin"].json["email"]}}`
   - **Body**:
     ```html
     <p>⚠️ Lỗi khi tạo subscriber Beehiiv cho email: <strong>{{$node["On New Systeme.io Optin"].json["email"]}}</strong></p>
     <p>Lỗi chi tiết: <strong>{{$node["Create New Beehiiv Subscriber"].error.message}}</strong></p>
     <p>Chi tiết opt-in:</p>
     <pre>{{JSON.stringify($node["On New Systeme.io Optin"].json, null, 2)}}</pre>
     ```
   - **Người nhận**: Sử dụng biến `email_alert_recipients` từ **Environment Variables**.

#### **🔹 Bước 5: Kiểm tra logic điều kiện (node `if`)**
Node **"Subscriber Created?"** (loại `if`) sẽ kiểm tra:
- **Nếu Beehiiv trả về status code 201 (tạo thành công)**: Workflow tiếp tục.
- **Nếu lỗi**: Workflow chuyển sang node **gmail** để gửi cảnh báo.

**Không cần chỉnh sửa gì** trong node này, vì nó đã cấu hình sẵn.

---

### **3. Kích hoạt ⚡️ Workflow**
1. **Test run với dữ liệu mẫu**:
   - Tạo một opt-in giả trên Systeme.io (hoặc sử dụng **n8n Webhook Simulator** để test).
   - Kiểm tra:
     - Subscriber có được tạo trên Beehiiv không?
     - Nếu có lỗi, email cảnh báo có được gửi không?
2. **Bật Active workflow**:
   - Nhấn **Active** ở góc trên bên phải của canvas.

---

## **✍️ Mẹo & gợi ý nâng cao**

### **🔹 1. Tối ưu hóa theo dõi UTM tags**
- Nếu bạn muốn **theo dõi chi tiết hơn**, thêm các UTM tags khác như:
  ```json
  "utm_content": "{{$node["On New Systeme.io Optin"].json["utm_content"]}}",
  "utm_term": "{{$node["On New Systeme.io Optin"].json["utm_term"]}}"
  ```
- **Lưu ý**: Chỉ thêm nếu Systeme.io cung cấp dữ liệu này.

### **🔹 2. Gửi thông báo thành công (optional)**
- Thêm node **Slack/Telegram** để thông báo khi subscriber được tạo thành công.
- Ví dụ:
  ```json
  {
    "text": "🎉 Subscriber created successfully!\nEmail: {{$node["On New Systeme.io Optin"].json["email"]}}"
  }
  ```

### **🔹 3. Lưu log hoạt động**
- Thêm node **Sticky Note** (`n8n-nodes-base.stickyNote`) để ghi lại lịch sử opt-in.
- **Cách sử dụng**:
  - Mở node **"Clean Data"** (loại `set`).
  - Thêm **Sticky Note** sau node này để lưu dữ liệu opt-in vào log.

### **🔹 4. Xử lý opt-in từ nhiều funnel**
- Nếu bạn có **nhiều funnel Systeme.io**, tạo **bộ workflow riêng** cho mỗi funnel.
- **Lưu ý**: Mỗi workflow cần **cấu hình riêng `beehiiv_publication_id` và `email_alert_recipients`**.

### **🔹 5. Cập nhật API key Beehiiv**
- Nếu API key Beehiiv hết hạn, **cập nhật lại** trong node `httpRequest` mà không cần thay đổi workflow.

---

## **📌 Kết luận**
Workflow này **giải phóng bạn khỏi công việc nhập liệu thủ công**, giúp **tự động hóa hoàn toàn** quy trình chuyển opt-in từ Systeme.io sang Beehiiv. Kết quả:
✔ **Danh sách email luôn đồng bộ**, không mất khách hàng.
✔ **Theo dõi nguồn gốc khách hàng** chính xác với UTM tags.
✔ **Cảnh báo lỗi tự động**, không bỏ lỡ bất kỳ opt-in nào.
✔ **Hoạt động 24/7**, không phụ thuộc vào thời gian làm việc.

**🚀 Hãy áp dụng ngay để tối ưu hóa chiến dịch marketing của mình!**

---
:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**🔗 Xem thêm workflow của Vincent Belmehel:**
👉 [https://n8n.io/creators/belmehel/](https://n8n.io/creators/belmehel/)