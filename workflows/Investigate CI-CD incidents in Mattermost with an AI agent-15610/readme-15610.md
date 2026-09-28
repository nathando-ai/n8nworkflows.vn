---
title: "🚀 Tự động điều tra sự cố CI/CD trên Mattermost bằng AI Agent và n8n"
description: "Xây dựng AI Agent thông minh tích hợp n8n, OpenRouter và các MCP Servers để tự động phân tích, chẩn đoán lỗi CI/CD, Kubernetes và Grafana trực tiếp trên Mattermost."
slug: "tu-dong-dieu-tra-su-co-ci-cd-mattermost-ai-agent-n8n"
tags: [n8n, automation, devops, ai-agent, mattermost, kubernetes, grafana]
keywords: [n8n workflow, tự động hóa devops, ai agent mattermost, ci cd incident investigation, openrouter mcp]
---

# 🚀 Tự động điều tra sự cố CI/CD trên Mattermost bằng AI Agent

Các sếp làm DevOps chắc hẳn đều ngán ngẩm cảnh nửa đêm nhận thông báo lỗi pipeline, hì hục mở terminal, truy cập Grafana, kiểm tra log Kubernetes và lật tung GitHub để tìm nguyên nhân. Quá mất thời gian và căng thẳng! 

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách kết hợp **AI Agent**, **OpenRouter**, **MCP Servers** và **Mattermost**. Khi kỹ sư báo lỗi trên chat, AI Agent sẽ tự động nhảy vào "soi" log, kiểm tra hệ thống và trả về kết quả chuẩn chỉnh trực tiếp trong thread mà không hề làm thay đổi cấu hình hệ thống (read-only diagnostic).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và kết nối mượt mà với các hệ thống nội bộ, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian debug:** AI tự động gom log từ GitHub, kiểm tra metrics từ Grafana và pod status từ Kubernetes.
- **Phản hồi tức thì trong Chat:** Câu trả lời chi tiết, nguyên nhân gốc rễ (root cause) được bắn thẳng về thread Mattermost của kỹ sư.
- **An toàn tuyệt đối:** Agent hoạt động ở chế độ chẩn đoán (read-only), không tự ý thực hiện các lệnh thay đổi hệ thống nguy hiểm.
- **Hoạt động 24/7 không mệt mỏi:** Thay thế ca trực đêm vất vả bằng một "trợ lý ảo" siêu cấp thông minh.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các mảnh ghép sau:
- **Tài khoản OpenRouter / OpenAI / Anthropic:** Lấy API Key để cấp cho model `OpenRouter Chat Model` (Workflow khuyến nghị dùng `openai/gpt-5.3-codex`).
- **Mattermost Bot & Credentials:** Kết nối API Mattermost để gửi tin nhắn.
- **Hệ thống MCP Servers:** Các Model Context Protocol servers đã được triển khai (Grafana, GitHub, Kubernetes, Mattermost).
- **Sub-workflows đi kèm:** Sub-workflow `attachmentsAnalyzer` (phân tích file đính kèm) và `httpProbeTool` (cung cấp tool `probe_url`).
- **Parent Workflow:** Workflow phân loại yêu cầu ban đầu gọi đến sub-workflow này qua node `Execute Workflow`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ n8n hoặc copy toàn bộ JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File / Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy trơn tru, các sếp cần chú ý cấu hình các node cốt lõi sau:
- **SetVars:** Điền các biến môi trường và cấu hình runtime phù hợp với hệ thống của công ty các sếp.
- **OpenRouter Chat Model:** Chọn credential `openRouterApi` và cấu hình model AI mong muốn (ví dụ: `openai/gpt-5.3-codex`).
- **AI Agent:** Tinh chỉnh lại System Prompt của Agent cho phù hợp với quy trình xử lý sự cố đặc thù của đội ngũ kỹ thuật công ty.
- **MCP Tool Nodes (Github, Grafana, k8s, Mattermost):** Cung cấp đúng URL endpoint của các remote MCP servers mà đội ngũ DevOps đã dựng sẵn.
- **Post a message:** Chọn đúng credentials của Mattermost để bot có quyền bắn tin nhắn trả lời vào đúng channel/thread yêu cầu.

#### 3. Kích hoạt ⚡️
- Kiểm tra lại luồng dữ liệu đầu vào từ node `When Executed by Another Workflow`.
- Nhấn **Execute Workflow** với dữ liệu mẫu (payload giả lập từ Mattermost) để test thử xem Agent gọi tool và phản hồi thế nào.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để bật chế độ tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Slack:** Nếu công ty các sếp dùng đa kênh chat, có thể mở rộng nhánh output để bắn thông báo song song qua Slack hoặc Telegram.
- **Lưu lịch sử sự cố:** Thêm node Google Sheets hoặc Airtable vào cuối luồng để lưu lại toàn bộ các ca sự cố và cách AI chẩn đoán, làm tài liệu tổng kết hàng tuần.
- **Auto-remediation (Nâng cao):** Sau khi AI chẩn đoán xong và độ tin cậy (confidence) đạt 100%, có thể viết thêm một nhánh phê duyệt (Approval) để tự động chạy lệnh rollback hoặc restart pod qua Kubernetes MCP.

### 📌 Kết luận
Việc tích hợp AI Agent vào quy trình DevOps với n8n không chỉ giúp giảm tải áp lực cho kỹ sư trực chiến mà còn chuẩn hóa quy trình xử lý sự cố cực kỳ chuyên nghiệp. Hãy triển khai ngay để đội ngũ DevOps của các sếp được "thở phào" mỗi khi cóincident xảy ra!