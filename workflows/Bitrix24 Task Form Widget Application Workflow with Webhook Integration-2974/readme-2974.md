---
title: "🚀 Tự Động Hóa Widget Nút Nút Task Bitrix24 Với n8n (Không Code)"
description: "Hướng dẫn cài đặt và cấu hình workflow n8n để tạo widget nhúng Bitrix24, cho phép nhân viên xem và thao tác task trực tiếp trên website mà không cần đăng nhập CRM."
slug: "widget-task-bitrix24-n8n"
tags: [n8n, bitrix24, automation, no-code, crm, webhook]
keywords: [n8n workflow, bitrix24 integration, task widget, tự động hóa crm, n8n bitrix24]
---

# 🚀 Tự Động Hóa Widget Nút Nút Task Bitrix24 Với n8n (Không Code)

Các sếp đang dùng Bitrix24 làm CRM chắc hẳn đã quen với việc nhân viên phải mở app hoặc website CRM để xem task. Nhưng làm sao để nhân viên có thể xem nhanh thông tin task quan trọng ngay trên website công ty, trong email, hoặc các trang nội bộ khác mà không cần rời khỏi trang hiện tại?

Đây chính là nỗi đau mà workflow **Bitrix24 Task Form Widget Application** giải quyết. Thay vì phải code lại một ứng dụng web phức tạp để nhúng dữ liệu Bitrix24, các sếp chỉ cần dùng n8n để xử lý webhook, lấy dữ liệu task và trả về định dạng HTML/JSON chuẩn. Workflow này hoạt động như một "cầu nối" thông minh, nhận lệnh từ widget phía client, truy vấn Bitrix24 API, và trả về dữ liệu đã định dạng sẵn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và đảm bảo độ trễ thấp cho widget, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Trải nghiệm liền mạch:** Nhân viên xem task Bitrix24 trực tiếp trên website/ứng dụng khác mà không cần đăng nhập lại CRM.
- **An toàn & Kiểm soát:** Dữ liệu được xử lý qua n8n, các sếp có thể thêm logic kiểm tra quyền (permission) trước khi trả dữ liệu.
- **Không cần Code Frontend:** Workflow xử lý toàn bộ logic backend, các sếp chỉ cần nhúng một đoạn code widget nhỏ vào trang web.
- **Tùy biến cao:** Dễ dàng thay đổi cách hiển thị dữ liệu (Format Task Data) hoặc thêm các trường dữ liệu bổ sung từ Bitrix24.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Chạy local hoặc self-hosted.
- **Tài khoản Bitrix24:** Có quyền truy cập API.
- **Bitrix24 API Credentials:** Cần `Portal ID` và `API Token` (hoặc OAuth credentials) để gọi API Bitrix24.
- **Website/Ứng dụng đích:** Nơi các sếp muốn nhúng widget (cần có khả năng gọi POST request đến n8n).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** hoặc **Import from File**.
3. Dán link workflow gốc: `https://n8n.io/workflows/2974` hoặc tải file JSON về và import.
4. Workflow sẽ hiển thị với 21 nodes, bao gồm Webhook, HTTP Request, Code, và các node xử lý dữ liệu.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Workflow này khá phức tạp vì nó xử lý cả quá trình **cài đặt widget** (installation) lẫn **lấy dữ liệu task** (runtime). Các sếp cần chú ý các node sau:

**A. Cấu hình Webhook (Node: `Bitrix24 Handler`)**
- Đây là điểm vào chính. Đảm bảo URL webhook được cấu hình đúng (Production URL nếu chạy trên VPS).
- Path mặc định là `bitrix24/widgethandler.php`. Các sếp có thể đổi path này cho dễ nhớ, ví dụ: `bitrix24-widget`.

**B. Cấu hình Credentials Bitrix24 (Node: `Get Task Data`)**
- Click vào node `Get Task Data`.
- Chọn **Bitrix24 API** credentials đã tạo.
- Kiểm tra tham số `URL` và `Body`. Node này sẽ gọi API Bitrix24 để lấy chi tiết task dựa trên ID task được truyền từ widget.
- *Lưu ý:* Đảm bảo API Token có quyền đọc task (`task.read`).

**C. Xử lý Logic Cài Đặt (Nodes: `Is Installation?`, `Register Placement`, `Save Installation Settings`)**
- Workflow có cơ chế "self-install". Khi widget lần đầu chạy, nó sẽ gửi request để đăng ký vị trí (placement) và lưu cấu hình.
- Node `Save Installation Settings` (type: `readWriteFile`) sẽ ghi file cấu hình vào thư mục của n8n.
- **Quan trọng:** Nếu chạy trên VPS, đảm bảo user n8n có quyền ghi (write) vào thư mục data. Nếu chạy local, kiểm tra đường dẫn file trong node này.
- Node `Register Placement` (type: `httpRequest`) có thể cần chỉnh sửa nếu các sếp muốn lưu thông tin cài đặt vào database thay vì file, hoặc gọi API quản trị khác.

**D. Định dạng Dữ Liệu (Node: `Format Task Data`)**
- Đây là node `function` (hoặc `code` trong các phiên bản n8n mới).
- Tại đây, các sếp có thể tùy biến cách hiển thị dữ liệu task trả về cho widget.
- Ví dụ: Chỉ hiển thị tiêu đề, người phụ trách, deadline, hoặc thêm link xem chi tiết trong Bitrix24.
- *Mẹo:* Dùng `JSON.stringify` hoặc template literals để tạo HTML/JSON sạch sẽ.

**E. Xử lý Lỗi (Node: `Error Response`)**
- Đảm bảo node này trả về thông báo lỗi thân thiện cho widget phía client, tránh để lộ thông tin kỹ thuật nhạy cảm.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Tạo một task mẫu trong Bitrix24.
   - Chạy workflow với dữ liệu mẫu (mock data) mô phỏng request từ widget.
   - Kiểm tra xem node `Task View Response` có trả về dữ liệu đúng không.
2. **Bật Active:**
   - Bật công tắc **Active** ở góc trên bên phải n8n.
   - Copy URL Webhook (Production) để đưa vào code widget phía frontend.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Cache:** Nếu task không thay đổi thường xuyên, các sếp có thể thêm node `Redis` hoặc `Cache` để giảm tải cho Bitrix24 API.
- **Gửi Thông Báo:** Khi có task mới hoặc sắp đến hạn, kết hợp thêm node `Slack` hoặc `Telegram` để gửi cảnh báo cho người phụ trách.
- **Log Hoạt Động:** Thêm node `Google Sheets` hoặc `Database` để log lại ai đã xem task nào, vào lúc nào, phục vụ cho việc phân tích hành vi nhân viên.
- **Bảo Mật:** Thêm node `Verify Token` hoặc kiểm tra IP whitelist trước khi xử lý request để đảm bảo chỉ widget hợp lệ mới được truy cập.

### 📌 Kết luận
Workflow **Bitrix24 Task Form Widget** là một giải pháp tuyệt vời để "mang" Bitrix24 ra khỏi CRM và đưa vào mọi nơi trong hệ sinh thái số của doanh nghiệp. Với n8n, các sếp không cần là lập trình viên frontend để làm được điều này. Hãy thử ngay để trải nghiệm sự tiện lợi của việc xem task chỉ với một cái nhìn!