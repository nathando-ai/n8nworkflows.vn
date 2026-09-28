---
title: "📁 Tự Động Tạo & Chia Sẻ Thư Mục Khách Hàng Từ Google Sheets Sang Google Drive (N8n)"
description: "Giải pháp tự động hóa hoàn toàn không code để quản lý khách hàng hiệu quả: Tạo thư mục Google Drive cho khách mới, chia sẻ quyền truy cập tự động, và cập nhật liên kết ngay trên Google Sheets. Giúp các sếp tiết kiệm thời gian quản lý file lên đến 80%!"
slug: "tu-dong-hoa-tao-chia-se-thu-muc-khach-hang-google-sheets-google-drive"
tags: [n8n, automation, google-drive, google-sheets, file-management, no-code]
keywords: [tự động hóa n8n, tạo thư mục google drive tự động, chia sẻ file google drive, quản lý khách hàng tự động, workflow google sheets google drive]
---

# 🚀 **Tự Động Tạo & Chia Sẻ Thư Mục Khách Hàng Từ Google Sheets Sang Google Drive**

### **Giải pháp cho ai?**
Các sếp **chụp ảnh, studio ảnh, công ty tư vấn, hoặc bất kỳ doanh nghiệp dịch vụ nào** cần quản lý khách hàng hiệu quả mà không phải mất thời gian thủ công tạo thư mục và chia sẻ quyền truy cập. Hãy tưởng tượng:
- **Khách hàng mới** đăng ký → **tự động** có một thư mục riêng trên Google Drive.
- **Tất cả file** (tài liệu, ảnh, video) được sắp xếp theo cấu trúc **Documents/Media** một cách logic.
- **Chia sẻ quyền truy cập** cho khách hàng **với một cú nhấp chuột** (không cần copy-paste liên kết).
- **Liên kết thư mục** được cập nhật **ngay trên Google Sheets**, giúp bạn theo dõi dễ dàng.

Workflow này **giải phóng bạn khỏi công việc lặp lại**, giúp tập trung vào việc **chăm sóc khách hàng** thay vì quản lý file.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần tạo thư mục thủ công cho từng khách hàng mới.
✅ **Chính xác 100%**: Không lo quên chia sẻ quyền hoặc cập nhật liên kết.
✅ **Cá nhân hóa**: Mỗi khách hàng có một thư mục riêng với cấu trúc **Documents/Media** sẵn sàng.
✅ **Hoạt động liên tục**: Workflow chạy **24/7** ngay cả khi bạn ngủ.
✅ **Dễ dàng theo dõi**: Liên kết thư mục được cập nhật **tự động** trên Google Sheets.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** (đã kết nối với Google Sheets và Google Drive).
2. **Google Sheets** với **bảng dữ liệu** có các cột sau:
   - **Code** (mã khách hàng, ví dụ: `CLIENT-001`)
   - **Name** (tên khách hàng)
   - **Email** (địa chỉ email chia sẻ, có thể nhiều email cách nhau bằng dấu phẩy)
   - **Drive** (cột để lưu **ID thư mục** sau khi tạo)
   - **Url** (cột để lưu **liên kết chia sẻ** thư mục)
3. **Thư mục cha (Parent Folder)** trên Google Drive để lưu tất cả thư mục khách hàng.
4. **Credentials OAuth2** cho:
   - **Google Sheets** (để đọc và cập nhật bảng).
   - **Google Drive** (để tạo, chia sẻ và quản lý thư mục).

---
:::note[LƯU Ý QUAN TRỌNG]
- **Không cần code**: Workflow này **hoàn toàn không cần viết dòng code nào**.
- **Hoạt động khi có dữ liệu mới**: Workflow sẽ **nghe** khi có **dòng mới** được thêm vào Google Sheets.
- **Tùy chỉnh dễ dàng**: Bạn có thể thay đổi tên thư mục con (**Documents/Media**) hoặc thêm cột mới theo nhu cầu.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
**Cách 1: Từ file JSON**
1. Tải workflow từ [đây](https://n8n.io/workflows/16019) (nút **Export**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

**Cách 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Tạo workflow mới.
2. Nhấn **Import** → Chọn **Paste JSON**.
3. Dán toàn bộ JSON từ [đây](https://n8n.io/workflows/16019) (nút **Export**).
4. Nhấn **Import**.

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp **phải cấu hình** các node sau:

##### **A. Cấu hình Credentials (OAuth2)**
1. **Google Sheets OAuth2**
   - Đi đến **Credentials** → **Add new credential** → Chọn **Google Sheets OAuth2**.
   - Theo hướng dẫn để **đăng nhập và cấp quyền** cho n8n truy cập Google Sheets.
   - **Lưu ý**: Chọn **Scopes** là `https://www.googleapis.com/auth/spreadsheets` và `https://www.googleapis.com/auth/drive`.

2. **Google Drive OAuth2**
   - Tương tự như trên, tạo **Google Drive OAuth2**.
   - Chọn **Scopes** là `https://www.googleapis.com/auth/drive` và `https://www.googleapis.com/auth/drive.file`.

##### **B. Cấu hình Node "Configuration" (Set)**
- Mở node **"Configuration"** → Điền **Parent Folder URL** của thư mục cha trên Google Drive.
  - Ví dụ: `https://drive.google.com/drive/folders/1AbCdEfGhIjKlMnOpQrStUvWxYz`

##### **C. Cấu hình Node "Parse client emails" (Code)**
- Mở node **"Parse client emails"** → Sửa code để **phân tách email** từ cột **Email** trong Google Sheets.
  - Code mặc định đã hỗ trợ **email cách nhau bằng dấu phẩy**, nhưng các sếp có thể **tùy chỉnh** nếu cần.
  - **Ví dụ**:
    ```javascript
    // Nếu email là "a@example.com, b@example.com"
    const emails = $input.all().email.split(',').map(email => email.trim());
    $node.set("emails", emails);
    ```

##### **D. Kiểm tra Node "Share folder with client" (Google Drive)**
- Đảm bảo **quyền chia sẻ** được cấu hình đúng:
  - **Role**: Chọn **Viewer** (đọc) hoặc **Editor** (sửa) tùy nhu cầu.
  - **Notify recipients**: Bật để **gửi email thông báo** khi chia sẻ.

##### **E. Kiểm tra Node "Update sheet with folder URL" (Google Sheets)**
- Đảm bảo cột **Drive** và **Url** trong Google Sheets **được định nghĩa đúng**:
  - **Drive**: Lưu **ID thư mục** (ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
  - **Url**: Lưu **liên kết chia sẻ** (ví dụ: `https://drive.google.com/drive/folders/1AbCdEfGhIjKlMnOpQrStUvWxYz`).

---

#### **3. Kích hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Thêm **một dòng mới** vào Google Sheets (ví dụ: `CLIENT-001`, `John Doe`, `john@example.com`).
   - Chạy **manual test** trong n8n để kiểm tra workflow hoạt động như thế nào.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động khi có dữ liệu mới.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm cột theo dõi trạng thái**
   - Thêm cột **Status** vào Google Sheets để ghi **trạng thái** (ví dụ: `Pending`, `Created`, `Shared`).
   - Sử dụng node **Code** để cập nhật trạng thái sau khi tạo thư mục.

2. **Gửi thông báo Slack/Telegram khi tạo thư mục**
   - Thêm node **Slack** hoặc **Telegram** sau node **"Create Client folder"** để **gửi thông báo** khi thư mục được tạo thành công.

3. **Lưu log hoạt động**
   - Thêm node **Google Sheets** hoặc **Google Docs** để **ghi log** tất cả hoạt động (ví dụ: thời gian tạo, người tạo, email chia sẻ).

4. **Tùy chỉnh cấu trúc thư mục**
   - Thay đổi tên **subfolders** (ví dụ: `Documents` → `Contracts`, `Media` → `Photos & Videos`).
   - Thêm **thư mục con mới** như `Contracts`, `Invoices`, `Presentations`.

5. **Sử dụng Google Drive API để chia sẻ với nhóm**
   - Nếu khách hàng là **nhóm người dùng**, thay vì chia sẻ cho email cá nhân, bạn có thể chia sẻ cho **nhóm Google Drive** hoặc **địa chỉ email nhóm**.

---

### 📌 **Kết luận**
Workflow này **giải phóng các sếp khỏi công việc lặp lại** khi quản lý khách hàng, giúp **tự động hóa toàn bộ quy trình** từ tạo thư mục đến chia sẻ quyền truy cập. **Không cần code**, không cần kỹ thuật cao – chỉ cần **cấu hình đúng credentials** và **thêm dữ liệu vào Google Sheets**, workflow sẽ làm tất cả!

**Hành động ngay hôm nay:**
1. **Cài đặt n8n trên VPS** (nếu chưa có).
2. **Import workflow** và **cấu hình credentials**.
3. **Thêm dữ liệu mẫu** vào Google Sheets để test.
4. **Bật Active** và **nhận thư mục khách hàng tự động**!

👉 **Bắt đầu tự động hóa ngay bây giờ** – [Tải workflow từ đây](https://n8n.io/workflows/16019)!

---
**Cần hỗ trợ?** Hãy để lại bình luận bên dưới hoặc liên hệ với **Agung Jati Kusumo** (tác giả workflow) qua [n8n Community](https://community.n8n.io/). 🚀