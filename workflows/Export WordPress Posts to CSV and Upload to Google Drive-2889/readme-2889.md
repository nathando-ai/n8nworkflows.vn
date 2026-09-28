---
title: "🚀 Tự động xuất bài viết WordPress ra file CSV và lưu trữ trực tiếp lên Google Drive"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy toàn bộ bài viết từ WordPress, chuyển đổi thành định dạng CSV gọn gàng và lưu trữ an toàn lên Google Drive chỉ với vài cú click."
slug: "export-wordpress-posts-to-csv-and-upload-to-google-drive"
tags: [n8n, automation, no-code, wordpress, google-drive, marketing]
keywords: [n8n workflow, export wordpress to csv, upload to google drive, tu dong hoa wordpress, n8n viet nam]
---

# 🚀 Tự động xuất bài viết WordPress ra file CSV và lưu trữ trực tiếp lên Google Drive

Các sếp làm content, SEO hay quản trị website WordPress chắc hẳn đã quá quen thuộc với việc phải thủ công export từng danh sách bài viết, copy số liệu để làm báo cáo hoặc lưu trữ backup. Việc này không chỉ tốn thời gian, nhàm chán mà còn dễ bỏ sót dữ liệu khi website ngày càng phát triển.

Giải pháp là gì? Hãy để workflow **Export WordPress Posts to CSV and Upload to Google Drive** lo thay các sếp! Quy trình tự động hóa này sẽ quét toàn bộ bài viết từ trang WordPress của các sếp, chuyển đổi chúng thành một file CSV ngăn nắp và tự động đồng bộ thẳng lên thư mục Google Drive một cách mượt mà.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Không cần copy-paste thủ công hay dùng các plugin cồng kềnh.
- **Báo cáo chuyên nghiệp:** Dữ liệu bài viết được chuẩn hóa vào file CSV, sẵn sàng để phân tích trên Excel hoặc Google Sheets.
- **Backup dữ liệu tự động:** Lưu trữ bản sao bài viết an toàn trên đám mây Google Drive.
- **Linh hoạt tùy chỉnh:** Dễ dàng lọc bớt hoặc thêm thắt các trường dữ liệu (tiêu đề, ngày đăng, trạng thái, đường dẫn...) theo nhu cầu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Tài khoản WordPress:** Cần có quyền truy cập (API Key/Application Password hoặc thông tin đăng nhập REST API).
- **Tài khoản Google:** Có quyền truy cập vào Google Drive để tạo file.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ mã JSON của workflow này dán trực tiếp vào giao diện làm việc của n8n (n8n Editor).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 5 nodes cơ bản, các sếp cần tập trung cấu hình kỹ các node sau:

- **Get Wordpress Posts (`wordpress`):** 
  - Kết nối tài khoản WordPress của các sếp bằng cách chọn **Credentials** (`wordpressApi`). 
  - Đảm bảo các thông số kết nối (URL trang web, Username và Application Password) chính xác để n8n có quyền lấy danh sách bài viết (`getAll`).
- **Adjust Fields (`set`):** 
  - Node này giúp lọc và tinh chỉnh các trường thông tin của bài viết trước khi xuất file. 
  - Các sếp có thể bấm vào node này để thêm hoặc bớt các trường dữ liệu tùy ý (ví dụ: ID bài viết, tiêu đề, ngày tạo, slug...).
- **Convert to CSV File (`convertToFile`):** 
  - Node này tự động nhận dữ liệu dạng JSON từ bước trên và đóng gói thành một file `.csv` hoàn chỉnh mà không cần code phức tạp.
- **Upload to Google Drive (`googleDrive`):** 
  - Chọn **Credentials** Google API (`googleApi`) của các sếp.
  - Chọn thư mục đích trên Google Drive nơi file CSV sẽ được lưu trữ tự động.

#### 3. Kích hoạt ⚡️
- Bấm nút **Test workflow** (`When clicking ‘Test workflow’`) để chạy thử nghiệm xem file CSV đã được tạo và đẩy lên Google Drive thành công chưa.
- Kiểm tra lại trên Google Drive của các sếp. Nếu mọi thứ đã mượt mà, hãy gạt công tắc sang chế độ **Active** để hệ thống tự động chạy theo lịch trình (nếu cài đặt cron/schedule).

### ✍️ Mẹo & gợi ý nâng cao
Để workflow trở nên "lợi hại" hơn, các sếp có thể mở rộng thêm một chút:
- **Thêm thông báo:** Kết nối thêm node Telegram hoặc Slack để nhận thông báo ngay khi file CSV bài viết đã được đẩy lên Google Drive thành công.
- **Lên lịch tự động:** Thay thế node `Manual Trigger` bằng node `Schedule Trigger` để n8n tự động xuất báo cáo bài viết mỗi tuần hoặc mỗi tháng một lần mà không cần sờ tay vào.
- **Kết hợp Google Sheets:** Thay vì chỉ lưu file CSV trên Drive, có thể đẩy trực tiếp vào Google Sheets để team marketing dễ dàng theo dõi trực tuyến.

### 📌 Kết luận
Chỉ với vài bước cấu hình đơn giản trên n8n, các sếp đã sở hữu ngay một trợ thủ tự động hóa đắc lực giúp quản lý và backup dữ liệu bài viết WordPress. Triển khai ngay thôi các sếp ơi!