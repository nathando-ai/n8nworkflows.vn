---
title: "🚀 Tự Động Backup n8n Workflows Lên GitLab Mỗi Ngày"
description: "Giải pháp DevOps tự động hóa 100% việc sao lưu toàn bộ workflows n8n lên GitLab, phát hiện thay đổi và cập nhật mã nguồn một cách thông minh, không cần code."
slug: "tu-dong-backup-n8n-workflows-len-gitlab"
tags: [n8n, automation, devops, gitlab, backup, version-control]
keywords: [n8n workflow backup, gitlab automation, devops n8n, sao lưu workflow, version control n8n]
---

# 🚀 Tự Động Backup n8n Workflows Lên GitLab Mỗi Ngày

Trong môi trường DevOps hiện đại, việc quản lý cấu hình (Configuration as Code) là yếu tố sống còn. Tuy nhiên, nhiều doanh nghiệp vẫn đang vận hành n8n một cách "thủ công": tạo workflow, chạy, và quên mất việc sao lưu. Rủi ro là gì? Một cú click nhầm, một lỗi cập nhật phần mềm, hoặc đơn giản là quên backup có thể khiến bạn mất hàng tuần công sức xây dựng các quy trình tự động hóa phức tạp.

Workflow **"Automated Daily Backup of n8n Workflows to GitLab Repositories"** do *Akhil Varma Gadiraju* phát triển chính là giải pháp "cứu tinh" cho vấn đề này. Nó hoạt động như một người gác cổng thầm lặng, tự động quét toàn bộ workflows trong instance n8n của bạn, so sánh với phiên bản cũ trên GitLab, và chỉ thực hiện commit khi có thay đổi thực sự. Kết quả? Bạn có một kho lưu trữ mã nguồn (source of truth) hoàn chỉnh, có lịch sử version rõ ràng, và khả năng khôi phục (rollback) tức thì khi có sự cố.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này chạy ổn định 24/7 và đảm bảo tính liên tục của dữ liệu, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **An toàn dữ liệu tuyệt đối:** Mọi workflow đều được sao lưu định kỳ, loại bỏ rủi ro mất dữ liệu do lỗi hệ thống hoặc thao tác sai.
- **Quản lý phiên bản (Version Control):** Tận dụng sức mạnh của GitLab để xem lịch sử thay đổi, ai đã sửa gì, và khi nào.
- **Tối ưu hóa lưu trữ:** Workflow thông minh chỉ ghi đè (commit) khi có thay đổi thực sự, tránh việc spam commit rỗng làm loãng lịch sử.
- **Tự động hóa 100%:** Không cần can thiệp thủ công, hệ thống tự chạy theo lịch (Schedule Trigger), phù hợp cho môi trường sản xuất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1.  **Tài khoản GitLab:** Một repository (có thể là Private) để lưu trữ các file JSON của workflows.
2.  **Personal Access Token (PAT) cho GitLab:** Quyền `api` hoặc `read_repository` và `write_repository` để đọc/ghi file.
3.  **N8n API Key:** Token để workflow truy cập vào chính instance n8n của bạn nhằm liệt kê và đọc nội dung các workflows.
4.  **Instance n8n:** Đã được cài đặt và chạy (khuyến nghị Self-hosted).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1.  Tải file JSON của workflow từ link gốc: [n8n.io/workflows/4035](https://n8n.io/workflows/4035).
2.  Mở n8n Editor của bạn.
3.  Chọn **Import from File** hoặc **Import from URL** và chọn file vừa tải.
4.  Workflow sẽ xuất hiện với đầy đủ 19 nodes, bao gồm các node GitLab, Code, và Logic xử lý.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần cấu hình credentials và tham số cho các node sau:

*   **Node `GitLab` (và các node GitLab khác):**
    *   Chọn **Credentials**: Tạo mới hoặc chọn credentials GitLab đã có.
    *   **Project ID:** Điền ID của repository GitLab nơi bạn muốn lưu backup.
    *   *Lưu ý:* Các node `Get file`, `Create file`, `New file version` đều dùng chung credentials này.

*   **Node `Retrieve all workflows`:**
    *   Chọn **Credentials**: Chọn credentials N8n API (thường là `n8nApi`).
    *   Đảm bảo API Key có quyền đọc (read) danh sách workflows.

*   **Node `Globals` (Set Node):**
    *   Kiểm tra các biến toàn cục. Thường các sếp có thể cần chỉnh sửa đường dẫn thư mục (folder path) trong repository GitLab nếu muốn lưu backup vào một thư mục con cụ thể (ví dụ: `/backups/n8n/`).

*   **Node `File status` (Code Node):**
    *   Node này chứa logic so sánh nội dung JSON. Các sếp không cần sửa code trừ khi muốn thay đổi logic so sánh (ví dụ: bỏ qua các trường `id` hoặc `active` khi so sánh để tránh commit thừa).

*   **Node `Schedule Trigger`:**
    *   Mặc định có thể là chạy hàng ngày. Các sếp có thể chỉnh lại tần suất (ví dụ: mỗi 6 giờ, hoặc hàng giờ) tùy theo mức độ thay đổi workflows trong team.

*   **Node `Switch`:**
    *   Node này phân luồng dựa trên kết quả so sánh:
        *   **File exists & Same:** Bỏ qua.
        *   **File exists & Different:** Cập nhật file (`New file version`).
        *   **File not exists:** Tạo file mới (`Create file`).
    *   Đảm bảo các điều kiện trong node này khớp với logic mong muốn.

#### 3. Kích hoạt ⚡️
1.  **Test Run:**
    *   Nhấn nút **Execute Workflow** (hoặc chọn một workflow mẫu và chạy).
    *   Kiểm tra output của node `Result` (NoOp) để xem trạng thái: File được tạo mới, cập nhật, hay không thay đổi.
    *   Vào GitLab repository, kiểm tra xem file JSON có được tạo/commit đúng không.
2.  **Bật Active:**
    *   Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải n8n.
    *   Workflow sẽ tự động chạy theo lịch đã thiết lập trong `Schedule Trigger`.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node **Slack** hoặc **Telegram** sau node `Result` để gửi thông báo khi có backup thất bại hoặc khi có thay đổi lớn.
- **Backup theo nhóm:** Sử dụng node `Switch` hoặc `Filter` để chỉ backup các workflows có tag cụ thể (ví dụ: `production`, `critical`), giúp tách biệt môi trường dev và prod.
- **Kiểm tra sức khỏe (Health Check):** Thêm một node HTTP Request để ping một endpoint bên ngoài nếu backup thất bại, giúp phát hiện sự cố sớm.
- **Lưu trữ dài hạn:** Kết hợp với **S3** hoặc **Google Drive** để lưu trữ các snapshot hàng tháng, bên cạnh backup hàng ngày trên GitLab.

### 📌 Kết luận
Việc tự động hóa backup n8n workflows lên GitLab không chỉ là một "nice-to-have" mà là **bắt buộc** cho bất kỳ hệ thống tự động hóa nghiêm túc nào. Với workflow này, các sếp có thể yên tâm phát triển, thử nghiệm và thay đổi workflows mà không lo lắng về việc mất dữ liệu. Hãy import, cấu hình và bật Active ngay hôm nay để bảo vệ tài sản số của doanh nghiệp!