---
title: "🗂️ Tự Động Hoàn Chỉnh & Sao Lược Workflow n8n Sang Google Drive (JSON Tích Hợp)"
description: "Workflow này tự động phân loại và sao lưu tất cả workflow n8n của bạn thành 4 file JSON riêng biệt (Active, Template, Done, Archived) và upload lên Google Drive một cách tự động. Giúp quản lý hàng trăm workflow trở nên đơn giản, an toàn và dễ truy cập 24/7."
slug: "tieu-dong-hoan-chinh-sao-luoc-workflow-n8n-sang-google-drive"
tags: [n8n, automation, file-management, google-drive, backup, no-code]
keywords: [tự động hóa n8n, sao lưu workflow n8n, quản lý workflow n8n, google drive n8n, backup tự động, tổ chức workflow]
---

# 🚀 **Tự Động Hoàn Chỉnh & Sao Lược Workflow n8n Sang Google Drive (JSON Tích Hợp)**

### **Giải quyết vấn đề gì?**
Các sếp đang gặp khó khăn khi quản lý **hàng trăm workflow n8n** thủ công? Lo ngại mất dữ liệu khi n8n bị reset hoặc chuyển đổi môi trường? Hoặc chỉ đơn giản là muốn **tìm kiếm và truy cập workflow nhanh chóng** mà không phải scroll qua hàng trăm trang?

Workflow này **tự động hóa toàn bộ quy trình** bằng cách:
✅ **Lấy tất cả workflow** từ n8n (Cloud hoặc Self-hosted) qua API.
✅ **Phân loại tự động** theo trạng thái (Active, Template, Done, Archived) và **tags** (nếu có).
✅ **Chuyển đổi thành JSON** và **upload lên Google Drive** theo thư mục riêng biệt.
✅ **Sao lưu định kỳ** (thông qua Schedule Trigger) hoặc **kích hoạt thủ công** khi cần.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần sao lưu thủ công hàng tháng.
- **Dữ liệu an toàn**: Sao lưu định kỳ, không phụ thuộc vào bộ nhớ n8n.
- **Tìm kiếm dễ dàng**: Tất cả workflow được **sắp xếp theo danh mục** trong Google Drive.
- **Hoạt động liên tục**: Hoạt động 24/7 khi được kết nối với VPS.
- **Hoàn chỉnh & mở rộng**: Dễ dàng kết hợp với **Slack/Telegram** để báo cáo hoặc **lưu log** cho quản lý.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (để lưu trữ file JSON).
2. **Tài khoản n8n** (Cloud hoặc Self-hosted) và **API Key** của n8n.
3. **Thư mục Google Drive đã tạo sẵn** (để lưu kết quả).
4. **Tags trong n8n**:
   - **Template**: Dùng cho workflow mẫu.
   - **Done**: Dùng cho workflow đã hoàn thành.
   - **Không tag**: Workflow đang tiến hành sẽ được phân loại vào danh mục **"Work-in-Progress"**.
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON bằng cách:
- **Tải file JSON** từ [n8n.io/workflows/15038](https://n8n.io/workflows/15038).
- **Copy toàn bộ JSON** và dán vào **n8n Editor** (trong tab "Import").
- **Hoặc** tải file JSON từ link này: **[Tải Workflow](https://raw.githubusercontent.com/n8n-io/n8n-workflows/master/workflows/organize-and-backup-n8n-workflows-to-google-drive/15038.json)**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **phức tạp** vì phải kết nối với **Google Drive** và **API n8n**, nên các sếp **phải cấu hình chính xác** các node sau:

#### **A. Cấu hình Node "Configuration" (Thiết lập cơ bản)**
- **Google Drive Folder ID**:
  - Mở Google Drive → Chọn thư mục muốn lưu → **Chia sẻ** → **Lấy liên kết** → **Copy ID** từ URL (vd: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
  - Điền vào **Google Drive Folder ID** trong node **"Configuration"**.

- **Base URL của n8n**:
  - **N8n Cloud**: `https://<subdomain>.app.n8n.cloud` (không thêm `/` sau `.cloud`).
  - **Self-hosted**: `http://<domain>:5678` (vd: `http://localhost:5678`).
  - **Không điền** phần sau `:5678` hoặc `.cloud`.

#### **B. Cấu hình API Key n8n**
Workflow hỗ trợ **2 phương pháp** để kết nối API Key:
##### **Phương pháp 1: Đặt trực tiếp trong Node (Quick Start)**
- Trong node **"Workflows"** (type: `httpRequest`):
  - **Authentication**: `None`.
  - **Send Headers**: `on`.
  - Thêm **Header mới**:
    - **Name**: `X-N8N-API-KEY`.
    - **Value**: **API Key** của n8n (tìm ở **Settings → API → Create API Key**).

##### **Phương pháp 2: Sử dụng Credential (Recommended)**
- **Bước 1**: Tạo **Generic Credential** trong n8n:
  - Mở **Credentials** → **Add Credential** → Chọn **Generic**.
  - **Name**: `X-N8N-API-KEY`.
  - **Value**: **API Key** của n8n.
- **Bước 2**: Trong node **"Workflows"**:
  - **Authentication**: `Generic Credential Type`.
  - **Generic Auth Type**: `Header Auth`.
  - **Header Auth**: Chọn credential vừa tạo.

> ⚠️ **Lưu ý**:
> - **Không bao giờ chia sẻ API Key** với ai!
> - Nếu dùng **n8n Cloud trial**, **không thể tạo API Key** (do giới hạn của phiên bản thử nghiệm).

#### **C. Cấu hình Node "Folder" (Google Drive)**
- **Credentials**: Chọn `googleDriveOAuth2Api` (đã cấu hình trước khi import).
- **Resource**: `folder`.
- **Folder ID**: Điền **ID của thư mục** đã tạo sẵn (đã cấu hình ở trên).

#### **D. Kích hoạt Schedule Trigger (Nếu muốn tự động)**
- Mở node **"Schedule"** (type: `scheduleTrigger`).
- **Chọn thời gian chạy** (vd: `0 0 * * *` = chạy hàng ngày lúc 00:00).
- **Active** workflow.

---
### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Chọn node **"onCommand"** (type: `manualTrigger`) → **Run Workflow**.
  - Kiểm tra **Google Drive** để xem file JSON đã được tạo không.
- **Active Workflow**:
  - Chuyển **Active** node **"Schedule"** (nếu muốn tự động) hoặc **"onCommand"** (nếu muốn thủ công).

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram** sau khi upload thành công để báo cáo.
   - Ví dụ: `"Workflow đã sao lưu thành công! Link: [Google Drive Link]"`.
2. **Lưu log hoạt động**:
   - Sử dụng node **Google Sheets** hoặc **Notion** để ghi lại lịch sử sao lưu.
3. **Tự động xóa file cũ**:
   - Sử dụng **Google Apps Script** để xóa file JSON cũ hơn 30 ngày.
4. **Sao lưu định kỳ lên GitHub**:
   - Nếu cần, các sếp có thể **tạo phiên bản GitHub** của workflow này (liên hệ tác giả để nhận).
5. **Phân loại thêm theo tags**:
   - Nếu muốn phân loại theo **tags khác**, các sếp có thể **mở rộng logic** bằng node **Set** và **If**.
:::

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để các sếp:
✔ **Tự động hóa sao lưu** workflow n8n một cách an toàn.
✔ **Quản lý hàng trăm workflow** một cách logic và dễ dàng.
✔ **Truy cập dữ liệu** từ bất kỳ thiết bị nào qua Google Drive.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Kích hoạt Schedule Trigger** để sao lưu tự động hàng ngày.
3. **Kết hợp với Slack** để được thông báo khi sao lưu thành công.

---
### **🎁 Đăng ký VPS để chạy 24/7**
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**.
:::

---
**Chúc các sếp thành công!** 🚀
Nếu có vấn đề, hãy **comment bên dưới** hoặc liên hệ tác giả [Ziana Mitchell](https://n8n.io/workflows/15038) để hỗ trợ.