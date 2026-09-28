---
title: "💾 **Tự Động Hoàn Hảo: Backup Tất Cả Workflow n8n Sang GitHub (Với Subfolders) - Không Cần Code!**"
description: "Giải pháp hoàn hảo để tự động sao lưu tất cả workflow n8n của bạn lên GitHub, đảm bảo an toàn và dễ quản lý. Hỗ trợ chia sẻ, khôi phục và theo dõi lịch sử thay đổi một cách đơn giản."
slug: "tự-dộng-hoàn-hảo-backup-workflow-n8n-sang-github"
tags: [n8n, automation, backup, github, no-code, self-hosted]
keywords: [backup workflow n8n, tự động hóa lưu trữ GitHub, sao lưu workflow n8n, subfolders GitHub, n8n workflow automation]
---

# 💾 **Backup Tất Cả Workflow n8n Sang GitHub (Với Subfolders) - Không Cần Code!**

### **🚨 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Các sếp đã từng gặp phải tình huống này chưa?
- **Sao lưu workflow n8n thủ công** mất nhiều thời gian và dễ bị quên.
- **Không có lịch sử thay đổi**, khó khăn khi khôi phục phiên bản cũ.
- **Không chia sẻ dễ dàng** với team, dẫn đến trùng lặp hoặc mất mát dữ liệu.
- **Rủi ro mất mát dữ liệu** khi server bị lỗi hoặc bị xóa vô tình.

**Giải pháp?** **Workflow này tự động sao lưu tất cả workflow n8n của bạn lên GitHub**, với cấu trúc subfolders rõ ràng, giúp các sếp:
✅ **Tiết kiệm thời gian** (không cần làm thủ công).
✅ **An toàn tuyệt đối** (dữ liệu được lưu trữ trên GitHub).
✅ **Dễ quản lý** (chia sẻ, khôi phục phiên bản cũ một cách đơn giản).
✅ **Hoạt động liên tục** (không phụ thuộc vào người dùng).

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động sao lưu** tất cả workflow n8n lên GitHub **mỗi khi có thay đổi**.
- **Cấu trúc subfolders** rõ ràng, giúp quản lý dễ dàng (ví dụ: `workflows/ID.json`).
- **Khôi phục phiên bản cũ** một cách nhanh chóng bằng GitHub.
- **Chia sẻ workflow** với team một cách an toàn và hiệu quả.
- **Không phụ thuộc vào người dùng**, hoạt động **24/7** mà không cần can thiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản GitHub** và **API Token** (có quyền `repo`).
✔ **Tài khoản n8n** (để lấy API Key của n8n).
✔ **Repository GitHub** để lưu trữ backup (ví dụ: `n8n-backups`).
✔ **Thiết lập subfolder** trong repo (ví dụ: `workflows/`).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Mở **n8n Editor** trên trang web hoặc VPS.
2. Nhấn **"Import"** và chọn file JSON (hoặc paste JSON).
3. Chọn **"Import"** để hoàn tất.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này sử dụng **subworkflow** để giảm tải bộ nhớ và tối ưu hiệu suất. Các bước quan trọng cần chỉnh:

##### **A. Cấu Hình Node "Globals" (Node `set`)**
Mở node **"Globals"** và cập nhật các tham số sau:
- **`repo.owner`**: Tên tài khoản GitHub của bạn (ví dụ: `john-doe`).
- **`repo.name`**: Tên repository GitHub (ví dụ: `n8n-backups`).
- **`repo.path`**: Đường dẫn subfolder trong repo (ví dụ: `workflows/`).

**Ví dụ:**
```json
{
  "repo.owner": "john-doe",
  "repo.name": "n8n-backups",
  "repo.path": "workflows/"
}
```

##### **B. Cấu Hình Credentials GitHub**
1. Mở **Credentials Manager** trong n8n.
2. Tạo **mới một credential** với loại `githubApi`.
3. Điền:
   - **Token**: API Token của GitHub (có quyền `repo`).
   - **Owner**: Tên tài khoản GitHub (đã nhập ở trên).
   - **Repository**: Tên repository (đã nhập ở trên).

##### **C. Kích Hoạt Schedule Trigger (Nếu Muốn Tự Động Hàng Ngày)**
Node **"Schedule Trigger"** cho phép chạy backup **tự động** theo lịch (ví dụ: hàng ngày lúc 2 giờ sáng).
- Mở node và chỉnh:
  - **Schedule**: `0 2 * * *` (lúc 2 giờ sáng hàng ngày).
  - **Active**: Bật để kích hoạt.

##### **D. Test Run Trước Khi Bật Active**
1. Nhấn **"Execute"** để chạy test với dữ liệu mẫu.
2. Kiểm tra **GitHub** xem file backup đã được tạo không.
3. Nếu thành công, chuyển sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Lưu Log Backup**:
   - Thêm node **Slack/Telegram** để thông báo khi backup thành công/thất bại.
   - Ví dụ: Sau node **"Create new file"** hoặc **"Edit existing file"**, thêm node **webhook** để gửi tin nhắn.

2. **Backup Định Kỳ + Email Báo Cáo**:
   - Kết hợp với **node `email`** để gửi báo cáo backup hàng tuần cho team.

3. **Sử Dụng Tags Cho Workflow**:
   - Node **"tag?"** (switch) có thể được sử dụng để phân loại workflow theo tags (ví dụ: `production`, `testing`).

4. **Khôi Phục Workflow Từ GitHub**:
   - Nếu cần khôi phục, các sếp chỉ cần **download file JSON** từ GitHub và import vào n8n.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để các sếp **tự động hóa sao lưu workflow n8n** lên GitHub, đảm bảo **an toàn, dễ quản lý và tiết kiệm thời gian**. Không cần code, không phụ thuộc vào người dùng, và hỗ trợ **chia sẻ, khôi phục phiên bản cũ** một cách đơn giản.

**Hãy áp dụng ngay và bảo vệ dữ liệu của mình!** 🚀

---
**🔗 [Tải workflow nguyên bản từ n8n.io](https://n8n.io/workflows/2868)**