---
title: "🚀 Tự động lưu trữ phiên bản workflow n8n trong GitLab với phân loại khách hàng"
description: "Hướng dẫn chi tiết cách tự động sao lưu workflow n8n vào GitLab với phân loại khách hàng, đảm bảo quản lý phiên bản và tổ chức hiệu quả."
slug: "tu-dong-luu-tru-phien-ban-workflow-n8n-trong-gitlab"
tags: [n8n, automation, no-code, devops, gitlab]
keywords: [n8n workflow, tự động hóa, lưu trữ phiên bản, gitlab, devops]
---

# 🚀 Tự động lưu trữ phiên bản workflow n8n trong GitLab với phân loại khách hàng

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý nhiều workflow n8n và cần lưu trữ phiên bản một cách hiệu quả. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code để sao lưu workflow vào GitLab với phân loại khách hàng.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động sao lưu workflow n8n vào GitLab với phân loại khách hàng
- Quản lý phiên bản hiệu quả cho các workflow quan trọng
- Tiết kiệm thời gian và giảm lỗi trong quá trình quản lý workflow
- Hoạt động liên tục 24/7 với lịch trình tự động
- Tạo lịch sử thay đổi rõ ràng cho từng workflow
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n với quyền truy cập API
- Tài khoản GitLab với quyền truy cập API
- Các workflow cần sao lưu đã được gắn tag `backup-workflows`
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **When clicking ‘Execute workflow’** (manualTrigger):
   - Không cần cấu hình gì thêm

2. **Schedule Trigger** (scheduleTrigger):
   - Cấu hình lịch trình sao lưu (ví dụ: `0 3 * * *` để chạy mỗi ngày lúc 3:00 sáng)

3. **Prepare Workflow JSON for UI-Compatible Export** (code):
   - Không cần cấu hình gì thêm

4. **Clean & Normalize Workflow Name** (code):
   - Không cần cấu hình gì thêm

5. **Fetch Workflows from n8n** (n8n):
   - Cấu hình credentials `n8nApi`
   - Đảm bảo các workflow cần sao lưu đã được gắn tag `backup-workflows`

6. **Fetch Existing File from GitLab** (gitlab):
   - Cấu hình credentials `gitlabApi`
   - Đảm bảo có quyền truy cập vào repository GitLab

7. **Update Existing File in GitLab** (gitlab):
   - Cấu hình credentials `gitlabApi`
   - Đảm bảo có quyền truy cập vào repository GitLab

8. **Create New File in GitLab** (gitlab):
   - Cấu hình credentials `gitlabApi`
   - Đảm bảo có quyền truy cập vào repository GitLab

9. **Normalize Backup Output** (set):
   - Không cần cấu hình gì thêm

10. **Set Global GitLab Variables** (set):
    - Cấu hình các biến toàn cục:
      - `gitlab_owner`: Chủ sở hữu repository GitLab
      - `gitlab_project`: Tên project GitLab
      - `gitlab_root_path`: Đường dẫn gốc trong repository (ví dụ: `workflow_definitions/`)
      - `tag_filter`: Tag để lọc workflow (ví dụ: `backup-workflows`)

11. **Prepare GitLab File Path** (code):
    - Không cần cấu hình gì thêm

12. **Compare Workflow with GitLab Version** (if):
    - Không cần cấu hình gì thêm

13. **Mark as Created** (set):
    - Không cần cấu hình gì thêm

14. **Mark as Updated** (set):
    - Không cần cấu hình gì thêm

15. **Mark as Unchanged** (set):
    - Không cần cấu hình gì thêm

16. **Summarize Backup Results** (code):
    - Không cần cấu hình gì thêm

17. **Merge** (merge):
    - Không cần cấu hình gì thêm

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi báo cáo kết quả qua Slack/Telegram sau khi hoàn thành sao lưu
- Tạo lịch trình sao lưu hàng tuần/tháng để lưu trữ lịch sử lâu dài
- Kết hợp với workflow khác để tự động hóa việc khôi phục workflow từ GitLab
- Thêm node để tạo file index cho các workflow đã sao lưu
- Tích hợp với hệ thống giám sát để theo dõi quá trình sao lưu

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động sao lưu và quản lý phiên bản workflow n8n trong GitLab với phân loại khách hàng. Bằng cách sử dụng workflow này, các sếp có thể tiết kiệm thời gian, giảm lỗi và đảm bảo tính nhất quán của các workflow quan trọng trong doanh nghiệp.