```yaml
---
title: "🚀 Tự động phân loại Issues GitHub với AI Gemini, gắn nhãn và cảnh báo Slack"
description: "Hướng dẫn tự động hóa phân loại issues GitHub bằng AI Gemini, gắn nhãn tự động và gửi cảnh báo Slack - tiết kiệm 80% thời gian xử lý issues"
slug: "tu-dong-phan-loai-issues-github-voi-ai-gemini"
tags: [n8n, automation, no-code, github, slack]
keywords: [n8n workflow, tự động hóa, github issues, ai gemini, slack alerts]
---

# 🚀 Tự động phân loại Issues GitHub với AI Gemini, gắn nhãn và cảnh báo Slack

[Các sếp đang gặp khó khăn khi phải xử lý hàng trăm issues trên GitHub mỗi ngày. Phân loại thủ công, gắn nhãn và thông báo đến đúng người là một công việc tốn thời gian và dễ gây lỗi. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này chỉ trong vài bước đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm **80% thời gian** xử lý issues GitHub
- Phân loại chính xác hơn nhờ AI Gemini
- Gắn nhãn tự động cho issues
- Cảnh báo ngay đến Slack channel phù hợp
- Hoạt động liên tục 24/7 không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với API key cho Google Gemini
- Tài khoản Slack với quyền gửi tin nhắn
- Tài khoản GitHub với quyền truy cập vào repository cần xử lý
- Google Sheet để lưu trữ nhật ký hoạt động (tùy chọn)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13874](https://n8n.io/workflows/13874)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Webhook**: Cấu hình webhook URL để nhận events từ GitHub
   - Truy cập repository GitHub của bạn
   - Vào Settings > Webhooks > Add webhook
   - Điền URL của webhook node trong n8n (vd: `https://your-n8n-instance.com/webhook/your-webhook-id`)
   - Chọn Content type: `application/json`
   - Chọn các events cần theo dõi (thường là "Issues")

2. **Node HTTP Request (Google Gemini)**: Cấu hình API key
   - Tạo credentials mới trong n8n cho Google Gemini
   - Điền API key của bạn vào credentials này
   - Trong node HTTP Request, chọn credentials vừa tạo

3. **Node Slack**: Cấu hình thông tin Slack
   - Tạo credentials mới trong n8n cho Slack
   - Điền thông tin token Slack vào credentials này
   - Trong node Slack, chọn credentials vừa tạo và cấu hình channel cần gửi thông báo

4. **Node Google Sheets** (tùy chọn): Cấu hình Google Sheet
   - Tạo credentials mới trong n8n cho Google Sheets
   - Điền thông tin xác thực Google vào credentials này
   - Trong node Google Sheets, chọn credentials vừa tạo và cấu hình ID của Google Sheet cần lưu trữ

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Workflow" để test với dữ liệu mẫu
2. Kiểm tra các node để đảm bảo dữ liệu được xử lý đúng
3. Khi đã ổn định, click vào nút "Activate" để bật workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh prompt cho AI**: Chỉnh sửa prompt trong node HTTP Request để phù hợp với nhu cầu của dự án
2. **Thêm nhiều channel Slack**: Sao chép node Slack và cấu hình cho các channel khác nhau
3. **Tích hợp với các công cụ khác**: Kết nối với các công cụ như Jira, Trello để tạo ticket tự động
4. **Cấu hình email thông báo**: Thêm node gửi email để nhận thông báo ngoài Slack

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình xử lý issues GitHub, từ phân loại đến thông báo. Với AI Gemini, các sếp có thể phân loại issues chính xác hơn và tiết kiệm đáng kể thời gian. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của team! 🚀
```