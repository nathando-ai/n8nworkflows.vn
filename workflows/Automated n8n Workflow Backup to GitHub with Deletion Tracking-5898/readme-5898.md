---
title: "🚀 Tự Động Hoàn Hảo: Backup & Theo Dõi Xóa Workflow n8n Sang GitHub (Không Cần Code)"
description: "Workflow tự động hóa hoàn hảo để sao lưu tất cả workflow n8n của bạn lên GitHub và theo dõi mọi thay đổi/xóa, đảm bảo dữ liệu an toàn 24/7. Giúp các sếp không lo mất dữ liệu khi cập nhật hoặc xóa workflow."
slug: "tự-dộng-hoàn-hảo-backup-workflow-n8n-sang-github"
tags: [n8n, automation, devops, github, backup, no-code]
keywords: [backup workflow n8n, tự động hóa devops, sao lưu dữ liệu n8n, theo dõi xóa workflow, n8n workflow automation]
---

# 🚀 **Backup & Theo Dõi Xóa Workflow n8n Sang GitHub (100% Tự Động)**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Bạn đã bao giờ lo lắng khi:
- **Cập nhật phiên bản n8n mới** làm mất tất cả workflow cũ?
- **Xóa nhầm workflow** vì không có bản sao lưu?
- **Không theo dõi được** những thay đổi trong workflow?

Workflow này **giải quyết tất cả** bằng cách:
✅ **Sao lưu tự động** tất cả workflow n8n lên GitHub với định dạng `ID.json`.
✅ **Theo dõi xóa** và **khôi phục lại** workflow nếu bị xóa trên n8n.
✅ **Chạy liên tục** mà không cần can thiệp thủ công.
✅ **Giảm thiểu rủi ro** khi cập nhật hoặc xóa workflow.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **An toàn tuyệt đối**: Tất cả workflow được sao lưu định kỳ lên GitHub.
- **Khôi phục nhanh chóng**: Nếu xóa workflow trên n8n, workflow sẽ tự động khôi phục từ GitHub.
- **Tiết kiệm thời gian**: Không cần thủ công backup hoặc theo dõi xóa.
- **Dễ dàng chia sẻ**: Sao lưu trên GitHub giúp dễ dàng chia sẻ workflow với team.
- **Tối ưu tài nguyên**: Sử dụng subworkflow để giảm tải bộ nhớ.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản GitHub** với quyền **write** vào repository.
2. **API Key OAuth2 của GitHub** (cấu hình trong n8n dưới `Credentials` → `githubOAuth2Api`).
3. **Repository GitHub** để lưu backup (ví dụ: `n8n-backups`).
4. **n8n Self-hosted** (không dùng phiên bản cloud).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/5898) hoặc copy/paste JSON vào **n8n Editor**.
- **Nhấn "Import"** để thêm workflow vào n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này chia thành **2 phần chính**:
- **Main Workflow** (chạy chính)
- **Subworkflow** (giúp giảm tải bộ nhớ)

##### **A. Cấu Hình `Globals` Node (Quá Trình Cấu Hình Cốt Lõi)**
Mở node **"Globals"** và cập nhật:
- **`repo.owner`**: Tên tài khoản GitHub của bạn (ví dụ: `john-doe`).
- **`repo.name`**: Tên repository lưu backup (ví dụ: `n8n-backups`).

**Ví dụ:**
```json
{
  "repo.owner": "john-doe",
  "repo.name": "n8n-backups"
}
```

##### **B. Cấu Hình Credentials GitHub**
- Đi đến **Credentials** → **Add New Credentials** → Chọn **GitHub OAuth2 API**.
- Nhập **Token Personal Access Token** của GitHub (có quyền `repo`).
- **Lưu** và chọn credential này trong các node **GitHub** của workflow.

##### **C. Cấu Hình Node `Schedule Trigger` (Chạy Định Kỳ)**
- Mở node **"Schedule Trigger"** và chọn **lịch trình chạy** (ví dụ: **ngày 12 giờ** để backup hàng ngày).
- **Lưu ý**: Nếu muốn chạy thủ công, có thể bỏ qua và sử dụng **Manual Trigger**.

##### **D. Kiểm Tra Node `Get many workflows`**
- Node này lấy danh sách tất cả workflow trên n8n.
- **Không cần chỉnh sửa**, chỉ cần đảm bảo **credentials `n8nApi`** đã cấu hình đúng (n8n API Key).

##### **E. Node `isDiffOrNew` & `isDeleted` (Logic So Sánh & Xóa)**
- Node này sử dụng **code logic** để:
  - **So sánh** giữa workflow trên n8n và GitHub.
  - **Xóa** file trên GitHub nếu workflow bị xóa trên n8n.
- **Không cần chỉnh sửa**, chỉ cần đảm bảo **credentials GitHub** đã đúng.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chọn **Manual Trigger** và nhấn **"Execute"**.
   - Kiểm tra **log** để đảm bảo backup thành công.
2. **Bật Active**:
   - Đánh dấu workflow thành **"Active"** để chạy tự động theo lịch trình.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động Khôi Phục Workflow Xóa**:
   - Nếu workflow bị xóa trên n8n, node `isDeleted` sẽ tự động **tải lại từ GitHub**.

2. **Lưu Log Theo Dõi**:
   - Thêm node **Slack/Telegram** sau node `Create new file` để **báo cáo backup thành công/thất bại**.

3. **Backup Định Kỳ Hàng Tuần**:
   - Cấu hình **Schedule Trigger** chạy vào **ngày đầu tuần** để đảm bảo dữ liệu mới nhất.

4. **Sao Lưu Nhiều Repository**:
   - Sử dụng **node `set`** để lưu nhiều repository khác nhau (ví dụ: `n8n-backups-dev`, `n8n-backups-prod`).

5. **Kiểm Tra Dung Lượng File**:
   - Nếu workflow quá lớn, node `If file too large` sẽ **bỏ qua** để tránh lỗi.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để các sếp:
✔ **Không lo mất dữ liệu** khi cập nhật n8n.
✔ **Tự động khôi phục** nếu xóa workflow.
✔ **Tiết kiệm thời gian** với backup định kỳ.

**Hãy áp dụng ngay và bảo vệ workflow của mình!** 🚀

---
**🔹 Bạn có thắc mắc gì?** Hãy để lại comment dưới đây, các sếp sẽ hỗ trợ! 😊