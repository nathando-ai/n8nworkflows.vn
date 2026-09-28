---
title: "🚀 Tự Động Xuất Khách Hàng QuickBooks Hàng Tháng Đến Google Sheets"
description: "Workflow chạy mỗi tháng, lấy danh sách khách hàng từ QuickBooks và ghi vào Google Sheets, giúp doanh nghiệp tiết kiệm thời gian, giảm lỗi nhập liệu và luôn có dữ liệu cập nhật."
slug: "export-khach-hang-quickbooks-hang-thang-google-sheets"
tags: [n8n, automation, no-code, quickbooks, google-sheets, crm]
keywords: [n8n workflow, tự động hóa, QuickBooks, Google Sheets, xuất dữ liệu khách hàng]
---

# 🚀 Tự Động Xuất Khách Hàng QuickBooks Hàng Tháng Đến Google Sheets

Doanh nghiệp thường phải **đối mặt với công việc sao chép danh sách khách hàng** từ QuickBooks sang Google Sheets để phân tích, báo cáo hay chia sẻ với các phòng ban.  
Quá trình này tốn **nhiều giờ đồng hồ**, dễ **sai sót dữ liệu** và **không đồng bộ** khi có thay đổi mới.  

Workflow này sẽ **tự động thực hiện toàn bộ quy trình** vào mỗi ngày 08:00 hàng tháng: lấy toàn bộ khách hàng từ QuickBooks, lọc những trường cần thiết và ghi trực tiếp vào Google Sheets. Không cần viết một dòng code nào – chỉ cần cấu hình một lần và để n8n chạy 24/7.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn thao tác sao chép thủ công mỗi tháng.  
- **Độ chính xác cao**: Dữ liệu được lấy trực tiếp từ QuickBooks, giảm lỗi nhập liệu.  
- **Cập nhật liên tục**: Bảng Google Sheets luôn có dữ liệu mới nhất, sẵn sàng cho báo cáo.  
- **Hoạt động tự động 24/7**: Workflow chạy trên server riêng, không phụ thuộc vào máy cá nhân.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản QuickBooks** với quyền **OAuth2** để tạo credential `quickBooksOAuth2Api`.  
- **Tài khoản Google** (Google Workspace hoặc Gmail) để tạo credential `googleSheetsOAuth2Api`.  
- **Google Sheet** đã tạo sẵn, có ít nhất một tab để ghi dữ liệu và **URL** của spreadsheet.  
- **n8n** đã được cài đặt (Self‑hosted hoặc Cloud) và có quyền **cài đặt các node**: `quickbooks`, `googleSheets`, `set`, `scheduleTrigger`.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. **Tải file JSON** của workflow (từ trang gốc https://n8n.io/workflows/7838) hoặc **sao chép nội dung JSON**.  
2. Vào **n8n Editor**, nhấn **“Import” → “From File”** (hoặc “From Clipboard”) và chọn file JSON.  
3. Workflow sẽ xuất hiện trên canvas với 4 node: `Monthly Export Trigger`, `Fetch Customers from QuickBooks`, `Prepare Customer Data`, `Export to Google Sheets`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cấu hình quan trọng | Hướng dẫn chi tiết |
|------|--------------------|--------------------|
| **Monthly Export Trigger** (scheduleTrigger) | - **Cron**: `0 8 1 * *` (08:00 ngày 1 hàng tháng) <br> - **Timezone**: chọn múi giờ phù hợp (ví dụ: Asia/Ho_Chi_Minh) | Đảm bảo thời gian chạy đúng với nhu cầu báo cáo của doanh nghiệp. |
| **Fetch Customers from QuickBooks** (quickbooks) | - **Credentials**: chọn `quickBooksOAuth2Api` đã tạo. <br> - **Operation**: `Get All` <br> - **Resource**: `Customer` | Kết nối thành công với QuickBooks, kiểm tra **Scope** trong OAuth để có quyền `accounting` và `read`. |
| **Prepare Customer Data** (set) | - Thêm **Fields**: `Period` (giá trị tĩnh: `{{ $now.format("YYYY-MM") }}`), `Id`, `Balance`, `Email`. <br> - **Keep Only Set**: bật **“Keep Only Set”** để loại bỏ các trường không cần. | Sử dụng biểu thức n8n để lấy ngày hiện tại, ví dụ: `{{ $now.format("YYYY-MM") }}`. |
| **Export to Google Sheets** (googleSheets) | - **Credentials**: chọn `googleSheetsOAuth2Api`. <br> - **Operation**: `Append`. <br> - **Spreadsheet ID**: lấy từ URL của Google Sheet (`https://docs.google.com/spreadsheets/d/<SPREADSHEET_ID>/edit`). <br> - **Sheet Name**: tên tab (ví dụ: `Customers`). <br> - **Columns**: ánh xạ các trường `Period`, `Id`, `Balance`, `Email` theo thứ tự cột. | Đảm bảo **Google Sheet** có quyền **Editor** cho tài khoản OAuth đã tạo. Nếu muốn ghi vào tab khác, chỉ cần thay đổi `Sheet Name`. |
| **Sticky Note** (n8n-nodes-base.stickyNote) | Không cần cấu hình, chỉ dùng để ghi chú. | Có thể xóa hoặc giữ lại để hướng dẫn nội bộ. |

> **Lưu ý:** Sau khi cấu hình xong, nhấn **“Execute Node”** từng node để kiểm tra dữ liệu trả về. Nếu có lỗi, mở **Execution Log** và xem chi tiết node có dấu đỏ.

#### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow bằng nút **“Execute Workflow”** và kiểm tra Google Sheet xem đã có dòng dữ liệu mới chưa.  
2. Khi mọi thứ ổn, bật **“Active”** (nút chuyển trạng thái ở góc trên bên phải).  
3. Kiểm tra **Execution History** sau lần chạy tự động đầu tiên (ngày 1 hàng tháng) để chắc chắn không có lỗi.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi báo cáo qua Email**: Thêm node `Email Send` sau `Export to Google Sheets` để gửi file CSV hoặc link sheet cho quản lý.  
- **Thông báo Slack/Telegram**: Dùng node `Slack` hoặc `Telegram` để gửi tin nhắn “Export thành công” kèm số lượng khách hàng mới.  
- **Lưu log vào Database**: Thêm node `Postgres` hoặc `MySQL` để lưu lịch sử xuất, giúp audit và phân tích xu hướng.  
- **Tự động tạo Sheet mới mỗi tháng**: Sử dụng node `Google Sheets` với operation `Create` để tạo tab “YYYY-MM” và ghi dữ liệu vào đó, giúp dữ liệu được phân tháng rõ ràng.

### 📌 Kết luận
Với workflow **Automated Monthly QuickBooks Customer Export to Google Sheets**, các sếp có thể **loại bỏ hoàn toàn công việc sao chép dữ liệu thủ công**, giảm lỗi và luôn có bảng khách hàng cập nhật để phục vụ báo cáo, phân tích và quyết định nhanh chóng. Hãy triển khai ngay hôm nay, để n8n làm việc thay bạn! 🚀