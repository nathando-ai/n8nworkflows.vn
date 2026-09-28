---
title: "🚀 Tự động sao lưu GitLab các workflow n8n theo username"
description: "Giải pháp sao lưu toàn bộ workflow n8n lên GitLab, tổ chức theo tên người dùng, chạy tự động hàng tuần hoặc kích hoạt thủ công, không cần viết code."
slug: "tu-dong-sao-luu-gitlab-workflow-n8n-theo-username"
tags: [n8n, automation, no-code, devops, backup, gitlab]
keywords: [n8n workflow, tự động sao lưu, gitlab backup, devops, backup workflow]
---

# 🚀 Tự động sao lưu GitLab các workflow n8n theo username

Trong môi trường DevOps, việc **sao lưu các workflow n8n** thường bị bỏ qua vì chúng được tạo và chỉnh sửa trực tiếp trên giao diện. Khi một thành viên rời đi, hoặc có lỗi hệ thống, các workflow quan trọng có thể mất vĩnh viễn. Việc sao lưu thủ công từng file JSON, đặt tên theo dự án, rồi đẩy lên GitLab là công việc tốn thời gian và dễ sai sót.

**Workflow “Automated GitLab Backup of Workflows with Username Organization”** giải quyết vấn đề này 100 % tự động:  
- **Kích hoạt** bằng nút **Manual Trigger** hoặc lịch **Weekly Schedule**.  
- **Lấy danh sách** tất cả workflow hiện có từ n8n API.  
- **Định dạng**, kiểm tra tồn tại file trên GitLab, **tạo** hoặc **cập nhật** theo tên người dùng.  
- **Ghi log** chi tiết và **gửi email** báo cáo thành công.  

Kết quả: mọi workflow luôn được lưu trữ an toàn trên GitLab, có thể khôi phục nhanh chóng, đồng thời tạo “audit trail” cho từng người dùng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: không còn phải sao lưu thủ công từng workflow.  
- **Đảm bảo độ chính xác**: file được tạo/được cập nhật tự động, không rủi ro lỗi con người.  
- **Phân quyền rõ ràng**: mỗi file được đặt tên `<username>_<workflow-id>.json`, dễ truy vết.  
- **Hoạt động liên tục**: chạy hàng tuần hoặc khi cần, luôn có bản sao mới nhất.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** với **API Key** (credential `n8nApi`).  
- **Tài khoản GitLab** có quyền **write** vào repository đích (credential `gitlabApi`).  
- **SMTP server** để gửi email báo cáo (credential `smtp`).  
- Repository GitLab đã tạo sẵn (ví dụ: `gitlab.com/your-org/n8n-backup`).  
- (Tùy chọn) Địa chỉ email nhận báo cáo.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Đăng nhập vào n8n Dashboard.  
2. Chọn **Import** → **Upload JSON** và tải file `Automated_GitLab_Backup.json` (hoặc copy toàn bộ JSON vào ô **Paste JSON**).  
3. Nhấn **Import** → Workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Hành động cần cấu hình | Ghi chú |
|------|-----------------------|---------|
| **Manual Backup Trigger** | Không cần cấu hình, dùng để khởi chạy thủ công. | |
| **Scheduled Weekly Backup** | Chọn **Cron**: `0 0 * * 0` (đầu tuần lúc 00:00). | Đảm bảo timezone đúng với môi trường. |
| **Fetch N8N Workflows** (`n8n`) | Credential: **n8nApi**. <br>Operation: **Get All**. | Lấy danh sách workflow hiện có. |
| **Prepare Backup Metadata** (`set`) | Thêm trường `backupDate = {{$now}}`, `username = {{$json["owner"]["username"]}}`. | Định dạng metadata cho file. |
| **Process Each Workflow** (`splitInBatches`) | Batch size: **1** (xử lý từng workflow một). | Đảm bảo không vượt limit API. |
| **Format Workflow for GitLab** (`set`) | Tạo trường `filePath = /backups/{{ $json["username"] }}/{{ $json["id"] }}.json` và `fileContent = {{$json}}` (JSON string). | Đường dẫn sẽ tạo thư mục theo username. |
| **Rate Limit Control** (`wait`) | Wait time: **2 seconds**. | Giảm nguy cơ hitting GitLab rate limit. |
| **Check Backup Status** (`if`) | Condition: **File exists?** → `resource: file`, `operation: get`, `path: {{$json["filePath"]}}`. | Nếu tồn tại → **Update**, else → **Create**. |
| **Log Backup Results** (`set`) | Thêm trường `status = {{$node["Check Backup Status"].json["exists"] ? "updated" : "created"}}`. | Dùng để báo cáo email. |
| **Update Backup Summary** (`gitlab` – edit) | Credential: **gitlabApi**. <br>Repository: **your‑repo**. <br>File path: `{{$json["filePath"]}}`. <br>Content: `{{$json["fileContent"]}}`. | Cập nhật file đã tồn tại. |
| **Create to GitLab Repository** (`gitlab` – create) | Credential: **gitlabApi**. <br>Repository: **your‑repo**. <br>File path: `{{$json["filePath"]}}`. <br>Content: `{{$json["fileContent"]}}`. | Tạo file mới nếu chưa tồn tại. |
| **Send email** (`emailSend`) | Credential: **smtp**. <br>To: **{{ $json["reportEmail"] }}**. <br>Subject: **“[Backup] Kết quả sao lưu workflow n8n – {{ $now }}”**. <br>Body: **Báo cáo chi tiết (status, filePath, thời gian)**. | Đảm bảo SMTP cho phép gửi HTML. |

> **Lưu ý quan trọng**:  
> - Kiểm tra **permissions** của token GitLab (`api` scope) để có thể `create` và `edit` file.  
> - Nếu repository có **branch protection**, hãy dùng branch `main` hoặc tạo một branch riêng cho backup (`backup`).  
> - Đối với môi trường có **proxy**, cấu hình proxy trong n8n Settings.

#### 3. Kích hoạt ⚡️
1. **Test chạy**: Nhấn nút **Execute Workflow** trên node **Manual Backup Trigger** và kiểm tra log từng bước.  
2. Kiểm tra repository GitLab: các file `username_workflowId.json` đã xuất hiện/được cập nhật.  
3. Khi mọi thứ ổn, bật **Active** (toggle ở góc phải) để cho phép **Scheduled Weekly Backup** tự động chạy.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` sau node `Send email` để nhận thông báo nhanh trên kênh nhóm.  
- **Lưu log vào Database**: Dùng node `Postgres` hoặc `MongoDB` để lưu lịch sử backup, hỗ trợ dashboard thống kê.  
- **Nén file**: Trước khi đẩy lên GitLab, dùng node `Function` để gzip nội dung, giảm dung lượng lưu trữ.  
- **Backup đa repo**: Thêm một `Switch` dựa trên `username` để lưu vào các repository riêng cho từng team.  

### 📌 Kết luận
Với workflow này, các sếp có thể **yên tâm** rằng mọi workflow n8n luôn được sao lưu an toàn, được tổ chức rõ ràng theo người dùng và được thông báo ngay khi có thay đổi. Hãy **import**, **cấu hình credential**, **test** và **bật Active** ngay hôm nay để không còn lo lắng về mất mát dữ liệu quan trọng! 🚀