---
title: "🚀 Tự động hóa trích xuất dữ liệu Revit BIM và tạo báo cáo khối lượng tường HTML tương tác"
description: "Hướng dẫn xây dựng workflow n8n thực hiện quy trình ETL tự động chuyển đổi mô hình Revit (RVT) thành báo cáo khối lượng tường dạng HTML tương tác."
slug: "tu-dong-hoa-bao-cao-khoi-luong-revit-bim-n8n"
tags: [n8n, automation, bim, revit, etl, construction]
keywords: [n8n workflow, revit to html, bims automation, etl cad bim, data driven construction]
---

# 🚀 Tự động hóa trích xuất dữ liệu Revit BIM và tạo báo cáo khối lượng tường HTML tương tác

Trong ngành xây dựng và kiến trúc (AEC), việc trích xuất khối lượng vật liệu thủ công từ các mô hình BIM/Revit thường tốn rất nhiều thời gian, dễ xảy ra sai sót và bị cô lập trong các phần mềm chuyên dụng đắt đỏ. 

Workflow n8n này áp dụng quy trình **ETL (Extract, Transform, Load)** chuẩn mực để tự động hóa hoàn toàn từ khâu đọc file Revit, lọc dữ liệu tường (`OST_Walls`), tính toán tổng khối lượng theo chủng loại, cho đến việc xuất ra một báo cáo HTML tương tác cực kỳ chuyên nghiệp mà không cần can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình BIM Data**: Chuyển đổi dữ liệu từ mô hình Revit sang định dạng web có thể đọc hiểu bởi bất kỳ ai.
- **Tiết kiệm hàng giờ đồng hồ**: Không còn phải xuất Excel thủ công, lọc dữ liệu bằng tay hay vẽ biểu đồ so sánh khối lượng.
- **Báo cáo trực quan, chuyên nghiệp**: Dashboard HTML tương tác có sẵn thẻ thống kê (summary cards) và thanh tiến trình (progress bars) trực quan theo từng loại tường (`Type Name`).
- **Ứng dụng tư duy ETL hiện đại**: Đưa dữ liệu BIM ra khỏi vòng cô lập của các phần mềm 3D để tích hợp vào hạ tầng dữ liệu của doanh nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Hệ thống n8n (Self-hosted được khuyến nghị vì cần thực thi lệnh trên hệ điều hành và truy cập ổ đĩa cục bộ).
- Công cụ chuyển đổi Revit (Revit converter) được cài đặt trên môi trường chạy n8n để xuất file RVT sang Excel.
- Thư mục lưu trữ file trên máy chủ để n8n đọc/ghi file (`Setup - Define file paths`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã nguồn JSON.
- Mở giao diện n8n Editor, chọn **Add workflow** -> **Import from File / Clipboard** và dán nội dung vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 14 nodes được chia thành 3 giai đoạn chính:

- **Giai đoạn EXTRACT (`Setup - Define file paths`, `Extract - Run Revit converter`, `Check - Did extraction succeed?`, `Extract - Read Excel file from disk`, `Extract - Parse Excel to data`)**:
  - `Setup - Define file paths`: Cấu hình chính xác đường dẫn thư mục chứa file mô hình Revit (`.rvt`) và đường dẫn lưu file Excel đầu ra trên máy chủ của bạn.
  - `Extract - Run Revit converter`: Node này thực thi lệnh hệ thống (`executeCommand`) để chạy bộ chuyển đổi. Hãy đảm bảo dòng lệnh gọi đúng công cụ converter trên môi trường cài đặt n8n.
  - `Extract - Read Excel file from disk` & `Extract - Parse Excel to data`: Đọc file Excel đã chuyển đổi thành công và phân tích thành dữ liệu cấu trúc dạng JSON cho các bước tiếp theo.

- **Giai đoạn TRANSFORM (`Transform - Filter only OST_Walls`, `Transform - Clean wall data`, `Transform - Group by Type Name & sum Volume`, `Transform - Generate HTML Report`)**:
  - `Transform - Filter only OST_Walls`: Bộ lọc (`IF`) chỉ lấy các bản ghi có danh mục là `OST_Walls` (đối tượng Tường trong Revit).
  - `Transform - Clean wall data` & `Transform - Group by Type Name & sum Volume`: Làm sạch dữ liệu (lấy ID, Type Name, Volume), nhóm theo tên chủng loại (`Type Name`) và tính tổng thể tích (`Volume`) cho từng nhóm.
  - `Transform - Generate HTML Report`: Node JavaScript (`function`) tạo cấu trúc mã HTML kèm CSS nhúng, chuyển hóa dữ liệu số liệu thành các thẻ thống kê và biểu đồ thanh trực quan.

- **Giai đoạn LOAD (`Load - Save HTML Report`, `Success - Final results`)**:
  - `Load - Save HTML Report`: Ghi file (`writeBinaryFile`) nội dung HTML vừa tạo xuống ổ đĩa, sẵn sàng để mở bằng bất kỳ trình duyệt web nào.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Start - Click to begin** (`manualTrigger`) để chạy thử nghiệm (Test Run) với dữ liệu mẫu.
- Kiểm tra kết quả trả về ở các node cuối cùng và file HTML được tạo trên thư mục chỉ định.
- Khi mọi thứ đã chạy mượt mà, bật công tắc **Active** để sẵn sàng sử dụng chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Kết hợp thêm node Telegram hoặc Slack ở cuối workflow để gửi file báo cáo hoặc thông báo ngay khi trích xuất mô hình Revit hoàn tất.
- **Tự động hóa theo lịch**: Thay thế `manualTrigger` bằng `Schedule Trigger` để n8n tự động cập nhật báo cáo khối lượng mỗi tuần/mỗi tháng từ thư mục chia sẻ của dự án.
- **Lưu trữ Cloud**: Thay vì lưu HTML trên ổ đĩa local, có thể tích hợp Google Drive hoặc AWS S3 node để tự động đẩy báo cáo lên mây cho các bên liên quan cùng truy cập.

### 📌 Kết luận
Ứng dụng quy trình ETL vào dữ liệu CAD/BIM chính là chìa khóa giúp các kỹ sư và chủ đầu tư tối ưu hóa quản lý khối lượng công trình. Hãy triển khai ngay workflow này để nâng tầm quy trình làm việc BIM của doanh nghiệp các sếp nhé!