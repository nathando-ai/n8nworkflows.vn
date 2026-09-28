---
title: "🚨 Tự động phân loại sự cố và thực thi SLA với Gemini, Groq, Google Sheets và Slack"
description: "Hướng dẫn chi tiết cách tự động phân loại sự cố, phân tích bằng AI và thực thi SLA với n8n, Gemini và Google Sheets. Tiết kiệm thời gian và nâng cao hiệu quả xử lý sự cố."
slug: "tu-dong-phan-loai-su-co-voi-gemini-groq-google-sheets-slack"
tags: [n8n, automation, no-code, AI, incident management]
keywords: [n8n workflow, tự động hóa sự cố, AI phân loại sự cố, SLA tự động, quản lý sự cố]
---

# 🚨 Tự động phân loại sự cố và thực thi SLA với Gemini, Groq, Google Sheets và Slack

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi xử lý sự cố IT thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động phân loại sự cố với độ chính xác cao (95%+)
- Thực thi SLA tự động (15 phút cho P1, 60 phút cho P2)
- Tạo kênh War Room tự động cho sự cố cấp bách
- Tự động escalate khi không có phản hồi
- Theo dõi toàn bộ quá trình xử lý sự cố trong Google Sheets
- Tiết kiệm 80% thời gian xử lý sự cố thủ công
- Giảm thời gian phản hồi trung bình từ 2 giờ xuống còn 15 phút
- Tạo audit trail hoàn chỉnh cho các quy trình xử lý sự cố
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (cho Google Sheets)
- Tài khoản Slack (cho thông báo và kênh War Room)
- API Key cho Google Gemini và Groq
- Google Sheet với 3 tab: Runbooks, Incidents và AI_Audit_Log
- Tài khoản n8n (self-hosted hoặc cloud)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/14237](https://n8n.io/workflows/14237)
2. Nhấn nút "Import" trên trang workflow
3. Trong n8n Editor, chọn "Import from URL" và dán link workflow
4. Hoàn tất import và mở workflow trong Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Google Sheets Nodes** (5 nodes):
   - Tạo 3 tab trong Google Sheet: Runbooks, Incidents, AI_Audit_Log
   - Thêm credentials Google Sheets OAuth2 vào tất cả các node Google Sheets
   - Cấu hình tham số:
     - Sheet ID: ID của Google Sheet bạn tạo
     - Sheet Name: Tên tab tương ứng (Runbooks, Incidents, AI_Audit_Log)
     - Range: Để trống để sử dụng toàn bộ tab

2. **Slack Nodes** (6 nodes):
   - Thêm credentials Slack OAuth2
   - Cập nhật tên kênh Slack:
     - #incidents-critical (cho sự cố P1)
     - #incidents (cho sự cố P2)
     - #management-escalation (cho escalation)
     - #engineering-leads (cho sự cố P2)

3. **LLM Nodes** (4 nodes):
   - Thêm credentials cho Google Gemini vào 2 node Gemini LLM
   - Thêm credentials cho Groq vào 2 node Groq LLM
   - Có thể thay thế bằng OpenAI/Anthropic nếu cần

4. **Webhook Nodes** (3 nodes):
   - Cấu hình các endpoint:
     - /incident-report (cho báo cáo sự cố mới)
     - /incident-acknowledge (cho xác nhận sự cố)
     - /incident-feedback (cho phản hồi về quyết định AI)

5. **Runbook Sheet**:
   - Điền thông tin vào tab Runbooks:
     - Tên dịch vụ
     - Các vấn đề đã biết
     - Danh sách liên hệ cần liên lạc

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Gửi một POST request đến endpoint /incident-report với dữ liệu mẫu
   - Kiểm tra kết quả trong Google Sheets và Slack
2. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh ngưỡng nghiêm trọng**:
   - Chỉnh sửa prompt trong Agent 1 để phù hợp với định nghĩa mức độ ảnh hưởng của tổ chức

2. **Điều chỉnh SLA**:
   - Thay đổi thời gian chờ trong các node Wait (15 phút cho P1, 60 phút cho P2)

3. **Kết hợp với các hệ thống khác**:
   - Thay thế Slack bằng PagerDuty, Teams hoặc SMS
   - Kết nối với các hệ thống giám sát khác như Datadog, Prometheus

4. **Sử dụng các mô hình AI khác**:
   - Thay thế Gemini/Groq bằng OpenAI, Claude hoặc các mô hình local

5. **Tùy chỉnh kênh War Room**:
   - Chỉnh sửa tên kênh War Room và thêm các thành viên mặc định

### 📌 Kết luận
Workflow này biến đổi cách xử lý sự cố của các sếp từ thủ công thành tự động hoàn toàn. Bằng cách kết hợp sức mạnh của AI với các công cụ quản lý hiện có, các sếp có thể:
- Phản hồi nhanh hơn với sự cố cấp bách
- Giảm thời gian xử lý sự cố trung bình
- Tạo audit trail hoàn chỉnh cho các quy trình xử lý sự cố
- Tự động hóa các quy trình lặp lại
- Giảm tải cho các kỹ sư và quản lý

Hãy thử ngay và trải nghiệm cách tự động hóa chuyển đổi quy trình xử lý sự cố của bạn!