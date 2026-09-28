---
title: "🚀 Tự động duyệt đơn hàng Google Sheets qua email & thông báo LINE"
description: "Giải pháp n8n tự động lấy đơn hàng từ Google Sheets, gửi email duyệt, nhận phản hồi và thông báo ngay trên LINE, giảm 90% công việc thủ công."
slug: "tu-dong-duyet-don-hang-google-sheets-email-line"
tags: [n8n, automation, no-code, google-sheets, gmail, line-notify, document-extraction]
keywords: [n8n workflow, tự động hóa, Google Sheets, email approval, LINE notification]
---

# 🚀 Tự động duyệt đơn hàng Google Sheets qua email & thông báo LINE

Doanh nghiệp thường phải **làm thủ công**: mở Google Sheets, sao chép dữ liệu, gửi email duyệt, chờ phản hồi, rồi lại cập nhật trạng thái và thông báo cho bộ phận liên quan. Quy trình này không chỉ tốn thời gian mà còn dễ gây lỗi nhập liệu, mất đồng bộ và làm chậm vòng quay bán hàng.

**Workflow n8n** này sẽ **tự động**:
1. Lấy danh sách đơn hàng mới từ Google Sheets.
2. Gửi email duyệt cho người phụ trách.
3. Nhận phản hồi (phê duyệt/ từ chối) qua email.
4. Cập nhật trạng thái trong Google Sheets.
5. Gửi thông báo ngay lập tức qua LINE cho nhóm bán hàng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: giảm tới 90% công việc kiểm tra và gửi email.  
- **Độ chính xác cao**: cập nhật trạng thái tự động, không còn sai sót nhập liệu.  
- **Thông báo tức thời**: LINE bot gửi tin nhắn ngay khi có quyết định.  
- **Hoạt động liên tục**: workflow chạy 24/7, không cần can thiệp thủ công.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Google Account** có quyền truy cập Google Sheet chứa đơn hàng.  
- **Gmail Account** (hoặc Google Workspace) để gửi và nhận email duyệt.  
- **LINE Notify Token** (đăng ký tại https://notify-bot.line.me/).  
- **n8n Credentials**:  
  - `Google Sheets OAuth2` (hoặc Service Account).  
  - `Gmail OAuth2`.  
  - `HTTP Request` (để gọi LINE Notify).  
- **Webhook URL**: n8n sẽ tạo tự động khi bạn bật node `Webhook`.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. **Tải file JSON** của workflow (được cung cấp ở phần cuối tài liệu hoặc tại link gốc).  
2. Vào n8n → **Workflows** → **Import** → Chọn file JSON → **Import**.  
3. Hoặc **Copy/Paste** toàn bộ JSON vào cửa sổ **Import from Clipboard**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Vai trò | Cấu hình cần thay đổi |
|------|---------|-----------------------|
| **Webhook** | Nhận phản hồi email duyệt (đường link trong email). | - `HTTP Method`: **GET** hoặc **POST** tùy email template.<br>- `Response Mode`: **On Received**.<br>- **Save** URL để chèn vào email. |
| **Google Sheets Trigger** | Kích hoạt khi có hàng mới trong Sheet. | - Chọn **Spreadsheet ID** và **Worksheet** chứa đơn hàng.<br>- Đánh dấu **Trigger on New Row**. |
| **Set (Prepare Email)** | Tạo nội dung email duyệt. | - Đặt các biến: `orderId`, `customerName`, `orderDetails`.<br>- Tạo **HTML body** với link webhook (được tạo ở node Webhook). |
| **Gmail** | Gửi email duyệt tới người phụ trách. | - Chọn **Credential** Gmail đã tạo.<br>- Điền **To**, **Subject**, **HTML Body** (sử dụng biến từ node Set). |
| **If** | Kiểm tra phản hồi (phê duyệt / từ chối). | - Điều kiện: `emailSubject` chứa **"Approve"** hoặc **"Reject"**.<br>- Đặt **Output** `true` cho duyệt, `false` cho từ chối. |
| **Google Sheets (Update Row)** | Cập nhật trạng thái đơn hàng. | - Chọn cùng **Spreadsheet ID**.<br>- Dùng **Row ID** từ trigger.<br>- Cập nhật cột **Status** = `Approved` hoặc `Rejected`. |
| **HTTP Request (LINE Notify)** | Gửi tin nhắn LINE thông báo. | - **Method**: POST.<br>- **URL**: `https://notify-api.line.me/api/notify`.<br>- **Headers**: `Authorization: Bearer <LINE_TOKEN>`.<br>- **Body**: `message=Đơn hàng #{{orderId}} đã được {{status}}`. |
| **Respond To Webhook** | Trả lời email người dùng (tùy chọn). | - Nội dung **HTML**: “Cảm ơn, quyết định của bạn đã được ghi nhận.” |
| **Sticky Note** | Ghi chú hướng dẫn nội bộ (không ảnh hưởng workflow). | - Không cần cấu hình, chỉ để mô tả luồng. |

> **Lưu ý quan trọng**:  
> - Đảm bảo **Google Sheets Trigger** và **Google Sheets Update** dùng cùng **Credential** để tránh lỗi quyền.  
> - Khi tạo **LINE Notify Token**, chọn **"Send notifications to chat"** và sao chép token vào credential `HTTP Request`.  
> - Kiểm tra **Webhook URL** trong email mẫu; nếu email client chặn GET request, chuyển sang **POST** và thêm body `{ "orderId": "{{orderId}}" }`.

#### 3. Kích hoạt ⚡️
1. **Test run**: Thêm một hàng mẫu vào Google Sheet → Kiểm tra email được gửi.  
2. Nhấp vào link trong email → Xác nhận webhook trả về **200 OK**.  
3. Kiểm tra Google Sheet: cột **Status** đã thay đổi.  
4. Kiểm tra LINE: nhận được tin nhắn thông báo.  
5. Khi mọi thứ ổn, bật **Active** workflow (nút toggle ở góc trên bên phải).

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack**: Thêm node `Slack` để đồng thời gửi thông báo tới kênh Slack nội bộ.  
- **Lưu log chi tiết**: Dùng node `Write Binary File` hoặc `Google Drive` để lưu bản sao email và phản hồi cho mục đích audit.  
- **Báo cáo định kỳ**: Thêm `Cron` + `Google Sheets` để tổng hợp số đơn đã duyệt/hủy mỗi ngày và gửi báo cáo qua Gmail.  
- **AI Review**: Kết hợp LLM (OpenAI) để tự động phân loại nội dung đơn hàng trước khi gửi email duyệt, giảm thiểu lỗi nhập liệu.

### 📌 Kết luận
Với workflow này, các sếp sẽ **đánh bại mọi công việc lặp đi lặp lại** trong quy trình duyệt đơn hàng, giảm chi phí nhân lực, tăng độ chính xác và luôn nhận được thông báo kịp thời qua LINE. Hãy **import ngay**, cấu hình các credential cần thiết và để n8n làm việc thay bạn! 🚀