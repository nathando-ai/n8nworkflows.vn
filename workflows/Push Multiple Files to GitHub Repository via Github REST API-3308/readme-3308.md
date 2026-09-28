---
title: "🚀 Tự Động Hoàn Thành Push Nhiều File Lên GitHub Mới Nhất (Không Cần Code)"
description: "Workflow này tự động đẩy đồng thời nhiều file lên GitHub mà không bị giới hạn của node GitHub native (chỉ hỗ trợ 1 file). Giúp các sếp tiết kiệm thời gian và tránh thủ công, đặc biệt hữu ích cho dự án DevOps, CI/CD hoặc quản lý tài liệu."
slug: "tu-dong-hoan-thanh-push-nhieu-file-len-github"
tags: [n8n, automation, devops, github, api, no-code]
keywords: [n8n workflow github, tự động hóa đẩy file lên github, upload batch file github, devops automation, push nhiều file github api]
---

# 🚀 **Tự Động Push Nhiều File Lên GitHub Mới Nhất (Không Cần Code)**

### **Nỗi Đau Của Các Sếp**
Các sếp thường phải **thủ công** đẩy nhiều file lên GitHub, đặc biệt khi:
- Cập nhật tài liệu dự án (README, config, script).
- Tự động hóa CI/CD với nhiều file phụ thuộc.
- Quản lý các file cấu hình cho nhiều môi trường (dev/staging/prod).

**Giải pháp?** Workflow này **tự động hóa toàn bộ quá trình**, đẩy **nhiều file cùng lúc** lên GitHub mà không bị giới hạn của node GitHub native (chỉ hỗ trợ 1 file).

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần copy/paste từng file thủ công.
- **Chính xác 100%**: Tránh lỗi do người dùng gây ra khi push nhiều file.
- **Hoạt động liên tục**: Hoạt động 24/7 khi self-hosted trên VPS.
- **Hỗ trợ batch**: Đẩy **tất cả file** trong một lần (không giới hạn số lượng).
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
- **Tài khoản GitHub** và **Personal Access Token** (PAT) với quyền:
  - **Read & Write** cho **Contents** (để push file).
  - **Repository access** cho repo mục tiêu.
- **Danh sách file** muốn đẩy (có thể là file trong máy hoặc nội dung text).
- **VPS tự host n8n** (để workflow hoạt động 24/7).
:::

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/3308) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  ```bash
  # Nếu tải file JSON:
  1. Mở n8n Editor → Nhấn "Import" → Chọn file JSON.
  # Nếu copy/paste:
  1. Mở n8n Editor → Nhấn "Import" → Chọn "Paste JSON".
  ```

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này gồm **9 node**, nhưng **3 node quan trọng nhất** cần cấu hình kỹ:

##### **A. Cấu Hình GitHub Info (Node "Set Github Info")**
- **Tham số cần điền**:
  - `repository`: Tên repo (ví dụ: `my-repo`).
  - `owner`: Tên owner (ví dụ: `tino-host`).
  - `accessToken`: **Personal Access Token** (PAT) đã tạo trước.
  - `branch`: Branch muốn đẩy (ví dụ: `main`).

##### **B. Thêm File (Node "File 1", "File 2", ...)**
- **Cách thêm file**:
  - **Nội dung file**: Điền **nội dung text** của file (ví dụ: `content: "Hello World"`).
  - **Tên file**: Đặt tên file (ví dụ: `file1.txt`).
  - **Lưu ý**:
    - Có thể thêm **nhiều node "File X"** cho nhiều file khác nhau.
    - Nếu file là **binary** (như PDF, Excel), cần **encode base64** trước khi đẩy.

##### **C. Test API (Node "httpRequest")**
- Workflow tự động gọi **GitHub REST API** để:
  1. Lấy **SHA của commit cũ** (`Get latest commit SHA`).
  2. Tạo **tree mới** (`Create new tree`) với tất cả file.
  3. **Commit** và **push** lên branch (`Create commit` + `Update branch`).

---
#### **3. Kích Hoạt ⚡️**
- **Test run**:
  - Nhấn **"Test workflow"** để kiểm tra.
  - Kiểm tra **log** trong n8n để đảm bảo file đẩy thành công.
- **Bật Active**:
  - Sau khi test thành công, **bật workflow** và **lưu**.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH LÀM NGOÀI THƯỜNG]
- **Tự động hóa từ folder local**:
  - Sử dụng **node "File System"** để quét folder và tự động đẩy tất cả file.
- **Gửi thông báo Slack/Telegram**:
  - Kết nối với **Slack/Telegram** để báo cáo kết quả push.
- **Lưu log vào Google Sheets**:
  - Sử dụng **Google Sheets** để ghi lại lịch sử push.
- **Chạy định kỳ**:
  - Sử dụng **n8n Cron** để đẩy file theo lịch (ví dụ: hàng ngày).
:::

---
### 📌 **Kết Luận**
Workflow này **giải quyết hoàn toàn vấn đề đẩy nhiều file lên GitHub** mà không cần code, giúp các sếp **tiết kiệm thời gian và tránh lỗi thủ công**. **Hãy tự động hóa ngay** và **tận hưởng hiệu quả cao**!

👉 **Bắt đầu ngay** với **VPS TinoHost** (giảm 39% với mã **VPSN8N**):
🔗 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)
🔗 [Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---