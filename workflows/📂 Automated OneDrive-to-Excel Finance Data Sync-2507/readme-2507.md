---
title: "🚀 Đồng bộ dữ liệu tài chính từ OneDrive sang Excel tự động"
description: "Giải pháp tự động 100% không cần code, đồng bộ dữ liệu CSV mới nhất từ thư mục OneDrive vào bảng tính Excel, giúp doanh nghiệp tiết kiệm thời gian và giảm sai sót."
slug: "dong-bao-dieu-kien-tai-chinh-tong-voi-excel"
tags: [n8n, automation, no-code, finance, excel, onedrive]
keywords: [n8n workflow, tự động hóa, đồng bộ dữ liệu, onedrive to excel, csv import]
---

# 🚀 Đồng bộ dữ liệu tài chính từ OneDrive sang Excel tự động

Bạn đang phải lặp lại công việc nhập dữ liệu CSV từ OneDrive vào Excel mỗi ngày? Mỗi lần thao tác thủ công đều có thể gây sai sót, mất thời gian và làm gián đoạn quy trình làm việc. Workflow này sẽ giúp bạn **đồng bộ dữ liệu 100% tự động** ngay khi có file mới trong thư mục OneDrive, kiểm tra định dạng, trích xuất dữ liệu, làm sạch và cập nhật vào bảng tính Excel – hoàn toàn không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thao tác thủ công, dữ liệu cập nhật ngay khi file mới được tải lên.
- **Độ chính xác cao**: Kiểm tra định dạng CSV, làm sạch dữ liệu trước khi ghi vào Excel.
- **Tự động hóa liên tục**: Chạy 24/7, không phụ thuộc vào lịch trình làm việc của nhân viên.
- **Dễ dàng mở rộng**: Thêm các bước gửi báo cáo qua Slack, lưu log, hoặc gửi email tự động.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Microsoft OneDrive**: Tài khoản OneDrive với quyền truy cập thư mục chứa file CSV.
- **Microsoft Excel**: Tài khoản Office 365 hoặc Excel Online, bảng tính đã được tạo sẵn với sheet cần cập nhật.
- **API Keys / Credentials**:
  - `OneDrive` credential (OAuth2) – cho phép đọc file và metadata.
  - `Excel` credential (OAuth2) – cho phép ghi dữ liệu vào bảng tính.
- **File CSV mẫu**: Định dạng chuẩn, có header, các cột cần nhập vào Excel.

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON từ link gốc: <https://n8n.io/workflows/2507>.
2. Mở **n8n Editor** → `File` → `Import workflow` → chọn file JSON vừa tải.
3. Hoặc copy toàn bộ JSON và dán vào ô `Import workflow` → `Paste JSON`.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Mô tả | Tham số cần cấu hình |
|------|-------|----------------------|
| **Triggers if new file in watched folder** (`microsoftOneDriveTrigger`) | Gửi trigger khi có file mới trong thư mục. | `Folder ID` (đường dẫn thư mục OneDrive). |
| **Checks if it's CSV format** (`if`) | Kiểm tra phần mở rộng file. | `Condition: fileName.endsWith('.csv')`. |
| **Not CSV** (`stopAndError`) | Dừng workflow nếu file không phải CSV. | Không cần cấu hình thêm. |
| **Gets the new file infos** (`microsoftOneDrive`) | Lấy metadata file. | `File ID` (được truyền từ trigger). |
| **Downloads the new file** (`microsoftOneDrive`) | Tải nội dung file. | `File ID` (được truyền từ node trước). |
| **Extracts data from csv** (`extractFromFile`) | Phân tích CSV thành mảng đối tượng. | `Delimiter: ,` (hoặc tùy chỉnh). |
| **Cleans the output** (`code`) | Làm sạch dữ liệu (loại bỏ dòng trống, trim). | `Code` (JavaScript) – ví dụ: `return items.map(i => ({json: {...i.json, amount: parseFloat(i.json.amount)}}));` |
| **Prepares the fields to put in the excel table** (`set`) | Chuẩn bị dữ liệu cho Excel. | `Fields` – mapping từ CSV sang cột Excel. |
| **Updates the excel table** (`microsoftExcel`) | Ghi dữ liệu vào bảng tính. | `Spreadsheet ID`, `Worksheet Name`, `Data` (được truyền từ node `set`). |
| **Logs the update on sheet** (`microsoftExcel`) | Ghi log vào sheet riêng. | `Spreadsheet ID`, `Worksheet Name`, `Data` (định dạng log). |
| **No Operation, do nothing** (`noOp`) | Bỏ qua bước nếu cần. | Không cần cấu hình. |

> **Lưu ý**: Mỗi node `microsoftOneDrive` và `microsoftExcel` cần được gán **credential** tương ứng. Mở node → `Credentials` → chọn hoặc tạo mới.

### 3. Kích hoạt ⚡️

1. **Test run**: Chạy workflow với file CSV mẫu (bấm `Execute workflow`). Kiểm tra logs, dữ liệu đã được ghi vào Excel chưa.
2. **Bật Active**: Sau khi xác nhận chạy đúng, bật `Active` (đèn xanh) để workflow tự động chạy khi có file mới.

## ✍️ Mẹo & gợi ý nâng cao

- **Gửi báo cáo qua Slack**: Thêm node `Slack` sau `Updates the excel table` để gửi tin nhắn khi cập nhật thành công.
- **Lưu log vào Google Sheets**: Thay `Logs the update on sheet` bằng node `Google Sheets` để lưu lịch sử cập nhật.
- **Định kỳ gửi email**: Kết hợp node `Email` để gửi báo cáo hàng ngày/tuần.
- **Thêm bước xác thực dữ liệu**: Sử dụng node `IF` để kiểm tra tính hợp lệ của các trường (ví dụ: `amount > 0`).

## 📌 Kết luận

Workflow **Automated OneDrive-to-Excel Finance Data Sync** giúp các sếp giảm thiểu công việc thủ công, tăng độ chính xác và đảm bảo dữ liệu luôn cập nhật kịp thời. Hãy triển khai ngay, tận hưởng quy trình làm việc mượt mà và hiệu quả hơn!