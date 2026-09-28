---
title: "🚀 Tự Động Hóa Chuyển Nhận Thông Tin Thẻ Business Từ QR Code Sang KlickTipp (GDPR Compliant)"
description: "Workflow này giúp các sếp **quét thẻ business qua QR code**, tự động **trích xuất dữ liệu** (tên, email, số điện thoại, địa chỉ...) và **nộp hồ sơ khách hàng** vào KlickTipp với **Double Opt-In (DOI)**. Giúp tiết kiệm thời gian, giảm sai sót và tối ưu hóa quy trình lead generation tại các sự kiện."
slug: "tu-dong-hoa-chuyen-nhan-thong-tin-tha-business-tu-qr-code-sang-klicktipp"
tags: [n8n, automation, lead-generation, klicktipp, qr-code, no-code]
keywords: [n8n workflow tự động hóa, chuyển nhận thẻ business qua QR code, KlickTipp tự động, Double Opt-In DOI, lead generation sự kiện]
---

# 🚀 **Tự Động Hóa Chuyển Nhận Thẻ Business Từ QR Code Sang KlickTipp (GDPR Compliant)**

## **🔥 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hàng ngày, các sếp phải **quét hàng chục thẻ business** tại các sự kiện, hội nghị, hoặc buổi gặp gỡ khách hàng. Quá trình này tốn thời gian, dễ xảy ra **sai sót** (ghi nhầm tên, email, số điện thoại) và **không thể tự động hóa** để tích hợp vào hệ thống CRM. Kết quả?
- **Tốn thời gian** (tính bằng giờ/lần sự kiện).
- **Không đảm bảo tính chính xác** (do ghi nhớ hoặc nhập sai).
- **Không tích hợp tự động** vào hệ thống marketing, dẫn đến mất cơ hội theo dõi khách hàng.

**Workflow này giải quyết tất cả!** Chỉ cần **quét QR code trên thẻ business**, hệ thống sẽ **tự động trích xuất dữ liệu**, **tạo hồ sơ khách hàng** trong KlickTipp với **Double Opt-In (DOI)** (tuân thủ GDPR), và **gắn thẻ** để phân loại dễ dàng.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm thời gian** (không cần nhập liệu thủ công).
✅ **Tăng độ chính xác** (trích xuất tự động từ vCard).
✅ **Tuân thủ GDPR** (Double Opt-In bắt buộc).
✅ **Tích hợp tự động** vào KlickTipp (CRM & Marketing Automation).
✅ **Phân loại khách hàng** (gắn thẻ "vCard QR code scan").
✅ **Hoạt động 24/7** (không phụ thuộc vào nhân viên).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản KlickTipp** (đã kích hoạt API).
2. **Tài khoản AllCodeRelay** (để quét QR code).
3. **Thẻ business có QR code vCard** (cần định dạng **vCard trực tiếp**, không phải URL).
4. **Mã API KlickTipp** (tạo từ **Settings > API Access**).
5. **Thẻ phân loại trong KlickTipp** (ví dụ: `vCard QR code scan`).

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow từ file JSON** hoặc **copy/paste JSON vào n8n Editor**:
1. Tải workflow từ [n8n.io/workflows/13621](https://n8n.io/workflows/13621).
2. Trong **n8n Editor**, nhấn **Import** và chọn file JSON.
   **Hoặc**:
   - Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/13621) (đã được chuyển đổi sang định dạng dễ dàng).
   - Trong n8n, nhấn **Create New Workflow** → **Import from JSON** → Dán JSON và nhấn **Import**.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **4 node chính**, các sếp cần **cấu hình kỹ lưỡng** như sau:

#### **🔹 Node 1: AllCodeRelay: Scan Webhook (n8n-nodes-base.webhook)**
- **Chức năng**: Nhận dữ liệu từ AllCodeRelay khi quét QR code.
- **Cấu hình**:
  - **Path**: `qr-code-scanner` (không thay đổi).
  - **HTTP Method**: `POST` (không thay đổi).
  - **Credentials**: Không cần thiết (sử dụng mặc định).
  - **Lưu ý**:
    - Sau khi import, mở node này và **copy URL Test** (hoặc URL Production sau khi publish).
    - Trong **AllCodeRelay**, tạo **webhook destination** và dán URL này vào.

#### **🔹 Node 2: Filter: vCard Only (n8n-nodes-base.filter)**
- **Chức năng**: Lọc chỉ giữ lại dữ liệu có định dạng **vCard** (chứa `BEGIN:VCARD` và `END:VCARD`).
- **Cấu hình**:
  - **Condition**: `$.payload.includes("BEGIN:VCARD") && $.payload.includes("END:VCARD")`.
  - **Lưu ý**:
    - Nếu QR code chỉ chứa **URL** (không phải vCard trực tiếp), workflow **không hoạt động**.
    - Đảm bảo QR code trên thẻ business **chứa toàn bộ nội dung vCard** (không phải link đến trang web).

#### **🔹 Node 3: Parse: vCard → Contact Fields (n8n-nodes-base.code)**
- **Chức năng**: Trích xuất và **chuyển đổi vCard thành các trường dữ liệu chuẩn** (tên, email, số điện thoại, địa chỉ...).
- **Cấu hình**:
  - Mở node này và **chỉnh sửa code JavaScript** như sau:
    ```javascript
    // Trích xuất và định dạng dữ liệu từ vCard
    const vcard = $input.all()[0].json.payload;
    const lines = vcard.split('\n');
    const contact = {};

    for (const line of lines) {
      const [property, value] = line.split(':');
      if (property && value) {
        // Lọc các trường cần thiết
        switch (property) {
          case 'FN': contact.firstName = value; break;
          case 'N': {
            const parts = value.split(';');
            contact.lastName = parts[0];
            contact.firstName = parts[1];
            break;
          }
          case 'EMAIL': contact.email = value; break;
          case 'TEL;TYPE=CELL': contact.mobile = value; break;
          case 'ORG': contact.company = value; break;
          case 'TITLE': contact.position = value; break;
          case 'ADR;TYPE=WORK': {
            const addressParts = value.split(';');
            contact.street = addressParts[0];
            contact.city = addressParts[1];
            contact.state = addressParts[2];
            contact.zip = addressParts[3];
            contact.country = addressParts[4];
            break;
          }
          case 'URL': contact.website = value; break;
        }
      }
    }

    return { json: { contact } };
    ```
  - **Lưu ý**:
    - Nếu vCard có **trường bổ sung** (ví dụ: fax, email thứ 2), các sếp có thể **mở rộng code** để trích xuất.
    - **Test run** với một vCard mẫu để đảm bảo dữ liệu trích xuất chính xác.

#### **🔹 Node 4: KlickTipp: Add Contact with DOI (n8n-nodes-klicktipp.klicktipp)**
- **Chức năng**: **Tạo hoặc cập nhật hồ sơ khách hàng** trong KlickTipp với **Double Opt-In (DOI)**.
- **Cấu hình**:
  1. **Thiết lập credentials**:
     - Nhấn **Add Credentials** → Chọn **KlickTipp**.
     - Điền **tên tài khoản**, **username**, và **password** (hoặc API key).
  2. **Chọn operation**:
     - **Operation**: `subscribe` (đăng ký khách hàng mới).
     - **Resource**: `subscriber` (hồ sơ khách hàng).
  3. **Mapping dữ liệu**:
     - **firstName** → `firstName` (trường tên trong KlickTipp).
     - **lastName** → `lastName`.
     - **email** → `email`.
     - **mobile** → `phone` (hoặc `mobile` nếu KlickTipp hỗ trợ).
     - **company** → `company`.
     - **position** → `jobTitle`.
     - **street**, **city**, **state**, **zip**, **country** → **Address fields** (nếu KlickTipp có).
     - **website** → `website`.
  4. **Double Opt-In (DOI)**:
     - Bật tùy chọn **Double Opt-In** và chọn **tag** đã tạo trước (`vCard QR code scan`).
  - **Lưu ý**:
    - **Test run** với một contact mẫu để đảm bảo **không có lỗi API**.
    - Nếu KlickTipp yêu cầu **thêm trường tùy chỉnh**, các sếp có thể **mở rộng node code** để thêm.

### **3. Kích Hoạt ⚡️**
1. **Test run** với một vCard mẫu:
   - Quét QR code trên thẻ business (đảm bảo chứa vCard trực tiếp).
   - Kiểm tra **log** trong n8n để xác nhận:
     - Dữ liệu đã được **lọc** (Node Filter).
     - Dữ liệu đã được **trích xuất** (Node Code).
     - Hồ sơ đã được **nộp thành công** vào KlickTipp (Node KlickTipp).
2. **Bật Active workflow**:
   - Nhấn **Publish** → **Active** để workflow hoạt động liên tục.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Gửi thông báo Slack/Telegram khi thành công**:
   - Thêm **node Slack/Telegram** sau Node KlickTipp để **báo cáo kết quả** khi tạo contact thành công.
   - Ví dụ: `📩 Khách hàng mới được tạo: [Tên] ([Email]) từ QR code!`.

2. **Lưu log vào Google Sheets/Notion**:
   - Thêm **node Google Sheets** hoặc **Notion** để **ghi lại lịch sử quét QR code**.
   - Dữ liệu có thể bao gồm: **Tên, Email, Ngày giờ quét, Thẻ phân loại**.

3. **Tự động gửi email chào mừng**:
   - Sử dụng **node Email** (Gmail/SendGrid) để **gửi email chào mừng** cho khách hàng mới với liên kết DOI.

4. **Phân loại khách hàng theo ngành nghề**:
   - Nếu vCard chứa **trường `ORG` (công ty)**, các sếp có thể **tự động gắn thẻ** theo ngành nghề (ví dụ: `Tech`, `Finance`).

5. **Hỗ trợ vCard đa email**:
   - Mở rộng **node code** để trích xuất **nhiều email** (ví dụ: `EMAIL;TYPE=WORK`, `EMAIL;TYPE=HOME`).

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc **nhập liệu thủ công**, đồng thời **tăng độ chính xác** và **tích hợp tự động** vào KlickTipp. Với **Double Opt-In (DOI)**, các sếp **tuân thủ GDPR** và xây dựng danh sách khách hàng **chất lượng cao**.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (nếu chưa có).
2. **Import workflow** và **cấu hình các node**.
3. **Test với QR code mẫu** và **bật workflow**.
4. **Quét thẻ business tại sự kiện** và **nhận kết quả tự động**!

👉 **Bắt đầu tự động hóa ngay hôm nay!** 🚀

---
**💡 Cần hỗ trợ thêm?**
- **Trang hỗ trợ n8n**: [https://n8n.io/docs](https://n8n.io/docs)
- **Community KlickTipp**: [https://klicktipp.com](https://klicktipp.com)
- **Hỏi đáp nhanh**: Đăng câu hỏi trên [Forum n8n](https://community.n8n.io/).