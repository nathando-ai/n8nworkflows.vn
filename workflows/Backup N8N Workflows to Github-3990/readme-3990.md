---
title: "💾 **Tự Động Hoàn Hảo: Backup Tất Cả Workflows n8n Sang GitHub 24/7 - Không Cần Code!**"
description: "Giải pháp tự động hóa hoàn toàn để sao lưu tất cả workflows n8n của bạn lên GitHub hàng ngày, đảm bảo an toàn và dễ quản lý. Kết hợp Discord thông báo thực thời, so sánh file tự động, và lưu trữ theo định dạng ngày tháng chi tiết."
slug: "backup-n8n-workflows-to-github"
tags: [n8n, automation, backup, github, discord, no-code, workflow-management]
keywords: [backup workflow n8n, tự động hóa lưu trữ n8n, sao lưu workflow git, n8n github integration, tự động hóa doanh nghiệp]
---

# 🚀 **Backup Tất Cả Workflows n8n Sang GitHub - Không Cần Code!**

## **🔥 Nỗi Đau Của Các Sếp**
Bạn đã bao giờ lo lắng về việc **mất dữ liệu workflows n8n** do lỗi hệ thống, xóa nhầm, hoặc cập nhật phiên bản không đúng cách? Hoặc phải **tốn thời gian thủ công** sao lưu mỗi workflow một? Với **Workflow này**, các sếp sẽ:
✅ **Tự động sao lưu tất cả workflows** lên GitHub **mỗi ngày** (hoặc theo lịch bạn thiết lập).
✅ **So sánh và cập nhật tự động** nếu có thay đổi mới.
✅ **Nhận thông báo Discord thực thời** khi backup thành công/thất bại.
✅ **Lưu trữ theo định dạng ngày tháng** (`yyyy/MM/dd`) để dễ quản lý.

Không cần viết một dòng code nào, chỉ cần **cài đặt và chạy**!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **An toàn tuyệt đối**: Sao lưu tự động hàng ngày, không lo mất dữ liệu.
- **Tiết kiệm thời gian**: Không cần thủ công sao lưu mỗi workflow.
- **So sánh tự động**: N8n sẽ **xóa hoặc cập nhật** file nếu có thay đổi.
- **Quản lý dễ dàng**: Lưu trữ theo **định dạng ngày tháng** (`yyyy/MM/dd`).
- **Thông báo Discord**: Biết ngay khi backup thành công/thất bại.
- **Hoạt động liên tục**: Chạy 24/7 mà không cần can thiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
✔ **Tài khoản GitHub** (để lưu trữ backup).
✔ **Tài khoản Discord** (để nhận thông báo).
✔ **API Keys**:
   - `githubApi` (tạo từ [Settings > Developer Settings > Personal Access Tokens](https://github.com/settings/tokens)).
   - `discordBotApi` (tạo từ [Discord Developer Portal](https://discord.com/developers/applications)).
✔ **Workflow n8n** (đã cài đặt và chạy trên VPS).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/3990](https://n8n.io/workflows/3990).
- **Mở n8n Editor** → **Import Workflow** → Chọn file JSON.
- **Hoặc copy/paste JSON** từ file vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này được chia thành **2 phần chính**:
- **Main Workflow Loop** (lặp lại sao lưu).
- **Subworkflow** (xử lý từng workflow riêng).

##### **A. Cấu Hình GitHub (Node "Config")**
- Mở node **"Config"** → Điền:
  - **`repo_owner`**: Tên tài khoản GitHub của bạn.
  - **`repo_name`**: Tên repository muốn lưu backup (ví dụ: `n8n-workflows-backup`).

##### **B. Cấu Hình Đường Dẫn Backup (Node "Create sub path")**
- Mở node **"Create sub path"** → Thay đổi định dạng đường dẫn backup (mặc định: `yyyy/MM/dd`).
  - Ví dụ: `backups/${$json["$.date"]}` (lưu vào thư mục `backups/` theo ngày).

##### **C. Cấu Hình Thông Báo Discord**
Mở **3 node Discord** để tùy chỉnh thông điệp:
1. **"Starting Message"** → Thông báo khi backup bắt đầu.
   - Ví dụ: `🚀 **Backup n8n workflows bắt đầu!** (Ngày: ${$json["$.date"]})`
2. **"Inform Success Flows"** → Thông báo khi backup thành công.
   - Ví dụ: `✅ **Backup workflow "${$json["$.name"]}" thành công!**`
3. **"Inform Failed Flows"** → Thông báo khi backup thất bại.
   - Ví dụ: `❌ **Backup workflow "${$json["$.name"]}" thất bại!**`
4. **"Completed Notification"** → Thông báo tổng kết sau khi backup xong.
   - Ví dụ: `🎉 **Backup hoàn tất! Tổng số workflow: ${$json["$.total"]} (${$json["$.success"]} thành công, ${$json["$.failed"]} thất bại)``

##### **D. Node "verifyTheDifference" (So Sánh File)**
- Node này **so sánh file cũ vs mới** bằng JavaScript (sử dụng **Underscore.js**).
- **Không cần chỉnh sửa** (n8n tự động xử lý).

##### **E. Node "Schedule Trigger" (Lịch Sao Lưu)**
- Mở node **"Schedule Trigger"** → Chọn **lịch chạy** (ví dụ: `0 0 * * *` = chạy hàng ngày lúc 00:00).
- **Hoặc kích hoạt thủ công** bằng node **"Manual Trigger"**.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Chọn **node "Execute Workflow Trigger"** → Nhấn **Run**.
  - Kiểm tra **Discord** xem có thông báo không.
- **Bật Active**:
  - Đánh dấu **Active** trên workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Lưu Log Chi Tiết**:
   - Thêm node **Google Sheets** hoặc **Notion** để lưu lịch sử backup.
   - Ví dụ: Lưu tên workflow, ngày giờ, trạng thái (thành công/thất bại).

2. **Kết Hợp Slack**:
   - Thay vì Discord, sử dụng **Slack Webhook** để thông báo.
   - Cài đặt node **Slack** và cấu hình tương tự.

3. **Backup Định Kỳ Theo Ngày**:
   - Sử dụng **node "Schedule Trigger"** để chạy hàng tuần/tháng.
   - Ví dụ: `0 0 1 * *` (chạy hàng tháng ngày 1).

4. **Xóa File Cũ Sau 30 Ngày**:
   - Thêm **node "GitHub"** với operation `delete` để tự động xóa backup cũ.
   - Ví dụ: Xóa file ngoài `backups/2024/01/` sau 30 ngày.

5. **Backup Nhiều Repository**:
   - Sử dụng **node "Switch"** để chia workflow sao lưu cho nhiều repo GitHub khác nhau.

---

### 📌 **Kết Luận**
**Workflow này là giải pháp hoàn hảo** để các sếp:
✔ **Không lo mất dữ liệu** nhờ sao lưu tự động.
✔ **Tiết kiệm thời gian** với việc không cần thủ công sao lưu.
✔ **Quản lý dễ dàng** với định dạng ngày tháng và thông báo Discord.

**Hãy áp dụng ngay!**
1. **Import workflow** vào n8n.
2. **Cấu hình GitHub & Discord**.
3. **Bật Schedule Trigger** để chạy tự động hàng ngày.
4. **Nhận thông báo** và yên tâm dữ liệu an toàn!

---
**💡 Mẹo cuối**: Nếu gặp lỗi, kiểm tra **node "verifyTheDifference"** (so sánh file) và **credentials GitHub/Discord**. Nếu cần hỗ trợ, comment bên dưới hoặc liên hệ tác giả [Dat Proto](https://n8n.io/workflows/3990). 🚀