---
title: "🚀 Gộp nhiều file Excel thành 1 file đa Sheet có trang tổng hợp bằng n8n"
description: "Hướng dẫn tự động hóa quy trình gộp hàng loạt file Excel thành một file duy nhất với nhiều Sheet riêng biệt kèm theo trang Summary tổng hợp cực kỳ chuyên nghiệp."
slug: "gop-nhieu-file-excel-thanh-1-file-da-sheet-n8n"
tags: [n8n, automation, no-code, excel, file-processing, javascript]
keywords: [n8n workflow, gộp file excel, multi-sheet excel, tự động hóa excel, nodejs xlsx]
---

# 🚀 Gộp nhiều file Excel thành 1 file đa Sheet có trang tổng hợp bằng n8n

Các sếp có bao giờ cảm thấy mệt mỏi mỗi cuối tháng khi phải thu thập hàng chục file Excel từ các phòng ban, sau đó copy-paste thủ công vào từng sheet, rồi lại lập một trang tổng hợp (summary) báo cáo? Công việc nhàm tẻ này không chỉ ngốn hàng giờ đồng hồ mà còn rất dễ xảy ra sai sót số liệu.

Đừng lo, bài toán này sẽ được giải quyết triệt để 100% tự động với workflow n8n cực kỳ thông minh do tác giả **Simone** xây dựng. Workflow này sẽ tự động đọc toàn bộ file Excel từ thư mục, trích xuất dữ liệu, gộp chung thành một file Excel duy nhất với mỗi file gốc là một Sheet riêng biệt, kèm theo một trang Summary tổng hợp toàn cảnh. Không cần code phức tạp, chạy mượt mà ngay trên hệ thống tự động hóa của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Gom nhóm và xử lý hàng loạt file Excel chỉ bằng 1 cú click hoặc kích hoạt theo lịch trình.
- **Cấu trúc chuyên nghiệp:** Mỗi file nguồn tự động biến thành một Sheet riêng biệt trong file đích, kèm theo trang Summary tổng hợp trực quan.
- **Lọc dữ liệu thông minh:** Tự động làm sạch các dòng trống, chuẩn hóa định dạng dữ liệu JSON trước khi ghi file.
- **Tiết kiệm thời gian:** Thay vì mất hàng giờ đồng hồ thao tác thủ công, hệ thống xử lý xong trong vài giây.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (ưu tiên Self-hosted qua Docker để dễ dàng cấu hình thư mục lưu trữ file và cài đặt thư viện bên ngoài).
- **Thư mục lưu trữ trên Server:** Cần chuẩn bị thư mục `n8n_files/` được mount vào container n8n để đọc và ghi file Excel.
- **Môi trường n8n:** Cho phép sử dụng module ngoài `xlsx` trong các Code Node.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã nguồn JSON của workflow (từ nguồn chia sẻ) và dán trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Vì workflow này sử dụng JavaScript để xử lý file Excel thông qua thư viện bên ngoài, các sếp cần lưu ý cấu hình kỹ các node sau:

- **Node `Read XLXS Files from Disk` & `Save XLXS to Disk` (readWriteFile):** Đảm bảo đường dẫn thư mục đọc file từ đĩa (ví dụ: `n8n_files/`) và thư mục lưu file kết quả (`n8n_files/output/`) đã được map chính xác với thư mục trên máy chủ Docker của các sếp.
- **Node `XLSX to Json List` (extractFromFile):** Cấu hình thao tác (`operation`) là `xlsx` để bóc tách dữ liệu thô từ từng file Excel thành danh sách JSON chuẩn xác.
- **Node `Create Multi-Sheet Excel` & `Collect and Process Data` (code):** 
  - Các node này sử dụng thư viện `xlsx` của Node.js để tạo file Excel đa sheet.
  - **⚠️ CỰC KỲ QUAN TRỌNG:** Để các Code Node này chạy được, các sếp bắt buộc phải cấu hình môi trường Docker cho n8n như sau:
    1. Thêm biến môi trường vào file `docker-compose.yml` hoặc `.env`:
       ```yaml
       NODE_FUNCTION_ALLOW_EXTERNAL=xlsx
       ```
    2. Nếu build lại image Docker, hãy tạo một file `Dockerfile` với nội dung:
       ```dockerfile
       FROM n8nio/n8n:latest
       USER root
       RUN npm install xlsx
       ENV NODE_FUNCTION_ALLOW_EXTERNAL=xlsx
       ENV NODE_PATH=/home/node/node_modules
       USER node
       ```

#### 3. Kích hoạt ⚡️
- Đưa các file Excel mẫu vào thư mục `n8n_files/`.
- Nhấn nút **When clicking ‘Execute workflow’** để chạy thử nghiệm thủ công (Manual Trigger).
- Kiểm tra thư mục `n8n_files/output/` xem file Excel tổng hợp đã xuất hiện và đúng định dạng chưa.
- Sau khi test thành công, các sếp có thể thay thế node Trigger thủ công bằng *Schedule Trigger* (chạy định kỳ hàng tuần/tháng) hoặc *Webhook* để hệ thống tự động chạy ngầm.

### ✍️ Gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Thêm một node gửi thông báo về chat nội bộ ngay khi file Excel tổng hợp được tạo thành công kèm theo đường dẫn tải file.
- **Tự động gửi Email:** Kết hợp node Gmail hoặc SMTP để tự động gửi báo cáo tổng hợp này đến Ban Giám đốc hoặc các trưởng bộ phận đúng hạn.
- **Lưu trữ Cloud:** Thay vì lưu trên ổ cứng VPS, có thể bổ sung các node đẩy file trực tiếp lên Google Drive, OneDrive hoặc Dropbox để tiện chia sẻ.

### 📌 Kết luận
Workflow gộp nhiều file Excel thành file đa Sheet kèm trang Summary này là một "vũ khí" tối ưu hóa văn phòng cực kỳ mạnh mẽ. Chỉ cần thiết lập một lần, các sếp sẽ giải phóng bản thân khỏi những thao tác Excel thủ công nhàm chán mỗi kỳ báo cáo. Áp dụng ngay hôm nay để tối ưu hóa hiệu suất doanh nghiệp nhé!