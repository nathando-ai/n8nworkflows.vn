---
title: "🚀 Tự Động Giải Nén File ZIP và Tải Lên Google Drive với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động nhận file ZIP từ form, giải nén và tải toàn bộ các tệp tin bên trong lên Google Drive một cách nhanh chóng."
slug: "tu-dong-giai-nen-file-zip-va-tai-len-google-drive"
tags: [n8n, automation, google-drive, file-management, no-code]
keywords: [n8n workflow, giải nén file zip, tự động upload google drive, n8n compression, google drive oauth2]
---

# 🚀 Tự Động Giải Nén File ZIP và Tải Lên Google Drive

Các sếp có bao giờ gặp cảnh khách hàng hoặc đối tác gửi một file `.zip` chứa hàng chục, hàng trăm file nhỏ bên trong, rồi phải thủ công tải về, giải nén từng thư mục rồi lục đục đẩy lên Google Drive chưa? Việc này vừa tốn thời gian, vừa dễ sót file và cực kỳ nhàm chán.

Đừng lo, trong bài viết này, tôi sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ xịn sò do chuyên gia David Soden xây dựng. Workflow này sẽ tự động hóa từ A-Z: nhận file ZIP qua Web Form, lưu trữ tạm, giải nén tự động và đẩy toàn bộ các tệp con lên Google Drive chỉ trong một nốt nhạc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian thủ công**: Không còn cảnh giải nén và upload thủ công từng file.
- **Xử lý hàng loạt mượt mà**: Tự động bóc tách (split out) mọi file ẩn chứa bên trong định dạng nén.
- **Tổ chức khoa học**: Đẩy thẳng dữ liệu lên Google Drive cá nhân hoặc doanh nghiệp một cách ngăn nắp.
- **Vận hành 24/7**: Hoạt động tự động mỗi khi có yêu cầu mới gửi qua Form.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n đang hoạt động ổn định.
- Tài khoản Google Drive và cấu hình **Google Drive OAuth2 API Credentials** trên n8n để cấp quyền upload file.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng mã nguồn JSON của workflow (từ nguồn n8n.io/workflows/9795) để import trực tiếp vào n8n Editor của mình bằng cách copy và dán vào vùng làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 6 nodes chính được chia làm 4 bước xử lý logic rõ ràng:

- **Bước 1: Nhận file (Node `On form submission` - loại `formTrigger`)**
  - Đây là giao diện Form tùy chọn để thu thập file `.zip` từ người dùng. Form này được thiết kế tối giản với một trường dữ liệu (field) duy nhất để nhận file tải lên, giúp đơn giản hóa quy trình.
- **Bước 2: Xử lý cục bộ (Nodes `Read/Write Files from Disk` & `Read/Write Files from Disk1`)**
  - Node này chịu trách nhiệm tải file `.zip` vừa gửi qua form xuống bộ nhớ tạm (local server của n8n) nhằm cung cấp quyền truy cập cục bộ cho bước giải nén kế tiếp.
- **Bước 3: Giải nén & Tách file (Nodes `Compression` & `Split Out`)**
  - Node **Compression** sẽ tiến hành giải nén file `.zip`, mở quyền truy cập vào một hoặc nhiều tệp tin bên trong.
  - Ngay sau đó, node **Split Out** sẽ bóc tách từng file riêng lẻ để hệ thống có thể xử lý hàng loạt (batch process) ở các bước tiếp theo mà không bị nghẽn dữ liệu.
- **Bước 4: Đẩy lên mây (Node `Upload to Google Drive` - loại `googleDrive`)**
  - Tại đây, các sếp cần kết nối tài khoản thông qua **Google Drive OAuth2 API Credentials**.
  - Cấu hình thư mục đích (Folder ID) trên Google Drive nơi các sếp muốn lưu trữ các tệp đã được giải nén.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và tải lên một file `.zip` mẫu qua form để test thử nghiệm xem file đã bay gọn gàng lên Google Drive chưa.
- Sau khi test thành công, gạt công tắc sang **Active** để chính thức đưa vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp thông báo**: Thêm node Telegram hoặc Slack vào cuối chuỗi để nhận thông báo ngay khi quá trình giải nén và upload hoàn tất.
- **Dọn dẹp tệp tạm**: Thêm bước xóa file tạm trên ổ cứng local của n8n sau khi đã upload xong lên Google Drive để tiết kiệm dung lượng server.
- **Phân loại thư mục thông minh**: Dựa vào tên file hoặc định dạng file sau khi giải nén để tự động phân loại vào các thư mục con khác nhau trên Google Drive (Ví dụ: Ảnh vào thư mục Ảnh, Tài liệu vào thư mục Docs).

### 📌 Kết luận
Một workflow tuy nhỏ nhưng giải quyết cực kỳ gọn gàng bài toán xử lý file nén cồng kềnh cho các sếp. Hãy áp dụng ngay vào hệ thống của mình để tối ưu hóa thời gian quản lý tài liệu ngay hôm nay!