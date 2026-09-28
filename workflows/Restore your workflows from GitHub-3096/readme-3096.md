---
title: "🔄 **Tự Động Khôi Phục Workflow n8n Từ GitHub – Không Cần Code!**"
description: "Khôi phục tất cả workflow n8n của bạn từ backup trên GitHub chỉ với một cú nhấp chuột. Giảm thiểu thời gian setup từ 2 tiếng xuống 5 phút, đảm bảo tính nhất quán và an toàn dữ liệu cho hệ thống tự động hóa."
slug: "tự-dộng-khôi-phục-workflow-n8n-tu-github"
tags: [n8n, automation, no-code, github, backup-restore, self-hosted]
keywords: [tự động hóa n8n, khôi phục workflow n8n, backup workflow, tự động hóa không code, n8n github integration]
---

# 🔄 **Khôi phục Workflow n8n Từ GitHub – Giải Pháp Tự Động Hóa 100%**

### **Nỗi Đau Của Các Sếp Khi Khôi Phục Workflow n8n**
Bạn đã từng phải mất **2 tiếng** để khôi phục workflow n8n từ backup thủ công? Hay gặp tình trạng **lỗi cấu hình** khi copy-paste JSON từ GitHub? Với **workflow này**, các sếp chỉ cần **nhấp nút "Test"** và tất cả workflow sẽ tự động được khôi phục lên hệ thống n8n của mình – **không cần viết một dòng code nào!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động ổn định 24/7, các sếp nên **self-host n8n** trên VPS riêng để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Khôi phục tất cả workflow trong **5 phút** thay vì 2 tiếng thủ công.
✅ **Đảm bảo chính xác**: Không lo lỗi copy-paste JSON hoặc cấu hình sai.
✅ **Hoạt động liên tục**: Khôi phục tự động khi cần, không phụ thuộc vào thời gian làm việc.
✅ **An toàn dữ liệu**: Backup workflow trên GitHub được bảo mật, dễ dàng phục hồi khi hệ thống bị lỗi.
✅ **Tích hợp hoàn hảo**: Hoạt động với **n8n self-hosted** và **GitHub** một cách mượt mà.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản GitHub** với quyền **read/write** vào repository chứa backup workflow.
2. **API Token GitHub** (Personal Access Token) có quyền `repo` (cài đặt tại: **Settings → Developer Settings → Personal Access Tokens**).
3. **n8n self-hosted** (không hỗ trợ phiên bản cloud).
4. **Repository GitHub** chứa file backup workflow (dạng `.json`) trong một **folder cụ thể** (ví dụ: `workflows/`).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [link gốc](https://n8n.io/workflows/3096) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/3096) và paste vào **Create Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này sử dụng **node `Globals`** để cấu hình thông tin repository. Các sếp **phải chỉnh** các tham số sau:

##### **a. Cấu Hình Node `Globals`**
Mở node **`Globals`** và cập nhật 3 trường sau:
- **`repo.owner`**: Tên tài khoản GitHub của bạn (ví dụ: `john-doe`).
- **`repo.name`**: Tên repository chứa backup (ví dụ: `n8n-backups`).
- **`repo.path`**: Đường dẫn đến folder chứa file workflow (ví dụ: `workflows/`).

**Ví dụ**:
```
repo.owner = "john-doe"
repo.name = "n8n-backups"
repo.path = "workflows/"
```

##### **b. Cấu Hình Credentials**
Workflow cần **2 loại credentials**:
1. **`githubApi`**:
   - Mở **Credentials** → **Add** → **GitHub**.
   - Nhập **Personal Access Token** (tạo tại GitHub).
   - Chọn **Permissions**: `repo` (để có quyền đọc và tải file).
2. **`n8nApi`**:
   - Mở **Credentials** → **Add** → **n8n API**.
   - Chọn **URL** của n8n self-hosted (ví dụ: `http://localhost:5678`).
   - Nhập **API Key** (tạo tại **Settings → API** trong n8n).

##### **c. Kiểm Tra Node `Get all files in given path`**
- Node này sẽ **lấy danh sách tất cả file JSON** trong folder đã chỉ định trên GitHub.
- **Lưu ý**: Nếu folder không tồn tại hoặc không có file `.json`, workflow sẽ **không hoạt động**.

##### **d. Node `Convert files to JSON`**
- Node này **chuyển file backup** (dạng `.json`) thành định dạng JSON để n8n có thể khôi phục.
- **Không cần chỉnh sửa** nếu file backup đã đúng định dạng.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấp vào nút **"Test"** để chạy workflow với dữ liệu mẫu.
   - Kiểm tra **log** để đảm bảo tất cả workflow được khôi phục thành công.
2. **Bật Workflow**:
   - Sau khi test thành công, **bật `Active`** để workflow hoạt động tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự Động Khôi Phục Định Kỳ**:
   - Kết hợp với **node `schedule`** để khôi phục workflow hàng ngày/ngày nhất định.
   - Ví dụ: Khôi phục vào **giờ 2h sáng** để tránh ảnh hưởng đến hoạt động bình thường.

2. **Lưu Log Khôi Phục**:
   - Sử dụng **node `slack`** hoặc **node `email`** để gửi thông báo khi khôi phục thành công/lỗi.
   - Ví dụ: Gửi tin nhắn Slack như:
     ```
     🚀 Workflow khôi phục thành công! Tổng số workflow: [X]
     ```

3. **Backup Định Kỳ**:
   - Tự động **backup workflow** lên GitHub trước khi khôi phục bằng cách kết hợp với **node `github`** và **node `schedule`**.

4. **Xử Lý Lỗi File Hỏng**:
   - Thêm **node `if`** để kiểm tra file JSON trước khi khôi phục.
   - Nếu file hỏng, workflow sẽ **bỏ qua** và tiếp tục với file khác.

---

### 📌 **Kết Luận**
Khôi phục workflow n8n từ GitHub **không bao giờ dễ dàng như vậy!** Với workflow này, các sếp:
✔ **Tiết kiệm thời gian** và công sức.
✔ **Đảm bảo an toàn dữ liệu** với backup tự động.
✔ **Không phụ thuộc vào kỹ thuật** để khôi phục.

**Hãy áp dụng ngay và tự động hóa quy trình khôi phục workflow của mình!** 🚀

---
**💡 Cần hỗ trợ thêm?**
- **Book tư vấn 1:1** với **Automation Specialist** (10+ năm kinh nghiệm) tại: [Link tư vấn](https://bangank36.com/consultation).
- **Khám phá thêm workflow tự động hóa** tại: [n8n Community](https://community.n8n.io/).