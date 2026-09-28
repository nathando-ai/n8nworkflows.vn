---
title: "🏗️ Tự Động Hóa Chuyển Đổi CAD/BIM sang Excel & 3D với DataDrivenConstruction"
description: "Hướng dẫn cài đặt workflow n8n giúp chuyển đổi file Revit, IFC, DWG, DGN sang Excel và mô hình 3D tự động, hỗ trợ QTO và kiểm tra dữ liệu AEC."
slug: "chuyen-doi-cad-bim-sang-excel-3d"
tags: [n8n, automation, bim, cad, construction-tech, aec]
keywords: [n8n workflow, chuyển đổi CAD BIM, tự động hóa xây dựng, QTO, DataDrivenConstruction]
---

# 🏗️ Tự Động Hóa Chuyển Đổi CAD/BIM sang Excel & 3D với DataDrivenConstruction

Trong ngành xây dựng và kỹ thuật (AEC), việc xử lý các file thiết kế như Revit, IFC, DWG hay DGN luôn là một thách thức lớn. Các kỹ sư thường phải mất hàng giờ để xuất dữ liệu, kiểm tra tính nhất quán của mô hình và tạo báo cáo QTO (Quantity Take-Off) thủ công. Sai sót nhỏ trong quá trình nhập liệu có thể dẫn đến những sai lệch chi phí nghiêm trọng.

Workflow n8n này, do **Artem Boiko** (Founder của DataDrivenConstruction.io) phát triển, là giải pháp "chìa khóa trao tay" để tự động hóa quy trình chuyển đổi file CAD/BIM sang định dạng Excel và mô hình 3D. Với chỉ 3 nodes đơn giản, các sếp có thể tích hợp quy trình này vào hệ thống tự động hóa của mình, loại bỏ hoàn toàn thao tác thủ công và đảm bảo dữ liệu đầu ra luôn chính xác, nhất quán.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi xử lý các file CAD/BIM dung lượng lớn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian xử lý:** Tự động hóa quá trình xuất file từ Revit/IFC/DWG sang Excel và 3D, giảm thời gian từ hàng giờ xuống còn vài phút.
- **Độ chính xác cao:** Sử dụng thư viện `datadrivenlibs` chuyên dụng giúp giảm thiểu lỗi khi chuyển đổi định dạng phức tạp.
- **Tích hợp linh hoạt:** Kết nối dễ dàng với các hệ thống quản lý dự án, ERP hoặc gửi báo cáo tự động qua Email/Slack.
- **Hỗ trợ QTO & Kiểm tra:** Dữ liệu xuất ra có cấu trúc rõ ràng, sẵn sàng cho việc tính toán khối lượng và kiểm tra chất lượng mô hình.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Bản self-hosted hoặc cloud.
2. **Thư viện DataDrivenConstruction:** Tải bộ công cụ chuyển đổi từ [GitHub DataDrivenConstruction](https://github.com/datadrivenconstruction/cad2data-Revit-IFC-DWG-DGN-pipeline-with-conversion-validation-qto).
3. **Môi trường chạy lệnh:** Workflow sử dụng node `Execute Command`, do đó server n8n cần có quyền thực thi file `.exe` (thường là Windows Server hoặc WSL trên Linux).
4. **File mẫu:** Một file CAD/BIM (Revit, IFC, DWG, DGN) để test.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/5867](https://n8n.io/workflows/5867) và copy JSON.
2. Trong n8n Editor, chọn **Import from URL** hoặc **Import from File** và dán JSON vào.
3. Workflow sẽ hiển thị 3 nodes chính: `Manual Trigger`, `Set`, và `Execute Command`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Workflow này hoạt động dựa trên việc gọi lệnh dòng lệnh (CLI) từ thư viện bên ngoài.

**Node 1: `Set` (Cấu hình đường dẫn)**
- Node này dùng để định nghĩa đường dẫn tuyệt đối (absolute path) đến thư mục chứa công cụ chuyển đổi.
- **Hành động:** Mở node `Set`, tìm trường dữ liệu chứa đường dẫn.
- **Chỉnh sửa:** Thay thế đường dẫn mặc định bằng đường dẫn thực tế trên server của các sếp.
  - Ví dụ: `C:\Users\YourUser\Downloads\DDC_Exporter_1234567`
  - *Lưu ý:* Đảm bảo đường dẫn không chứa khoảng trắng nếu có thể, hoặc bọc trong dấu nháy kép.

**Node 2: `Execute Command` (Thực thi chuyển đổi)**
- Node này chạy lệnh để thực hiện việc chuyển đổi file.
- **Hành động:** Mở node `Execute Command`.
- **Chỉnh sửa lệnh:**
  - Lệnh mặc định có thể trỏ trực tiếp vào file `.exe`. Tuy nhiên, theo ghi chú của tác giả, nếu gặp lỗi, các sếp **BẮT BUỘC** phải sửa đường dẫn để trỏ vào thư mục `datadrivenlibs`.
  - **Sai (Gây lỗi):** `"DDC_Exporter_XXXXXXX\XxxExporter.exe"`
  - **Đúng (Khuyến nghị):** `"DDC_Exporter_XXXXXXX\datadrivenlibs\XxxExporter.exe"`
  - Các sếp cần thay `XxxExporter.exe` bằng tên file thực tế tương ứng với định dạng đầu vào (ví dụ: `RevitExporter.exe`, `IFCExporter.exe`, `DWGExporter.exe`).
  - Thêm các tham số cần thiết sau file `.exe` (ví dụ: đường dẫn file input, đường dẫn output, tên sheet Excel...). Tham khảo README trong thư mục GitHub để biết cú pháp lệnh chính xác cho từng loại file.

**Node 3: `When clicking ‘Test workflow’`**
- Đây là trigger thủ công. Các sếp có thể thay thế bằng `Webhook` hoặc `Cron` nếu muốn tự động hóa hoàn toàn khi nhận file mới.

#### 3. Kích hoạt ⚡️
1. **Test Run:** Nhấn nút **Test workflow**.
2. Kiểm tra output: Đảm bảo không có lỗi trong node `Execute Command`. Nếu có lỗi, kiểm tra lại đường dẫn trong node `Set` và cú pháp lệnh trong node `Execute Command`.
3. **Active:** Sau khi test thành công, bật công tắc **Active** để workflow sẵn sàng nhận dữ liệu.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa đầu vào:** Thay vì trigger thủ công, các sếp có thể thêm node `Google Drive Trigger` hoặc `Email Trigger` để tự động lấy file CAD/BIM khi có file mới được upload hoặc gửi email.
- **Gửi báo cáo tự động:** Thêm node `Send Email` hoặc `Slack` sau node `Execute Command` để gửi file Excel vừa tạo cho đội ngũ kỹ sư hoặc quản lý dự án.
- **Lưu trữ lịch sử:** Kết nối với `S3` hoặc `Google Drive` để lưu trữ các file Excel và mô hình 3D đã chuyển đổi, tạo thành kho dữ liệu trung tâm.
- **Kiểm tra chất lượng (Validation):** Workflow gốc có hỗ trợ kiểm tra dữ liệu. Các sếp có thể thêm logic để cảnh báo nếu file đầu vào không hợp lệ trước khi chạy lệnh chuyển đổi, tránh lãng phí tài nguyên server.

### 📌 Kết luận
Việc chuyển đổi dữ liệu CAD/BIM sang định dạng dễ sử dụng như Excel là bước nền tảng cho mọi quy trình quản lý dự án xây dựng hiện đại. Với workflow n8n này, các sếp có thể loại bỏ hoàn toàn công đoạn thủ công, tăng tốc độ phản hồi và đảm bảo độ chính xác của dữ liệu QTO.

Hãy bắt đầu ngay hôm nay để trải nghiệm sự khác biệt mà tự động hóa mang lại cho ngành AEC. Nếu các sếp thấy công cụ hữu ích, đừng quên **star** repository trên [GitHub](https://github.com/datadrivenconstruction/cad2data-Revit-IFC-DWG-DGN-pipeline-with-conversion-validation-qto) để ủng hộ cộng đồng phát triển!