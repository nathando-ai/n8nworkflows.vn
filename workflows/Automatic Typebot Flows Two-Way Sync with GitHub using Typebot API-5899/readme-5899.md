---
title: "🔄 **Tự Động Hóa Sync Hai Chiều Typebot & GitHub: Bảo Mật & Khôi Phục Dữ Liệu 100% Miễn Phí**"
description: "Workflow này tự động đồng bộ hóa toàn bộ Typebot (các chatbot tương tác) của bạn với GitHub, bao gồm cả việc sao lưu và khôi phục khi có sự thay đổi hoặc xóa. Giúp các sếp bảo vệ dữ liệu quan trọng mà không cần viết một dòng code nào."
slug: "tieu-dong-hoa-sync-typebot-github"
tags: [n8n, automation, devops, typebot, github, backup, no-code]
keywords: [tự động hóa typebot, backup typebot github, sync hai chiều typebot, lưu trữ chatbot, bảo mật dữ liệu typebot]
---

# 🔄 **Tự Động Hóa Sync Hai Chiều Typebot & GitHub: Bảo Mật & Khôi Phục Dữ Liệu 100% Miễn Phí**

## **🚨 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Bạn đã bao giờ lo lắng về việc mất dữ liệu quan trọng trong Typebot (chatbot tương tác) chưa? Hay phải tốn thời gian sao lưu thủ công mỗi khi cập nhật một chatbot mới? Với **Workflow này**, các sếp sẽ **tự động đồng bộ hóa toàn bộ Typebot với GitHub**, bao gồm cả việc **sao lưu, khôi phục và theo dõi sự thay đổi** một cách liên tục, **không cần viết code**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🎯 Kết Quả Các Sếp Nhận Được**
- **🔒 Sao lưu tự động** tất cả Typebot vào GitHub với định dạng `ID.json` (không mất dữ liệu dù có xóa trên Typebot).
- **🔄 Sync hai chiều** giữa Typebot và GitHub: Thay đổi trên Typebot sẽ tự động cập nhật lên GitHub, và ngược lại.
- **📅 Khôi phục nhanh chóng** nếu có sự cố (xóa, lỗi cấu hình).
- **📊 Theo dõi sự thay đổi** một cách minh bạch (tạo, sửa, xóa).
- **💡 Tiết kiệm thời gian** lên đến **90%** so với sao lưu thủ công.

---

### **🔧 Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
✅ **Tài khoản GitHub** (để lưu trữ backup).
✅ **Tài khoản Typebot** (cần **URL Typebot** và **ID Workspace**).
✅ **API Key GitHub OAuth 2.0** (để n8n có quyền truy cập vào repo).
✅ **Một repository GitHub** để lưu trữ backup (ví dụ: `n8n-backups`).

---

### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/5899](https://n8n.io/workflows/5899) hoặc copy/paste JSON vào **n8n Editor**.
- **Chọn "Import"** và chọn file JSON đã tải.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này được chia thành **2 phần chính**:
- **Workflow chính** (sync hai chiều Typebot ↔ GitHub).
- **Subworkflow** (giúp giảm tải bộ nhớ).

##### **🔹 Cấu Hình Node "Globals" (Quá Trình Cấu Hình Cốt Lõi)**
Mở node **"Globals"** và cập nhật các tham số sau:
```json
{
  "repo.owner": "tên_tài_khoản_github_của_bạn", // Ví dụ: "john-doe"
  "repo.name": "tên_repository_github",         // Ví dụ: "n8n-backups"
  "typebot.url": "https://your-typebot-url.com", // URL Typebot của bạn
  "typebot.workspace.id": "ID_workspace_của_bạn" // Tìm trên Typebot Docs
}
```
🔹 **Lấy ID Workspace Typebot**:
- Mở [Typebot Docs](https://docs.typebot.io/api-reference/how-to).
- Đăng nhập và tìm **Workspace ID** trong phần **API Settings**.

##### **🔹 Cấu Hình Node GitHub (Credentials)**
- Đăng nhập vào **n8n** → **Credentials** → **Add GitHub OAuth 2.0**.
- Chọn **GitHub OAuth 2.0** và cấp quyền cho n8n truy cập vào repo.
- **Lưu ý**: Nếu repo là **private**, cần cấp quyền **repo** cho OAuth.

##### **🔹 Cấu Hình Node "Schedule Trigger" (Đồng Bộ Hóa Định Kỳ)**
- Mở node **"Schedule Trigger"** và chọn **thời gian chạy tự động** (ví dụ: **mỗi ngày 2 giờ sáng**).
- **Lưu ý**: Nếu muốn chạy thủ công, có thể bỏ qua và sử dụng **Manual Trigger**.

#### **3. Kích Hoạt ⚡️**
- **Test Run** với dữ liệu mẫu (nếu có).
- **Bật Active** workflow và **chờ đồng bộ hoàn tất**.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **📌 Thêm Log Lịch Sử**:
   - Sử dụng **Slack/Telegram** để thông báo khi có sự thay đổi (tạo, sửa, xóa).
   - **Cách làm**: Thêm node **HTTP Request** → **Webhook Slack/Telegram**.

2. **📊 Báo Cáo Định Kỳ**:
   - Sử dụng **Google Sheets** hoặc **Notion** để lưu trữ lịch sử thay đổi.
   - **Cách làm**: Thêm node **Google Sheets** sau **Merge** để ghi dữ liệu.

3. **🔄 Sync Lại Từ GitHub Sang Typebot**:
   - Nếu muốn **khôi phục Typebot từ GitHub**, có thể thêm **Workflow mới** để pull dữ liệu từ repo.

4. **🔒 Bảo Mật API Key**:
   - **Không bao giờ push API Key GitHub lên GitHub** (sử dụng **n8n Credentials** thay vì hardcode).

---

### **📌 Kết Luận**
Workflow này **giải quyết hoàn toàn vấn đề mất dữ liệu Typebot** bằng cách **tự động sao lưu và sync hai chiều với GitHub**. Các sếp không cần lo lắng về việc **xóa nhầm chatbot** hoặc **không sao lưu kịp thời** nữa.

**🚀 Hãy áp dụng ngay và bảo vệ dữ liệu Typebot của mình!**
Nếu có vấn đề, hãy để lại **comment** dưới đây hoặc liên hệ với **n8n Community** để hỗ trợ.

---
**💡 Gợi Ý Tiếp Theo**:
- Nếu muốn **tự động khôi phục Typebot từ GitHub**, có thể xây dựng **Workflow phụ** để pull dữ liệu.
- **Kết hợp với Notion** để quản lý chatbot một cách chuyên nghiệp hơn.