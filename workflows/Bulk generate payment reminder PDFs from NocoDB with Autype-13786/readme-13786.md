---
title: "🚀 Tự động tạo PDF nhắc thanh toán hàng loạt từ NocoDB với Autype"
description: "Giải pháp tự động lấy dữ liệu hoá đơn từ NocoDB, tạo PDF nhắc thanh toán bằng Autype và gửi email, giảm 100% công việc thủ công."
slug: "tu-dong-tao-pdf-nhac-thanh-toan-nocodb-autype"
tags: [n8n, automation, no-code, invoicing, AI]
keywords: [n8n workflow, tự động hóa, PDF nhắc thanh toán, NocoDB, Autype]
---

# 🚀 Tự động tạo PDF nhắc thanh toán hàng loạt từ NocoDB với Autype

Doanh nghiệp thường phải **làm thủ công** việc lấy danh sách hoá đơn chưa thanh toán, tạo file PDF nhắc nhở và gửi email cho từng khách hàng.  
Quá trình này tốn hàng giờ, dễ sai sót và không thể thực hiện 24/7.  

Workflow **Bulk generate payment reminder PDFs from NocoDB with Autype** sẽ **tự động**:

1. Lấy dữ liệu hoá đơn chưa thanh toán từ NocoDB.  
2. Dùng Autype (AI multimodal) tạo PDF nhắc thanh toán cá nhân hoá.  
3. Gửi PDF qua email tới khách hàng.  

Kết quả: **tiết kiệm thời gian, giảm lỗi, tăng độ chuyên nghiệp** mà không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80‑90% thời gian** so với việc tạo PDF và gửi email thủ công.  
- **Độ chính xác 100%**: dữ liệu lấy trực tiếp từ NocoDB, không còn nhập sai.  
- **Cá nhân hoá**: mỗi PDF chứa tên, số tiền, hạn thanh toán riêng của khách.  
- **Hoạt động liên tục**: workflow có thể chạy theo lịch (hàng ngày/giờ) mà không cần giám sát.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản NocoDB** + **API Key** (hoặc token) để truy cập bảng hoá đơn.  
- **Tài khoản Autype** + **API Key** để gọi dịch vụ tạo PDF.  
- **SMTP server** (hoặc dịch vụ email như Gmail, SendGrid) và **credentials** để gửi email.  
- **n8n** đã cài đặt (Self‑hosted hoặc Cloud) và có quyền **install community nodes** (Autype).  
- (Tùy chọn) **Domain/email sender** để tránh spam.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập **n8n > Workflows**.  
2. Nhấn **Import** → **Upload JSON** và chọn file `bulk-generate-payment-reminder.json` (được tải từ trang gốc).  
3. Hoặc **Copy/Paste** nội dung JSON vào ô **Import from Clipboard**.  

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là danh sách **node** quan trọng và cách cấu hình:

| Node | Mô tả | Cấu hình cần thay đổi |
|------|------|-----------------------|
| **Manual Trigger** / **Schedule Trigger** | Khởi động workflow (bằng nút hoặc lịch định kỳ). | - Nếu dùng **Schedule Trigger**, đặt tần suất (ví dụ: mỗi ngày 08:00). |
| **NocoDB (Get All)** | Lấy danh sách hoá đơn chưa thanh toán. | - **Resource**: `Table` <br> - **Operation**: `Get All` <br> - **Base ID**: ID của workspace NocoDB <br> - **Table Name**: tên bảng hoá đơn (ví dụ: `invoices`) <br> - **Filters**: `status = "unpaid"` |
| **Code (Prepare Data)** | Chuyển đổi dữ liệu NocoDB sang định dạng mà Autype yêu cầu (JSON array). | - **Language**: JavaScript <br> - **Code** (mẫu): <br>```js\nreturn items.map(item => ({\n  customerName: item.json.customer_name,\n  email: item.json.email,\n  amount: item.json.amount_due,\n  dueDate: item.json.due_date,\n  invoiceId: item.json.id,\n}));\n``` |
| **Autype (Generate PDF)** | Dùng mô hình AI tạo PDF nhắc thanh toán. | - **Credentials**: Autype API Key <br> - **Prompt**: (ví dụ) `Create a payment reminder PDF for {{customerName}} with amount {{amount}} VND, due on {{dueDate}}. Include invoice #{{invoiceId}}.` <br> - **Output Format**: `PDF` |
| **Email Send** | Gửi PDF tới khách hàng. | - **SMTP Credentials**: chọn tài khoản đã cấu hình <br> - **To**: `{{$json["email"]}}` <br> - **Subject**: `Nhắc nhở thanh toán - Hóa đơn #{{$json["invoiceId"]}}` <br> - **Attachments**: `{{$node["Autype"].json["pdfUrl"]}}` (hoặc `binary` nếu trả về file binary) |
| **Sticky Note** (tùy chọn) | Ghi chú thông tin workflow trong editor. | Không cần cấu hình, chỉ dùng để mô tả luồng. |

> **Lưu ý:** Đảm bảo **Credentials** cho NocoDB, Autype và Email đều được tạo trong **n8n > Credentials** trước khi gán vào node.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** để chạy thử với **dữ liệu mẫu** (có thể tạo một bản ghi “unpaid” trong NocoDB).  
2. Kiểm tra **log** của mỗi node, xác nhận PDF được tạo và email được gửi thành công.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải) để workflow tự động chạy theo lịch hoặc khi trigger thủ công.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi báo cáo tổng hợp**: Thêm một node **Google Sheets** hoặc **Airtable** để lưu log mỗi lần gửi, sau đó gửi báo cáo hàng tuần qua email.  
- **Thông báo Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** để gửi tin nhắn thông báo khi có lỗi hoặc khi hoàn thành batch.  
- **Xử lý lỗi retry**: Dùng node **Error Trigger** + **Set** để tự động retry các email thất bại sau 5 phút.  
- **Định dạng PDF chuyên nghiệp**: Tùy chỉnh **Prompt** của Autype để chèn logo công ty, QR code thanh toán, hoặc link thanh toán trực tuyến.  

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động hoá toàn bộ quy trình nhắc thanh toán** chỉ trong vài phút thiết lập, giảm tải công việc hành chính, nâng cao độ tin cậy và tạo ấn tượng chuyên nghiệp với khách hàng.  
Hãy **import ngay**, cấu hình các credentials và để n8n làm việc cho bạn 24/7! 🚀