---
title: "📝 Tự Động Hoàn Tất Bài Viết Cũ WordPress Sang Trạng Thái Nháp - Giảm Gánh Nặng Cho Admin"
description: "Workflow tự động hóa chuyển đổi bài viết cũ trên WordPress sang trạng thái nháp hàng quý, giúp tiết kiệm thời gian quản lý nội dung và tối ưu hóa hiệu suất trang web. Giúp các sếp giảm 30-50% công việc thủ công trong quản lý bài viết."
slug: "tieu-dong-hoan-tat-bai-viet-cu-wordpress-sang-nhap"
tags: [n8n, automation, wordpress, content-management, no-code]
keywords: [tự động hóa wordpress, lưu trữ bài viết cũ, quản lý nội dung tự động, workflow n8n wordpress, tự động hóa quản trị website]
---

# 🚀 **Tự Động Hoàn Tất Bài Viết Cũ WordPress Sang Trạng Thái Nháp - Giải Pháp Tiết Kiệm Thời Gian Cho Admin**

### **Nỗi Đau Thực Tế Của Các Sếp**
Quản lý một trang WordPress với hàng trăm bài viết cũ vẫn đang hoạt động? Các sếp thường phải:
- **Tìm kiếm thủ công** bài viết đã lỗi thời, không được cập nhật trong nhiều tháng.
- **Tốn thời gian** để chuyển đổi chúng sang trạng thái nháp (draft) hoặc xóa trực tiếp.
- **Lo ngại ảnh hưởng SEO** khi bài viết cũ vẫn hiển thị trong kết quả tìm kiếm.
- **Phải nhớ nhắc** mình thực hiện công việc này định kỳ, dễ bị quên hoặc trì hoãn.

**Workflow này tự động hóa toàn bộ quy trình**, giúp các sếp **tiết kiệm 30-50% thời gian quản lý nội dung** và đảm bảo trang web luôn sạch sẽ, chuyên nghiệp.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công hàng tháng.
- **Tối ưu hóa SEO**: Bài viết cũ không còn xuất hiện trong kết quả tìm kiếm.
- **Giảm tải cho server**: Trang web tải nhanh hơn khi loại bỏ nội dung lỗi thời.
- **Lưu trữ an toàn**: Bài viết cũ vẫn được bảo quản trong hệ thống (trạng thái nháp).
- **Thông báo tự động**: Nhận email cảnh báo khi có bài viết được hoàn tất.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản WordPress**:
   - API Key của WordPress (tạo từ **Settings > General > API**).
   - URL trang WordPress (ví dụ: `https://tênmientrang.com`).
2. **Tài khoản Email**:
   - Thông tin SMTP để gửi email thông báo (tên miền, port, username, password).
3. **VPS n8n Self-hosted** (khuyến cáo):
   - Để workflow chạy 24/7 ổn định, không phụ thuộc vào phiên bản miễn phí.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7418](https://n8n.io/workflows/7418) hoặc copy/paste JSON từ trang này.
- Mở **n8n Editor** (trang chủ của n8n) → Nhấn **"Import"** → Dán JSON → Chọn **"Import"**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **6 node chính**, các sếp cần cấu hình kỹ lưỡng như sau:

##### **A. Node "Quarterly Trigger" (n8n-nodes-base.scheduleTrigger)**
- **Cấu hình**:
  - **Schedule**: Chọn **"Cron"** với biểu thức `0 0 1 */3 *` (chạy vào ngày 1 của mỗi tháng thứ 3, tức hàng quý).
  - **Timezone**: Đặt theo múi giờ của trang WordPress (ví dụ: `Asia/Ho_Chi_Minh`).
- **Lưu ý**:
  - Nếu muốn chạy vào ngày khác (ví dụ: ngày 15), thay đổi biểu thức thành `0 0 15 */3 *`.

##### **B. Node "Find Old Posts" (n8n-nodes-base.wordpress)**
- **Cấu hình**:
  - **Operation**: Chọn **"Get All"** (lấy tất cả bài viết).
  - **Parameters**:
    - **Status**: Chọn **"publish"** (bài viết đã xuất bản).
    - **Date Query**: Thêm điều kiện lọc bài viết cũ (ví dụ: `last_modified < 2023-01-01`).
      - *Gợi ý*: Sử dụng **Expression** để lọc bài viết có `last_modified` trước ngày cụ thể (ví dụ: `{{ $node["Find Old Posts"].jsonpath("$.posts[*].last_modified") }} < "2023-01-01"`).
    - **Fields**: Chọn các trường cần lấy (tiêu đề, slug, ngày cập nhật, trạng thái).
- **Lưu ý**:
  - Nếu không có điều kiện lọc, workflow sẽ lấy tất cả bài viết, không hiệu quả.
  - *Mẹo*: Thêm **filter node** sau này để lọc bài viết có `views < 100` (ít người xem) hoặc `last_comment_date > 6 months ago` (không có bình luận mới).

##### **C. Node "Check if Posts Found" (n8n-nodes-base.if)**
- **Cấu hình**:
  - **Condition**: Kiểm tra `$.posts.length > 0` (có bài viết cũ hay không).
  - **True Branch**: Chuyển sang node **"Archive Post"** nếu có bài viết.
  - **False Branch**: Chuyển sang node **"Log No Posts"** (gửi thông báo không có bài viết).

##### **D. Node "Archive Post" (n8n-nodes-base.wordpress)**
- **Cấu hình**:
  - **Operation**: Chọn **"Update"**.
  - **Parameters**:
    - **Post ID**: Lấy từ output của node **"Find Old Posts"** (ví dụ: `{{ $node["Find Old Posts"].jsonpath("$.posts[*].id") }}`).
    - **Status**: Đặt thành **"draft"** (nháp).
    - **Post Content**: Có thể thêm **comment** tự động (ví dụ: `"This post was archived on {{ $node["Quarterly Trigger"].date }}"`).
- **Lưu ý**:
  - Sử dụng **Loop** để xử lý từng bài viết một (nếu có nhiều bài viết).
  - *Mẹo*: Thêm node **stickyNote** để ghi chú lý do hoàn tất (ví dụ: `"Archived due to low engagement"`).

##### **E. Node "Send Notification" (n8n-nodes-base.emailSend)**
- **Cấu hình**:
  - **Credentials**: Chọn SMTP đã cấu hình trước (ví dụ: Gmail, SendGrid).
  - **To**: Địa chỉ email của admin (ví dụ: `admin@tênmientrang.com`).
  - **Subject**: `"WordPress Archive Report - {{ $node["Quarterly Trigger"].date }}"`.
  - **Body**: Nội dung email tự động (ví dụ:
    ```html
    <p>Xin chào,</p>
    <p>Workflow tự động đã hoàn tất {{ $node["Archive Post"].jsonpath("$.posts.length") }} bài viết cũ sang trạng thái nháp.</p>
    <p>Danh sách bài viết:</p>
    <ul>{{ $node["Archive Post"].jsonpath("$.posts[*].title.rendered") | join(", ") }}</ul>
    <p>Trân trọng,</p>
    <p>Hệ thống tự động</p>
    ```).
- **Lưu ý**:
  - *Mẹo*: Thêm **attachment** là file CSV danh sách bài viết đã hoàn tất.

##### **F. Node "Log No Posts" (n8n-nodes-base.noOp)**
- **Cấu hình**:
  - **Action**: Thêm **stickyNote** để ghi chú (ví dụ: `"Không có bài viết cũ cần hoàn tất"`).
  - *Mẹo*: Kết hợp với node **emailSend** để thông báo không có bài viết.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhấn **"Run Workflow"** để kiểm tra với dữ liệu mẫu.
  - Kiểm tra email và WordPress để xác nhận bài viết đã được hoàn tất.
- **Bật Active**:
  - Sau khi test thành công, chuyển trạng thái workflow sang **"Active"**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Lọc bài viết theo tiêu chí cụ thể**:
   - Thêm node **filter** để chỉ hoàn tất bài viết có:
     - **Views < 100** (ít người xem).
     - **Last comment > 6 months ago** (không có bình luận mới).
     - **Category = "Tin tức cũ"** (loại bỏ bài viết trong danh mục đặc biệt).

2. **Gửi báo cáo định kỳ**:
   - Kết hợp với **Google Sheets** hoặc **Slack** để gửi báo cáo chi tiết hàng tháng.

3. **Xóa bài viết thay vì hoàn tất**:
   - Thay vì chuyển sang nháp, có thể **xóa bài viết** bằng cách thay đổi `status` thành `"trash"`.

4. **Thêm thông báo Slack**:
   - Kết nối với **Slack** để gửi cảnh báo khi có bài viết được hoàn tất (ví dụ: `@channel Bài viết "Tên bài viết" đã được hoàn tất`).

5. **Lưu log chi tiết**:
   - Sử dụng **Google Drive** hoặc **AWS S3** để lưu lịch sử hoạt động của workflow.
:::

---

### 📌 **Kết Luận**
Workflow **"Tự Động Hoàn Tất Bài Viết Cũ WordPress"** là giải pháp **tự động hóa hoàn toàn** cho việc quản lý nội dung, giúp các sếp:
✅ **Tiết kiệm thời gian** (không cần làm thủ công hàng tháng).
✅ **Tối ưu hóa SEO** (bài viết cũ không còn xuất hiện).
✅ **Giảm tải cho server** (trang web nhanh hơn).
✅ **Lưu trữ an toàn** (bài viết vẫn được bảo quản).

**Hành động ngay!**
1. **Cài đặt n8n Self-hosted** trên VPS (để workflow chạy 24/7).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và để hệ thống làm việc cho bạn!

**Cần hỗ trợ chuyên sâu?**
- Liên hệ **David Olusola** (tác giả workflow) qua email: [david@daexai.com](mailto:david@daexai.com) để có **hỗ trợ tối ưu hóa workflow** hoặc **học cách tự xây dựng workflow tự động hóa khác**.
- Đăng ký **VPS n8n** với mã giảm giá **VPSN8N** để chạy workflow ổn định!

---