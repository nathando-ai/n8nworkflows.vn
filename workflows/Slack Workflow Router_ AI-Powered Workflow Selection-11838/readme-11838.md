---
title: "🚀 Slack Workflow Router: Tự động hóa AI chọn Workflow từ Slack"
description: "Giải pháp tự động hóa 100% không cần code giúp các sếp quản lý nhiều workflow n8n từ 1 Slack app duy nhất, tiết kiệm thời gian và tối ưu quy trình làm việc."
slug: "slack-workflow-router-ai-powered"
tags: [n8n, automation, no-code, slack, ai]
keywords: [n8n workflow, tự động hóa, slack integration, ai workflow selection]
---

# 🚀 Slack Workflow Router: Tự động hóa AI chọn Workflow từ Slack

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Quản lý nhiều workflow từ 1 Slack app duy nhất
- Tối ưu quy trình: AI tự động chọn workflow phù hợp
- Tăng hiệu quả: Tự động hóa hoàn toàn quy trình
- Dễ bảo trì: Quản lý workflow tập trung trong data table
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Slack với quyền tạo app
- Tài khoản OpenAI API (API key)
- n8n đã được cài đặt và cấu hình
- 3-5 workflow n8n đã sẵn sàng để được gọi
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/11838)
2. Click nút "Download" để tải file JSON
3. Trong n8n Editor, click "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Slack Trigger"**:
   - Cấu hình credentials cho Slack API
   - Đảm bảo app Slack có quyền nhận mention

2. **Node "OpenAI Chat Model"**:
   - Thêm credentials OpenAI API
   - Chọn model phù hợp (gợi ý: gpt-4.1-mini)

3. **Node "Get the list of workflows"**:
   - Tạo data table với 3 cột:
     - workflow_id: ID của workflow (ví dụ: "sDF6oLXgxAD7O3wP/1a28ad")
     - workflow_name: Tên workflow
     - workflow_description: Mô tả chi tiết về workflow

4. **Node "Execute Workflow"**:
   - Đảm bảo workflow được gọi có trạng thái "Active"

#### 3. Kích hoạt ⚡️
1. Test workflow với tin nhắn mẫu trong Slack
2. Kiểm tra kết quả trong data table
3. Bật Active workflow khi đã kiểm tra thành công

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node "Slack" để gửi thông báo khi workflow được thực thi
- Kết hợp với node "Email" để gửi báo cáo định kỳ
- Tích hợp với node "Google Sheets" để lưu log các workflow được thực thi
- Sử dụng node "Delay" để tránh bị giới hạn API của Slack

### 📌 Kết luận
Workflow Slack Workflow Router giúp các sếp quản lý và kích hoạt nhiều workflow n8n từ 1 Slack app duy nhất, tiết kiệm thời gian và tối ưu quy trình làm việc. Với khả năng AI tự động chọn workflow phù hợp, giải pháp này không chỉ tiết kiệm thời gian mà còn giảm thiểu lỗi do con người gây ra. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của đội ngũ!