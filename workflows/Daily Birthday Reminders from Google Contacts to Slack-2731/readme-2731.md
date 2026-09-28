---
title: "🎉 Tự Động Gửi Nhắc Nhở Sinh Nhật Hàng Ngày Từ Google Contacts Sang Slack - Không Cần Code!"
description: "Workflow tự động hóa gửi nhắc nhở sinh nhật hàng ngày từ danh bạ Google Contacts sang Slack, giúp các sếp không bao giờ quên sinh nhật của đồng nghiệp, khách hàng hay thành viên trong nhóm. Giúp tăng cường sự gắn kết và chuyên nghiệp trong môi trường làm việc."
slug: "tự-dộng-gửi-nhắc-nhở-sinh-nhật-từ-google-contacts-sang-slack"
tags: [n8n, tự động hóa, google-contacts, slack, nhắc nhở sinh nhật, no-code, team-management]
keywords: [n8n workflow sinh nhật, tự động hóa nhắc nhở sinh nhật, gửi sinh nhật qua slack, tự động hóa google contacts, lưu trữ sinh nhật, quản lý sinh nhật nhóm]
---

# 🎉 **Tự Động Gửi Nhắc Nhở Sinh Nhật Hàng Ngày Từ Google Contacts Sang Slack**

### **🔥 Bạn đã bao giờ quên sinh nhật của đồng nghiệp, khách hàng hay thành viên trong nhóm?**
Trong môi trường làm việc hiện đại, việc nhắc nhở sinh nhật không chỉ thể hiện sự quan tâm mà còn giúp tăng cường tinh thần đồng đội và sự chuyên nghiệp. Tuy nhiên, việc làm thủ công không chỉ tốn thời gian mà còn dễ bị quên lãng. **Workflow này giải quyết vấn đề này hoàn toàn tự động hóa, chỉ cần cài đặt một lần là nó sẽ hoạt động 24/7!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định và không bị gián đoạn, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải kiểm tra danh bạ hàng ngày.
- **Chính xác 100%**: Nhắc nhở sinh nhật chính xác theo ngày tháng.
- **Tích hợp Slack**: Nhắc nhở được gửi trực tiếp vào kênh Slack của nhóm.
- **Hoạt động liên tục**: Sử dụng trigger hàng ngày để không bỏ lỡ bất kỳ sinh nhật nào.
- **Dễ dàng tùy chỉnh**: Thêm thông tin cá nhân hóa như lời chúc, hình ảnh hoặc link chúc mừng.
:::

---

### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** với quyền truy cập vào **Google Contacts**.
2. **Tài khoản Slack** và **API Key OAuth2** của Slack (để kết nối với kênh Slack).
3. **Thời gian chạy hàng ngày** (ví dụ: 8h sáng hàng ngày).
4. **Danh sách liên lạc** trong Google Contacts có thông tin sinh nhật đầy đủ.
:::

---

### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải file JSON của workflow từ [đây](https://n8n.io/workflows/2731) (hoặc copy JSON từ trang này).
- **Bước 2**: Mở **n8n Editor** và chọn **"Import"** từ menu.
- **Bước 3**: Dán JSON vào và chọn **"Import"**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **5 node chính**, các sếp cần chú ý cấu hình như sau:

##### **🔹 Node 1: Schedule Trigger (Trigger hàng ngày)**
- **Cấu hình**:
  - Chọn **Cron expression** phù hợp (ví dụ: `0 8 * * *` để chạy lúc 8h sáng hàng ngày).
  - Đảm bảo **Active** được bật.

##### **🔹 Node 2: Google Contacts (Lấy tất cả liên lạc)**
- **Cấu hình**:
  - Chọn **Credentials**: Tạo mới hoặc chọn **Google OAuth2** đã có sẵn.
  - **Operation**: Đảm bảo chọn **"Get All"** để lấy toàn bộ danh bạ.
  - **Thông tin cần thiết**: Workflow sẽ tự động lấy thông tin sinh nhật từ trường **"Birthday"** trong Google Contacts.

##### **🔹 Node 3: Filter (Lọc sinh nhật ngày hôm nay)**
- **Cấu hình**:
  - **Condition**: Chọn **"Date"** và so sánh với ngày hiện tại (`$currentDate`).
  - **Filter logic**: Chỉ giữ lại liên lạc có sinh nhật **ngày hôm nay**.
  - **Lưu ý**: Nếu không có sinh nhật trong Google Contacts, node này sẽ trả về **dữ liệu rỗng**.

##### **🔹 Node 4: If (Kiểm tra dữ liệu)**
- **Cấu hình**:
  - **Condition**: Kiểm tra nếu có **dữ liệu sinh nhật** (`$json["birthday"]`).
  - **Nếu có**: Chuyển sang node Slack để gửi thông báo.
  - **Nếu không**: Dừng workflow (không cần xử lý).

##### **🔹 Node 5: Slack (Gửi nhắc nhở)**
- **Cấu hình**:
  - **Credentials**: Chọn **Slack OAuth2 API** đã cấu hình trước.
  - **Channel**: Chọn kênh Slack muốn gửi thông báo (ví dụ: `#birthday-reminders`).
  - **Message template**: Tùy chỉnh nội dung như:
    ```
    🎉 **Happy Birthday!** 🎂
    Name: $json["name"]
    Birthday: $json["birthday"]
    ```
  - **Lưu ý**: Đảm bảo kênh Slack đã được tạo và các sếp có quyền gửi tin nhắn.

#### **3. Kích hoạt ⚡️**
- **Bước 1**: **Test Run** với dữ liệu mẫu để kiểm tra logic.
- **Bước 2**: Bật **Active** trên workflow.
- **Bước 3**: Đợi đến thời gian chạy hàng ngày (ví dụ: 8h sáng) để nhận kết quả đầu tiên.

---

### **✍️ Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh thông báo Slack**:
   - Thêm **emoji**, **hình ảnh** hoặc **link** chúc mừng từ Google Drive.
   - Ví dụ: `🎁 *$json["name"]* sinh nhật hôm nay! 🎂 [Chúc mừng](https://example.com/wish)`.
2. **Lưu log hoạt động**:
   - Sử dụng **Sticky Note** hoặc **Google Sheets** để lưu lịch sử sinh nhật đã nhắc nhở.
3. **Kết hợp với Google Calendar**:
   - Nếu sinh nhật được lưu trong **Google Calendar**, có thể kết hợp với **Google Calendar API** để lấy dữ liệu chính xác hơn.
4. **Gửi nhắc nhở qua Email**:
   - Thêm node **Email** để gửi thông báo sinh nhật đến cá nhân hoặc nhóm.
5. **Tự động tạo Post-it trên Trello/Notion**:
   - Kết hợp với **Trello API** hoặc **Notion API** để tạo task nhắc nhở sinh nhật.

---

### **📌 Kết luận**
Workflow này không chỉ giúp các sếp **không bao giờ quên sinh nhật** của ai nữa mà còn **tăng cường sự gắn kết trong nhóm** một cách tự động hóa. **Chỉ cần cài đặt một lần là nó sẽ hoạt động mãi!**

🚀 **Hãy áp dụng ngay và làm cho môi trường làm việc của mình trở nên thân thiện hơn!**
Nếu có bất kỳ câu hỏi hoặc gặp khó khăn, hãy để lại comment bên dưới. Chúc các sếp thành công! 🎂🎉