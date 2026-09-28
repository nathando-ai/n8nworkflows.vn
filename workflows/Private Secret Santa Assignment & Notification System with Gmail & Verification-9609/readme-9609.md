---
title: "🎄 **Hệ Thống Giao Tặng Bí Mật (Secret Santa) Tự Động Hoá Với Gmail & Xác Minh - Không Cần Code!**"
description: "Workflow tự động hóa hoàn toàn cho Secret Santa giúp các sếp phân phối ngẫu nhiên, gửi thông báo email cá nhân hóa và xóa tin nhắn đã gửi để bảo mật. Giúp tiết kiệm thời gian lên đến 90% so với cách làm thủ công!"
slug: "hop-dong-secret-santa-tu-dong-hoa-voi-gmail"
tags: [n8n, automation, secret-santa, gmail, no-code]
keywords: [n8n workflow secret santa, tự động hóa secret santa, gửi email tự động, phân phối ngẫu nhiên, bảo mật email]
---

# 🎄 **Hệ Thống Giao Tặng Bí Mật (Secret Santa) Tự Động Hoá Với Gmail & Xác Minh**

### **🔥 Nỗi Đau Của Các Sếp Trong Dịp Lễ Giáng Sinh/Hội Ngộ**
Mỗi năm, việc tổ chức **Secret Santa** trong công ty hay gia đình lại là một "đau đầu" lớn:
- **Phân phối ngẫu nhiên thủ công**: Lo ngại có người tự chọn mình hoặc bị trùng lặp.
- **Gửi thông báo email cá nhân hóa**: Phải viết hàng chục email riêng biệt, dễ quên hoặc sai thông tin.
- **Bảo mật tin nhắn**: Email đã gửi vẫn hiện trong hộp thư "Đã gửi", làm lộ thông tin bí mật.
- **Quá trình lâu dài**: Tốn thời gian lên đến **5-10 tiếng** cho một nhóm 50+ người.

**Workflow này giải quyết tất cả!** Với chỉ **một lần setup**, hệ thống sẽ:
✅ **Phân phối ngẫu nhiên** không trùng lặp và không tự chọn mình.
✅ **Gửi email cá nhân hóa** tự động đến từng người nhận.
✅ **Xóa tin nhắn đã gửi** để bảo mật.
✅ **Gửi báo cáo tổng hợp** với kết quả cuối cùng.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Từ **5-10 tiếng** xuống còn **5 phút** setup + **0 thời gian** cho quá trình phân phối.
- **Trải nghiệm cá nhân hóa**: Mỗi email đều có nội dung riêng, không giống nhau.
- **Bảo mật tuyệt đối**: Email đã gửi được xóa ngay, không để lại dấu vết.
- **Không sai sót**: Không có trường hợp trùng lặp hoặc tự chọn mình.
- **Hoạt động 24/7**: Chỉ cần kích hoạt một lần, hệ thống tự động thực hiện.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Gmail chính thức** (để gửi email tự động):
   - **OAuth2 credentials** cho Gmail (cài đặt trong n8n).
   - **Email chính** để nhận báo cáo kết quả cuối cùng.
2. **Danh sách tham gia Secret Santa**:
   - Cấu trúc JSON như sau (điền vào node **"Emails and name"**):
     ```json
     {
       "Jesus": "example1@gmail.com",
       "John": "example2@gmail.com",
       "Alice": "example3@gmail.com"
     }
     ```
   - **Lưu ý**: Không có khoảng trắng trong tên hoặc email.

3. **n8n Self-hosted** (không dùng phiên bản miễn phí trên cloud để đảm bảo hoạt động liên tục).
   :::info[Gợi ý hạ tầng cho n8n]
   Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
   :::
---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/9609) hoặc copy toàn bộ mã JSON từ đây.
- **Cách 1**: Nhấn **"Import"** trong n8n Editor → Dán JSON → Chọn **"Import"**.
- **Cách 2**: Copy toàn bộ mã JSON (trừ phần `---` đầu và cuối) và dán vào **n8n Editor** → Nhấn **"Create Workflow"**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **9 node**, nhưng các node quan trọng cần cấu hình kỹ như sau:

##### **A. Node "Emails and name" (Set)**
- **Nội dung**: Điền danh sách tham gia dưới dạng JSON như ví dụ trên.
- **Lưu ý**:
  - **Không có khoảng trắng** trong tên hoặc email.
  - **Không trùng lặp email**.

##### **B. Node "Send a message" (Gmail)**
- **Credentials**: Chọn **"gmailOAuth2"** (đã cấu hình trước khi import).
- **Nội dung email**:
  - **Tiêu đề**: `"Bạn đã được chỉ định cho Secret Santa!"` (có thể chỉnh sửa).
  - **Nội dung**: Sử dụng template mặc định (hoặc chỉnh sửa trong node **Code** nếu cần).

##### **C. Node "Random" (Code)**
- **Nội dung**: Node này tự động phân phối ngẫu nhiên, **không cần chỉnh sửa**.

##### **D. Node "Delete a message" (Gmail)**
- **Credentials**: Chọn **"gmailOAuth2"** (giống node gửi email).
- **Lưu ý**: Node này **xóa email đã gửi** để bảo mật, **không cần chỉnh sửa**.

##### **E. Node "Name to INT" (Code)**
- **Nội dung**: Tạo báo cáo tổng hợp dưới dạng HTML (ví dụ: `"1 sent to 2<br>2 sent to 3"`).
- **Không cần chỉnh sửa** (nếu muốn thay đổi, mở node và sửa mã JavaScript).

##### **F. Node "Send a message results" (Gmail)**
- **Credentials**: Chọn **"gmailOAuth2"**.
- **Email nhận**: Điền **email chính** của bạn (để nhận báo cáo kết quả).
- **Tiêu đề email**: `"Amic invisible"` (có thể đổi thành `"Kết quả Secret Santa"`).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Run Workflow"** và kiểm tra:
     - Email đã được gửi cho từng người tham gia.
     - Email đã được xóa khỏi hộp thư "Đã gửi".
     - Báo cáo tổng hợp đã được gửi đến email chính.
2. **Bật Active**:
   - Sau khi test thành công, chuyển trạng thái workflow sang **"Active"**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Slack/Telegram Notification**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo kết quả ngay khi workflow hoàn thành.
   - **Cách làm**:
     - Thêm node **Slack Webhook** sau node **"Send a message results"**.
     - Cấu hình với webhook của Slack (tạo tại [api.slack.com](https://api.slack.com/messaging/webhooks)).

2. **Lưu Log Lịch Sử**:
   - Thêm node **Google Sheets** hoặc **Notion** để lưu lại danh sách Secret Santa của năm trước.
   - **Cách làm**:
     - Sau node **"Name to INT"**, thêm node **Google Sheets** với action **"Create Spreadsheet"**.
     - Cấu hình sheet để lưu dữ liệu dưới dạng bảng.

3. **Gửi Báo Cáo Định Kỳ**:
   - Nếu muốn gửi báo cáo kết quả vào ngày trước Lễ Giáng Sinh, sử dụng **n8n Trigger** (n8n.io/triggers) kết hợp với **Google Calendar** hoặc **IFTTT**.

4. **Tùy Chỉnh Nội Dung Email**:
   - Mở node **"Send a message"** → Nhấn **"Edit"** → Chỉnh sửa template email theo phong cách riêng.

---

### 📌 **Kết Luận**
Workflow **Secret Santa Tự Động Hoá** này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tiết kiệm thời gian** và tránh stress trong dịp lễ.
✔ **Bảo mật tuyệt đối** với email đã gửi.
✔ **Trải nghiệm cá nhân hóa** cho từng thành viên.

**Hành động ngay!**
1. **Setup** trên VPS (để workflow hoạt động 24/7).
2. **Import** và **cấu hình** theo hướng dẫn.
3. **Kích hoạt** và chia sẻ với đồng nghiệp!

**Nếu muốn khám phá thêm workflow tự động hóa sáng tạo**, hãy ghé thăm [n8n Creator của Oriol Seguí](https://n8n.io/creators/oxsr11/) để tìm nhiều ý tưởng thú vị khác!

---
**Chúc các sếp có một Secret Santa thành công và vui vẻ!** 🎁✨