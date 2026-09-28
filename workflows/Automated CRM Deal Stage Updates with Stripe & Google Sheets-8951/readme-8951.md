---
title: "🚀 Tự Động Cập Nhật Giai Đoạn Deal CRM Từ Stripe & Google Sheets"
description: "Workflow n8n tự động đồng bộ hóa hóa đơn đã thanh toán từ Stripe, tra cứu khách hàng trên Google Sheets và cập nhật trạng thái Deal thành 'Closed' trong CRM mà không cần code."
slug: "tu-dong-cap-nhat-deal-crm-stripe-google-sheets"
tags: [n8n, automation, no-code, stripe, crm, google-sheets]
keywords: [n8n workflow, tự động hóa CRM, stripe integration, google sheets automation, deal stage update]
---

# 🚀 Tự Động Cập Nhật Giai Đoạn Deal CRM Từ Stripe & Google Sheets

Việc theo dõi và cập nhật trạng thái các thương vụ (Deals) trong CRM thường là một gánh nặng lớn cho các đội ngũ kinh doanh và vận hành. Khi một khách hàng thanh toán thành công trên Stripe, nhân viên thường phải mất thời gian để vào hệ thống CRM (như HubSpot, Pipedrive hoặc một bảng tính đơn giản) và thủ công chuyển trạng thái Deal từ "Open" sang "Closed-Won".

Quá trình này không chỉ tốn thời gian mà còn dễ dẫn đến sai sót: quên cập nhật, nhập sai ID, hoặc dữ liệu không đồng bộ giữa hệ thống thanh toán và hệ thống quản lý khách hàng. Workflow n8n này giải quyết triệt để vấn đề đó bằng cách tự động hóa 100% quy trình: nó sẽ quét các hóa đơn đã thanh toán trên Stripe, tìm kiếm thông tin khách hàng tương ứng trên Google Sheets, và tự động cập nhật trạng thái Deal thành "Closed" một cách chính xác và liên tục.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian vận hành:** Loại bỏ hoàn toàn bước nhập liệu thủ công, giúp đội ngũ tập trung vào việc chốt đơn mới thay vì cập nhật dữ liệu cũ.
- **Độ chính xác tuyệt đối:** Dữ liệu được đồng bộ trực tiếp từ nguồn (Stripe) nên không lo sai lệch do con người.
- **CRM luôn cập nhật:** Trạng thái Deal phản ánh chính xác tình trạng thanh toán thực tế, hỗ trợ ra quyết định kinh doanh nhanh chóng.
- **Hoạt động liên tục:** Chạy theo lịch trình (Daily/Hourly) tự động, đảm bảo không bỏ sót bất kỳ giao dịch nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Đã cài đặt và chạy (Self-hosted hoặc Cloud).
2. **Tài khoản Stripe:** Có API Key với quyền đọc (Read) các hóa đơn (Invoices).
3. **Tài khoản Google:** Đã tạo Google Sheet làm bảng CRM tạm thời hoặc bảng theo dõi.
4. **Cấu trúc Google Sheet:** Bảng cần có các cột tiêu chuẩn (sẽ hướng dẫn chi tiết bên dưới).
5. **Credentials trong n8n:**
   - `googleSheetsOAuth2Api`: Kết nối với tài khoản Google.
   - `stripeApi`: Kết nối với tài khoản Stripe.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from File** hoặc **Import from URL**.
3. Dán link workflow gốc hoặc tải file JSON về và import.
4. Workflow sẽ hiện ra với 6 nodes chính đã được kết nối sẵn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần kiểm tra và cấu hình lại các node sau:

**🔹 Node: ⏰ Daily Trigger**
- Mặc định workflow chạy hàng ngày. Các sếp có thể chỉnh lại tần suất (ví dụ: mỗi giờ, mỗi 30 phút) tùy thuộc vào nhu cầu cập nhật dữ liệu của mình.

**🔹 Node: 🔍 Find Customer in CRM Sheet**
- **Credentials:** Chọn credentials `googleSheetsOAuth2Api` đã tạo.
- **Document ID:** Chọn đúng Google Sheet chứa dữ liệu khách hàng.
- **Sheet Name:** Chọn đúng tab chứa danh sách khách hàng.
- **Cấu trúc Sheet (Rất quan trọng):**
  - Cột A: `Stripe Email` (Email khách hàng dùng để thanh toán).
  - Cột B: `HubSpot Deal ID` (hoặc ID Deal của CRM bạn dùng).
  - Cột C: `Pipedrive Deal ID` (nếu dùng Pipedrive).
  - Cột D: `Deal Status` (Trạng thái hiện tại).
- **Lookup Column:** Chọn cột `Stripe Email` để tìm kiếm.
- **Lookup Value:** Gán giá trị từ node trước (thường là email của khách hàng trong hóa đơn Stripe).

**🔹 Node: 💳 Get Paid Invoices from Stripe**
- **Credentials:** Chọn credentials `stripeApi`.
- **URL:** Mặc định là `/v1/invoices?status=paid`. Đảm bảo API key của bạn có quyền truy cập vào endpoint này.
- **Method:** GET.

**🔹 Node: 📋 Split Invoice List**
- Node này tự động tách mảng dữ liệu hóa đơn từ Stripe thành từng item riêng lẻ. Không cần chỉnh sửa gì thêm, chỉ cần đảm bảo nó được kết nối đúng từ node Stripe.

**🔹 Node: 🧹 Clean Data & Mark as Closed**
- Đây là node Code. Mặc định nó sẽ:
  - Loại bỏ trùng lặp (nếu cùng một email xuất hiện nhiều lần).
  - Lọc bỏ các dòng rỗng.
  - Gán giá trị `Deal: Closed` vào trường trạng thái.
- **Tùy chỉnh:** Nếu CRM của các sếp dùng tên giai đoạn khác (ví dụ: `Closed-Won`, `Won`, `Paid`), hãy mở node Code và sửa chuỗi `'Closed'` thành tên giai đoạn tương ứng.

**🔹 Node: ✅ Update CRM Sheet with Closed Deals**
- **Credentials:** Chọn credentials `googleSheetsOAuth2Api`.
- **Document ID & Sheet Name:** Chọn đúng sheet như ở bước tra cứu.
- **Operation:** Chọn `AppendOrUpdate`.
- **Match by:** Chọn cột `Stripe Email` để xác định dòng cần cập nhật.
- **Columns Mapping:**
  - `Stripe Email`: Gán từ input.
  - `HubSpot Deal ID`: Gán từ input (giữ nguyên ID cũ).
  - `Pipedrive Deal ID`: Gán từ input.
  - `Deal Status`: Gán giá trị `Closed` (hoặc giá trị đã tùy chỉnh ở node Code).

#### 3. Kích hoạt ⚡️
1. **Test Run:** Nhấn nút **Execute Workflow** (hoặc chạy từng node) với dữ liệu mẫu.
   - Kiểm tra xem node Stripe có trả về danh sách hóa đơn không.
   - Kiểm tra xem node Google Sheets có tìm thấy khách hàng không.
   - Kiểm tra xem dữ liệu cuối cùng có được cập nhật đúng vào Sheet không.
2. **Bật Active:** Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow chạy tự động theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo:** Thêm node **Slack** hoặc **Telegram** sau bước cập nhật Sheet để gửi thông báo "Deal [Tên khách] đã đóng" cho đội ngũ sales.
- **Lưu Log lịch sử:** Thay vì chỉ cập nhật trạng thái, các sếp có thể thêm một cột `Last Updated Date` và ghi lại thời điểm cập nhật để theo dõi lịch sử.
- **Xử lý lỗi:** Thêm một node **Error Trigger** hoặc **IF** node để xử lý trường hợp khách hàng trong Stripe không có trong Google Sheet (ví dụ: gửi email cảnh báo cho admin).
- **Đa dạng CRM:** Nếu các sếp dùng HubSpot hoặc Pipedrive trực tiếp thay vì Google Sheets, có thể thay thế node Google Sheets bằng các node API chính thức của HubSpot/Pipedrive để cập nhật Deal Stage trực tiếp trên nền tảng đó.

### 📌 Kết luận
Workflow **Automated CRM Deal Stage Updates with Stripe & Google Sheets** là một giải pháp nhỏ nhưng cực kỳ hiệu quả để duy trì sự đồng bộ giữa hệ thống thanh toán và hệ thống quản lý khách hàng. Bằng cách tự động hóa việc cập nhật trạng thái Deal, các sếp không chỉ tiết kiệm thời gian mà còn đảm bảo dữ liệu CRM luôn phản ánh chính xác thực tế kinh doanh. Hãy import và cấu hình ngay hôm nay để trải nghiệm sự khác biệt!