---
title: "🚀 Tự động phát hiện hóa đơn & tạo nhắc nhở với Gmail & Google Tasks"
description: "Giải pháp tự động nhận diện email hóa đơn, tóm tắt nội dung bằng AI và tạo công việc trong Google Tasks, hoàn toàn không cần code."
slug: "tự-động-hóa-xử-lý-hóa-don-gmail-google-tasks"
tags: [n8n, automation, no-code, gmail, google-tasks, ai-summarization]
keywords: [n8n workflow, tự động hóa, gmail, google tasks, ai summarization, invoice processing]
---

# 🚀 Tự động phát hiện hóa đơn & tạo nhắc nhở với Gmail & Google Tasks

Bạn đang phải lướt qua hàng trăm email mỗi ngày để tìm kiếm những hóa đơn cần thanh toán? Mỗi lần bạn phải mở email, đọc nội dung, trích xuất ngày đáo hạn và tạo công việc trong Google Tasks, mất thời gian và dễ bị sai sót.  
Workflow này sẽ **đọc email, nhận diện tự động các email chứa hóa đơn, tóm tắt nội dung bằng AI, và tự động tạo công việc trong Google Tasks** – hoàn toàn không cần viết code, chỉ cần cấu hình một vài thông số.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần mở email, đọc từng dòng, chỉ cần một lần chạy workflow.  
- **Độ chính xác cao**: AI tóm tắt nội dung, giảm sai sót khi trích xuất ngày đáo hạn.  
- **Tự động hóa liên tục**: Workflow chạy theo lịch (mỗi giờ) mà không cần can thiệp.  
- **Tích hợp liền mạch**: Giao tiếp giữa Gmail và Google Tasks, giúp công việc được quản lý ngay trong danh sách công việc của bạn.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Tài khoản Gmail**: Cần quyền đọc, gắn nhãn, đánh dấu đã đọc, và thêm nhãn.  
- **Tài khoản Google Tasks**: Để tạo công việc.  
- **OpenAI API Key**: Để sử dụng mô hình GPT-4o cho việc tóm tắt và trích xuất thông tin.  
- **Nhãn Gmail “Invoice”**: Được dùng để đánh dấu email đã được xử lý.  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/5863).  
2. Mở n8n Editor → **Import** → **Import from file** → chọn file JSON.  
3. Hoặc copy toàn bộ nội dung JSON và dán vào ô **Import from clipboard**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên Node | Cấu hình cần chỉnh | Ghi chú |
|------|----------|---------------------|---------|
| 1 | Schedule Trigger | `Interval` (giờ) | Mặc định 1 giờ, thay đổi tùy nhu cầu. |
| 2 | AI Agent | `Prompt` | Đặt prompt để AI nhận diện hóa đơn và trích xuất ngày đáo hạn. |
| 3 | OpenAI Chat Model | `API Key`, `Model` | Đảm bảo API Key đã được lưu trong **API Credentials**. |
| 4 | Structured Output Parser | `Schema` | Định nghĩa cấu trúc JSON trả về (ví dụ: `{"due_date":"2024-10-15","amount":"$200"}`). |
| 5 | No Operation, do nothing | - | Không cần cấu hình. |
| 6 | Create a task | `Task title`, `Notes` | Sử dụng dữ liệu từ Structured Output Parser (ví dụ: `Pay invoice from {{sender}} by {{due_date}}`). |
| 7 | Add Label to Email | `Label` | Nhãn “Invoice”. |
| 8 | Mark Email as read | - | Không cần tham số. |
| 9 | Get Unread Emails | `Label` | Chỉ lấy email chưa đọc, có nhãn “Invoice”. |
| 10 | Check If Email is Invoice | `Condition` | Kiểm tra tiêu đề hoặc nội dung có chứa từ khóa “invoice”. |

#### Gợi ý cấu hình Prompt (Node “AI Agent”)

```
You are an assistant that identifies invoices in emails.
Given the email subject and body, output a JSON with:
{
  "is_invoice": true/false,
  "due_date": "YYYY-MM-DD",
  "amount": "$XXX"
}
If not an invoice, set is_invoice to false.
```

#### Gợi ý cấu hình Structured Output Parser

- **JSON schema**:
```json
{
  "type": "object",
  "properties": {
    "is_invoice": {"type": "boolean"},
    "due_date": {"type": "string", "format": "date"},
    "amount": {"type": "string"}
  },
  "required": ["is_invoice"]
}
```

### 3. Kích hoạt ⚡️

1. **Test run**: Chạy workflow với dữ liệu mẫu (đảm bảo email mẫu có nhãn “Invoice”). Kiểm tra log để xác nhận AI đã trích xuất đúng thông tin.  
2. **Bật Active**: Đánh dấu workflow là **Active** để nó tự động chạy theo lịch.  
3. Kiểm tra Google Tasks: Công việc mới đã xuất hiện với tiêu đề và ghi chú đúng.

## ✍️ Mẹo & gợi ý nâng cao

- **Slack/Telegram notification**: Thêm node “Slack” hoặc “Telegram” sau “Create a task” để thông báo ngay khi công việc được tạo.  
- **Lưu log vào Google Sheets**: Thêm node “Google Sheets” để ghi lại lịch sử email đã xử lý, ngày tạo công việc, và trạng thái thanh toán.  
- **Định kỳ gửi báo cáo**: Sử dụng node “Schedule Trigger” khác để gửi email báo cáo hàng ngày/tuần về các công việc chưa thanh toán.  
- **Tùy chỉnh tiêu đề công việc**: Sử dụng biến `{{sender}}`, `{{due_date}}`, `{{amount}}` để làm tiêu đề chi tiết hơn.  

## 📌 Kết luận

Workflow “Automatic Invoice Detection & Reminder Creation with Gmail & Google Tasks” giúp các sếp **tiết kiệm thời gian, giảm sai sót và tăng tính minh bạch** trong quản lý hóa đơn.  
Hãy thử ngay, cấu hình nhanh, chạy liên tục và cảm nhận sự khác biệt!