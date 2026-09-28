---
title: "💾 **Tự Động Hoàn Hảo: Backup Tất Cả Workflow n8n Sang GitHub Miễn Phí - Không Cần Code!**"
description: "Giải pháp tự động hóa hoàn hảo để sao lưu tất cả workflow n8n của bạn lên GitHub, đảm bảo an toàn dữ liệu và dễ dàng phục hồi. Khắc phục nỗi lo mất dữ liệu khi server bị lỗi hoặc bạn muốn chia sẻ workflow với team."
slug: "backup-workflow-n8n-sang-github"
tags: [n8n, automation, backup, github, no-code, self-hosted]
keywords: [backup workflow n8n, tự động hóa n8n, sao lưu workflow, lưu trữ an toàn workflow, n8n github integration]
---

# 🚀 **Backup Tất Cả Workflow n8n Sang GitHub - Không Cần Code!**

### **Giải pháp hoàn hảo cho các sếp lo mất dữ liệu khi server bị lỗi hoặc muốn chia sẻ workflow với team**

Hãy tưởng tượng một tình huống: **Bạn đã xây dựng hàng chục workflow n8n phức tạp, nhưng một ngày nào đó server bị lỗi, hoặc bạn muốn chia sẻ workflow cho đồng nghiệp.** Lúc đó, bạn sẽ phải **tìm kiếm từng file JSON trong hệ thống**, hoặc **tải lại từ đầu** nếu không có bản sao lưu. **Thật tốn thời gian và nguy hiểm!**

Với **workflow này**, các sếp sẽ **tự động sao lưu tất cả workflow n8n lên GitHub** mỗi khi có thay đổi, **không cần code**, **không cần cài đặt gì thêm**, và **miễn phí**. Dữ liệu được lưu trữ an toàn với định dạng `ID.json`, giúp bạn **phục hồi nhanh chóng** khi cần.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **An toàn tuyệt đối**: Sao lưu tự động hàng ngày (hoặc theo lịch bạn thiết lập) để tránh mất dữ liệu do lỗi server.
✅ **Dễ dàng chia sẻ**: Chia sẻ workflow với team hoặc đồng nghiệp chỉ bằng một link GitHub.
✅ **Không cần code**: Cấu hình đơn giản, chỉ cần điền thông tin GitHub là xong.
✅ **Tiết kiệm thời gian**: Không phải thủ công tải xuống từng workflow nữa.
✅ **Phục hồi nhanh chóng**: Khi server bị lỗi, bạn chỉ cần **tải workflow từ GitHub** và import lại.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
✔ **Tài khoản GitHub** (đã có API Token với quyền `repo`).
✔ **Repository GitHub** để lưu trữ backup (ví dụ: `n8n-backups`).
✔ **Thông tin sau để cấu hình trong `Globals` node**:
   - `repo.owner`: Tên tài khoản GitHub của bạn (ví dụ: `john-doe`).
   - `repo.name`: Tên repository (ví dụ: `n8n-backups`).
   - `repo.path`: Đường dẫn thư mục trong repo (ví dụ: `workflows/`).
✔ **N8n Self-hosted** (không thể sử dụng n8n.cloud vì không hỗ trợ backup tự động).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/2652) và import vào n8n Editor.
- **Copy toàn bộ JSON** từ link trên và **dán vào n8n Editor** (tab `Import`).

:::note[**Lưu ý quan trọng**]
- **Không sử dụng n8n.cloud** vì không hỗ trợ backup tự động.
- **N8n phải được cài trên VPS riêng** (Self-hosted) để workflow hoạt động 24/7.
:::

---

### **2. Các bước cấu hình BẮT BUỘC phải chỉnh 📌**

#### **A. Cấu hình `Globals` node (quan trọng nhất!)**
- Mở node **`Globals`** (type: `set`).
- Điền thông tin sau:
  ```json
  {
    "repo.owner": "tên_tài_khoản_github_của_bạn",
    "repo.name": "tên_repository_github",
    "repo.path": "workflows/"  // hoặc bất kỳ thư mục nào bạn muốn
  }
  ```
  **Ví dụ**:
  ```json
  {
    "repo.owner": "john-doe",
    "repo.name": "n8n-backups",
    "repo.path": "workflows/"
  }
  ```

#### **B. Cấu hình GitHub API Token**
- Trong **Credentials GitHub** (n8n-nodes-base.github):
  - **Tạo một API Token mới** trên GitHub (Settings → Developer settings → Personal access tokens).
  - **Chọn quyền `repo`** (full control of private repositories).
  - **Paste token** vào n8n với tên `githubApi`.

#### **C. Cấu hình lịch chạy (Schedule Trigger)**
- Mở node **`Schedule Trigger`** (type: `scheduleTrigger`).
- Chọn **lịch chạy tự động** (ví dụ: `0 0 * * *` để chạy hàng ngày lúc 00:00).
- Hoặc **chạy thủ công** bằng node **`On clicking 'execute'`** (type: `manualTrigger`).

#### **D. Kiểm tra và kích hoạt workflow**
1. **Test run** với một workflow đơn giản để đảm bảo backup hoạt động.
2. **Bật `Active`** workflow để nó chạy tự động theo lịch.

---
### **3. Các node quan trọng cần chú ý**
| **Node** | **Loại** | **Lưu ý** |
|----------|----------|------------|
| **`n8n`** | `n8n` | Sử dụng credentials `n8nApi` (đã cấu hình mặc định). |
| **`Get File`** | `httpRequest` | Lấy dữ liệu workflow từ n8n API. |
| **`If file too large`** | `if` | Xử lý trường hợp file quá lớn (nếu cần). |
| **`Create new file` / `Edit existing file`** | `github` | Tạo hoặc cập nhật file JSON trên GitHub. |
| **`Schedule Trigger`** | `scheduleTrigger` | Xác định thời gian chạy tự động. |
| **`Execute Workflow`** | `executeWorkflow` | Chạy workflow con để giảm tải bộ nhớ. |

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[**Cải thiện hiệu suất & an toàn**]
🔹 **Lọc workflow quan trọng**: Sử dụng node **`isDiffOrNew`** (type: `code`) để chỉ backup workflow có thay đổi.
🔹 **Lưu log hoạt động**: Thêm node **`stickyNote`** để ghi lại lịch sử backup.
🔹 **Gửi thông báo Slack/Telegram**: Kết nối với **Slack API** hoặc **Telegram Bot** để nhận báo cáo khi backup thành công/thất bại.
🔹 **Backup định kỳ**: Sử dụng **cron job** trên VPS để chạy workflow hàng ngày.
🔹 **Phân quyền GitHub**: Đặt repository GitHub là **private** để bảo mật.
:::

---
## 📌 **Kết luận**
**Backup workflow n8n sang GitHub là giải pháp hoàn hảo** để các sếp **an tâm về dữ liệu**, **chia sẻ dễ dàng** và **tiết kiệm thời gian**. Với workflow này, bạn **không cần lo mất dữ liệu** khi server bị lỗi, và **cũng không cần code** để cấu hình.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình `Globals` node.
2. **Kích hoạt lịch chạy tự động**.
3. **Phục hồi workflow trong giây lát** khi cần!

**👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%) để n8n chạy ổn định 24/7!**

---
**Cần hỗ trợ?** Liên hệ với tác giả Solomon qua:
📧 **automations.solomon@gmail.com**
💬 **Telegram**: [@solomon_automations](https://t.me/solomon_automations) (trả lời nhanh nhất!)