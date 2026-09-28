---
title: "🚀 **Tự Động Hoàn Hảo: Backup Tất Cả Workflow n8n Sang Google Drive Với Lịch Sử Phiên Bản**"
description: "Giải pháp tự động hóa 100% không code để sao lưu toàn bộ workflow từ nhiều instance n8n sang Google Drive, hỗ trợ lịch sử phiên bản và đồng bộ tự động hàng ngày. Giảm thiểu rủi ro mất dữ liệu và tiết kiệm thời gian quản lý thủ công."
slug: "backup-workflows-n8n-sang-google-drive"
tags: [n8n, automation, devops, backup, google-drive, self-hosted]
keywords: [backup workflow n8n, tự động hóa sao lưu, google drive n8n, version control workflow, devops n8n]
---

# 🚀 **Backup Tất Cả Workflow n8n Sang Google Drive Với Lịch Sử Phiên Bản**

## **🔥 Nỗi Đau Của Các Sếp Khi Quản Lý Workflow n8n Thủ Công**
Hiện nay, khi các sếp tự động hóa quy trình với **n8n**, việc quản lý và sao lưu workflow trở thành một **đầu mối đau đầu**:
- **Mất dữ liệu không mong muốn**: Một lần nhấn sai nút hoặc lỗi server có thể xóa bỏ tất cả công việc tự động hóa đã xây dựng.
- **Không đồng bộ giữa các instance**: Nếu có nhiều máy chủ n8n (dev/staging/prod), sao lưu thủ công trở nên **khó khăn và dễ sai sót**.
- **Không có lịch sử phiên bản**: Khi cần khôi phục lại một phiên bản cũ của workflow, các sếp phải **tìm kiếm trong các file JSON rải rác** hoặc nhớ lại ngày giờ backup.
- **Tốn thời gian**: Sao lưu thủ công hàng ngày hoặc hàng tuần **gián đoạn công việc** và dễ bị quên lãng.

**Giải pháp?** **Workflow này tự động hóa toàn bộ quy trình sao lưu**, đồng bộ workflow từ **nhiều instance n8n** sang **Google Drive** với **lịch sử phiên bản** và **không cần code nào!**

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **An toàn tuyệt đối**: Sao lưu tự động hàng ngày, không phụ thuộc vào hành động của con người.
✅ **Lịch sử phiên bản**: Sử dụng tính năng **version history** của Google Drive để khôi phục bất kỳ phiên bản workflow cũ nào.
✅ **Dồng bộ nhiều instance**: Quản lý workflow từ **n8n Host 1, Host 2, hoặc thậm chí nhiều hơn** trong một nơi duy nhất.
✅ **Tiết kiệm thời gian**: Không cần phải **copy-paste JSON** hoặc **tải xuống thủ công** hàng ngày.
✅ **Tự động xử lý cập nhật**: Nếu workflow được chỉnh sửa, hệ thống sẽ **cập nhật tự động** trên Google Drive mà không làm mất phiên bản cũ.
✅ **Không phụ thuộc vào máy chủ**: Dữ liệu lưu trữ trên **Google Drive**, an toàn ngay cả khi máy chủ n8n gặp sự cố.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Các instance n8n** (cần có **API Key** để truy cập):
   - Đăng nhập vào **n8n Web UI** → **Settings** → **Credentials** → Tạo **n8n API Key** cho mỗi instance.
   - Lưu ý: **Không chia sẻ API Key** với bất kỳ ai.
2. **Tài khoản Google Drive** với quyền **quản trị viên folder**:
   - Tạo **một folder riêng** cho mỗi instance n8n (ví dụ: `n8n-host-1-backup`, `n8n-host-2-backup`).
   - **Lấy ID Folder** từ URL khi mở folder trong Google Drive (ví dụ: `https://drive.google.com/drive/folders/[FOLDER_ID]`).
3. **Tài khoản n8n có quyền quản lý**:
   - Các sếp cần quyền **Admin** để chạy workflow và truy cập API của n8n.

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ file JSON**
1. Tải workflow từ [n8n.io/workflows/12747](https://n8n.io/workflows/12747) (chọn **Download JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Tạo workflow mới.
2. Nhấn **Import** → Chọn **Paste JSON** → Dán nội dung JSON từ [n8n.io/workflows/12747](https://n8n.io/workflows/12747) (chọn **Copy JSON**).
3. Nhấn **Import**.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 Cấu hình Credentials cho n8n API**
Workflow cần **2 credentials n8n API** (một cho mỗi instance):
1. Trong **n8n Editor**, nhấn **Credentials** (góc trên bên phải) → **Add new credential**.
2. Chọn **n8n API** → Điền:
   - **Name**: `n8nApi` (hoặc `n8nApiHost2` nếu có nhiều instance).
   - **URL**: `https://[TÊN_DOMAIN_N8N].com` (ví dụ: `https://n8n.example.com`).
   - **API Key**: Copy từ **Settings → Credentials** trên n8n Web UI.
3. Lặp lại cho **instance thứ 2** (nếu có).

#### **🔹 Cấu hình Google Drive OAuth2**
1. Trong **n8n Editor**, nhấn **Credentials** → **Add new credential**.
2. Chọn **Google Drive OAuth2** → Đăng nhập tài khoản Google.
3. Chọn **quyền truy cập** cần thiết (chọn **Drive** và **Drive Appdata**).
4. Lưu **credentials** với tên `googleDriveOAuth2Api`.

#### **🔹 Cấu hình Folder ID trong Google Drive**
Workflow cần **ID Folder** để lưu backup:
1. Mở folder trên Google Drive (ví dụ: `n8n-host-1-backup`).
2. Copy **ID Folder** từ URL (ví dụ: `https://drive.google.com/drive/folders/[FOLDER_ID]`).
3. Trong node **"Config Host 1"** và **"Config Host 2"** (cả hai là **Set nodes**), điền:
   - **Folder ID**: Paste ID vừa copy.
   - **Workflow Name Prefix**: Đặt tên prefix (ví dụ: `n8n-host-1_`).

#### **🔹 Cấu hình Schedule Trigger**
Workflow có **Schedule Trigger** để chạy tự động hàng ngày:
1. Trong node **"Run daily"**, chỉnh sửa **Schedule**:
   - Chọn **Daily** → Đặt thời gian (ví dụ: **8:00 AM**).
   - Chọn **Timezone** phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).

#### **🔹 Cấu hình Node "Execute Workflow"**
Workflow này **gọi lại chính nó** để xử lý backup:
1. Trong node **"Call 'n8n auto-backup to google drive'"**, điền:
   - **Workflow ID**: ID của workflow này (có thể copy từ URL khi mở workflow trong n8n Editor).

#### **🔹 Cấu hình Node "Filter archived workflows"**
Workflow sẽ **bỏ qua workflow đã được đánh dấu là "archived"**:
1. Trong node **"Filter archived workflows"**, chỉnh sửa **Filter**:
   - Đặt **Condition**: `$.archived === false` (để chỉ backup workflow **không bị xóa**).

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** → Chọn **Test Execution**.
   - Kiểm tra **log** để đảm bảo workflow chạy đúng.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động theo lịch.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Tạo Folder Đặc Biệt Cho Mỗi Instance**
- **Không nên lưu tất cả workflow vào một folder**: Tạo **folder riêng** cho mỗi instance (ví dụ: `n8n-dev`, `n8n-prod`) để **tránh nhầm lẫn** và **quản lý dễ dàng**.

### **2. Sử Dụng Google Drive Version History**
- Google Drive tự động lưu **lịch sử phiên bản** cho tất cả file JSON.
- **Cách khôi phục**:
  1. Mở file JSON trong Google Drive.
  2. Nhấn **More (⋮)** → **See version history**.
  3. Chọn phiên bản cũ → **Restore**.

### **3. Gửi Báo Cáo Backup Định Kỳ**
- **Kết hợp với Slack/Telegram**:
  - Thêm node **Slack** hoặc **Telegram Bot** sau workflow để **gửi thông báo** khi backup thành công/thất bại.
  - Ví dụ:
    ```json
    {
      "operation": "sendMessage",
      "text": "Backup workflow n8n hoàn tất! {{ $json("success") ? "Thành công" : "Thất bại" }}"
    }
    ```

### **4. Sao Lưu Lại Các Credentials**
- **Không lưu API Key trong workflow**: Nếu workflow bị rò rỉ, **tài khoản n8n có thể bị hack**.
- **Lưu credentials ở nơi an toàn**:
  - Sử dụng **n8n Credentials Manager** (đã được cấu hình ở trên).
  - **Không commit vào GitHub** nếu workflow được quản lý trên mã nguồn mở.

### **5. Xử Lý Lỗi Hàng Loạt**
- **Node "Error Handling"**: Thêm node **Set Error** hoặc **Notify** để **log lỗi** và **gửi cảnh báo** khi backup thất bại.
- **Retry Logic**: Sử dụng node **Schedule Trigger** với **delay** (ví dụ: chạy lại sau 1 giờ nếu thất bại).

---

## **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** để các sếp:
✔ **Tự động hóa sao lưu workflow n8n** sang Google Drive **không cần code**.
✔ **Quản lý nhiều instance** trong một nơi duy nhất.
✔ **Khôi phục phiên bản cũ** một cách dễ dàng.
✔ **Tiết kiệm thời gian** và **giảm rủi ro mất dữ liệu**.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình credentials** và **Folder ID**.
3. **Bật Schedule Trigger** để backup tự động hàng ngày.
4. **Quên lo lắng về mất dữ liệu**!

---
**💡 Cần hỗ trợ thêm?** Đừng ngần ngại liên hệ với **CryoZeroLabs** hoặc cộng đồng n8n trên [Discord](https://discord.gg/n8n) để được trợ giúp! 🚀