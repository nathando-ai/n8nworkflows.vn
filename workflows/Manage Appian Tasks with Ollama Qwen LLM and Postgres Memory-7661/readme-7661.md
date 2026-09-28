---
title: "🚀 Quản lý công việc Appian tự động bằng AI Agent, Ollama Qwen và Postgres Memory trong n8n"
description: "Hướng dẫn xây dựng trợ lý AI nội bộ sử dụng Ollama Qwen2.5, Postgres Chat Memory và n8n để quản lý, tạo và liệt kê task Appian qua chat hoặc webhook."
slug: "quan-ly-cong-viec-appian-ollama-postgres-n8n"
tags: [n8n, automation, ai-agent, ollama, postgresql, appian]
keywords: [n8n workflow, appian task automation, ollama qwen n8n, ai agent postgres memory, quan ly task appian ai]
---

# 🚀 Quản lý công việc Appian tự động bằng AI Agent, Ollama Qwen và Postgres Memory

Các sếp có đang gặp khó khăn khi phải thao tác thủ công liên tục trên hệ thống Appian để tạo mới, tra cứu hay theo dõi danh sách công việc? Việc chuyển đổi qua lại giữa các màn hình không chỉ tốn thời gian mà còn dễ gây sót việc. 

Giải pháp hoàn hảo cho các sếp chính là workflow n8n tích hợp **AI Agent**, mô hình ngôn ngữ **Ollama (Qwen)** chạy nội bộ, kết hợp cùng **Postgres Chat Memory** để ghi nhớ ngữ cảnh hội thoại. Workflow này giúp tự động hóa hoàn toàn việc tương tác với hệ thống Appian thông qua giao diện chat hoặc webhook một cách thông minh, mượt mà và bảo mật tuyệt đối.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa quản lý Task:** Liệt kê, phân loại và tạo task trực tiếp trên Appian thông qua câu lệnh ngôn ngữ tự nhiên.
- **Bảo mật dữ liệu tối đa:** Sử dụng mô hình Ollama chạy cục bộ (local LLM) kết hợp cơ sở dữ liệu PostgreSQL để lưu trữ bộ nhớ trò chuyện, đảm bảo dữ liệu doanh nghiệp không bị rò rỉ ra bên ngoài.
- **Trải nghiệm thông minh:** AI Agent tự động hiểu ý định người dùng, gọi đúng công cụ (Appian API) và phản hồi chính xác.
- **Hoạt động 24/7:** Sẵn sàng tiếp nhận yêu cầu qua Webhook bất cứ lúc nào từ các ứng dụng bên thứ ba.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng self-hosted để kết nối mượt mà với Ollama local).
- **Ollama Server:** Đang chạy mô hình `qwen2.5:7b` (hoặc model tương thích).
- **PostgreSQL Database:** Dùng để làm bộ nhớ ngữ cảnh trò chuyện (`Postgres Chat Memory`).
- **Appian API Credentials:** Thông tin kết nối và xác thực tới API của hệ thống Appian.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow (từ nguồn n8n.io/workflows/7661) và paste trực tiếp vào màn hình n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công, các sếp cần cấu hình chính xác các node quan trọng sau đây:
- **Template Vars & Normalize Chat Input:** Điền các biến môi trường cấu hình chung, định dạng lại thông tin đầu vào cho chuẩn cú pháp của AI Agent.
- **Ollama Chat Model:** Thiết lập kết nối đến server Ollama của sếp và đảm bảo chọn đúng tên model `model: qwen2.5:7b`.
- **Postgres Chat Memory:** Cấu hình credentials kết nối đến Database PostgreSQL để lưu lịch sử chat, giúp AI nhớ được ngữ cảnh các câu hỏi trước đó.
- **List Tasks (Appian), List Task Types (Appian), Create Task (Appian):** Các node dạng `httpRequestTool` này dùng để tương tác với Appian API. Các sếp cần cấu hình lại URL endpoint, phương thức HTTP (GET/POST) và thêm thông tin xác thực (Bearer Token/API Key) phù hợp với hệ thống Appian của công ty.
- **Webhook & Respond to Webhook:** Nếu tích hợp nhận request từ bên ngoài, hãy cập nhật lại `path` tại node Webhook cho khớp với hệ thống gọi tới.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test workflow) bằng cách gửi một câu lệnh chat mẫu (ví dụ: *"Liệt kê giúp tôi các task đang chờ xử lý"* hoặc *"Tạo một task mới loại X"*).
- Kiểm tra kết quả trả về qua node phản hồi.
- Bật công tắc **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat:** Kết nối node `When chat message received` với Slack, Telegram hoặc Microsoft Teams để nhân viên có thể quản lý task trực tiếp trên ứng dụng chat hàng ngày.
- **Lưu log chi tiết:** Thêm một node lưu lịch sử hoạt động vào Google Sheets hoặc Database phụ để theo dõi các lệnh đã được AI thực thi.
- **Bổ sung công cụ (Tools):** Có thể mở rộng AI Agent bằng cách thêm các `httpRequestTool` khác để cập nhật trạng thái hoặc xóa task trên Appian.

### 📌 Kết luận
Workflow tích hợp AI Agent, Ollama và Appian này là bước tiến tuyệt vời giúp tối ưu hóa quy trình làm việc nội bộ mà vẫn đảm bảo tính bảo mật dữ liệu cao. Hãy triển khai ngay hôm nay để giải phóng sức lao động thủ công cho đội ngũ của các sếp!