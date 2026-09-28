---
title: "🚀 Tự Động Backup Code Injection Squarespace Lên GitHub"
description: "Giải pháp tự động hóa 100% để sao lưu code Header/Footer Injection của Squarespace lên GitHub, đảm bảo an toàn dữ liệu và dễ dàng khôi phục khi cần."
slug: "backup-squarespace-injection-github"
tags: [n8n, automation, no-code, squarespace, github, backup]
keywords: [n8n workflow, tự động hóa backup, squarespace injection, github api, no-code]
---

# 🚀 Tự Động Backup Code Injection Squarespace Lên GitHub

Các sếp đang vận hành website trên Squarespace chắc hẳn đều hiểu nỗi đau khi phải chèn các đoạn code (Header/Footer Injection) cho mục đích phân tích, tracking hoặc tùy chỉnh giao diện. Vấn đề là gì? Code nằm trong CMS, nếu không cẩn thận bị xóa nhầm, hoặc khi migrate website, việc tìm lại chính xác từng dòng code đã chèn trước đó là cực kỳ khó khăn và dễ gây lỗi.

Workflow này chính là "người gác cổng" tự động, giúp các sếp **sao lưu (backup) toàn bộ code Injection của Header và Footer** từ Squarespace lên một repository GitHub riêng biệt. Không cần code, không cần lo lắng, cứ để n8n lo!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **An toàn tuyệt đối:** Code Injection được lưu trữ an toàn trên GitHub, tránh mất dữ liệu do lỗi CMS hoặc thao tác nhầm.
- **Lịch sử thay đổi (Version Control):** Mỗi lần backup, GitHub sẽ ghi lại lịch sử, giúp các sếp xem được code đã thay đổi như thế nào theo thời gian.
- **Tự động hóa hoàn toàn:** Chạy theo lịch (Schedule) hoặc thủ công, không tốn công sức sao chép thủ công.
- **Tổ chức rõ ràng:** Code được tách riêng theo từng trang (Header/Footer) và lưu trong các thư mục con riêng biệt trong repo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã cài đặt và chạy n8n (Cloud hoặc Self-hosted).
- **Tài khoản GitHub:** Có quyền tạo repository hoặc truy cập vào repository hiện có.
- **GitHub Personal Access Token (PAT):** Để n8n có quyền ghi (write) vào repository.
- **URL Website Squarespace:** Địa chỉ website cần backup (ví dụ: `https://yourwebsite.com`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from File** hoặc **Import from URL**.
3. Tải file JSON của workflow này và import vào.
4. Workflow sẽ hiển thị với các node được sắp xếp sẵn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Các sếp cần cấu hình 3 node chính sau:

**1. Node `Get Squarespace data` (HTTP Request)**
- Đây là node lấy dữ liệu từ website Squarespace.
- **Cần chỉnh:** Trong phần **URL**, thay thế bằng địa chỉ website Squarespace của các sếp.
  - Ví dụ: `https://your-website.com`
  - Lưu ý: Workflow sẽ tự động thêm các endpoint cần thiết để lấy code Injection.

**2. Node `Globals` (Set Node)**
- Node này chứa các biến toàn cục để định hướng dữ liệu lưu vào đâu trên GitHub.
- **Cần chỉnh các giá trị sau:**
  - `repo.owner`: Tên user GitHub của các sếp (ví dụ: `john-doe`).
  - `repo.name`: Tên repository trên GitHub (ví dụ: `n8n-backups`).
  - `repo.path`: Thư mục con trong repository để lưu file backup (ví dụ: `squarespace-backup/`).
- **Ví dụ cấu hình:**
  ```json
  {
    "repo": {
      "owner": "john-doe",
      "name": "n8n-backups",
      "path": "squarespace-backup/"
    }
  }
  ```

**3. Node `Edit Injection data` & `Create Injection data` (GitHub Nodes)**
- Hai node này chịu trách nhiệm ghi file lên GitHub.
- **Cần chỉnh:** Chọn **Credentials** (GitHub API) mà các sếp đã tạo.
  - Đảm bảo PAT (Personal Access Token) có quyền `repo` (full control) hoặc ít nhất là `contents:write`.
- **Logic hoạt động:**
  - Workflow sẽ kiểm tra xem file đã tồn tại chưa.
  - Nếu **có**: Node `Edit Injection data` sẽ cập nhật nội dung file.
  - Nếu **không**: Node `Create Injection data` sẽ tạo file mới.

**4. Node `Schedule Trigger` (Tùy chọn)**
- Mặc định workflow có cả `Manual Trigger` và `Schedule Trigger`.
- Nếu muốn backup tự động hàng ngày, các sếp chỉnh `Schedule Trigger` (ví dụ: mỗi 24 giờ).
- Nếu chỉ muốn backup khi cần, các sếp có thể tắt `Schedule Trigger` và dùng `Manual Trigger` (nút "Execute Workflow").

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Nhấn nút **Execute Workflow** (hoặc dùng Manual Trigger).
   - Kiểm tra xem các node có chạy thành công không (màu xanh lá cây).
   - Vào GitHub, kiểm tra xem file `header-injection.html` và `footer-injection.html` đã được tạo/cập nhật trong thư mục `squarespace-backup/` chưa.
2. **Bật Active:**
   - Nếu test thành công, nhấn nút **Active** ở góc trên bên phải để workflow chạy tự động theo lịch.

### ✍️ Mẹo & gợi ý nâng cao
- **Backup nhiều website:** Các sếp có thể nhân bản workflow này cho từng website Squarespace khác nhau, chỉ cần thay đổi URL trong node `Get Squarespace data` và `repo.path` để phân biệt thư mục lưu trữ.
- **Gửi thông báo qua Slack/Telegram:** Thêm node `Slack` hoặc `Telegram` sau node GitHub để nhận thông báo khi backup thành công hoặc thất bại.
- **Kiểm tra sự khác biệt (Diff):** Sử dụng GitHub Actions hoặc các công cụ khác để so sánh (diff) code Injection giữa các lần backup, giúp phát hiện thay đổi không mong muốn.
- **Lưu trữ dài hạn:** Nếu muốn lưu trữ lâu dài, các sếp có thể thêm node để đẩy dữ liệu lên S3 hoặc Google Drive bên cạnh GitHub.

### 📌 Kết luận
Workflow này là một công cụ đơn giản nhưng cực kỳ hữu ích cho bất kỳ ai đang sử dụng Squarespace và có code Injection. Việc tự động hóa backup giúp các sếp yên tâm hơn trong quá trình vận hành website, tránh được rủi ro mất dữ liệu và tiết kiệm thời gian đáng kể. Hãy import và cấu hình ngay hôm nay để bảo vệ "tài sản" code của mình!