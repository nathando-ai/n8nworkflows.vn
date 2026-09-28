---
title: "🚀 Tự động tạo Google Slides cá nhân hoá từ CSV cho chiến dịch Cold Outreach"
description: "Giải pháp n8n tự động tạo bài thuyết trình Google Slides dựa trên dữ liệu CSV, giúp các sếp gửi outreach chuyên nghiệp mà không tốn công sức thủ công."
slug: "tu-dong-tao-google-slides-tu-csv-cho-cold-outreach"
tags: [n8n, automation, no-code, marketing, google-slides, google-sheets, google-drive]
keywords: [n8n workflow, tự động tạo slides, cold outreach, Google Slides, CSV]
---

# 🚀 Tự động tạo Google Slides cá nhân hoá từ CSV cho chiến dịch Cold Outreach

Khi các sếp phải chuẩn bị hàng chục, hàng trăm bản thuyết trình cho chiến dịch cold outreach, việc sao chép, chỉnh sửa nội dung thủ công không chỉ tốn thời gian mà còn dễ gây lỗi, mất tính nhất quán.  
Workflow **Create Customized Google Slides Presentations from CSV Data for Cold Outreach** sẽ tự động:

1. Đọc file CSV mới được tải lên Google Drive.  
2. Tạo một bản sao của mẫu Google Slides đã chuẩn bị.  
3. Thay thế các placeholder trong slide bằng dữ liệu cá nhân hoá từ CSV.  
4. Lưu trữ bản thuyết trình mới vào thư mục Lead List và cập nhật ID vào Google Sheet quản lý leads.

Kết quả: các sếp có ngay những bản slide chuyên nghiệp, cá nhân hoá 100 % mà không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ giảm còn vài phút cho mỗi batch slide.  
- **Độ chính xác 100 %**: Không còn lỗi đánh máy hay dữ liệu sai vị trí.  
- **Cá nhân hoá sâu**: Mỗi slide chứa tên, công ty, thông tin liên hệ riêng của lead.  
- **Hoạt động liên tục**: Khi có file CSV mới, workflow tự động chạy mà không cần can thiệp.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Google** với quyền **Google Drive, Google Sheets, Google Slides** (OAuth2).  
- **API Credentials** trong n8n: `googleDriveOAuth2Api`, `googleSheetsOAuth2Api`, `googleSlidesOAuth2Api`.  
- **Mẫu Google Slides** đã chuẩn bị sẵn, có các placeholder (ví dụ: `{{Name}}`, `{{Company}}`).  
- **Thư mục Google Drive**:  
  - `Template Folder` chứa mẫu slide.  
  - `Lead List Folder` sẽ lưu các slide đã tạo.  
- **Google Sheet** để quản lý leads (cột ID slide, tên, email, …).  
- **File CSV** với tiêu đề cột khớp với placeholder trong slide.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n → **Workflows** → **Import**.  
2. Chọn **Upload JSON** và tải file workflow (hoặc copy/paste JSON từ trang gốc).  
3. Nhấn **Import** → Workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là danh sách các node quan trọng và cách cấu hình chúng:

| Node | Mô tả | Cấu hình cần chỉnh |
|------|------|--------------------|
| **New Leads Arrived** (Google Drive Trigger) | Kích hoạt khi có file CSV mới trong `Template Folder`. | - **Folder ID**: ID của thư mục chứa CSV. <br> - **Event**: `File Created`. |
| **File Type?** (Switch) | Kiểm tra định dạng file. | - **Condition**: `File Extension` = `csv`. |
| **Download by ID** (Google Drive) | Tải file CSV về để xử lý. | - **File ID**: `{{$json["id"]}}` (được truyền từ trigger). |
| **Extract Information from CSV file** (Extract From File) | Đọc nội dung CSV thành mảng JSON. | - **File Binary Property**: `data`. |
| **Copy Presentation Template** (Google Drive) | Tạo bản sao của mẫu slide. | - **File ID**: ID của mẫu Google Slides. <br> - **Destination Folder**: ID của `Lead List Folder`. |
| **Create Custom Presentation** (Google Slides) | Thay thế placeholder bằng dữ liệu lead. | - **Presentation ID**: `{{$node["Copy Presentation Template"].json["id"]}}`. <br> - **Replace Text**: Định dạng `{{Placeholder}}` → `{{$json["column_name"]}}`. |
| **Combine Empty New Document with CSV Data** (Merge) | Gộp dữ liệu CSV với ID slide mới. | - **Mode**: `Append`. <br> - **Input 1**: Kết quả từ `Extract Information`. <br> - **Input 2**: Kết quả từ `Copy Presentation Template` (ID slide). |
| **Merge Data for new Lead Document** (Google Sheets – Append) | Ghi dữ liệu lead + ID slide vào Sheet “Lead List”. | - **Spreadsheet ID**: ID của Google Sheet quản lý leads. <br> - **Sheet Name**: `Leads`. |
| **Add Presentation ID to Lead List** (Google Sheets – Update) | Cập nhật cột ID slide cho lead tương ứng. | - **Spreadsheet ID**: Như trên. <br> - **Range**: Dòng chứa lead. |
| **Get all Leads** (Google Sheets – Read) | Đọc toàn bộ danh sách leads (nếu cần báo cáo). | - **Spreadsheet ID**: Như trên. |
| **Create new Sheet** (Google Sheets – Create) | Tạo sheet tạm thời nếu cần lưu dữ liệu trung gian. | - **Spreadsheet ID**: Như trên. <br> - **Sheet Name**: `Temp`. |

**Lưu ý quan trọng**  
- Đảm bảo **Credentials** được gán đúng cho từng node (Google Drive, Sheets, Slides).  
- Kiểm tra **Scope** của OAuth2: cần `https://www.googleapis.com/auth/drive`, `.../spreadsheets`, `.../presentations`.  
- Các placeholder trong mẫu slide phải trùng khớp **đúng** với tiêu đề cột CSV (không có khoảng trắng thừa).  

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** → Chọn **Run Once** để kiểm tra với một file CSV mẫu.  
2. Kiểm tra:  
   - File slide mới xuất hiện trong `Lead List Folder`.  
   - Dòng tương ứng trong Google Sheet được cập nhật ID slide.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải). Workflow sẽ tự động chạy mỗi khi có CSV mới.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node Slack hoặc Telegram sau `Create Custom Presentation` để gửi link slide cho team sales ngay lập tức.  
- **Lưu log vào Google Sheet**: Dùng node Google Sheets (Append) để ghi thời gian chạy, số lượng lead xử lý, và trạng thái lỗi (nếu có).  
- **Báo cáo định kỳ**: Kết hợp node **Cron** + **Google Slides** để tự động tạo báo cáo tổng hợp các slide đã gửi trong tuần.  
- **Kiểm tra duplicate**: Thêm một node **Switch** trước khi tạo slide để kiểm tra xem lead đã có slide chưa (dựa trên ID trong Sheet), tránh tạo bản sao không cần thiết.

### 📌 Kết luận
Với workflow này, các sếp có thể biến một file CSV đơn giản thành hàng loạt bản thuyết trình Google Slides cá nhân hoá, giảm thiểu công sức, tăng độ chính xác và đẩy nhanh tốc độ outreach. Hãy triển khai ngay, kết nối các tài khoản Google, và để n8n làm việc thay bạn! 🚀