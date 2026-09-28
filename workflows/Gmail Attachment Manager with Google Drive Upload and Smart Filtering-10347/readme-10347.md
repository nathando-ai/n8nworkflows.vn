---
title: "🚀 Quản lý tệp đính kèm Gmail tự động lên Google Drive với n8n"
description: "Tự động trích xuất tệp đính kèm từ Gmail, lọc thông minh theo định dạng file, giải nén file ZIP, lưu trữ lên Google Drive và gửi thông báo qua Slack."
slug: "quan-ly-tep-dinh-kem-gmail-tu-dong-google-drive-n8n"
tags: [n8n, automation, gmail, google-drive, slack, file-management, no-code]
keywords: [n8n workflow, tự động hóa gmail, lưu tệp đính kèm google drive, quản lý file n8n, lọc email thông minh]
---

# 🚀 Quản lý tệp đính kèm Gmail tự động lên Google Drive và lọc thông minh

Các sếp có bao giờ cảm thấy mệt mỏi mỗi khi phải tải thủ công từng tệp đính kèm từ hàng loạt email đến, phân loại chúng theo định dạng rồi lại ì ạch upload lên Google Drive hay chuyển tiếp cho các phòng ban? Việc làm thủ công này không chỉ ngốn rất nhiều thời gian mà còn dễ dẫn đến sai sót, bỏ quên tài liệu quan trọng của đối tác hoặc khách hàng.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow **Gmail Attachment Manager with Google Drive Upload and Smart Filtering** do chuyên gia Ossian Madisson thiết kế. Quy trình này sẽ tự động hóa 100% các thao tác từ lúc email có tệp đính kèm đổ về cho đến khi lưu trữ gọn gàng và báo cáo qua Slack!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công từ khâu nhận email, bóc tách file đến lưu trữ.
- **Lọc thông minh**: Dễ dàng chỉ định người gửi cụ thể và lọc định dạng file (PDF, hình ảnh, ZIP,...) cần xử lý.
- **Xử lý linh hoạt**: Hỗ trợ giải nén file ZIP tự động hoặc phân luồng xử lý riêng cho từng loại file khác nhau.
- **Minh bạch và kiểm soát**: Gửi thông báo tức thì qua Slack ngay khi tệp đã được xử lý và lưu trữ thành công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow vận hành trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và kết nối sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Gmail Credentials**: OAuth2 hoặc App Password để trigger email và đánh dấu đã đọc/lưu trữ.
- **Google Drive Credentials**: Để phân quyền upload file tự động lên thư mục chỉ định.
- **Slack Workspace & Bot Token**: Để nhận thông báo kết quả xử lý.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow từ n8n template, sau đó dán (Paste) trực tiếp vào giao diện n8n Editor của mình hoặc import file JSON tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này là một "khung xương" (skeleton) hoàn hảo để các sếp tùy biến theo nhu cầu thực tế. Hãy chú ý cấu hình các node cốt lõi sau:

- **Trigger on incoming email with attachment (`gmailTrigger`)**: Kết nối tài khoản Gmail của các sếp và cấu hình điều kiện nhận email có đính kèm tệp.
- **Filter based on sender or receiver (`filter`)**: Thiết lập điều kiện lọc (nếu có) để chỉ định rõ email từ những nhà cung cấp hoặc khách hàng cụ thể nào mới được xử lý.
- **Filter based on file type (`filter`)**: Cấu hình bộ lọc theo định dạng tệp (mimeTypes) mà các sếp muốn nhận (ví dụ: chỉ nhận file PDF hoặc hình ảnh).
- **Treat different file types different (`switch`)**: Tùy chỉnh các nhánh rẽ nếu workflow cần xử lý các định dạng file khác nhau theo các cách khác nhau (ví dụ: giải nén file `Decompress zip` nếu là tệp nén).
- **Upload file to Google Drive (`googleDrive`)**: Chọn tài khoản Google Drive và chỉ định chính xác thư mục (Folder ID) mà các sếp muốn lưu file tải lên. (Có thể thay thế bằng node `Post file to webhook` nếu muốn đẩy dữ liệu đi hệ thống khác).
- **Send a message (`slack`)**: Cấu hình credentials Slack và tùy chỉnh nội dung thông báo sẽ gửi về kênh khi hoàn tất.
- **Mark read and archive email (`gmail`)**: Đảm bảo node này được cấu hình đúng để dọn dẹp hộp thư đến (gỡ nhãn/lưu trữ) sau khi xử lý xong email.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi một email mẫu có tệp đính kèm đến Gmail đã kết nối để test thử luồng chạy.
- Sau khi kiểm tra mọi thứ mượt mà, gạt công tắc sang **Active** để workflow tự động chiến đấu 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng lưu trữ đa nền tảng**: Thay vì chỉ lưu Google Drive, các sếp có thể kết hợp thêm node OneDrive, Dropbox hoặc gửi trực tiếp vào bảng Google Sheets để quản lý danh sách file đã nhận.
- **Tích hợp AI tóm tắt tài liệu**: Kết nối thêm OpenAI/Anthropic node sau khi tải file lên Drive để AI đọc nội dung file PDF và gửi bản tóm tắt qua Slack cho các sếp nắm bắt nhanh.
- **Log hệ thống**: Thêm một bước ghi log vào Notion hoặc Airtable để dễ dàng tra cứu lịch sử xử lý file theo thời gian thực.

### 📌 Kết luận
Workflow **Gmail Attachment Manager with Google Drive Upload and Smart Filtering** là trợ thủ đắc lực giúp giải phóng thời gian quản lý tài liệu thủ công cho cá nhân và doanh nghiệp. Hãy cài đặt ngay hôm nay để tối ưu hóa quy trình làm việc của đội ngũ các sếp nhé!