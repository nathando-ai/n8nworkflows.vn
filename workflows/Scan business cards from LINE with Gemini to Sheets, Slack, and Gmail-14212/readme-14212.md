---
title: "🚀 Tự Động Hóa Quét & Trích Xuất Thông Tin Thẻ Doanh Nghiệp từ LINE bằng Gemini → Sheets, Slack & Email (Không Cần Code)"
description: "Workflow tự động hóa hoàn toàn quét ảnh thẻ doanh nghiệp từ LINE, trích xuất dữ liệu bằng AI Gemini, lưu vào Google Sheets, thông báo Slack và gửi email cảm ơn tự động. Giúp các sếp tiết kiệm 100% thời gian thủ công sau các buổi networking."
slug: "tieu-xuat-thanh-tin-the-doanh-nghiep-tu-line-bang-gemini"
tags: [n8n, automation, no-code, ai-integration, google-sheets, slack, gmail, line-bot, gemini-ai]
keywords: [tự động hóa quét thẻ doanh nghiệp, n8n workflow gemini, quét ảnh thẻ bằng ai, lưu dữ liệu vào google sheets, thông báo slack tự động, gửi email cảm ơn từ line]
---

# 🚀 **Tự Động Hóa Quét Thẻ Doanh Nghiệp từ LINE → AI Gemini → Sheets, Slack & Email (Không Cần Code)**

### **🔥 Nỗi Đau Của Các Sếp Sau Buổi Networking?**
Sau mỗi buổi gặp gỡ, bạn phải:
- **Quét hàng chục thẻ doanh nghiệp** bằng tay (tốn thời gian, dễ sai sót).
- **Ghi chép dữ liệu** vào Google Sheets hoặc Excel (rất nhàm chán).
- **Lưu trữ và theo dõi** thông tin liên lạc của đối tác (rất khó quản lý).
- **Bỏ lỡ cơ hội** vì không có thời gian liên hệ lại ngay sau buổi gặp.

**Workflow này giải quyết tất cả!** Chỉ cần **chụp ảnh thẻ doanh nghiệp và gửi lên LINE**, AI Gemini sẽ tự động:
✅ **Trích xuất** tên, công ty, chức vụ, email, điện thoại, địa chỉ.
✅ **Lưu vào Google Sheets** (cập nhật tự động).
✅ **Thông báo Slack** cho toàn bộ team.
✅ **Gửi email cảm ơn** nếu có địa chỉ email.
✅ **Xác nhận thành công** trên LINE.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**).
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (ổn định, tốc độ cao).
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian thủ công** sau buổi networking.
- **Dữ liệu chính xác 100%** nhờ AI Gemini trích xuất tự động.
- **Cập nhật liên tục** vào Google Sheets (không cần update thủ công).
- **Thông báo ngay** cho team qua Slack và gửi email cảm ơn tự động.
- **Xác nhận thành công** trên LINE, tránh mất thông tin.
- **Dễ dàng mở rộng** (thêm LinkedIn, địa chỉ, số điện thoại...).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản LINE Developer** (để tạo Webhook).
✔ **Google Gemini API Key** (miễn phí cho phiên bản free tier).
✔ **Google Sheet** (cần chia sẻ với service account của n8n).
✔ **Slack Workspace** (để thiết lập channel thông báo).
✔ **Tài khoản Gmail** (để gửi email cảm ơn tự động).
✔ **Credentials trong n8n**:
   - LINE Messaging API.
   - Google Sheets (OAuth hoặc chia sẻ sheet).
   - Slack Token.
   - Gmail OAuth.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/14212](https://n8n.io/workflows/14212).
- **Mở n8n Editor** → **Import Workflow** → Chọn file JSON.
- **Hoặc copy toàn bộ JSON** vào **Create Workflow** → **Paste JSON**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **14 node**, các sếp cần chú ý cấu hình sau:

##### **🔹 Node 1: LINE Webhook**
- **Cấu hình Webhook**:
  - **Path**: `line-webhook` (không đổi).
  - **HTTP Method**: `POST`.
  - **URL**: Sau khi import, copy **Webhook URL** từ node này và **đăng ký trong LINE Developer Console**.
    - Trên [LINE Developers](https://developers.line.biz/), tạo **Channel** → **Messaging API** → **Add Webhook URL**.
    - **Channel Secret** và **Channel Access Token** sẽ cần trong **Credentials** của n8n.

##### **🔹 Node 3: Set Config Values**
- **Thiết lập biến mặc định**:
  - `sheetName`: Tên sheet trong Google Sheets (ví dụ: `Business_Cards`).
  - `slackChannel`: Tên channel Slack (ví dụ: `#contacts`).
  - `gmailSubject`: Tiêu đề email (ví dụ: `Thank you for connecting!`).

##### **🔹 Node 5: Is Image Message? (Node IF)**
- **Kiểm tra loại tin nhắn**:
  - Nếu **không phải ảnh**, workflow sẽ **bỏ qua** và gửi phản hồi "Vui lòng gửi ảnh thẻ doanh nghiệp".
  - Nếu **là ảnh**, workflow tiếp tục xử lý.

##### **🔹 Node 6: Download Image from LINE**
- **Không cần chỉnh sửa**, node này tự động tải ảnh từ LINE.

##### **🔹 Node 7 & 8: Gemini AI Trích Xuất Dữ Liệu**
- **Node 7 (Parse Gemini JSON response)**: **Code Node** (JavaScript).
  - **Mã nguồn**:
    ```javascript
    // Chỉnh sửa để phù hợp với cấu trúc JSON trả về từ Gemini
    const data = {
      name: $input.all().imageData.name,
      company: $input.all().imageData.company,
      position: $input.all().imageData.position,
      email: $input.all().imageData.email || "N/A",
      phone: $input.all().imageData.phone || "N/A",
      address: $input.all().imageData.address || "N/A"
    };
    return data;
    ```
  - **Lưu ý**: Cần **đảm bảo cấu trúc JSON** từ Gemini phù hợp với mã trên. Nếu không, cần **cập nhật mã** để trích xuất đúng dữ liệu.

- **Node 8 (Google Gemini Chat Model)**:
  - **Prompt mặc định**:
    ```plaintext
    You are an expert in extracting business card information.
    Given an image of a business card, extract the following fields:
    - Name (Full Name)
    - Company Name
    - Position/Title
    - Email Address (if available)
    - Phone Number (if available)
    - Address (if available)
    Return the result in JSON format:
    {
      "name": "John Doe",
      "company": "TechCorp",
      "position": "CEO",
      "email": "john.doe@techcorp.com",
      "phone": "+1234567890",
      "address": "123 Main St, San Francisco, CA"
    }
    ```
  - **Không cần chỉnh sửa** nếu muốn sử dụng mặc định.

##### **🔹 Node 9: Save Contact to Google Sheets**
- **Chọn Credentials**:
  - **Google Sheets OAuth** (nếu đã cấu hình trước).
  - **Sheet Name**: Đặt theo biến `sheetName` trong **Set Config Values**.
  - **Headers**: Đảm bảo trùng khớp với cột trong sheet (ví dụ: `Name`, `Company`, `Email`, `Phone`, `Address`).

##### **🔹 Node 10: Notify Team on Slack**
- **Cấu hình Slack**:
  - **Token**: Chọn **Slack Token** trong Credentials.
  - **Channel**: Đặt theo biến `slackChannel`.
  - **Message Blocks**: Có thể chỉnh sửa nội dung thông báo (ví dụ thêm emoji, link).

##### **🔹 Node 11: Has Email Address? (Node IF)**
- **Kiểm tra xem có email không**:
  - Nếu **có email**, workflow sẽ **tiếp tục gửi email**.
  - Nếu **không có email**, workflow sẽ **bỏ qua** node Gmail.

##### **🔹 Node 12: Send Thank-you Email via Gmail**
- **Cấu hình Gmail**:
  - **Credentials**: Chọn **Gmail OAuth**.
  - **Subject**: Đặt theo biến `gmailSubject`.
  - **Body**: Có thể chỉnh sửa nội dung email (ví dụ thêm thông tin chi tiết).

##### **🔹 Node 13 & 14: Reply Success/Error on LINE**
- **Node 13 (Reply success message)**: Gửi tin nhắn thành công.
- **Node 14 (Reply no-image message)**: Gửi tin nhắn nếu không phải ảnh.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Gửi **một ảnh thẻ doanh nghiệp** từ LINE đến Webhook.
   - Kiểm tra:
     - **Google Sheets** có cập nhật dữ liệu không?
     - **Slack** có thông báo không?
     - **Gmail** có gửi email không?
     - **LINE** có phản hồi thành công không?

2. **Bật Active**:
   - Sau khi test thành công, **bật workflow** để hoạt động liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tweak Prompt Gemini**:
   - Mở rộng để trích xuất thêm **LinkedIn**, **địa chỉ chi tiết**, **số điện thoại quốc tế**.
   - Ví dụ:
     ```plaintext
     Extract LinkedIn URL if available, and include department information.
     ```

2. **Lưu Log Dữ Liệu**:
   - Thêm **node `stickyNote`** để lưu lịch sử trích xuất (giúp debug nếu có lỗi).

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **node `set` + `schedule`** để gửi báo cáo hàng tuần về số lượng contact mới.

4. **Kết Nối với CRM**:
   - Thêm **node HubSpot** hoặc **Salesforce** để tự động thêm contact vào hệ thống CRM.

5. **Tự Động Xóa Ảnh**:
   - Thêm **node `httpRequest`** để xóa ảnh sau khi xử lý (giảm dung lượng lưu trữ).

---

### 📌 **Kết Luận**
Workflow này **giải phóng hoàn toàn thời gian** của các sếp sau các buổi networking, đồng thời **tăng cường hiệu quả** trong quản lý contact. **Chỉ cần chụp ảnh và gửi lên LINE**, AI sẽ làm tất cả!

**🚀 Hành động ngay**:
1. **Import workflow** vào n8n.
2. **Cấu hình credentials** (LINE, Google, Slack, Gmail).
3. **Test với một ảnh thẻ** và **bật workflow**!
4. **Mở rộng** theo nhu cầu (thêm Slack, email, CRM...).

**Nếu có vấn đề**, hãy để lại comment bên dưới hoặc liên hệ với **Ryo Sayama** (tác giả) qua [n8n Community](https://community.n8n.io/). Chúc các sếp thành công! 💪

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/14212)** | **📌 [Cài đặt n8n Self-hosted](https://docs.n8n.io/)**