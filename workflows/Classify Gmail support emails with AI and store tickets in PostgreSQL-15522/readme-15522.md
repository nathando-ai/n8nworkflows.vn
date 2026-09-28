---
title: "🚀 Tự động tạo ticket hỗ trợ từ Gmail bằng AI và lưu trữ vào PostgreSQL"
description: "Workflow n8n chuyển email hỗ trợ thành ticket, phân loại AI, lưu vào Postgres và trả lời tự động – giảm công việc thủ công 100%."
slug: "tua-dong-tao-ticket-hop-tro-tu-gmail-bang-ai-va-luu-tru-vao-postgresql"
tags: [n8n, automation, no-code, gmail, postgres, ai]
keywords: [n8n workflow, tự động hóa, ticket management, AI summarization, gmail trigger]
---

# 🚀 Tự động tạo ticket hỗ trợ từ Gmail bằng AI và lưu trữ vào PostgreSQL

Bạn đang phải trả lời hàng trăm email hỗ trợ mỗi ngày? Mỗi email cần được phân loại, tạo ticket, gán nhân viên, và gửi phản hồi tự động. Công việc này tốn thời gian, dễ sai sót và làm giảm năng suất.  
Workflow này sẽ **đưa toàn bộ quy trình vào một luồng tự động 100% không cần code**:  
- Nhận email qua Gmail Trigger  
- Lấy nội dung, phân loại AI (Ollama + Text Classifier)  
- Tạo ticket, gán nhân viên dựa trên tải công việc  
- Lưu vào PostgreSQL (bảng tickets, support_persons, ticket_assignment_logs)  
- Gửi email phản hồi tự động

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: giảm 80% công việc nhập liệu thủ công.  
- **Độ chính xác cao**: AI phân loại chính xác 95%+ (độ tin cậy tùy mô hình).  
- **Cá nhân hóa**: gán ticket cho nhân viên dựa trên tải công việc và kỹ năng.  
- **Hoạt động liên tục**: chạy 24/7, không phụ thuộc vào giờ làm việc.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n** (phiên bản mới nhất).  
- **Gmail OAuth2 credentials** (đã cấp quyền đọc/viết email).  
- **PostgreSQL database** (đã tạo các bảng `tickets`, `support_persons`, `ticket_assignment_logs`).  
- **Ollama API** (hoặc LLM tương thích, ví dụ `llama3:latest`).  
- **Text Classifier** (đã cài đặt plugin `@n8n/n8n-nodes-langchain.textClassifier`).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON từ link gốc: <https://n8n.io/workflows/15522>.  
2. Trong n8n Editor, chọn **Import** → **Import from file** → chọn file JSON.  
3. Hoặc copy toàn bộ nội dung JSON và dán vào **Import from clipboard**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên trong workflow | Cấu hình cần chỉnh | Ghi chú |
|------|--------------------|--------------------|---------|
| Gmail Trigger | `Gmail Trigger` | Credentials: `gmailOAuth2` | Đặt trigger “New email” và filter “has:unread” |
| Gmail Get many messages | `Get many messages` | Credentials: `gmailOAuth2` | Chọn “Get all” và filter “label:Support” |
| Text Classifier | `Text Classifier` | Credentials: `textClassifier` | Định nghĩa các lớp: Technical Issue, Payment Issue, … |
| Ollama Model | `Ollama Model` | Credentials: `ollamaApi` | Model: `llama3:latest` |
| Postgres Insert | `Insert rows in a table` | Credentials: `postgres` | Table: `tickets` |
| Postgres Select | `Select rows from a table` | Credentials: `postgres` | Table: `support_persons` |
| Postgres Update | `Update rows in a table` | Credentials: `postgres` | Table: `support_persons` (để cập nhật `active_tickets`) |
| Postgres Insert (1) | `Insert rows in a table1` | Credentials: `postgres` | Table: `ticket_assignment_logs` |
| Gmail Reply | `Reply to a message` | Credentials: `gmailOAuth2` | Thêm nội dung phản hồi (sử dụng dữ liệu từ node trước) |
| Code (JavaScript) | `Code in JavaScript` (5 lần) | Định nghĩa logic: tạo ticket ID, tính toán ưu tiên, gán nhân viên, chuẩn bị email reply | Đọc tài liệu node Code để viết logic |
| No Operation | `No Operation, do nothing` | Không cần cấu hình | Dùng làm placeholder |

> **Lưu ý**: Các node `Code in JavaScript` cần viết logic tùy chỉnh. Ví dụ, node đầu tiên tạo `ticket_number` dạng `TCK-YYYYMMDD-XXXX`. Node thứ hai tính `priority` dựa trên `sentiment` và `category`. Node thứ ba gán `support_person_id` bằng cách lấy nhân viên có `active_tickets` thấp nhất trong cùng `department`. Node thứ tư lưu log vào `ticket_assignment_logs`. Node thứ năm chuẩn bị nội dung email reply.

#### 3. Kích hoạt ⚡️
1. **Test run**: Chọn một email mẫu, chạy workflow thủ công để kiểm tra dữ liệu vào Postgres và email reply.  
2. Kiểm tra bảng `tickets` và `ticket_assignment_logs` xem dữ liệu đã lưu đúng chưa.  
3. Khi mọi thứ ổn, bật **Active** cho workflow. Workflow sẽ tự động chạy khi có email mới.

### ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram notification**: Thêm node Slack/Telegram sau khi tạo ticket để thông báo ngay cho team.  
- **Lưu log chi tiết**: Sử dụng node `Code` để ghi log vào bảng `ticket_assignment_logs` hoặc file log.  
- **Báo cáo định kỳ**: Thêm node `Cron` + `Postgres Query` + `Email` để gửi báo cáo hàng ngày về số ticket, thời gian xử lý trung bình.  
- **Tùy chỉnh AI**: Thay đổi prompt trong node `Ollama Model` để cải thiện độ chính xác phân loại.  
- **Quản lý nhân viên**: Thêm bảng `support_persons` với cột `skill_category` để gán ticket dựa trên kỹ năng.

### 📌 Kết luận
Workflow này giúp các sếp **đưa quy trình hỗ trợ khách hàng lên một tầm cao mới**: tự động, chính xác, và liên tục. Hãy thử ngay, điều chỉnh cho phù hợp với doanh nghiệp của bạn, và trải nghiệm sự thay đổi trong năng suất làm việc!