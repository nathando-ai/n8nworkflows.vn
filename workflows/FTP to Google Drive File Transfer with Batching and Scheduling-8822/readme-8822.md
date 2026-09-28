---
title: "🚀 Tự động đồng bộ file từ FTP lên Google Drive với n8n (Có chia lô & Lịch trình)"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy danh sách file từ máy chủ FTP, xử lý theo lô (batch) và đồng bộ an toàn lên Google Drive 24/7."
slug: "tu-dong-dong-bo-file-ftp-len-google-drive-voi-n8n"
tags: [n8n, automation, no-code, ftp, google-drive, cloud-storage]
keywords: [n8n workflow, ftp to google drive, tự động hóa lưu trữ, n8n tutorial tiếng việt, đồng bộ file tự động]
---

# 🚀 Tự động đồng bộ file từ FTP lên Google Drive với n8n

Các sếp có đang gặp khó khăn khi phải thủ công tải các file từ máy chủ FTP cũ kỹ rồi lại lật đật upload lên Google Drive mỗi ngày? Việc này không chỉ tốn thời gian, dễ sót file mà còn tiềm ẩn rủi ro khi dung lượng file lớn làm nghẽn hệ thống.

Được sáng tạo bởi chuyên gia tự động hóa **Avkash Kakdiya (iTechNotion)**, workflow n8n này chính là giải pháp tự động hóa 100% không cần code giúp các sếp giải quyết triệt để bài toán đồng bộ dữ liệu giữa FTP và Google Drive một cách mượt mà và thông minh.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chạy theo lịch trình định sẵn (Schedule Trigger) mà không cần sự can thiệp thủ công.
- **Xử lý thông minh theo lô (Batch Processing):** Chia nhỏ các file để tải và upload tuần tự, tránh tình trạng quá tải hệ thống hay tràn bộ nhớ (Memory Limit).
- **Giữ nguyên vẹn tên file:** Tên file trên FTP được giữ nguyên khi đẩy lên Google Drive, đảm bảo tính nhất quán của dữ liệu.
- **Hoạt động bền bỉ 24/7:** Giúp đội ngũ tiết kiệm hàng chục giờ làm việc mỗi tháng và loại bỏ hoàn toàn sai sót con người.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
- **Hệ thống n8n:** Đã cài đặt phiên bản n8n (Cloud hoặc Self-hosted).
- **FTP Credentials:** Thông tin kết nối máy chủ FTP (Host, Username, Password, Port).
- **Google Drive Account:** Tài khoản Google để kết nối API thông qua OAuth2.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng mã JSON của workflow, copy và paste trực tiếp vào giao diện n8n Editor của mình. Workflow bao gồm 5 nodes chính liên kết chặt chẽ với nhau:
1. `⏯️ Schedule Trigger`: Khởi động lịch trình tự động.
2. `📂 List Files from FTP`: Quét và lấy danh sách file từ thư mục FTP chỉ định.
3. `🔀 Batch Files`: Chia nhỏ danh sách file để xử lý lần lượt.
4. `⬇️ Download File from FTP`: Tải từng file từ server FTP xuống.
5. `☁️ Upload to Google Drive`: Đẩy file vừa tải lên thư mục Google Drive đích.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `📂 List Files from FTP` & `⬇️ Download File from FTP`:** 
  - Cần cấu hình **FTP Credentials** chính xác với thông tin máy chủ của các sếp.
  - Tại trường `Path` trong node List Files, điền đúng đường dẫn thư mục chứa file trên FTP (ví dụ: `/path/to/your/files`).
  - Tại node Download File, đảm bảo tham số đường dẫn trỏ đúng tên file lấy từ dữ liệu đầu vào (`={{ $json.name }}`).
- **Node `☁️ Upload to Google Drive`:**
  - Kết nối tài khoản Google Drive thông qua **Google Drive OAuth2 API**.
  - Chọn thư mục đích (Folder ID) trên Google Drive nơi các sếp muốn lưu trữ các file đồng bộ.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm với một vài file mẫu xem hệ thống đã nuốt dữ liệu thành công chưa.
- Kiểm tra lại trên Google Drive xem file đã xuất hiện đúng tên chưa.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm thông báo Telegram/Slack:** Gắn thêm node thông báo sau khi upload thành công hoặc khi xảy ra lỗi để nắm bắt tình hình tức thì.
- **Xóa file gốc trên FTP:** Sau khi upload thành công lên Google Drive, có thể bổ sung node xóa file trên FTP để tiết kiệm dung lượng máy chủ lưu trữ cũ.
- **Lưu log vào Google Sheets:** Ghi lại lịch sử thời gian, tên file và trạng thái đồng bộ vào Google Sheets để tiện kiểm toán (Audit Log).

### 📌 Kết luận
Workflow "FTP to Google Drive File Transfer" là một cỗ máy tự động hóa nhỏ gọn nhưng cực kỳ mạnh mẽ, giải quyết trọn gói bài toán di chuyển dữ liệu nặng nhọc. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa vận hành ngay hôm nay!