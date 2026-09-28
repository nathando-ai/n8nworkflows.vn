---
title: "🚀 Tự Động Hóa Nhận Lead Từ Form Web Sang HubSpot Với SubmitraX – Không Cần Backend!"
description: "Workflow tự động hóa 100% không code giúp doanh nghiệp thu thập lead từ form HTML và đồng bộ tự động vào HubSpot, tiết kiệm thời gian và tối ưu quy trình bán hàng. Phù hợp cho marketer, đội ngũ bán hàng và nhà phát triển."
slug: "tu-dong-hoa-nhan-lead-tu-form-web-sang-hubspot"
tags: [n8n, automation, lead-generation, hubspot, submitrax, no-code]
keywords: [tự động hóa n8n, thu thập lead, form web tự động, đồng bộ hubspot, submitrax api, tự động hóa bán hàng]
---

# 🚀 **Tự Động Hóa Nhận Lead Từ Form Web Sang HubSpot Với SubmitraX – Không Cần Backend!**

### **Giải pháp hoàn hảo cho marketer, đội ngũ bán hàng và nhà phát triển**
Cần thu thập lead từ website nhưng không muốn phức tạp với backend, hosting hay chi phí form platform? **Workflow này giúp bạn:**
- **Tạo form HTML tự động** (không cần hosting riêng).
- **Thu thập lead** từ form và đồng bộ **tự động** vào HubSpot.
- **Tiết kiệm thời gian** bằng cách loại bỏ công việc nhập liệu thủ công.
- **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định và an toàn**, các sếp nên **self-host n8n** trên VPS để tránh giới hạn của phiên bản Cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao cho workflow)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** – Không cần nhập liệu lead thủ công.
✅ **Chính xác 100%** – Dữ liệu tự động đồng bộ vào HubSpot.
✅ **Không phụ thuộc backend** – Form hoạt động trên n8n mà không cần hosting riêng.
✅ **Hoạt động liên tục** – Thu thập lead ngay cả khi bạn ngủ.
✅ **Cá nhân hóa lead** – Dữ liệu từ form được tự động gắn vào HubSpot.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản SubmitraX** ([Đăng ký miễn phí](https://submitrax.com)) với **API Key**.
✔ **Tài khoản HubSpot** và **OAuth2 credentials** đã cấu hình trong n8n.
✔ **n8n (v1.x trở lên)** – Có thể là phiên bản **Cloud** hoặc **Self-hosted**.
✔ **Email để nhận cảnh báo** khi có lead mới (được cấu hình trong form).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải workflow** từ [n8n.io](https://n8n.io/workflows/16298) hoặc sử dụng file JSON đã cung cấp.
- **Cách import:**
  - Mở **n8n Editor** → Nhấn **"Import"** → Chọn file JSON.
  - **Hoặc** copy toàn bộ JSON và paste vào **"Import from JSON"** trong Editor.

#### **2. Các bước cấu hình BẮT BUỘC phải chỉnh 📌**
Workflow này được chia thành **3 giai đoạn chính**, các sếp cần theo dõi từng node quan trọng:

##### **📌 Giai đoạn 1: Tạo Form (Setup One-Time)**
1. **Node "Click here to start" (manualTrigger)**
   - Nhấn nút này để bắt đầu **setup ban đầu** (tạo workspace và form).
2. **Node "get workspace ID" (CUSTOM.submitrax)**
   - **Không cần chỉnh sửa**, nó tự lấy **ID workspace** từ SubmitraX.
3. **Node "Create a form" (CUSTOM.submitrax)**
   - **Chỉnh sửa `customHtml`** để thay đổi form:
     ```html
     <form>
       <input type="text" name="name" placeholder="Tên của bạn" required>
       <input type="email" name="email" placeholder="Email" required>
       <input type="text" name="company" placeholder="Công ty">
       <input type="text" name="website" placeholder="Website">
       <button type="submit">Gửi</button>
     </form>
     ```
   - **Thêm email nhận cảnh báo** trong `alertEmail` (ví dụ: `your-email@example.com`).
4. **Node "Get a form" (CUSTOM.submitrax)**
   - Sau khi tạo form, **copy `formId`** từ kết quả và **điền vào node này** (để lấy thông tin form).

##### **📌 Giai đoạn 2: Hiển thị Form (Webhook)**
5. **Node "Form viewer" (webhook)**
   - **Không cần chỉnh sửa**, nó sẽ **chuyển hướng** đến form khi người dùng truy cập URL.
6. **Node "Display the form" (respondToWebhook)**
   - **Không cần chỉnh sửa**, nó tự động **hiển thị form** khi người dùng truy cập URL production.
   - **Lưu ý:** Sau khi **publish workflow**, URL production sẽ được hiển thị ở góc trên bên phải.

##### **📌 Giai đoạn 3: Đồng bộ Lead Sang HubSpot**
7. **Node "SubmitraX Trigger" (CUSTOM.submitraxTrigger)**
   - **Điền `formId`** từ **Giai đoạn 1** vào đây để **nhận sự kiện submit**.
8. **Node "Create or update a contact" (hubspot)**
   - **Chỉnh sửa mapping dữ liệu** để phù hợp với trường HubSpot:
     - `$json.data.name` → **First Name**
     - `$json.data.email` → **Email**
     - `$json.data.company` → **Company**
     - `$json.data.website` → **Website**
   - **Chọn credentials HubSpot** đã cấu hình trước.
9. **Node "Code" (n8n-nodes-base.code)**
   - **Không cần chỉnh sửa**, nó **chuyển đổi dữ liệu** để phù hợp với HubSpot.

#### **3. Kích hoạt ⚡️**
- **Test run** với dữ liệu mẫu:
  1. Nhấn **"Run Workflow"** và kiểm tra **log** để đảm bảo mọi thứ hoạt động.
  2. Mở **URL production** của node **"Form viewer"** trong trình duyệt.
  3. **Điền form** và **submit** để kiểm tra lead có được đồng bộ vào HubSpot không.
- **Bật Active** khi đã kiểm tra xong.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH TĂNG CƯỜNG HỆ THỐNG]
- **Thêm Slack/Telegram thông báo lead mới:**
  - Sau node **"Create or update a contact"**, thêm **node Slack/Telegram** để gửi tin nhắn khi có lead mới.
- **Lưu log tự động:**
  - Thêm **node "Set"** sau **"Create or update a contact"** để lưu dữ liệu vào **Google Sheets** hoặc **Airtable**.
- **Thêm trang cảm ơn (Thank You Page):**
  - Sau node **"Create or update a contact"**, thêm **node "Respond to Webhook"** mới để hiển thị trang cảm ơn.
- **Tùy chỉnh CSS:**
  - Thay đổi **inline CSS** trong node **"Display the form"** để làm form đẹp hơn.
- **Đồng bộ với CRM khác:**
  - Thay thế node **HubSpot** bằng **Salesforce, Pipedrive** hoặc **Zoho CRM** và điều chỉnh mapping dữ liệu.
:::

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công thu thập lead, đồng thời **tối ưu hóa quy trình bán hàng** bằng cách tự động đồng bộ dữ liệu vào HubSpot. **Không cần backend, không cần hosting**, chỉ cần **n8n + SubmitraX + HubSpot** là đã có một hệ thống **hoạt động 24/7**.

**🚀 Hãy áp dụng ngay và bắt đầu thu thập lead tự động hôm nay!**
Nếu có vấn đề hoặc cần **tùy chỉnh thêm**, các sếp có thể liên hệ với tác giả qua: **[thomas@pollup.net](mailto:thomas@pollup.net)**.

---
**🔹 Xem thêm workflows hữu ích từ PollupAI tại:** [n8n.io/creators/zeerobug](https://n8n.io/creators/zeerobug)