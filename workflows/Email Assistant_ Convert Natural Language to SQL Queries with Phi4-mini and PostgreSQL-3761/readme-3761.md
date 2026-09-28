---
title: "🚀 Biến ngôn ngữ tự nhiên thành câu lệnh SQL với Phi4-mini và PostgreSQL trong n8n"
description: "Hướng dẫn cấu hình workflow n8n tự động hóa việc chuyển đổi câu hỏi bằng ngôn ngữ tự nhiên thành câu lệnh SQL và truy xuất dữ liệu từ PostgreSQL sử dụng AI Model Phi4-mini."
slug: "chuyen-doi-ngon-ngu-tu-nhien-thanh-sql-phi4-mini-postgresql"
tags: [n8n, automation, ai, postgresql, ollama, phi4-mini]
keywords: [n8n workflow, text to sql, ollama phi4-mini, postgresql automation, ai agent n8n]
---

# 🚀 Biến ngôn ngữ tự nhiên thành câu lệnh SQL với Phi4-mini và PostgreSQL

Các sếp có bao giờ cảm thấy mệt mỏi khi phải viết các câu lệnh SQL phức tạp mỗi lần cần trắc nghiệm dữ liệu, hay việc phải liên tục hỗ trợ đội ngũ kinh doanh/vận hành truy vấn database? Việc tra cứu dữ liệu thủ công vừa tốn thời gian, lại dễ gây nhầm lẫn.

Giải pháp ở đây là gì? Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình trên: người dùng chỉ cần nhập yêu cầu bằng **ngôn ngữ tự nhiên (Chat)**, AI Model **Phi4-mini** (chạy qua Ollama) sẽ tự động phân tích cấu trúc database (schema), dịch thành câu lệnh SQL chuẩn xác, truy vấn vào **PostgreSQL** và trả về kết quả ngay lập tức mà không cần viết một dòng code thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow xử lý các tác vụ AI và truy vấn database ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tối ưu thời gian:** Chuyển câu hỏi tiếng Việt/tiếng Anh thông thường thành câu lệnh SQL chỉ trong vài giây.
- **Bảo mật & Cục bộ:** Sử dụng mô hình AI **Phi4-mini** thông qua Ollama giúp chạy hoàn toàn local, bảo mật tuyệt đối dữ liệu doanh nghiệp.
- **Tương tác linh hoạt:** Hỗ trợ giao diện Chat Trigger thân thiện hoặc tích hợp như một sub-workflow vào các hệ thống khác.
- **Tự động cập nhật Schema:** Tự động quét và lưu trữ cấu trúc bảng dữ liệu từ PostgreSQL để AI có ngữ cảnh chính xác nhất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (bản self-hosted hoặc cloud).
- **Ollama:** Đã cài đặt Ollama và tải sẵn model `phi4-mini:latest`.
- **PostgreSQL Database:** Cơ sở dữ liệu nguồn chứa dữ liệu cần truy vấn.
- **Credentials:** Thông tin kết nối PostgreSQL (Host, Port, Database, User, Password) được cấu hình trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tạo một workflow mới trong n8n của các sếp, copy toàn bộ mã JSON của workflow này và dán trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow được chia thành 2 phần chính tương ứng với hướng dẫn trên canvas:
- **Phần khởi tạo Schema (Chạy thủ công hoặc định kỳ):**
  - Các node như `List all tables in a database`, `List all columns in a table` cần được cấu hình thông tin đăng nhập **PostgreSQL Credentials**.
  - Node `Save file locally` và `Load the schema from the local file` dùng để lưu và đọc file cấu trúc schema cục bộ trên ổ đĩa của n8n, giúp AI hiểu được tên bảng và cột mà không cần gọi API database liên tục.
- **Phần xử lý AI & Chat (Chat Trigger hoặc Sub-workflow):**
  - Node **`Ollama Chat Model`**: Đảm bảo model được cấu hình chính xác là `phi4-mini:latest` và trỏ đúng URL của Ollama server (ví dụ: `http://localhost:11434` hoặc qua Docker network).
  - Node **`AI Agent`** và các node set `Extract SQL query`, `Add trailing semicolon`: Đảm bảo prompt và logic xử lý dấu chấm phẩy (`;`) hoạt động tốt để câu lệnh SQL trả về không bị lỗi cú pháp trước khi chạy.
  - Node **`Postgres`** (trong phần thực thi câu lệnh SQL): Cần gán đúng credentials và nhận tham số câu lệnh SQL được sinh ra từ AI Agent.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (`When clicking "Test workflow"`) phần load schema để đảm bảo file JSON schema được lưu thành công.
- Mở cửa sổ **Chat Trigger** để test câu hỏi bằng ngôn ngữ tự nhiên (Ví dụ: *"Cho tôi xem danh sách 5 khách hàng mới nhất"*).
- Sau khi test thành công, bật trạng thái **Active** cho workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat:** Kết nối Chat Trigger với Telegram Bot hoặc Slack để nhân viên có thể tra cứu dữ liệu trực tiếp từ ứng dụng chat quen thuộc.
- **Lưu lịch sử truy vấn:** Thêm một node Google Sheets hoặc Postgres Insert để lưu lại lịch sử các câu hỏi và kết quả nhằm phục vụ việcAudit hoặc tối ưu Prompt sau này.
- **Lên lịch cập nhật schema:** Đặt một Schedule Trigger chạy mỗi tuần một lần để tự động cập nhật lại file schema nếu cơ sở dữ liệu có thay đổi cấu trúc bảng.

### 📌 Kết luận
Workflow chuyển đổi ngôn ngữ tự nhiên thành SQL sử dụng Phi4-mini và PostgreSQL là một trợ thủ đắc lực giúp dân kỹ thuật cũng như kinh doanh khai thác dữ liệu dễ dàng hơn bao giờ hết mà không sợ lộ lọt dữ liệu ra ngoài. Hãy import và cấu hình ngay hôm nay để tối ưu hóa hiệu suất làm việc của các sếp!