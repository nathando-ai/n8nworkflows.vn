---
title: "🚀 Tự động tạo & gửi bản tóm tắt buổi Zoom cho khách hàng qua Gmail & Airtable"
description: "Workflow n8n tự động trích xuất thông tin từ email Zoom, lưu vào Airtable và gửi bản tóm tắt cho khách hàng ngay trong hộp thư Gmail."
slug: "tu-dong-tao-gui-ban-tom-tat-zoom-gmail-airtable"
tags: [n8n, automation, no-code, CRM, Gmail, Airtable, Zoom]
keywords: [n8n workflow, tự động hóa, Gmail, Airtable, Zoom meetings, tóm tắt buổi họp]
---

# 🚀 Tự động tạo & gửi bản tóm tắt buổi Zoom cho khách hàng qua Gmail & Airtable

Bạn đã từng phải **đọc hàng chục email Zoom, sao chép thông tin khách hàng, tạo bản tóm tắt và nhập thủ công vào CRM**?  
Công việc này không chỉ tốn thời gian mà còn dễ gây sai sót, khiến bạn mất cơ hội theo dõi và chăm sóc khách hàng kịp thời.  

**Workflow này** sẽ giải quyết toàn bộ quy trình **100 % không cần code**:
- Khi nhận email Zoom mới → trích xuất tự động các trường quan trọng (ngày, thời gian, link, tên khách hàng).  
- Kiểm tra xem khách hàng đã tồn tại trong Airtable chưa → nếu chưa, tạo mới.  
- Gửi email tóm tắt buổi họp tới khách hàng ngay lập tức.  
- Lưu bản ghi buổi họp vào Airtable để quản lý và báo cáo.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động xử lý email và tạo bản tóm tắt trong vài giây.  
- **Độ chính xác cao**: Tránh lỗi nhập liệu thủ công, dữ liệu đồng nhất trong Airtable.  
- **Cá nhân hoá**: Email gửi đi được tùy chỉnh theo thông tin khách hàng và nội dung buổi họp.  
- **Hoạt động liên tục**: Workflow chạy 24/7, không cần can thiệp mỗi khi có email Zoom mới.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Gmail** (được cấp quyền đọc email và gửi email).  
- **API Key Airtable** và **Base ID** của bảng chứa thông tin khách hàng & buổi họp.  
- **Webhook URL (nếu muốn nhận thông báo Slack/Telegram)** – không bắt buộc.  
- **Quyền truy cập internet** cho n8n (để gọi API Gmail & Airtable).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.  
2. Nhấn **Import** → **Upload JSON** và chọn file `Create_Send_Client_Session_Summaries.json` (hoặc copy toàn bộ JSON vào ô **Paste JSON**).  
3. Nhấn **Import**, workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Hành động cần cấu hình | Ghi chú |
|------|------------------------|---------|
| **Gmail Trigger** | Chọn **Credential** của tài khoản Gmail, bật **Watch Emails** và đặt **Label** (ví dụ: `Zoom`) để chỉ theo dõi email Zoom. | Đảm bảo Gmail API đã được bật trong Google Cloud Console. |
| **Extract Fields** (Function) | Không cần thay đổi logic nếu email Zoom có định dạng chuẩn. Nếu email của bạn có mẫu khác, chỉnh sửa đoạn JavaScript để trích xuất đúng `meetingDate`, `meetingLink`, `clientName`, `clientEmail`. | Kiểm tra output trong **Execution Log** để chắc chắn các trường được trả về. |
| **If Exploratory** | Thiết lập điều kiện: `{{ $json["clientEmail"] !== "" }}` để chỉ tiếp tục khi có email khách hàng. | Có thể thêm các điều kiện phụ như kiểm tra ngày họp trong tương lai. |
| **Airtable: Search People** (HTTP Request) | - **Authentication**: API Key. <br> - **URL**: `https://api.airtable.com/v0/{{baseId}}/People?filterByFormula={Email}='{{ $json["clientEmail"] }}'` <br> - **Headers**: `Authorization: Bearer YOUR_API_KEY` | Đảm bảo tên bảng và trường `Email` khớp với cấu trúc Airtable của bạn. |
| **Send Email** (Gmail) | Chọn **Credential** Gmail, cấu hình **To** = `{{ $json["clientEmail"] }}`, **Subject** và **HTML Body** (sử dụng biến từ Extract Fields). | Thêm **CC/BCC** nếu cần gửi bản sao cho đội ngũ bán hàng. |
| **Airtable: Create Session** (HTTP Request) | - **Authentication**: API Key. <br> - **URL**: `https://api.airtable.com/v0/{{baseId}}/Sessions` <br> - **Method**: POST <br> - **Body (JSON)**: <br>```json { "fields": { "Client": "{{ $json["clientName"] }}", "Email": "{{ $json["clientEmail"] }}", "Date": "{{ $json["meetingDate"] }}", "Link": "{{ $json["meetingLink"] }}", "Summary": "{{ $json["summary"] }}" } }``` | Kiểm tra lại tên bảng `Sessions` và các trường (`Client`, `Email`, `Date`, `Link`, `Summary`). |

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi một email Zoom mẫu tới Gmail đã cấu hình, sau đó nhấn **Execute Workflow** để kiểm tra từng node.  
2. Kiểm tra **Airtable** xem bản ghi đã được tạo và **Gmail** nhận được email tóm tắt.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải) để workflow tự động chạy.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack**: Thêm node **Slack** sau `Send Email` để gửi thông báo nội bộ mỗi khi có buổi họp mới.  
- **Lưu log chi tiết**: Dùng node **Write Binary File** để ghi lại toàn bộ payload vào Google Drive hoặc S3, phục vụ audit.  
- **Báo cáo định kỳ**: Tạo một workflow khác chạy hàng tuần, truy vấn Airtable và gửi báo cáo tổng hợp qua Gmail hoặc Google Sheets.  
- **Xử lý đa ngôn ngữ**: Nếu khách hàng quốc tế, mở rộng node `Extract Fields` để nhận diện ngôn ngữ và dịch tự động bằng Google Translate API trước khi gửi email.

### 📌 Kết luận
Với workflow này, các sếp sẽ **bỏ qua mọi công đoạn thủ công** từ việc đọc email Zoom, nhập dữ liệu vào CRM, tới việc soạn email tóm tắt. Kết quả là **tiết kiệm thời gian, giảm lỗi và nâng cao trải nghiệm khách hàng**. Hãy import ngay, cấu hình nhanh và để n8n làm việc thay bạn! 🚀