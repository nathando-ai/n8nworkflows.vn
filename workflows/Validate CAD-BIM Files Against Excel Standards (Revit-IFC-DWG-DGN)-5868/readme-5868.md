---
title: "🚀 Tự động hóa kiểm tra file CAD/BIM theo chuẩn Excel (Revit-IFC-DWG-DGN)"
description: "Workflow n8n tự động kiểm tra và chuyển đổi file CAD/BIM sang Excel theo tiêu chuẩn, tiết kiệm 80% thời gian thủ công cho kỹ sư và kiến trúc sư"
slug: "tu-dong-hoa-kiem-tra-file-cad-bim-theo-chuan-excel"
tags: [n8n, automation, no-code, cad, bim, excel]
keywords: [n8n workflow, tự động hóa CAD, kiểm tra file BIM, chuyển đổi CAD sang Excel, quản lý dự án kiến trúc]
---

# 🚀 Tự động hóa kiểm tra file CAD/BIM theo chuẩn Excel (Revit-IFC-DWG-DGN)

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp kỹ sư và kiến trúc sư khi phải kiểm tra thủ công hàng chục file CAD/BIM theo chuẩn Excel. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian kiểm tra thủ công
- Giảm 90% lỗi do nhập liệu sai
- Tự động chuyển đổi file CAD/BIM sang Excel chuẩn
- Tạo báo cáo kiểm tra với mã màu trực quan (🟩 xanh = dữ liệu đúng, 🟥 đỏ = dữ liệu thiếu)
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- File Excel chứa tiêu chuẩn kiểm tra (validation rules)
- File CAD/BIM cần kiểm tra (Revit, IFC, DWG, DGN)
- Cài đặt phần mềm chuyển đổi CAD sang Excel (DDC_Exporter)
- Tài khoản n8n đã cài đặt các node: readBinaryFile, writeBinaryFile, executeCommand
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/5868)
2. Click vào nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Setup - Define file paths"**:
   - Cập nhật đường dẫn đến phần mềm chuyển đổi: `path_to_converter`
   - Cập nhật đường dẫn đến file dự án CAD/BIM: `project_file`

2. **Node "Set Validation Rules Path"**:
   - Cập nhật đường dẫn đến file chứa tiêu chuẩn kiểm tra: `validation_rules_path`

3. **Node "Extract - Run converter"**:
   - Đảm bảo đường dẫn đến file chuyển đổi đúng: `DDC_Exporter_XXXXXXX\datadrivenlibs\RvtExporter.exe`

4. **Node "Open Excel Report1"**:
   - Cập nhật đường dẫn đến chương trình Excel trên máy tính của bạn

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Workflow" để bắt đầu quá trình kiểm tra
2. Kiểm tra kết quả trên báo cáo Excel được tạo tự động
3. Bật Active workflow để chạy tự động khi có file mới

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi email báo cáo khi kiểm tra hoàn thành
- Kết hợp với Slack để thông báo kết quả kiểm tra
- Lưu log kiểm tra vào Google Sheets để theo dõi lịch sử
- Tự động gửi báo cáo hàng tuần cho quản lý dự án

### 📌 Kết luận
Workflow này giúp các sếp kỹ sư và kiến trúc sư tiết kiệm hàng giờ mỗi ngày trong việc kiểm tra và chuyển đổi file CAD/BIM. Hãy áp dụng ngay để nâng cao hiệu suất làm việc và giảm thiểu lỗi trong dự án của bạn!