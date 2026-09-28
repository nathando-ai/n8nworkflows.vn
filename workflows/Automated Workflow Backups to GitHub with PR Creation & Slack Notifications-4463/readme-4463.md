---
title: "🚀 Backups Workflow n8n tới GitHub với PR & Slack"
description: "Tự động sao lưu các workflow n8n vào kho GitHub, tạo Pull Request và gửi thông báo qua Slack – giải pháp DevOps 100% không cần code."
slug: "backups-workflow-n8n-github-pr-slack"
tags: [n8n, automation, no-code, devops, github, slack]
keywords: [n8n workflow, tự động hóa, backup n8n, GitHub PR, Slack notifications]
---

# 🚀 Backups Workflow n8n tới GitHub với PR & Slack

Bạn đang quản lý nhiều workflow n8n và lo lắng về mất dữ liệu khi cập nhật, hoặc muốn lưu trữ lịch sử thay đổi một cách có cấu trúc? Workflow này sẽ tự động **sao lưu** toàn bộ các workflow của bạn vào một kho GitHub, **tạo Pull Request** khi có thay đổi và gửi **thông báo Slack** ngay lập tức. Không cần viết code, chỉ cần cấu hình một vài credentials và chạy.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải sao lưu thủ công, workflow tự động chạy theo lịch hoặc trigger.  
- **Chính xác & an toàn**: Mọi thay đổi được lưu vào GitHub, có thể rollback hoặc xem lịch sử commit.  
- **Cá nhân hóa**: Tùy chỉnh thư mục, tên branch, thông báo Slack theo nhu cầu.  
- **Hoạt động liên tục**: Khi có thay đổi bất kỳ workflow nào, PR được tạo ngay, sếp chỉ cần review và merge.  
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **GitHub API credentials**: Personal Access Token với quyền `repo` (đọc/ghi).  
- **Slack Bot token**: Nếu muốn nhận thông báo PR.  
- **Repository details**: `github_owner`, `repo_name`, `workflow_dir` trong node **Define Local Variables**.  
- **n8n API key**: Để gọi API n8n trong node `n8n`.  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON từ link gốc: <https://n8n.io/workflows/4463>.  
2. Mở n8n Editor → **Import** → **Upload JSON** hoặc copy toàn bộ JSON vào ô **Import JSON**.  
3. Nhấn **Import** và workflow sẽ xuất hiện trong danh sách.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Tham số cần cấu hình |
|------|-------|----------------------|
| `n8n` | Gọi API n8n để lấy danh sách workflow. | `n8nApi` credentials |
| `Define Local Variables` | Định nghĩa biến `github_owner`, `repo_name`, `workflow_dir`, `branch_prefix`. | Thêm giá trị phù hợp với kho GitHub của bạn |
| `Get all workflows on GitHub` | Lấy danh sách file trong thư mục workflow. | `githubApi` credentials |
| `Get content for each workflow` | Lấy nội dung file. | `githubApi` credentials |
| `Base64decode workflow content` | Giải mã nội dung Base64. | Không cần cấu hình |
| `Create new branch via GitHub API` | Tạo branch mới. | `githubApi` credentials |
| `Get latest commit SHA on main` | Lấy SHA commit mới nhất. | `githubApi` credentials |
| `Create new commit to add new workflow` | Thêm file mới. | `githubApi` credentials |
| `Create new commit to update changed workflow` | Sửa file đã tồn tại. | `githubApi` credentials |
| `Create new PR via GitHub API` | Tạo PR. | `githubApi` credentials |
| `Slack` | Gửi thông báo. | `slackApi` credentials |
| `Click me to trigger` | Trigger thủ công. | Không cần cấu hình |

> **Lưu ý**: Các node `merge`, `filter`, `if`, `noOp` chỉ điều khiển luồng logic, không cần chỉnh thêm.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow thủ công bằng nút **Execute Workflow**. Kiểm tra log xem có lỗi không.  
2. **Bật Active**: Bật toggle **Active** ở góc trên bên phải. Workflow sẽ chạy tự động khi trigger (manual hoặc theo lịch nếu bạn thêm node `cron`).

## ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack/Telegram**: Thêm node `Telegram` để nhận thông báo cùng lúc.  
- **Lưu log vào Google Sheets**: Dùng node `Google Sheets` để ghi lại lịch sử PR, thời gian, trạng thái.  
- **Tự động merge PR**: Thêm node `GitHub` với operation `merge` sau khi PR được review.  
- **Sử dụng webhook**: Thay vì trigger thủ công, dùng webhook để tự động kích hoạt khi có thay đổi trong kho n8n.

## 📌 Kết luận
Workflow này giúp các sếp **đảm bảo an toàn dữ liệu** cho các workflow n8n, **giảm thiểu rủi ro** và **tăng tính minh bạch** trong quy trình DevOps. Hãy thử ngay, cấu hình nhanh, chạy liên tục và cảm nhận sự khác biệt!