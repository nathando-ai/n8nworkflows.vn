---
title: "🚀 Tự động gửi dữ liệu tới API XMLRPC chỉ với một click"
description: "Workflow n8n giúp các sếp gửi XML tới API XMLRPC, tự động tạo XML, kiểm tra thành công và xử lý phản hồi mà không cần viết code."
slug: "tu-dong-gui-du-lieu-api-xmlrpc"
tags: [n8n, automation, no-code, xmlrpc, marketing, integration]
keywords: [n8n workflow, tự động hóa, XMLRPC, HTTP request, API integration]
---

# 🚀 Tự động gửi dữ liệu tới API XMLRPC chỉ với một click

Khi các sếp phải **đánh tay gõ XML**, tạo request thủ công, rồi lại phải kiểm tra kết quả trả về – công việc tẻ nhạt, dễ sai sót và tiêu tốn rất nhiều thời gian. Đặc biệt trong môi trường marketing, việc đồng bộ dữ liệu lên các hệ thống XML‑RPC (ví dụ: CMS, hệ thống quản lý nội dung, hoặc các nền tảng quảng cáo) thường phải lặp đi lặp lại hàng chục, hàng trăm lần mỗi ngày.

**Workflow này** sẽ giải quyết toàn bộ quy trình:
1. **Tự động tạo XML** dựa trên các tham số cấu hình.  
2. **Gửi request** tới API XMLRPC bằng node `HTTP Request`.  
3. **Kiểm tra** phản hồi có thành công hay không.  
4. **Xử lý** kết quả XML trả về (có thể lưu, gửi email, hoặc chuyển sang hệ thống khác).  

Tất cả chỉ cần **kích hoạt một lần**, không cần viết một dòng code nào ngoài node `Code` để tạo XML.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút/đợt xuống còn vài giây tự động.  
- **Độ chính xác 100 %**: XML được sinh ra bằng script, không còn lỗi cú pháp do nhập tay.  
- **Hoạt động liên tục**: Workflow có thể chạy 24/7, không cần giám sát.  
- **Dễ mở rộng**: Thêm bước gửi thông báo Slack/Telegram hoặc lưu log chỉ bằng một node mới.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n** (cài đặt trên VPS hoặc Docker).  
- **Endpoint URL** của API XMLRPC mà các sếp muốn gọi.  
- **Thông tin xác thực** (nếu API yêu cầu) – thường là Basic Auth hoặc token, sẽ nhập vào `Credentials` của node `HTTP Request`.  
- **Dữ liệu mẫu** (ví dụ: `postId`, `title`, `content`) để cấu hình node `Set` → `Settings`.  
- **Quyền truy cập** để tạo/đọc file log nếu muốn lưu phản hồi.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n → **Workflows** → **Import**.  
2. Chọn **Import from File** và tải lên file JSON của workflow (hoặc copy toàn bộ JSON và dán vào ô **Paste JSON**).  
3. Nhấn **Import** → Workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Vai trò | Cấu hình cần chỉnh |
|------|----------|--------------------|
| **Settings** (Set) | Đặt các biến toàn cục như `apiUrl`, `username`, `password`, `postId`, `title`, `content`. | - Nhập giá trị thực tế của API URL và các trường dữ liệu. |
| **ManualTrigger** | Kích hoạt workflow thủ công (hoặc thay bằng Cron/Trigger tự động). | - Nếu muốn chạy định kỳ, thay node này bằng **Cron** và cấu hình lịch. |
| **PrepareXML** (Code) | Tạo chuỗi XML dựa trên dữ liệu từ `Settings`. | - Kiểm tra đoạn code JavaScript, đảm bảo các biến (`postId`, `title`, `content`) khớp với tên trong node `Settings`. |
| **PostRequest** (HTTP Request) | Gửi XML tới endpoint XMLRPC. | - **Method**: `POST`.<br>- **URL**: `{{$json["apiUrl"]}}` (hoặc nhập trực tiếp).<br>- **Authentication**: chọn **Basic Auth** → nhập `username` & `password` từ `Settings`.<br>- **Headers**: `Content-Type: text/xml`.<br>- **Body**: `Raw` → `{{$node["PrepareXML"].json["xml"]}}`. |
| **IsSuccessful** (If) | Kiểm tra HTTP status code (200) hoặc giá trị trong XML response. | - **Condition**: `{{$json["statusCode"]}}` **equals** `200` (hoặc tùy thuộc vào API trả về). |
| **HandleResponse** (XML) | Parse XML trả về thành JSON để sử dụng tiếp. | - **XML Property**: `{{$node["PostRequest"].json["body"]}}`.<br>- **Options**: bật `Parse Attributes` nếu cần. |
| **Success** (NoOp) | Đường đi khi request thành công – có thể nối tới email, Slack, hoặc lưu DB. | - Kết nối tới các node tiếp theo (ví dụ: **Send Email**). |
| **Error** (NoOp) | Đường đi khi request thất bại – gửi báo cáo lỗi. | - Kết nối tới **Send Email** hoặc **Telegram** để thông báo. |

> **Lưu ý:** Các node `StickyNote` trên canvas chỉ là ghi chú, không ảnh hưởng tới luồng. Bạn có thể xóa hoặc giữ lại để hướng dẫn nội bộ.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn nút **Execute Workflow** → Kiểm tra log của mỗi node, đặc biệt là `PostRequest` và `HandleResponse`.  
2. Nếu mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải).  
3. Đối với chạy tự động, thay `ManualTrigger` bằng **Cron** hoặc **Webhook** tùy nhu cầu.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi thông báo Slack**: Thêm node `Slack` sau `Success` để báo cho team biết dữ liệu đã được đồng bộ.  
- **Lưu log vào Google Sheets**: Dùng node `Google Sheets` để ghi lại `postId`, `status`, `timestamp`.  
- **Retry tự động**: Thêm node `Error Trigger` + `Delay` → `PostRequest` để thử lại khi gặp lỗi tạm thời.  
- **Bảo mật**: Sử dụng **n8n credentials** để lưu `username`/`password` thay vì để trong `Set`.  

### 📌 Kết luận
Với workflow **“Post to an XMLRPC API via the HTTP Request node”**, các sếp có thể **tự động hoá 100 %** quy trình gửi dữ liệu XML tới bất kỳ API XMLRPC nào, giảm thiểu lỗi, tăng tốc độ làm việc và mở rộng dễ dàng. Hãy import ngay, cấu hình các thông tin thực tế và để n8n lo phần còn lại – doanh nghiệp của các sếp sẽ chạy mượt mà hơn bao giờ hết! 🚀