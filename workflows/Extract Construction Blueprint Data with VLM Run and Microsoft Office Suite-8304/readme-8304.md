---
title: "🚀 Tự động trích xuất dữ liệu bản vẽ xây dựng từ OneDrive vào Excel với AI"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình đọc bản vẽ xây dựng bằng VLM Run AI và lưu trữ cấu trúc vào Microsoft Excel trên OneDrive."
slug: "tu-dong-trich-xuat-du-lieu-ban-ve-xay-dung-voi-vlm-run-va-excel"
tags: [n8n, automation, vlm-run, microsoft-excel, one-drive, ai-extraction]
keywords: [n8n workflow, trích xuất bản vẽ xây dựng, VLM Run, Microsoft OneDrive, tự động hóa Excel, AI document extraction]
---

# 🚀 Tự động trích xuất dữ liệu bản vẽ xây dựng từ OneDrive vào Excel với AI

Các kỹ sư xây dựng, quản lý dự án và nhân sự vận hành thường xuyên phải đối mặt với núi tài liệu phức tạp: bản vẽ kỹ thuật (blueprint), bản vẽ kiến trúc, sơ đồ điện nước dưới dạng PDF hoặc hình ảnh quét. Việc đọc thủ công, ghi chép thông tin dự án, số hiệu bản vẽ hay thông tin kỹ sư vào file Excel không chỉ tốn hàng giờ đồng hồ mà còn dễ xảy ra sai sót.

Giải pháp? Workflow n8n này sẽ tự động hóa **100%** quy trình từ lúc các sếp tải bản vẽ lên **Microsoft OneDrive**, sử dụng sức mạnh của **VLM Run AI** để đọc hiểu cấu trúc tài liệu, và tự động ghi nhận toàn bộ thông tin bóc tách được vào **Microsoft Excel** mà không cần đụng tay vào bất kỳ dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Nhận diện file mới trên OneDrive và xử lý ngay lập tức mà không cần thao tác thủ công.
- **Trích xuất thông minh:** Biến các bản vẽ phức tạp thành dữ liệu JSON cấu trúc rõ ràng nhờ AI (tên dự án, địa chỉ, mã giấy phép, thông tin kiến trúc sư...).
- **Đồng bộ hóa dữ liệu:** Tự động append (thêm dòng mới) dữ liệu đã bóc tách vào bảng tính Microsoft Excel để tracking, làm báo cáo hoặc kiểm toán.
- **Tối ưu năng suất:** Tiết kiệm 90% thời gian nhập liệu thủ công cho đội ngũ kỹ thuật và hành chính dự án.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản VLM Run** cùng với VLM Run API Key (hỗ trợ category `construction.blueprint`).
- **Tài khoản Microsoft OneDrive & Excel** để cấu hình OAuth2 kết nối với n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sao chép đoạn mã JSON của workflow từ nền tảng n8n và dán trực tiếp vào giao diện n8n Editor của mình (hoặc import file JSON trực tiếp).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 4 nodes chính, các sếp cần chú ý cấu hình kỹ lưỡng các điểm sau:

- **Microsoft OneDrive Trigger:** 
  - Cần kết nối tài khoản thông qua `microsoftOneDriveOAuth2Api`.
  - Chọn thư mục (Folder) trên OneDrive mà hệ thống sẽ theo dõi. Khi có file mới (JPG, PNG, WEBP, PDF) được upload vào thư mục này, trigger sẽ được kích hoạt.
- **Download a file:** 
  - Sử dụng resource/operation `download` để lấy nội dung file vừa được phát hiện từ OneDrive đưa vào bộ nhớ đệm của workflow chuẩn bị gửi cho AI.
- **VLM Run Parsing:** 
  - Cần cung cấp `vlmRunApi` credentials.
  - Node này sẽ gửi file bản vẽ đến VLM Run dưới danh mục `construction.blueprint` để trích xuất các thông tin chi tiết như: Tên dự án, địa chỉ, permit ID, các yếu tố bản vẽ (kích thước, vật liệu), thông tin kiến trúc sư/kỹ sư (tên, số giấy phép, ngày phê duyệt).
- **Append data to sheet:** 
  - Cần kết nối tài khoản `microsoftExcelOAuth2Api`.
  - Chọn đúng file Excel và Worksheet đích.
  - Map các trường dữ liệu JSON mà VLM Run trả về vào các cột tương ứng trong Excel (Ví dụ: Project Details, Document Type, Document Number, Issue Date, Author's Name, Drawing Title Numbers, Revision History...).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử tải một file bản vẽ mẫu lên thư mục OneDrive để test chạy thử.
- Kiểm tra kết quả trên file Excel xem dữ liệu đã được điền chính xác chưa.
- Bật công tắc **Active** để workflow chính thức vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ngay sau bước ghi dữ liệu vào Excel để bắn thông báo về group team dự án mỗi khi có bản vẽ mới được xử lý thành công.
- **Phân loại file lỗi:** Thêm nhánh `If` để kiểm tra nếu file tải lên không đúng định dạng bản vẽ, hệ thống sẽ tự động chuyển vào thư mục "Invalid Files" trên OneDrive.
- **Lưu lịch sử chạy (Logging):** Lưu trữ log trạng thái xử lý vào cơ sở dữ liệu hoặc Google Sheets phụ để dễ dàng kiểm tra khi có sự cố phát sinh.

### 📌 Kết luận
Việc tự động hóa trích xuất dữ liệu bản vẽ xây dựng không chỉ giúp doanh nghiệp tiết kiệm chi phí nhân sự nhập liệu mà còn đảm bảo tính chính xác và kịp thời cho các báo cáo dự án. Hãy cài đặt ngay workflow này để tối ưu hóa quy trình quản lý hồ sơ kỹ thuật của các sếp!