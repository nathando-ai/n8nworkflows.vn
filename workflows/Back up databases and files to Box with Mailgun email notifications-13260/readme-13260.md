---
title: "🚀 Tự Động Hoàn Chỉnh Sách Backup Dữ Liệu & Tệp Tới Box Với Thông Báo Email Mailgun (N8n)"
description: "Workflow tự động hóa backup cơ sở dữ liệu và tệp tin tới Box Cloud với thông báo email tự động qua Mailgun, giúp các sếp tiết kiệm thời gian và đảm bảo an toàn dữ liệu 24/7. Hỗ trợ backup định kỳ hoặc theo yêu cầu từ bên ngoài."
slug: "tự-dộng-hoàn-chỉnh-sách-backup-dữ-liệu-tới-box"
tags: [n8n, automation, devops, backup, box-cloud, mailgun, no-code]
keywords: [n8n backup database, tự động hóa backup tệp tin, backup tới Box, Mailgun email notification, tự động hóa DevOps]
---

# 🚀 **Backup Dữ Liệu & Tệp Tới Box Với Thông Báo Email Tự Động**

### **Giải quyết vấn đề gì?**
Các sếp đang gặp khó khăn khi phải **backup thủ công** cơ sở dữ liệu và tệp tin hàng ngày, lo ngại mất dữ liệu do lỗi người dùng hoặc hệ thống. Hoặc lại phải **quên backup định kỳ**, dẫn đến rủi ro mất mát không đáng có.

Workflow này **tự động hóa toàn bộ quy trình backup** từ việc lấy dữ liệu, nén, upload lên **Box Cloud**, cho đến việc **gửi thông báo email tự động** qua **Mailgun** khi backup thành công hoặc thất bại. **Không cần code**, chỉ cần cấu hình và chạy 24/7!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần backup thủ công hàng ngày.
✅ **An toàn dữ liệu**: Backup tự động, định kỳ hoặc theo yêu cầu.
✅ **Thông báo tức thời**: Email tự động khi backup thành công/thất bại.
✅ **Dữ liệu sắp xếp logic**: Mỗi backup được lưu trong **thư mục theo ngày** trên Box.
✅ **Hỗ trợ nhiều nguồn dữ liệu**: Backup từ **cơ sở dữ liệu, tệp tin, API**...
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Box Cloud** (để lưu backup) và **API Key** của Box.
2. **Tài khoản Mailgun** (để gửi email thông báo) và **API Key**.
3. **Các URL export dữ liệu** (để workflow lấy dữ liệu backup).
4. **IP của máy chủ n8n** (để whitelist trong các dịch vụ export).
5. **Scheduler ngoài (cron, CI/CD, hoặc webhook)** để kích hoạt backup theo lịch hoặc yêu cầu.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13260](https://n8n.io/workflows/13260) hoặc copy toàn bộ JSON từ link trên.
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON và chọn **"Import"**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **15 node**, các sếp cần chú ý cấu hình sau:

##### **🔹 Node Webhook (Backup Webhook Trigger)**
- **Path**: `scheduled-backup` (không thay đổi).
- **HTTP Method**: `POST`.
- **Lưu ý**: Cần **whitelist IP của n8n** trong các dịch vụ export (ví dụ: MySQL, PostgreSQL, FTP...).

##### **🔹 Node Set (Set Default Backup Config)**
- **Tham số mặc định**: Đảm bảo có **tối thiểu 3 nguồn backup** (cơ sở dữ liệu, tệp tin, cấu hình).
- **Cấu hình**:
  ```json
  {
    "database": "your_database_url",
    "fileStorage": "your_file_storage_url",
    "config": "your_config_file_url"
  }
  ```

##### **🔹 Node Box (Create Backup Folder)**
- **Tham số cần điền**:
  - **Folder Name**: `Backup_$(date +%Y-%m-%d)` (tự động tạo tên theo ngày).
  - **Parent Folder ID**: Điền **ID của thư mục cha** trên Box (tham khảo [Box API Docs](https://developer.box.com/)).

##### **🔹 Node Code (Prepare Backup Items & Compress Export)**
- **Node "Prepare Backup Items"**:
  - Chuyển đổi danh sách backup thành **mảng đối tượng** với cấu trúc:
    ```json
    {
      "url": "your_export_url",
      "folderId": "${{ $node["Create Backup Folder"].json["folderId"] }}"
    }
    ```
- **Node "Compress Export"**:
  - Sử dụng **zlib** (Node.js built-in) để nén dữ liệu thành **GZIP**.
  - **Mẫu mã code**:
    ```javascript
    const zlib = require('zlib');
    const gzip = zlib.createGzip();
    const chunks = [];
    for await (const chunk of $input.all()) {
      chunks.push(chunk);
    }
    const buffer = Buffer.concat(chunks);
    const compressed = await new Promise((resolve, reject) => {
      gzip.end(buffer, (err, result) => {
        if (err) reject(err);
        else resolve(result);
      });
    });
    return { binary: compressed, filename: `backup_${Date.now()}.gz` };
    ```

##### **🔹 Node Box (Upload to Box)**
- **Tham số cần điền**:
  - **Folder ID**: Điền **ID thư mục backup** từ node **"Create Backup Folder"**.
  - **File Name**: `${{ $node["Compress Export"].json["filename"] }}`.

##### **🔹 Node Mailgun (Send Success/Failure Notification)**
- **Tham số chung**:
  - **API Key**: Điền **API Key Mailgun**.
  - **Domain**: Điền **domain Mailgun**.
- **Node "Compose Success Email"**:
  - **Subject**: `Backup thành công: {{ $node["Prepare Backup Items"].json["url"] }}`.
  - **Body**:
    ```html
    <p>Backup {{ $node["Prepare Backup Items"].json["url"] }} thành công vào {{ $node["Create Backup Folder"].json["createdAt"] }}.</p>
    ```
- **Node "Compose Failure Email"**:
  - **Subject**: `Lỗi backup: {{ $node["Prepare Backup Items"].json["url"] }}`.
  - **Body**:
    ```html
    <p>Backup {{ $node["Prepare Backup Items"].json["url"] }} thất bại tại bước: {{ $node["Was Export Successful?"].json["error"] || $node["Was Upload Successful?"].json["error"] }}.</p>
    ```

#### **3. Kích hoạt ⚡️**
- **Test run**:
  - Gửi **POST request** tới `http://[your-n8n-server]/scheduled-backup` với payload mẫu:
    ```json
    {
      "database": "your_database_url",
      "fileStorage": "your_file_storage_url"
    }
    ```
  - Kiểm tra **email thông báo** từ Mailgun.
- **Bật Active workflow**:
  - Chuyển **switch Active** sang **ON**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Backup định kỳ với cron**:
   - Sử dụng **cron job** để gọi webhook hàng ngày:
     ```bash
     0 3 * * * curl -X POST http://[your-n8n-server]/scheduled-backup
     ```
2. **Gửi báo cáo tổng hợp**:
   - Thêm **node Set** sau Mailgun để tổng hợp kết quả backup thành **email báo cáo hàng tuần**.
3. **Lưu log chi tiết**:
   - Sử dụng **node StickyNote** để ghi log lỗi và debug.
4. **Kết hợp với Slack/Telegram**:
   - Thêm **node Slack/Telegram** để thông báo ngay khi backup thất bại.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc backup thủ công, đồng thời **đảm bảo dữ liệu an toàn** với thông báo tức thời. **Chỉ cần cấu hình 1 lần**, workflow sẽ chạy tự động hàng ngày!

**🚀 Hãy áp dụng ngay và bảo vệ dữ liệu của doanh nghiệp!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/13260)**
**💬 Có thắc mắc? Để lại comment bên dưới!**