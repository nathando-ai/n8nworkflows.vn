---
title: "🚀 Tự Động Hóa Phát Hành Séc Số Với OnlineCheckWriter & n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n để tạo và gửi séc số (digital checks) qua API OnlineCheckWriter. Giải pháp không cần code, tự động hóa quy trình thanh toán."
slug: "tu-dong-hoa-phat-hanh-sec-so-onlinecheckwriter"
tags: [n8n, automation, no-code, onlinecheckwriter, payment-automation, api-integration]
keywords: [n8n workflow, tự động hóa thanh toán, onlinecheckwriter api, phát hành séc số, n8n payment]
---

# 🚀 Tự Động Hóa Phát Hành Séc Số Với OnlineCheckWriter & n8n

Trong môi trường kinh doanh hiện đại, việc xử lý thanh toán thủ công thông qua séc giấy hoặc nhập liệu thủ công vào các hệ thống ngân hàng không chỉ tốn thời gian mà còn tiềm ẩn rủi ro sai sót cao. Đặc biệt, với các doanh nghiệp cần phát hành nhiều séc cho nhà cung cấp hoặc nhân viên, quy trình thủ công trở thành một "nút thắt cổ chai" lớn.

Workflow **Create Digital Checks with OnlineCheckWriter using Forms** chính là giải pháp "cứu tinh" cho vấn đề này. Bằng cách kết hợp sức mạnh của n8n với API của OnlineCheckWriter (OCW), các sếp có thể xây dựng một hệ thống tự động hóa 100% để thu thập thông tin người nhận, xác minh dữ liệu và phát hành séc số chỉ với vài cú click chuột, hoàn toàn không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa quy trình thanh toán:** Loại bỏ hoàn toàn thao tác nhập liệu thủ công vào hệ thống ngân hàng hoặc phần mềm kế toán.
- **Giảm thiểu sai sót:** Dữ liệu được định dạng chuẩn JSON và xác minh trước khi gửi đi, đảm bảo thông tin người nhận và số tiền chính xác tuyệt đối.
- **Truy xuất nguồn gốc dễ dàng:** Mỗi séc phát hành đều có ID duy nhất, giúp các sếp dễ dàng theo dõi trạng thái giao dịch trên nền tảng OCW.
- **Mở rộng linh hoạt:** Workflow có thể dễ dàng tích hợp thêm vào các quy trình phức tạp hơn (ví dụ: tự động phát hành séc khi có hóa đơn mới trong ERP).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Đã cài đặt và chạy (Self-hosted hoặc Cloud).
2. **Tài khoản OnlineCheckWriter (OCW):**
   - **API Key:** Lấy từ dashboard của OCW.
   - **Bank Account ID:** ID của tài khoản ngân hàng đã được xác minh trên OCW.
   - **Account Name:** Tên hiển thị cho tài khoản ngân hàng.
3. **Kiến thức cơ bản về n8n:** Biết cách import workflow và cấu hình credentials.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** hoặc **Import from File**.
3. Dán link workflow gốc: `https://n8n.io/workflows/8006` hoặc tải file JSON về và import.
4. Sau khi import, các sếp sẽ thấy 4 node chính: `OCW API Configuration`, `Check Details Form`, `Send Check via OCW API`, và `Success Response1`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Workflow này sử dụng cơ chế **Form Trigger** để thu thập dữ liệu. Các sếp cần chú ý cấu hình các node sau:

**A. Node: `OCW API Configuration` (formTrigger)**
Đây là node khởi đầu quy trình. Nó tạo ra một form web để người dùng nhập thông tin cấu hình API.
- **Path:** Mặc định là `e4f29ca4-5982-42ae-950c-e4d1d7b10a93`. Các sếp có thể đổi path này cho dễ nhớ (ví dụ: `ocw-config`).
- **Mục đích:** Form này thu thập `API Key`, `Bank Account ID`, và `Account Name`. Thông tin này sẽ được lưu trữ trong context của workflow để sử dụng cho các bước sau.

**B. Node: `Check Details Form` (form)**
Node này tạo form thu thập thông tin chi tiết của séc.
- Các trường bắt buộc: Tên người nhận (Payee), Địa chỉ, Số tiền, Ngày phát hành.
- Các trường tùy chọn: Ghi chú (Memo), Mã tham chiếu (Reference).
- **Lưu ý:** Đảm bảo các trường validation được cấu hình đúng để tránh gửi dữ liệu rác lên API.

**C. Node: `Send Check via OCW API` (httpRequest)**
Đây là node quan trọng nhất, nơi thực hiện việc gọi API để phát hành séc.
- **Method:** POST.
- **URL:** Mặc định trỏ đến endpoint test của OCW. **CẢNH BÁO:** Trước khi đưa vào production, các sếp **BẮT BUỘC** phải thay đổi URL sang endpoint production của OnlineCheckWriter.
- **Authentication:** Sử dụng **Bearer Token**.
  - Token được lấy từ trường `API Key` mà người dùng đã nhập ở bước `OCW API Configuration`.
- **Body (JSON):**
  - Dữ liệu được định dạng theo chuẩn JSON yêu cầu của OCW.
  - Các trường `bankAccountId`, `payeeName`, `payeeAddress`, `amount`, `issueDate` sẽ được ánh xạ từ dữ liệu form.
- **Timeout:** 30 giây (đủ cho hầu hết các giao dịch).
- **On Fail:** Được cấu hình là "Continue" để workflow không bị crash nếu có lỗi, thay vào đó sẽ xử lý lỗi ở bước phản hồi.

**D. Node: `Success Response1` (respondToWebhook)**
Node này gửi phản hồi lại cho người dùng sau khi séc được phát hành.
- Nội dung phản hồi bao gồm:
  - **Check ID:** Mã định danh của séc.
  - **Trạng thái:** Thành công hay thất bại.
  - **Chi tiết:** Số tiền, tên người nhận.
  - **Link theo dõi:** Link để xem trạng thái séc trên dashboard OCW.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Nhấn nút **Execute Workflow**.
   - Một form web sẽ mở ra. Nhập thông tin API Key và Bank Account ID (dùng dữ liệu test nếu có).
   - Tiếp theo, nhập thông tin người nhận và số tiền.
   - Kiểm tra xem node `Send Check via OCW API` có trả về mã 200 (Success) không.
2. **Bật Active:**
   - Sau khi test thành công, nhấn nút **Active** ở góc trên bên phải.
   - Copy link webhook của node `OCW API Configuration` để chia sẻ cho nhân viên hoặc tích hợp vào hệ thống nội bộ.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp với Email/Slack:** Thêm node `Send Email` hoặc `Slack` sau node `Send Check via OCW API` để tự động gửi thông báo cho người nhận séc hoặc lưu log vào kênh làm việc.
- **Lưu trữ lịch sử:** Thêm node `Google Sheets` hoặc `Airtable` để lưu lại toàn bộ lịch sử phát hành séc (ngày, người nhận, số tiền, ID séc) phục vụ cho việc đối soát kế toán.
- **Tự động hóa hoàn toàn:** Thay vì dùng Form Trigger, các sếp có thể thay bằng `Webhook Trigger` hoặc `Cron Trigger` để tự động đọc dữ liệu từ hệ thống ERP/CRM và phát hành séc hàng loạt mà không cần can thiệp thủ công.
- **Xử lý lỗi nâng cao:** Thêm node `IF` sau `Send Check via OCW API` để kiểm tra mã lỗi. Nếu thất bại, gửi cảnh báo cho quản lý thay vì chỉ hiển thị lỗi trên form.

### 📌 Kết luận
Workflow **Create Digital Checks with OnlineCheckWriter** là một ví dụ điển hình cho thấy sức mạnh của n8n trong việc tự động hóa các quy trình tài chính phức tạp. Với chỉ 4 node đơn giản, các sếp đã có thể xây dựng một hệ thống phát hành séc số chuyên nghiệp, chính xác và tiết kiệm thời gian. Hãy áp dụng ngay để nâng cao hiệu suất vận hành doanh nghiệp của mình!