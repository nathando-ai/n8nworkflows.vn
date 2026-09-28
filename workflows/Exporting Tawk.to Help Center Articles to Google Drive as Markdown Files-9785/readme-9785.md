---
title: "🚀 Tự động xuất bài viết Tawk.to Help Center ra Google Drive dưới dạng Markdown bằng n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động trích xuất toàn bộ bài viết từ Tawk.to Help Center, chuyển đổi sang định dạng Markdown và đồng bộ an toàn lên Google Drive mà không sợ trùng lặp."
slug: "tu-dong-xuat-tawk-to-help-center-ra-google-drive-markdown-n8n"
tags: [n8n, automation, no-code, tawk-to, google-drive, markdown, backup]
keywords: [n8n workflow, tawk.to help center, backup tawk.to to google drive, chuyen doi html sang markdown n8n, tu dong hoa n8n]
---

# 🚀 Tự động xuất bài viết Tawk.to Help Center ra Google Drive dưới dạng Markdown bằng n8n

Việc sao lưu hoặc di chuyển dữ liệu từ trang trợ giúp (Help Center) của Tawk.to sang một kho lưu trữ như Google Drive theo cách thủ công cực kỳ tẻ nhạt và mất thời gian. Các sếp sẽ phải copy từng bài, tạo từng file và dán nội dung, chưa kể việc định dạng HTML bị lỗi hay kiểm tra xem bài nào đã có trên Drive. 

Giải pháp? Workflow n8n này sẽ tự động hóa **100%** quy trình trên: cào dữ liệu từ Tawk.to, bóc tách danh mục, bài viết, chuyển đổi toàn bộ nội dung HTML sang định dạng Markdown gọn gàng và tự động đẩy lên Google Drive, đồng thời thông minh kiểm tra file trùng lặp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 99% thời gian:** Thay vì copy-paste thủ công hàng trăm bài viết, toàn bộ Help Center được đồng bộ chỉ với 1 click.
- **Định dạng chuẩn Markdown (.md):** Giúp lưu trữ nhẹ nhàng, dễ dàng đọc lại hoặc chuyển đổi sang các nền tảng kiến thức khác (Notion, Obsidian, GitHub...).
- **Chống trùng lặp thông minh:** Hệ thống tự động quét Google Drive trước khi tạo file mới, không lo bị rác file hoặc tạo bản sao thừa.
- **Hoạt động tự động:** Dễ dàng mở rộng để chạy định kỳ hàng tuần/tháng nhằm backup tài liệu tự động.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản Google Cloud / Google Drive tích hợp (để lấy Credentials cấp quyền tạo file và thư mục).
- URL trang Tawk.to Help Center của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (hoặc tải file JSON từ nguồn gốc) và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 15 nodes được thiết kế mạch lạc. Các sếp cần chú ý cấu hình các điểm sau:

- **Node `set-website`**: Đây là nơi các sếp điền đường dẫn trang Tawk.to Help Center của doanh nghiệp mình vào biến cấu hình.
- **Các node HTTP Request (`get-website-home`, `website-category`, `website-article`)**: Đảm bảo URL gọi đi khớp với cấu trúc website của các sếp.
- **Node HTML Extraction (`find-categories`, `find-category-articles`, `extract-article-content`)**: Sử dụng selectors chuẩn để bóc tách chính xác tiêu đề, danh mục và nội dung bài viết từ mã HTML của trang.
- **Node `convert-to-markdown`**: Thực hiện phép màu chuyển đổi HTML thô thành cú pháp Markdown sạch sẽ.
- **Node `Search files and folders` & `Create file from text` (Google Drive)**: 
  - Cần kết nối tài khoản Google qua **Google API Credentials**.
  - Cấu hình thư mục đích trên Google Drive (ví dụ: thư mục *“Meu Rastreio - Tutoriais”* trong template gốc) để lưu trữ các file `.md` xuất ra.
- **Node `is-duplicated` (If)**: Kiểm tra xem tên file đã tồn tại trên Drive hay chưa để quyết định bỏ qua hay tạo mới.

#### 3. Kích hoạt ⚡️
- Bấm nút **“Execute Workflow”** tại node `When clicking ‘Execute workflow’` để chạy thử nghiệm với dữ liệu thực tế.
- Kiểm tra kết quả trên Google Drive xem các file Markdown đã được tạo đúng chuẩn chưa.
- Sau khi test mượt mà, gạt công tắc **Active** để hoàn tất.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa theo lịch:** Thay thế node `manualTrigger` bằng `Schedule Trigger` để n8n tự động quét và backup Help Center hàng tuần.
- **Thông báo qua Telegram/Slack:** Thêm một node thông báo kết quả sau khi hoàn tất quá trình đồng bộ để các sếp biết có bao nhiêu bài viết mới được cập nhật.
- **Lưu log vào Google Sheets:** Kết hợp ghi lại lịch sử các bài viết đã đồng bộ thành công vào một bảng tính quản lý.

### 📌 Kết luận
Một workflow cực kỳ thực chiến và hữu ích cho các đội ngũ CSKH, Product hay Content muốn quản lý và sao lưu tài liệu trợ giúp một cách chuyên nghiệp. Hãy triển khai ngay để tối ưu hóa thời gian vận hành cho doanh nghiệp của các sếp!