---
title: "🚀 Tự Động Hóa Thông Báo Release GitHub Hàng Ngày Bằng Email - Giảm Thời Gian Lên Gấp 10 Lần"
description: "Workflow tự động hóa gửi email thông báo tất cả các release mới trên repo GitHub trong ngày qua, giúp dev team không bỏ lỡ bất kỳ update nào. Giúp tiết kiệm thời gian, tăng hiệu quả làm việc và đảm bảo mọi thành viên cập nhật kịp thời."
slug: "tieu-dong-hoa-thong-bao-release-github-hang-ngay-bang-email"
tags: [n8n, automation, github, email, no-code, devops, engineering]
keywords: [n8n workflow github, tự động hóa thông báo release, gửi email tự động từ github, devops automation, tiết kiệm thời gian cho dev team]
---

# 🚀 **Tự Động Hóa Thông Báo Release GitHub Hàng Ngày Bằng Email**

## **💡 Bạn đã bao giờ phải mất thời gian quét thủ công trên GitHub để tìm release mới của dự án?**
Mỗi ngày, các sếp và dev team phải tra cứu trên trang **Releases** của repo GitHub để kiểm tra có update mới không. Điều này không chỉ tốn thời gian mà còn dễ bỏ lỡ những thay đổi quan trọng, ảnh hưởng đến tiến độ phát triển sản phẩm.

**Workflow này giải quyết vấn đề đó bằng cách:**
✅ **Tự động lấy tất cả release mới trong ngày qua** từ repo GitHub.
✅ **Chuyển đổi nội dung Markdown thành HTML** để email đọc dễ dàng.
✅ **Gửi email tự động** đến dev team, quản lý sản phẩm hoặc marketing hàng ngày.
✅ **Không cần viết code** – chỉ cần cấu hình và chạy 24/7.

---
### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải tra cứu thủ công hàng ngày.
- **Đảm bảo không bỏ lỡ update**: Nhận thông báo tất cả release mới ngay vào email.
- **Cá nhân hóa thông báo**: Chỉ gửi đến những người cần thiết (dev, PM, marketing).
- **Hoạt động liên tục**: Workflow chạy tự động hàng ngày, không phụ thuộc vào người dùng.
- **Dễ dàng mở rộng**: Thêm repo khác hoặc thay đổi nội dung email theo nhu cầu.
:::

---
### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản GitHub** và **Token Personal Access** (có quyền đọc repo).
   - *Hướng dẫn tạo Token:* [GitHub Docs - Creating a personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)
   - **Quyền cần thiết**: `repo` (đọc repo).

2. **Tài khoản email SMTP** để gửi thông báo.
   - Nếu dùng **Gmail**, cần **App Password** (do Google yêu cầu 2FA).
   - Các sếp có thể dùng **SendGrid**, **Mailgun** hoặc SMTP của nhà cung cấp hosting.

3. **Repo GitHub** muốn theo dõi release.
   - Workflow sẽ lấy dữ liệu từ URL repo (ví dụ: `https://api.github.com/repos/username/repo/releases`).

---
### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow theo hai cách:
- **Tải file JSON** từ [n8n.io/workflows/2590](https://n8n.io/workflows/2590) và import vào **n8n Editor**.
- **Copy JSON** từ trang trên và dán vào **n8n Editor** (tab `Import`).

:::note[Lưu ý]
- Nếu tự tạo workflow, các sếp cần **sắp xếp nodes theo thứ tự sau**:
  1. **Daily Trigger** (scheduleTrigger)
  2. **If new release in the last day** (if)
  3. **Fetch Github Repo Releases** (httpRequest)
  4. **Split Out Content** (splitOut)
  5. **Convert Markdown to HTML** (markdown)
  6. **Send Email** (emailSend)
:::

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này có **6 node chính**, các sếp cần cấu hình kỹ lưỡng:

##### **🔹 Node 1: Daily Trigger (scheduleTrigger)**
- **Thời gian chạy**: Cấu hình để chạy **mỗi ngày lúc 9h sáng** (hoặc thời gian phù hợp).
- **Format**: `0 9 * * *` (UTC) hoặc điều chỉnh theo múi giờ của các sếp.

##### **🔹 Node 2: If new release in the last day (if)**
- **Điều kiện**: Kiểm tra release có được tạo trong **24 giờ qua** (so sánh `created_at` với thời gian hiện tại).
- **Cấu hình**:
  - **Condition**: `{{ $json["created_at"] }} > {{ $now }}`
  - **Thời gian so sánh**: `$now` là thời gian hiện tại của workflow.

##### **🔹 Node 3: Fetch Github Repo Releases (httpRequest)**
- **URL**: Thay đổi thành URL API của repo GitHub:
  ```
  https://api.github.com/repos/username/repo/releases
  ```
  - Ví dụ: `https://api.github.com/repos/n8n-io/n8n/releases`
- **Headers**:
  - `Accept: application/vnd.github+json`
  - `Authorization: token YOUR_GITHUB_TOKEN`
- **Method**: `GET`

##### **🔹 Node 4: Split Out Content (splitOut)**
- **Chức năng**: Tách dữ liệu release thành các phần riêng lẻ (tên, mô tả, ngày tạo...).
- **Cấu hình**:
  - **Split by**: `$.[]` (lấy tất cả release).
  - **Output**: Các trường như `title`, `body`, `published_at`.

##### **🔹 Node 5: Convert Markdown to HTML (markdown)**
- **Chức năng**: Chuyển nội dung Markdown của release thành HTML để email đọc dễ dàng.
- **Input**: `{{ $node["Split Out Content"].json }}`
- **Output**: `{{ $node["Convert Markdown to HTML"].json }}`

##### **🔹 Node 6: Send Email (emailSend)**
- **SMTP Configuration**:
  - **Host**: `smtp.gmail.com` (hoặc SMTP của nhà cung cấp khác).
  - **Port**: `587` (TLS).
  - **Username**: Email của các sếp.
  - **Password**: **App Password** (nếu dùng Gmail + 2FA).
- **Email Template**:
  - **Subject**: `🚀 New GitHub Releases - {{ $now | date("YYYY-MM-DD") }}`
  - **Body**:
    ```html
    <h2>New Releases Today</h2>
    <ul>
      {% for release in $json %}
        <li>
          <strong>{{ release.title }}</strong><br>
          <small>Published: {{ release.published_at }}</small><br>
          {{ release.body }}
        </li>
      {% endfor %}
    </ul>
    ```
- **To Email**: Thay đổi thành email của dev team hoặc nhóm cần thông báo (ví dụ: `dev-team@example.com`).

---
#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chạy workflow với **data mẫu** để kiểm tra email có gửi đúng không.
   - Kiểm tra **log** trong n8n để đảm bảo không có lỗi.

2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật workflow** để chạy tự động hàng ngày.

---
### **✍️ Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Thêm nhiều repo**:
   - Sử dụng **Loop** để lấy release từ nhiều repo khác nhau.
   - Ví dụ: Lấy release từ `repo1` và `repo2` trong cùng một email.

2. **Gửi báo cáo định kỳ**:
   - Thay vì gửi hàng ngày, các sếp có thể **tổng hợp release trong tuần** và gửi vào thứ 7.

3. **Kết hợp với Slack/Telegram**:
   - Thay vì email, các sếp có thể **gửi thông báo qua Slack** hoặc **Telegram Bot** bằng node `slackSend` hoặc `telegramSend`.

4. **Lưu log vào Google Sheets**:
   - Sử dụng node `googleSheets` để ghi lại lịch sử release và theo dõi.

5. **Thêm filter cho release**:
   - Chỉ gửi email khi có **release mới nhất** (ví dụ: `tag_name` mới nhất).

---
### **📌 Kết luận**
Workflow **Daily GitHub Release Notification by Email** là giải pháp **tự động hóa hoàn hảo** để dev team không phải mất thời gian tra cứu release trên GitHub. Với chỉ **6 node đơn giản**, các sếp có thể:
✔ **Tiết kiệm thời gian** hàng ngày.
✔ **Đảm bảo không bỏ lỡ update** quan trọng.
✔ **Cập nhật đồng bộ** cho cả team.

**Hãy áp dụng ngay và làm việc hiệu quả hơn!** 🚀

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Bạn có thắc mắc gì về workflow này không? Hãy để lại comment bên dưới!** 👇