---
title: "🔄 **Khôi phục Credentials n8n từ GitHub tự động – Giảm thiểu rủi ro mất dữ liệu API chỉ trong 1 click!**"
description: "Workflow này tự động khôi phục tất cả credentials của n8n (API keys, token, secrets) từ backup trên GitHub vào hệ thống, giúp các sếp tránh mất dữ liệu quan trọng khi cấu hình lại máy chủ hoặc nâng cấp phiên bản. Chỉ cần 1 lần setup, workflow hoạt động liên tục 24/7."
slug: "khoi-phuc-credentials-n8n-tu-github"
tags: [n8n, automation, no-code, backup-restore, github-api, credentials-management]
keywords: [n8n workflow khôi phục credentials, tự động hóa backup credentials, khôi phục API keys từ GitHub, n8n self-hosted, lưu trữ an toàn credentials]
---

# 🔄 **Khôi phục Credentials n8n từ GitHub tự động – Bảo vệ API keys của các sếp chỉ trong 1 click!**

### **Nỗi đau thực tế của các sếp khi mất credentials**
Các sếp đã từng trải qua cảnh:
- **Máy chủ bị reset** → Tất cả credentials API (Slack, Stripe, Google Sheets,...) bị xóa, phải nhập lại từ đầu.
- **Nâng cấp phiên bản n8n** → Các API key cũ không còn hoạt động, phải tìm lại hoặc tạo mới.
- **Thay đổi nhân viên** → Không ai biết vị trí lưu trữ credentials, dẫn đến mất thời gian tìm kiếm và rủi ro an toàn.

**Workflow này giải quyết tất cả!** Nó tự động **khôi phục tất cả credentials** từ một **repository GitHub** vào hệ thống n8n của các sếp, **không cần code**, chỉ cần **1 lần setup** và **chạy tự động 24/7**.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không phải nhập lại credentials thủ công khi reset máy chủ.
✅ **An toàn tuyệt đối**: Tất cả credentials được lưu trữ trên GitHub (không lưu trên máy chủ).
✅ **Hoạt động liên tục**: Khôi phục tự động khi cần (ví dụ: sau khi restart n8n).
✅ **Dễ dàng mở rộng**: Thêm/loại credentials mới chỉ cần update file JSON trên GitHub.
✅ **Không phụ thuộc vào nhân viên**: Mất nhân viên cũng không ảnh hưởng đến tính liên tục.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản GitHub** với quyền **read/write** vào repository chứa credentials.
2. **Repository GitHub** lưu trữ file credentials (dạng JSON) ở dạng:
   ```json
   {
     "slack_token": "xoxb-your-slack-token",
     "stripe_secret": "sk_test_abc123",
     "google_sheets_api": "AIzaSyD..."
   }
   ```
3. **Credentials API của GitHub** (tạo tại [GitHub Developer Settings](https://github.com/settings/tokens) với quyền `repo`).
4. **Credentials API của n8n** (tạo tại `Settings > Credentials` trong n8n Dashboard).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/3097) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và **paste** vào **Create Workflow** trong n8n.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Node "Globals" (Node `set`)**
Mở node **"Globals"** và cập nhật **3 tham số** sau:
- **`repo.owner`**: Tên tài khoản GitHub của các sếp (ví dụ: `john-doe`).
- **`repo.name`**: Tên repository chứa credentials (ví dụ: `n8n-backups`).
- **`repo.path`**: Đường dẫn đến folder chứa file credentials (ví dụ: `credentials/`).

**Ví dụ:**
```
repo.owner: john-doe
repo.name: n8n-backups
repo.path: credentials/
```

#### **B. Cấu hình Credentials GitHub**
1. Tại **n8n Dashboard > Credentials**, tạo **1 credential mới** với tên `githubApi`.
2. Chọn **GitHub** và điền:
   - **Token**: Token GitHub (tạo từ [Settings > Developer Settings > Tokens](https://github.com/settings/tokens) với quyền `repo`).
   - **Organization**: Để trống (nếu dùng tài khoản cá nhân).
   - **Repository**: Chọn repository chứa credentials.

#### **C. Cấu hình Credentials n8n**
1. Tại **n8n Dashboard > Credentials**, tạo **1 credential mới** với tên `n8nApi`.
2. Chọn **n8n API** và điền:
   - **API URL**: `https://<your-n8n-instance>/api/v1` (thay `<your-n8n-instance>` bằng URL của n8n).
   - **API Key**: API Key từ **Settings > Credentials** trong n8n Dashboard.

#### **D. Bỏ qua credentials không cần thiết (Node `if`)**
Node **"Check for skipped Credentials"** được thiết kế để **bỏ qua** các file JSON trống hoặc credentials không cần khôi phục (ví dụ: `n8n_account_api.json`).
Các sếp có thể **cập nhật điều kiện** tại node này để phù hợp với nhu cầu:
- **Bỏ qua file trống**: `{{ $json[""] === null || $json[""] === "" }}`
- **Bỏ qua credentials cụ thể**: `{{ $json["skip"] === true }}`

---

### **3. Kích hoạt ⚡️**
1. **Test run** với dữ liệu mẫu:
   - Nhấn **"Test Workflow"** và kiểm tra các bước:
     - Lấy danh sách file từ GitHub.
     - Trích xuất nội dung JSON.
     - Khôi phục credentials vào n8n.
2. **Bật Active workflow**:
   - Sau khi test thành công, chuyển trạng thái workflow sang **"Active"**.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Lưu log hoạt động**
Các sếp có thể **thêm node `stickyNote`** sau node **"Restore n8n Credentials"** để ghi log:
```json
{
  "operation": "add",
  "key": "last_restore_time",
  "value": "{{ $json["timestamp"] }}"
}
```
→ **Kết quả**: Tạo một sticky note lưu thời gian khôi phục cuối cùng.

### **2. Gửi thông báo Slack/Telegram khi khôi phục thành công**
Thêm node **`slack`** hoặc **`telegram`** sau node **"Restore n8n Credentials"** để thông báo:
```json
{
  "text": "✅ Credentials đã khôi phục thành công từ GitHub!",
  "username": "n8n-Bot",
  "icon_emoji": ":robot_face:"
}
```

### **3. Khôi phục định kỳ (dùng Cron Job)**
Nếu các sếp muốn **khôi phục tự động hàng tháng**, có thể:
- **Dùng `n8n CLI`** để chạy workflow định kỳ:
  ```bash
  n8n exec --workflow "Restore Credentials" --schedule "0 0 1 * *"  # Khôi phục vào ngày 1 hàng tháng
  ```
- **Sử dụng `n8n Cloud Scheduler`** (nếu dùng phiên bản Cloud).

### **4. Bảo mật thêm: Mã hóa credentials**
Nếu credentials chứa **dữ liệu nhạy cảm**, các sếp có thể:
- **Mã hóa file JSON** trước khi push lên GitHub (sử dụng `openssl` hoặc `gpg`).
- **Tách credentials thành nhiều file** (ví dụ: `slack.json`, `stripe.json`) và **bỏ qua file không cần thiết**.

---

## 📌 **Kết luận**
Workflow **"Restore your credentials from GitHub"** là **giải pháp hoàn hảo** để các sếp:
✔ **Khôi phục credentials một cách tự động** khi reset máy chủ.
✔ **Tránh mất dữ liệu quan trọng** do nhân viên thay đổi.
✔ **Tiết kiệm thời gian** so với cách làm thủ công.

**Hành động ngay!**
1. **Setup workflow** theo hướng dẫn trên.
2. **Backup credentials** lên GitHub trước khi reset máy chủ.
3. **Bật Active** và **quên đi lo lắng mất dữ liệu!**

👉 **Cần hỗ trợ cá nhân hóa?** Liên hệ tác giả [bangank36](https://n8n.io/workflows/3097) để **tư vấn custom workflow** cho doanh nghiệp của các sếp! 🚀