---
title: "🚀 Tự động hóa Import nhiều file CSV vào Google Sheets với n8n"
description: "Hướng dẫn chi tiết cách sử dụng n8n workflow để xử lý, lọc dữ liệu, loại bỏ trùng lặp và tự động import hàng loạt file CSV vào Google Sheets một cách nhanh chóng."
slug: "import-multiple-csv-to-google-sheets-n8n"
tags: [n8n, automation, no-code, google-sheets, csv, data-processing]
keywords: [n8n workflow, import csv google sheets, tự động hóa n8n, xử lý file csv n8n, google sheets integration]
---

# 🚀 Tự động hóa Import nhiều file CSV vào Google Sheets

Các sếp có đang cảm thấy mệt mỏi mỗi khi nhận được hàng loạt file CSV từ các phòng ban, đối tác hay hệ thống cũ, rồi phải mất hàng giờ mở từng file, copy-paste thủ công vào Google Sheets? Việc này không chỉ tốn thời gian, nhàm chán mà còn cực kỳ dễ xảy ra sai sót, nhầm lẫn dữ liệu.

Đừng lo, giải pháp tự động hóa 100% không cần code với n8n sẽ giúp các sếp giải quyết triệt để bài toán này chỉ trong vài nốt nhạc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Xử lý hàng loạt file CSV cùng lúc thay vì làm thủ công từng file một.
- **Dữ liệu sạch sẽ, chuẩn chỉnh:** Tự động lọc dữ liệu (ví dụ: chỉ giữ lại subscribers), loại bỏ các dòng trùng lặp và sắp xếp theo ngày tháng trước khi đẩy lên.
- **Đồng bộ tập trung:** Toàn bộ dữ liệu được gom về một bảng Google Sheets duy nhất, sẵn sàng cho việc báo cáo và phân tích.
- **Hoạt động linh hoạt:** Có thể kích hoạt thủ công hoặc hẹn giờ chạy tự động định kỳ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản Google có quyền truy cập Google Sheets.
- Thư mục chứa các file CSV cần import trên máy chủ/hệ thống mà n8n có thể truy cập (thông qua node `Read Binary Files`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ thư viện chính thức của n8n (Workflow ID: 1968) hoặc copy đoạn JSON tương ứng và paste thẳng vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 9 nodes phối hợp nhịp nhàng với nhau. Các sếp cần chú ý cấu hình các điểm mấu chốt sau:

- **When clicking "Execute Workflow" (`manualTrigger`):** Node kích hoạt thủ công. Các sếp có thể thay thế bằng node *Schedule Trigger* nếu muốn workflow chạy tự động theo lịch (ví dụ: chạy mỗi tối lúc 12h đêm).
- **Read Binary Files (`readBinaryFiles`):** Trỏ đường dẫn đến thư mục chứa các file CSV trên hệ thống của các sếp.
- **Split In Batches (`splitInBatches`):** Giúp xử lý lần lượt từng file CSV một cách mượt mà, tránh quá tải bộ nhớ (RAM) khi xử lý file dung lượng lớn.
- **Read CSV (`spreadsheetFile`):** Đọc nội dung bên trong từng file CSV đã được đọc dưới dạng binary.
- **Assign source file name (`set`):** Gắn nhãn hoặc thêm cột tên file nguồn vào dữ liệu để dễ dàng truy xuất nguồn gốc sau này.
- **Remove duplicates (`itemLists`):** Cấu hình keyParameters là `removeDuplicates` để lọc bỏ các bản ghi bị lặp lại trong file.
- **Keep only subscribers (`filter`):** Thiết lập điều kiện lọc (ví dụ: `status == subscriber`) để chỉ lấy những dòng dữ liệu thực sự quan trọng.
- **Sort by date (`itemLists`):** Cấu hình keyParameters là `sort` để sắp xếp danh sách theo thứ tự ngày tháng tăng dần/giảm dần.
- **Upload to spreadsheet (`googleSheets`):** 
  - Chọn **Credentials**: Kết nối tài khoản Google Sheets OAuth2 API của các sếp.
  - Cấu hình **Operation**: Chọn `appendOrUpdate` (thêm mới hoặc cập nhật nếu đã tồn tại).
  - Chọn đúng File Spreadsheet và Sheet Name đích mà các sếp muốn đổ dữ liệu vào.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử với một vài file CSV mẫu và kiểm tra kết quả trên Google Sheets.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow chính thức đi vào vận hành tự động.

### ✍️ Nâng cấp & gợi ý mở rộng
- **Gửi thông báo Telegram/Slack:** Thêm một node Slack hoặc Telegram ở cuối workflow để thông báo ngay cho đội ngũ khi quá trình import hoàn tất hoặc gặp lỗi.
- **Lưu trữ file sau khi xử lý:** Kết hợp thêm node di chuyển file CSV (Move File) vào thư mục "Processed" để tránh việc import lại cùng một file ở lần chạy sau.
- **Báo cáo định kỳ:** Tạo thêm một nhánh gửi email tổng kết số lượng dòng dữ liệu đã import thành công vào cuối ngày.

### 📌 Kết luận
Việc tự động hóa quy trình import dữ liệu CSV vào Google Sheets không chỉ giải phóng sức lao động cho đội ngũ vận hành mà còn giúp doanh nghiệp sở hữu nguồn dữ liệu sạch, nhanh chóng và chính xác. Hãy áp dụng ngay vào hệ thống của các sếp nhé!