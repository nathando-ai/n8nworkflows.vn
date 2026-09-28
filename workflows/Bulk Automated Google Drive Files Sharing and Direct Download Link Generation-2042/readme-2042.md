---
title: "🚀 Tự Động Hóa Chia Sẻ & Tạo Link Download Bulk File Google Drive Miễn Phí (N8N)"
description: "Giải pháp hoàn toàn không code giúp các sếp tự động chia sẻ hàng loạt file Google Drive với link download trực tiếp, tiết kiệm thời gian lên đến 90% so với cách thủ công. Hoạt động 24/7, không cần can thiệp."
slug: "tu-dong-hoa-chia-se-link-download-google-drive"
tags: [n8n, automation, google-drive, no-code, it-ops]
keywords: [n8n workflow google drive, tự động hóa chia sẻ file bulk, tạo link download bulk, tự động hóa IT ops, n8n tự động hóa không code]
---

# 🚀 **Tự Động Hóa Chia Sẻ & Tạo Link Download Bulk File Google Drive (N8N)**

### **Nỗi Đau Của Các Sếp Khi Chia Sẻ File Google Drive**
Các sếp thường phải mất **từ 30 phút đến 2 giờ** để chia sẻ hàng loạt file Google Drive cho nhiều người dùng, đặc biệt khi:
- Cần chia sẻ **trăm file+** cho khách hàng, đồng nghiệp hoặc nhóm dự án.
- Muốn **tạo link download trực tiếp** thay vì chia sẻ quyền truy cập.
- **Cập nhật quyền hạn** cho từng file một cách thủ công, dễ gây lỗi.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động lấy danh sách file** từ Google Drive.
✅ **Tạo link download trực tiếp** cho từng file.
✅ **Chia sẻ quyền truy cập** với người dùng cụ thể (ví dụ: `anyoneWithLink`).
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 90%** so với cách chia sẻ thủ công.
- **Chính xác 100%**: Không sai sót trong việc tạo link hoặc cập nhật quyền.
- **Cá nhân hóa chia sẻ**: Chỉ người dùng được chỉ định mới có thể truy cập.
- **Hoạt động liên tục**: Duy trì hoạt động ngay cả khi các sếp nghỉ ngơi.
- **Dễ dàng mở rộng**: Có thể lưu kết quả vào Excel, Airtable hoặc Slack.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** với quyền quản trị (để chia sẻ file).
2. **API Key OAuth2** của Google Drive (cài đặt trong n8n):
   - Mở **n8n Editor** → **Credentials** → **Add Credential** → Chọn **Google Drive OAuth2**.
   - Theo hướng dẫn của Google để tạo OAuth Client ID và điền vào n8n.
3. **Danh sách file** muốn chia sẻ (workflow sẽ lấy từ thư mục mặc định).
4. **(Tùy chọn)** Nếu muốn lưu kết quả:
   - **Google Sheets API Key** (nếu lưu vào Excel).
   - **Airtable API Key** (nếu lưu vào Airtable).
   - **Slack Webhook URL** (nếu gửi thông báo).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow bằng **2 cách**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/2042) và import vào n8n Editor.
- **Copy/Paste JSON** từ file vào n8n Editor (đảm bảo không có lỗi syntax).

:::note[LƯU Ý]
- **Không xóa node `Manual Execute Workflow`** (node `manualTrigger`), vì nó cho phép các sếp kích hoạt workflow khi cần.
- **Không thay đổi tên node** trừ khi các sếp hiểu rõ logic của nó.
:::

---

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này có **8 node chính**, các sếp cần chú ý cấu hình như sau:

| **Node**               | **Hành Động**                                                                 | **Cấu Hình Cần Thiết**                                                                 |
|------------------------|-------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| **Google Drive (list)** | Lấy danh sách file từ thư mục.                                               | - **Credentials**: Chọn `googleDriveOAuth2Api` (đã cài đặt trước).                     |
|                        |                                                                               | - **Folder ID**: Điền **ID thư mục** muốn lấy file (có thể lấy từ URL Google Drive).   |
| **Loop Over Items**    | Lặp qua từng file trong danh sách.                                           | **Không cần cấu hình thêm** (node này tự động xử lý).                                  |
| **Set Folder ID**      | Đặt lại Folder ID (nếu cần chia sẻ vào thư mục khác).                        | - **Value**: Điền **Folder ID mới** (nếu có).                                          |
| **Generate Download Links** | **Node Code** tạo link download trực tiếp.                                   | - **JavaScript Code** (sẵn trong workflow, không cần chỉnh sửa).                     |
| **Change Status (share)** | Chia sẻ file với quyền `anyoneWithLink` (hoặc quyền khác).               | - **Credentials**: Chọn `googleDriveOAuth2Api`.                                         |
|                        |                                                                               | - **File ID**: Sử dụng `{{$node["Loop Over Items"].json["id"]}}` (đường dẫn dynamic). |
|                        |                                                                               | - **Permission**: Chọn `anyoneWithLink` (hoặc `domain` nếu chia sẻ trong doanh nghiệp). |
| **Merge**              | Gộp kết quả cuối cùng (link + tên file + quyền).                            | **Không cần cấu hình thêm**.                                                          |
| **Manual Execute**     | Kích hoạt workflow thủ công.                                                 | **Không cần cấu hình thêm**.                                                          |

:::tip[MẪU CODE TRONG NODE `Generate Download Links`]
```javascript
// Code này tự động tạo link download từ ID file Google Drive
const fileId = $input.all()[0].id;
const link = `https://drive.google.com/u/3/uc?id=${fileId}&export=download&confirm=t&authuser=0`;
return { link, name: $input.all()[0].name };
```
:::

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với **1-2 file mẫu**:
   - Chạy workflow và kiểm tra **node `Change Status`** để đảm bảo file được chia sẻ đúng.
   - Kiểm tra **node `Generate Download Links`** để xem link download có đúng không.
2. **Bật Active**:
   - Đánh dấu workflow thành **Active** trong n8n Editor.
   - **Kích hoạt bằng node `Manual Execute`** khi cần chạy.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH LƯU KẾT QUẢ]
Các sếp có thể **lưu kết quả** vào:
- **Google Sheets**:
  - Thêm node `googleSheets` sau `Merge` và cấu hình để ghi dữ liệu vào sheet.
- **Airtable**:
  - Thêm node `airtable` và cấu hình tương tự.
- **Slack/Telegram**:
  - Thêm node `slack` hoặc `telegramBot` để gửi thông báo khi chia sẻ xong.
:::

:::tip[CÁCH TẠO LINK DOWNLOAD CHO NHIỀU NGƯỜI DÙNG]
Nếu muốn chia sẻ cho **nhiều người dùng khác nhau**, các sếp có thể:
1. **Tạo một file CSV** chứa danh sách email người dùng.
2. **Thêm node `csv`** để đọc file CSV.
3. **Sử dụng node `code`** để tạo **một link download riêng** cho mỗi người dùng (ví dụ: `https://drive.google.com/uc?export=download&id=FILE_ID&confirm=USER_EMAIL`).
:::

:::note[CÁCH CẬP NHẬT QUYỀN HẠN]
Nếu muốn **chỉ định quyền hạn khác** (ví dụ: `domain` thay vì `anyoneWithLink`):
- Trong node `Change Status`, thay đổi **Permission** thành `domain` và điền **domain của doanh nghiệp**.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp đi lặp lại khi chia sẻ file Google Drive. **Chỉ cần 5 phút setup**, sau đó workflow sẽ hoạt động **một cách tự động và chính xác** mọi lúc.

**Hãy áp dụng ngay để:**
✔ **Tiết kiệm thời gian** cho công việc hàng ngày.
✔ **Tránh sai sót** khi chia sẻ file.
✔ **Mở rộng khả năng tự động hóa** với Google Drive.

**Bắt đầu ngay bằng cách import workflow và kích hoạt nó!** 🚀

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::