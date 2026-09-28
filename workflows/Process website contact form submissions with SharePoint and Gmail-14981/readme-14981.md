---
title: "🚀 Tự Động Hóa Form Liên Hệ Website → Lưu SharePoint + Gửi Email Branded (Không Code)"
description: "Workflow tự động nhận dữ liệu từ form liên hệ website, lưu trữ vào SharePoint và gửi email thông báo có thiết kế branded, tiết kiệm 90% thời gian phản hồi cho các sếp. Hoạt động 24/7 mà không cần viết một dòng code."
slug: "tieu-dong-hoa-form-lien-he-website-luu-sharepoint-gui-email-branded"
tags: [n8n, automation, ticket-management, sharepoint, gmail, no-code]
keywords: [tự động hóa form liên hệ website, lưu dữ liệu sharepoint, gửi email branded, n8n workflow, tự động hóa không code]
---

# 🚀 **Tự Động Hóa Form Liên Hệ Website → Lưu SharePoint + Gửi Email Branded (Không Code)**

### **Giải pháp cho các sếp:**
- **Chán phải nhập liệu thủ công?** Form liên hệ website của bạn đang "tàng trữ" trong không gian ảo, khiến các sếp phải mất thời gian tìm kiếm và phản hồi?
- **Không biết cách kết nối dữ liệu?** Muốn lưu dữ liệu vào SharePoint và gửi email thông báo tự động, nhưng không biết bắt đầu từ đâu?
- **Email thông báo không chuyên nghiệp?** Các email phản hồi hiện tại trông như "máy gửi", không thể thể hiện thương hiệu của doanh nghiệp?

**Workflow này sẽ giải quyết tất cả!** Khi khách hàng gửi form liên hệ, hệ thống sẽ:
✅ **Tự động nhận dữ liệu** từ form (Tên, Email, Điện thoại, Nội dung, Thời gian).
✅ **Lưu trữ vào SharePoint** để quản lý và tra cứu dễ dàng.
✅ **Gửi email thông báo có thiết kế branded** (logo, màu sắc, tên doanh nghiệp) đến email của các sếp.
✅ **Cài đặt Reply-To tự động** để khách hàng có thể phản hồi một cách nhanh chóng.

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian phản hồi:** Không cần nhập liệu thủ công, dữ liệu tự động lưu vào SharePoint và gửi email.
- **Quản lý dễ dàng:** Tất cả thông tin khách hàng được lưu trữ sạch sẽ trong SharePoint, có thể tra cứu và phân loại dễ dàng.
- **Email chuyên nghiệp:** Email thông báo có thiết kế branded, tăng tính chuyên nghiệp và sự tin tưởng của khách hàng.
- **Hoạt động 24/7:** Hệ thống tự động hoạt động mà không cần can thiệp của con người.
- **Phản hồi nhanh chóng:** Khách hàng có thể phản hồi một cách dễ dàng nhờ tính năng Reply-To tự động.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
- **Tài khoản Microsoft SharePoint** (để lưu trữ dữ liệu form).
- **Tài khoản Gmail** (để gửi email thông báo).
- **API Key hoặc OAuth2 Credentials** cho:
  - **Microsoft SharePoint** (để kết nối với SharePoint).
  - **Gmail** (để gửi email).
- **URL Webhook** của website (để nhận dữ liệu từ form).
- **Logo và thông tin thương hiệu** (để tùy chỉnh email branded).
- **Danh sách email của các sếp** (để nhận thông báo).
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập vào tài khoản.
2. Vào **Workflow** → **Create new workflow**.
3. Nhấp vào **Import** và chọn file JSON (nếu có) hoặc copy/paste JSON từ [link gốc](https://n8n.io/workflows/14981).
4. Nhấp **Import** để hoàn tất.

:::note[LƯU Ý]
- Nếu các sếp tự động hóa trên **VPS**, hãy đảm bảo cài đặt n8n trên máy chủ ổn định (không bị ngắt kết nối).
- Để workflow hoạt động 24/7, các sếp nên cài đặt **n8n trên VPS riêng** (Self-hosted).
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **a. Node Webhook (Nhận dữ liệu từ form)**
- **Tên Node:** `Webhook`
- **Cấu hình:**
  - **Path:** `form-processor` (đảm bảo website form gửi dữ liệu đến đường dẫn này).
  - **HTTP Method:** `POST` (phù hợp với form submit).
- **Lưu ý:**
  - Đảm bảo website form của các sếp có **action URL** trỏ đến `https://<domain-n8n>/webhook/form-processor`.
  - Ví dụ: Nếu website của các sếp là `example.com`, thì form nên gửi dữ liệu đến `https://n8n.example.com/webhook/form-processor`.

#### **b. Node Log Submission to SharePoint (Lưu dữ liệu vào SharePoint)**
- **Tên Node:** `Log Submission to SharePoint`
- **Cấu hình:**
  - **Credentials:** Chọn `microsoftSharePointOAuth2Api` (đã cấu hình trước).
  - **Operation:** `create` (tạo mới mục trong danh sách SharePoint).
  - **Resource:** `item` (lưu vào mục item của danh sách).
  - **Site Address:** Nhập địa chỉ SharePoint của các sếp (ví dụ: `https://yourcompany.sharepoint.com/sites/YourSite`).
  - **List Name:** Chọn danh sách SharePoint muốn lưu dữ liệu.
  - **Columns Mapping:** Đảm bảo các trường (Name, Email, Phone, Message, Date, Time) trùng khớp với các cột trong danh sách SharePoint.
- **Lưu ý:**
  - Nếu danh sách SharePoint chưa có các cột tương ứng, các sếp cần **tạo mới** trước khi chạy workflow.
  - Ví dụ:
    ```json
    {
      "Name": "{{$json["Name"]}}",
      "Email": "{{$json["Email"]}}",
      "Phone": "{{$json["Phone"]}}",
      "Message": "{{$json["Message"]}}",
      "Date": "{{$json["Date"]}}",
      "Time": "{{$json["Time"]}}"
    }
    ```

#### **c. Node Build Branded Email HTML (Tạo email branded)**
- **Tên Node:** `Build Branded Email HTML`
- **Cấu hình:**
  - Đây là **node Code**, các sếp cần thay đổi nội dung trong `JavaScript` để phù hợp với thương hiệu.
  - **Thay đổi các biến sau trong code:**
    ```javascript
    const LOGO_URL      = 'https://yourwebsite.com/path/to/your-logo.png'; // Thay URL logo
    const BRAND_NAME    = 'Tên Công Ty Của Các Sếp'; // Thay tên công ty
    const BRAND_WEBSITE = 'yourwebsite.com'; // Thay domain website
    const COLOR_HEADER  = '#004080'; // Màu header (thay theo màu thương hiệu)
    const COLOR_ACCENT  = '#ffc107'; // Màu nhấn mạnh (thay theo màu thương hiệu)
    const COLOR_BUTTON  = '#008080'; // Màu nút CTA (thay theo màu thương hiệu)
    ```
  - **Lưu ý:**
    - Các sếp có thể sử dụng **HTML Editor** để tạo email đẹp hơn (nếu muốn).
    - Đảm bảo **logo và màu sắc** phù hợp với branding của doanh nghiệp.

#### **d. Node Send Email Notification (Gửi email)**
- **Tên Node:** `Send Email Notification`
- **Cấu hình:**
  - **Credentials:** Chọn `gmailOAuth2` (đã cấu hình trước).
  - **Send To:** Nhập email của các sếp (ví dụ: `team@example.com`).
  - **Subject:** Thay đổi tiêu đề email (ví dụ: `📩 Mới có tin nhắn từ khách hàng: {{$json["Name"]}}`).
  - **Reply-To:** Đặt thành `{{$json["Email"]}}` để khách hàng có thể phản hồi trực tiếp.
  - **HTML Body:** Sử dụng kết quả từ node `Build Branded Email HTML`.
- **Lưu ý:**
  - Nếu muốn **CC hoặc BCC** thêm người nhận, các sếp có thể thêm vào trường `CC` hoặc `BCC` trong node này.
  - Ví dụ:
    ```json
    {
      "cc": "support@example.com",
      "bcc": "manager@example.com"
    }
    ```

---

### **3. Kích hoạt ⚡️**
1. **Test Run:** Các sếp có thể gửi một dữ liệu mẫu từ form website để kiểm tra workflow.
   - Kiểm tra **SharePoint** xem dữ liệu có được lưu không.
   - Kiểm tra **Gmail** xem email có được gửi không.
2. **Active Workflow:** Sau khi kiểm tra thành công, các sếp có thể bật **Active** để workflow hoạt động liên tục.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::info[MỘT SỐ Ý TƯỞNG NÂNG CAO]
- **Gửi email báo cáo định kỳ:** Các sếp có thể thêm một node **Schedule** để gửi báo cáo tổng hợp số lượng form nhận được hàng ngày/tuần.
- **Kết nối với Slack/Telegram:** Thêm node **Slack** hoặc **Telegram** để thông báo tức thời khi có form mới.
- **Lưu log hoạt động:** Sử dụng node **StickyNote** hoặc **HTTP Request** để lưu log hoạt động của workflow.
- **Tùy chỉnh email theo loại form:** Nếu website có nhiều loại form (hỗ trợ, phản hồi, phản ánh), các sếp có thể thêm điều kiện trong node **Code** để gửi email khác nhau.
- **Xử lý lỗi tự động:** Thêm node **Set** hoặc **If** để xử lý trường hợp dữ liệu không hợp lệ (ví dụ: email trống).
:::

---

## 📌 **Kết luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn quá trình xử lý form liên hệ**, tiết kiệm thời gian và tăng tính chuyên nghiệp của doanh nghiệp. Bằng cách kết nối **form website → SharePoint → Email branded**, các sếp không chỉ quản lý dữ liệu hiệu quả mà còn cung cấp trải nghiệm tốt nhất cho khách hàng.

**Hãy áp dụng ngay và bắt đầu tự động hóa ngay hôm nay!** 🚀

---
:::note[CHÚ Ý CUỐI CÙNG]
- Nếu các sếp gặp khó khăn trong quá trình cấu hình, hãy tham khảo [hướng dẫn cài đặt n8n trên VPS](https://docs.n8n.io/hosting/self-hosted/) hoặc liên hệ với [AI Solutions](https://aisolutions.vn/) để hỗ trợ.
- Để tối ưu hóa hiệu suất, các sếp nên cài đặt n8n trên **VPS với tài nguyên cao** (ví dụ: VPS Xeon 4GB).
:::

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::