---
title: "🔄 **Tự Động Hoàn Chỉnh & Khôi Phục Workflow n8n Sang GitHub - Giải Pháp Backup 24/7 Miễn Lo Lắng**"
description: "Workflow này tự động sao lưu tất cả workflow n8n của các sếp lên GitHub hàng ngày (7h tối) và khôi phục lại khi cần, giúp bảo vệ dữ liệu khỏi mất mát, cập nhật tự động và phục hồi nhanh chóng sau sự cố. Đảm bảo không bao giờ mất một workflow nào!"
slug: "tự-dộng-hoàn-chỉnh-khôi-phục-workflow-n8n-sang-github"
tags: [n8n, automation, devops, backup-restore, github-integration, no-code]
keywords: [tự động hóa n8n, backup workflow n8n, khôi phục workflow n8n, sync n8n với github, tự động hóa devops, bảo vệ dữ liệu n8n]
---

# **🚀 Tự Động Hoàn Chỉnh & Khôi Phục Workflow n8n Sang GitHub - Bảo Vệ Dữ Liệu Miễn Lo Lắng**

## **💡 Nỗi Đau Của Các Sếp Và Giải Pháp Tự Động Hóa**
Các sếp đã từng trải qua những tình huống kinh hoàng như:
- **Mất workflow quan trọng** do lỗi xóa ngẫu nhiên hoặc reset n8n.
- **Không thể khôi phục lại** vì không có bản sao lưu.
- **Cập nhật thủ công** mỗi khi có thay đổi, tốn thời gian và dễ sai sót.
- **Không biết workflow nào đã được cập nhật** trên GitHub và n8n.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Sao lưu tất cả workflow** lên GitHub hàng ngày (7h tối).
✅ **Phát hiện thay đổi** (tạo mới, sửa đổi, đổi tên, xóa).
✅ **Khôi phục lại n8n** từ GitHub chỉ với một cú nhấp chuột.
✅ **Tối ưu hóa commit** để tránh spam và tiết kiệm API calls.

---

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo vệ dữ liệu 100%**: Không bao giờ mất workflow do lỗi hệ thống.
- **Tiết kiệm thời gian**: Sao lưu tự động hàng ngày, không cần can thiệp.
- **Cập nhật chính xác**: Phát hiện ngay khi có thay đổi trên cả hai hệ thống.
- **Khôi phục nhanh chóng**: Khôi phục lại workflow chỉ trong vài giây.
- **Lịch sử rõ ràng**: Commit messages tự động theo định dạng `[Tên Workflow] ([Thao Tác]) YYYY-MM-DD`.
:::

---

### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản GitHub**:
   - **OAuth App** được cấu hình với callback URL là URL của n8n instance.
   - **Repository** mới (public hoặc private) để lưu workflow.
2. **API Key của n8n**:
   - Tạo tại `Settings → API` và thêm vào workflow như credential.
3. **Dung lượng lưu trữ**:
   - Đảm bảo GitHub repo có đủ dung lượng cho tất cả workflow.
:::

---

### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/12721](https://n8n.io/workflows/12721).
2. Mở **n8n Editor** → Nhấn `Import` → Chọn file JSON.
3. **Hoặc** copy toàn bộ JSON vào `Import Workflow` và nhấn `Import`.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **2 phần chính**:
- **Backup** (sao lưu workflow lên GitHub).
- **Restore** (khôi phục workflow từ GitHub).

##### **A. Cấu Hình GitHub OAuth**
1. **Tạo OAuth App trên GitHub**:
   - Đi đến `Settings → Developer settings → OAuth Apps`.
   - Thêm **Authorization callback URL**: `https://<n8n-instance-url>/oauth2/callback/github`.
   - Lưu **Client ID** và **Client Secret**.

2. **Thêm Credential vào n8n**:
   - Đi đến `Credentials → New → GitHub OAuth2`.
   - Điền `Client ID` và `Client Secret` từ bước trên.

##### **B. Cấu Hình Repository**
1. **Tạo Repository mới** trên GitHub (ví dụ: `n8n-workflows-backup`).
2. **Cập nhật "Set Github Data"**:
   - Thay đổi `repo_owner` và `repo_name` trong node này:
     ```json
     {
       "repo_owner": "tên-tài-khoản-github",
       "repo_name": "n8n-workflows-backup"
     }
     ```

##### **C. Cấu Hình n8n API**
1. **Tạo API Key**:
   - Đi đến `Settings → API` → Nhấn `Create API Key`.
   - Chọn `n8nApi` credential trong workflow và điền API Key.

##### **D. Cấu Hình Schedule Trigger (Backup Hàng Ngày)**
1. Trong node **Schedule Trigger**, thay đổi `cron` thành:
   ```plaintext
   0 19 * * *  # Chạy hàng ngày lúc 7h tối (UTC)
   ```
   (Điều chỉnh theo múi giờ của các sếp).

##### **E. Cấu Hình Restore Workflow**
- **Manual Trigger**: Để khôi phục, các sếp nhấn nút `Execute` trên node **Manual Trigger**.

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chạy workflow **Backup** với mode `Test` để kiểm tra.
   - Kiểm tra GitHub repo có xuất hiện file `index.json` và các workflow tương ứng không.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển workflow sang **Active**.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
1. **Lưu Log Tự Động**:
   - Thêm node **Slack/Telegram** để thông báo khi backup/restore thành công/thất bại.
2. **Backup Định Kỳ**:
   - Sử dụng **Google Drive/Dropbox** để sao lưu thêm bản sao lưu của GitHub.
3. **Khôi Phục Lots Workflow**:
   - Cho phép khôi phục nhiều workflow cùng lúc bằng cách chỉnh sửa node **Split In Batches**.
4. **Báo Cáo Thống Kê**:
   - Tạo một workflow riêng để gửi báo cáo hàng tuần về số lượng workflow đã backup/restore.
:::

---

### **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** để các sếp:
✔ **Bảo vệ workflow** khỏi mất mát.
✔ **Tự động hóa backup** hàng ngày.
✔ **Khôi phục nhanh chóng** khi cần.
✔ **Tối ưu hóa commit** để tránh spam.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Bật backup hàng ngày** để yên tâm dữ liệu.
3. **Khôi phục lại workflow** chỉ trong vài giây khi cần.

**🎁 Đăng ký VPS cho n8n 24/7**:
:::info[HƯỚNG DẪN CÀI ĐẶT N8N TRÊN VPS]
Để workflow chạy ổn định, các sếp nên cài n8n trên **VPS riêng**:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

**Chúc các sếp thành công!** 🚀