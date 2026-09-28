---
title: "🚀 Lưu Sự Kiện Hotmart vào Google Sheets tự động, không cần code"
description: "Tự động nhận webhook từ Hotmart, chuyển đổi timestamp và ghi dữ liệu vào Google Sheets chỉ trong vài phút."
slug: "luu-su-kien-hotmart-vao-google-sheets"
tags: [n8n, automation, no-code, hotmart, google-sheets, webhook]
keywords: [n8n workflow, tự động hóa, Hotmart, Google Sheets, webhook]
---

# 🚀 Lưu Sự Kiện Hotmart vào Google Sheets tự động, không cần code

Khi bán hàng trên **Hotmart**, mỗi giao dịch, đăng ký hay hủy bỏ đều được gửi về dạng webhook.  
Nếu bạn vẫn đang **chép‑dán thủ công** các dữ liệu này vào bảng tính, công việc sẽ tốn thời gian, dễ sai sót và không thể theo dõi thời gian thực.  

**Workflow này** sẽ nhận mọi sự kiện từ Hotmart, **chuyển đổi timestamp** sang định dạng ngày‑giờ dễ đọc, rồi **đẩy tự động** vào một Google Sheet đã chuẩn bị sẵn. Bạn chỉ cần một lần thiết lập, mọi dữ liệu sẽ được ghi lại 24/7 mà không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Không còn nhập liệu thủ công, dữ liệu cập nhật ngay khi sự kiện xảy ra.  
- **Độ chính xác 100 %**: Loại bỏ lỗi nhập sai, dữ liệu đồng nhất trong mọi báo cáo.  
- **Theo dõi thời gian thực**: Nhìn ngay trong Google Sheets khi có giao dịch mới.  
- **Mở rộng dễ dàng**: Thêm các bước xử lý (email, Slack, báo cáo) chỉ bằng vài node.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản Hotmart**: Để tạo webhook URL (có trong Hotmart > Settings > Webhooks).  
- **Google Account** với **Google Sheets API** được bật và **OAuth2 credentials** (hoặc Service Account) để n8n có thể ghi vào Sheet.  
- **n8n** đã cài đặt (Self‑hosted hoặc Cloud).  
- **Google Sheet** đã tạo, có ít nhất các cột: `Timestamp`, `Event Type`, `Buyer Name`, `Email`, `Product ID`, `Amount`.  
- **API Key** (nếu bạn dùng Service Account) hoặc **OAuth2 token** cho node Google Sheets.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở **n8n Editor**.  
2. Nhấn **Import** → **Upload JSON** và chọn file `Save Hotmart events to Google Sheets.json` (hoặc copy toàn bộ JSON vào ô **Paste JSON**).  
3. Nhấn **Import**, workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cấu hình cần chỉnh |
|------|------|--------------------|
| **Webhook** | Nhận dữ liệu POST từ Hotmart | - **HTTP Method**: `POST` <br> - **Path**: `hotmart-events` (có thể đổi) <br> - **Response Mode**: `Respond with JSON` (để Hotmart nhận 200 OK) |
| **Set some data** | Lấy ra các trường quan trọng từ payload | - Thêm **Set** fields: <br>   - `event_type` → `{{$json["event"]["type"]}}` <br>   - `buyer_name` → `{{$json["event"]["buyer"]["name"]}}` <br>   - `email` → `{{$json["event"]["buyer"]["email"]}}` <br>   - `product_id` → `{{$json["event"]["product"]["id"]}}` <br>   - `amount` → `{{$json["event"]["sale"]["price"]}}` <br>   - `raw_timestamp` → `{{$json["event"]["created_at"]}}` |
| **Convert timestamp** | Chuyển `raw_timestamp` (Unix ms) sang `YYYY-MM-DD HH:mm:ss` | - **Input**: `{{$json["raw_timestamp"]}}` <br> - **Format**: `YYYY-MM-DD HH:mm:ss` <br> - **Output Field**: `timestamp_formatted` |
| **Switch** | Phân loại sự kiện (purchase, subscription, cancel…) | - **Value**: `{{$json["event_type"]}}` <br> - Thêm **case** cho các loại cần xử lý (ví dụ: `purchase`, `subscription_created`). Các case không quan tâm có thể để **Default** → **Stop**. |
| **Google Sheets** | Ghi dữ liệu vào Sheet | - **Operation**: `Append` <br> - **Spreadsheet ID**: (lấy từ URL Google Sheet) <br> - **Sheet Name**: `Hotmart Events` (hoặc tên bạn đặt) <br> - **Columns**: `timestamp_formatted, event_type, buyer_name, email, product_id, amount` <br> - **Credentials**: Chọn **Google OAuth2 API** hoặc **Service Account** đã tạo. |
| **Save execution data** | (Tùy chọn) Lưu toàn bộ payload vào n8n để debug | - Không cần thay đổi, chỉ bật **Enable** nếu muốn lưu log chi tiết. |

> **Lưu ý:** Đảm bảo **Webhook URL** được sao chép đầy đủ (ví dụ: `https://your-n8n-domain.com/webhook/hotmart-events`) và nhập vào mục **Webhooks** của Hotmart. Kiểm tra bằng công cụ **Postman** hoặc **cURL** trước khi bật thực tế.

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi một payload mẫu từ Hotmart (hoặc dùng Postman) tới webhook. Kiểm tra log của các node, đặc biệt là `Convert timestamp` và `Google Sheets`.  
2. Nếu dữ liệu xuất hiện trong Google Sheet → **Bật** workflow bằng nút **Active** (góc trên bên phải).  
3. Kiểm tra lại trong Hotmart khi có giao dịch thực tế để chắc chắn webhook được gọi thành công.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node Slack hoặc Telegram ngay sau node `Google Sheets` để gửi tin nhắn mỗi khi có giao dịch mới.  
- **Báo cáo hàng ngày**: Dùng node **Cron** + **Google Sheets** → **Email** để gửi báo cáo tổng hợp mỗi sáng.  
- **Lưu log chi tiết**: Kết hợp node **Write Binary File** để lưu JSON raw vào S3 hoặc Google Drive, phục vụ audit.  
- **Xử lý lỗi**: Dùng node **Error Trigger** để nhận thông báo khi webhook trả về lỗi (ví dụ: quota Google Sheets hết).  

### 📌 Kết luận
Với chỉ **6 node** đơn giản, workflow này giúp các sếp **tự động hoá toàn bộ quy trình ghi nhận sự kiện Hotmart** vào Google Sheets, giảm thiểu công việc thủ công, tăng độ chính xác và luôn có dữ liệu thời gian thực để phân tích. Hãy **import ngay**, cấu hình các credentials và để n8n làm việc cho bạn! 🚀