---
title: "🎁 Tự Động Hóa Email Khuyến Mãi Cá Nhân Hóa Cho Khách VIP Khách Sạn Với Salesforce, AI Gemini & Brevo"
description: "Workflow tự động hóa gửi email khuyến mãi độc quyền cho khách hàng tiêu thụ cao tại khách sạn, tăng cường trung thành và tái đặt phòng. Giảm 90% công việc thủ công, tối ưu hóa chi phí marketing."
slug: "tieu-dong-hoa-email-khuyen-mai-khach-vip-khach-san"
tags: [n8n, automation, salesforce, ai, brevo, email-marketing, no-code, chatbot-ai, gemini-ai]
keywords: [tự động hóa khách sạn, email cá nhân hóa, salesforce automation, gemini ai n8n, khuyến mãi khách hàng VIP, brevo email marketing, workflow n8n khách sạn]
---

# 🚀 **Tự Động Hóa Email Khuyến Mãi Cá Nhân Hóa Cho Khách VIP Khách Sạn**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp Khách Sạn**
Bạn đã bao giờ phải:
- **Làm thủ công** theo dõi khách hàng tiêu thụ cao sau checkout?
- **Gửi email khuyến mãi chung chung**, không phù hợp với sở thích cá nhân?
- **Phải tính toán thủ công** tổng chi tiêu của khách hàng từ nhiều dịch vụ (room service, minibar, late checkout...)?
- **Mất thời gian** viết email cá nhân hóa cho từng khách VIP?

Workflow này **giải quyết tất cả** bằng cách:
✅ **Tự động phát hiện** khách hàng tiêu thụ cao từ Salesforce.
✅ **Tính toán chính xác** tổng chi tiêu từ tất cả dịch vụ.
✅ **Sử dụng AI Gemini** để tạo **lời khuyến mãi cá nhân hóa** dựa trên hành vi sử dụng dịch vụ.
✅ **Gửi email tự động** qua Brevo (Sendinblue) với nội dung độc quyền, tăng tỷ lệ mở và chuyển đổi.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** so với cách làm thủ công.
- **Tăng trung thành khách hàng** với email cá nhân hóa (tỷ lệ mở cao hơn 30%).
- **Tối ưu chi phí marketing** bằng cách chỉ khuyến mãi cho khách VIP thực sự.
- **Hoạt động liên tục** 24/7, không cần can thiệp của nhân viên.
- **Tăng doanh thu tái đặt phòng** từ khách hàng đã tiêu thụ cao.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Salesforce** (với quyền truy cập vào đối tượng `Guest__c` và các dịch vụ như Room Service, Minibar, Late Checkout...).
✔ **API Key Salesforce OAuth2** (để kết nối với n8n).
✔ **Tài khoản Brevo (Sendinblue)** (để gửi email).
✔ **API Key Brevo** (để kết nối với n8n).
✔ **Google Vertex AI API Key** (để sử dụng Gemini AI).
✔ **Template email HTML** (để cá nhân hóa nội dung).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/5936](https://n8n.io/workflows/5936).
- Vào **n8n Editor** → Nhấn **Import** → Chọn file JSON vừa tải.
- **Hoặc** copy toàn bộ JSON và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **8 node** chính, các sếp cần chú ý cấu hình như sau:

##### **🔹 Node 1: "Check for any latest checkouts" (Salesforce Trigger)**
- **Kết nối với Salesforce** bằng `salesforceOAuth2Api`.
- **Chọn đối tượng** `Guest__c` (hoặc tương đương trong hệ thống của bạn).
- **Lọc theo trường** `Checkout_Date__c` (hoặc trường tương tự để phát hiện checkout mới).

##### **🔹 Node 2: "Extract Checkout information" (Salesforce)**
- **Chọn cùng credentials** `salesforceOAuth2Api`.
- **Operation**: `getAll` (lấy tất cả dữ liệu của đối tượng `Guest__c`).
- **Resource**: `customObject` (đối tượng tùy chỉnh `Guest__c`).

##### **🔹 Node 3: "Look For VIP Clients" (Code)**
- **Mã JavaScript** sẽ tính tổng chi tiêu từ các dịch vụ:
  ```javascript
  // Ví dụ: Tính tổng chi tiêu từ các trường như RoomService_Amount__c, Minibar_Amount__c, etc.
  const totalSpend = (
    item.RoomService_Amount__c +
    item.Minibar_Amount__c +
    item.Laundry_Amount__c +
    item.LateCheckout_Fee__c +
    item.ExtraBed_Fee__c +
    item.AirportTransfer_Fee__c
  );
  return { totalSpend };
  ```
- **Chú ý**: Các sếp cần **đổi tên trường** phù hợp với cấu trúc Salesforce của mình.

##### **🔹 Node 4: "Check the threshold exceedings" (If)**
- **Điều kiện**: `{{ $json.totalSpend }} >= 50` (hoặc ngưỡng khác tùy doanh nghiệp).
- Nếu khách hàng tiêu thụ ≥ **$50**, workflow tiếp tục.

##### **🔹 Node 5: "Give Away Personalised Offers" (LM Chat Google Vertex)**
- **Kết nối với Google Vertex AI** bằng `googleApi`.
- **Prompt AI** sẽ tự động tạo lời khuyến mãi cá nhân hóa:
  ```plaintext
  "Tôi là khách hàng VIP của khách sạn [Tên Khách Sạn]. Tôi đã sử dụng các dịch vụ sau:
  - Room Service: [Số lần]
  - Minibar: [Số lần]
  - Late Checkout: [Số lần]
  Hãy đề xuất một dịch vụ chưa được sử dụng mà tôi có thể nhận miễn phí trong lần tới."
  ```
- **Output**: AI trả về một lời khuyến mãi ví dụ: *"Enjoy a complimentary minibar selection on your next stay."*

##### **🔹 Node 6: "Structured Output Parser" (Output Parser Structured)**
- **Chuyển đổi output của AI** thành định dạng JSON dễ sử dụng.
- **Chú ý**: Cấu trúc JSON phải khớp với định dạng mà **Brevo** sẽ đọc.

##### **🔹 Node 7: "Send offer via email" (SendInBlue)**
- **Kết nối với Brevo** bằng `sendInBlueApi`.
- **Template email**: Sử dụng **HTML template** đã chuẩn bị (có thể là template mặc định hoặc tự tạo).
- **Thay đổi biến**:
  - `{{ $json.firstName }}` → Tên khách hàng.
  - `{{ $json.offer }}` → Lời khuyến mãi từ AI.
  - `{{ $json.email }}` → Email của khách hàng.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Nhấn **Run Workflow** với dữ liệu mẫu (ví dụ: một khách hàng đã checkout).
- **Kiểm tra email**: Đảm bảo email được gửi thành công và nội dung cá nhân hóa.
- **Bật Active**: Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** để thông báo khi có khách VIP mới nhận được khuyến mãi.
   - Ví dụ: *"Khách hàng [Tên] đã nhận khuyến mãi minibar miễn phí!"*

2. **Lưu log hoạt động**:
   - Sử dụng node **Sticky Note** hoặc **Google Sheets** để ghi lại lịch sử khuyến mãi đã gửi.

3. **Báo cáo định kỳ**:
   - Tạo một workflow phụ để **tính tổng doanh thu từ khuyến mãi** và gửi báo cáo hàng tháng qua email.

4. **Cập nhật ngưỡng VIP**:
   - Thay đổi ngưỡng `>= 50` thành `>= 100` nếu doanh nghiệp muốn khuyến mãi cho khách VIP cao cấp hơn.

5. **Tối ưu AI**:
   - Thử nghiệm với **prompt khác** để AI tạo ra lời khuyến mãi hấp dẫn hơn (ví dụ: thêm phần "Why this offer?").

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công, đồng thời **tăng trung thành khách hàng** bằng cách gửi email khuyến mãi **cá nhân hóa và độc quyền**. **Chỉ cần import, cấu hình và bật Active** – hệ thống sẽ tự động hoạt động 24/7!

**🚀 Hãy áp dụng ngay và thấy sự khác biệt trong doanh thu tái đặt phòng!**

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/5936)**
**💬 Có thắc mắc? Hãy để lại comment bên dưới!**