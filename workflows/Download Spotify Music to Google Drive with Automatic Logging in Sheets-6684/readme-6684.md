---
title: "🚀 Tự động tải nhạc Spotify lưu vào Google Drive và ghi log qua n8n"
description: "Xây dựng hệ thống tự động tải nhạc từ Spotify bằng URL, tự động lưu trữ file vào Google Drive và ghi log chi tiết trạng thái thành công/thất bại vào Google Sheets."
slug: "tu-dong-tai-nhac-spotify-google-drive-n8n"
tags: [n8n, automation, no-code, spotify, google-drive, google-sheets]
keywords: [n8n workflow, tải nhạc spotify tự động, lưu nhạc spotify google drive, n8n google sheets logging]
---

# 🚀 Tự động tải nhạc Spotify lưu vào Google Drive và ghi log qua Google Sheets

Các sếp có bao giờ cảm thấy phiền phức khi mỗi lần muốn tải một bài hát yêu thích từ Spotify về máy để nghe offline lại phải qua quá trình tìm kiếm, sử dụng các bên thứ ba kém an toàn và quản lý thủ công? Việc này không chỉ tốn thời gian mà còn khiến bộ nhớ máy tính quá tải, khó phân loại.

Giải pháp ở đây là gì? Một hệ thống tự động hóa 100% không cần code (No-code) với n8n! Workflow này sẽ cung cấp cho các sếp một giao diện form đơn giản, tự động gọi API lấy link tải nhạc, lưu file trực tiếp vào Google Drive gọn gàng, đồng thời ghi nhận toàn bộ lịch sử (thành công hay thất bại) vào Google Sheets một cách minh bạch.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Chỉ cần dán link Spotify vào Form, hệ thống tự lo phần còn lại từ tải xuống đến lưu trữ.
- **Lưu trữ đám mây thông minh**: File nhạc tự động đẩy lên Google Drive cá nhân, giải phóng dung lượng thiết bị.
- **Quản lý & Theo dõi chuyên nghiệp**: Mọi lượt tải (thành công/thất bại) đều được ghi log chi tiết vào Google Sheets kèm theo kích thước file (quy đổi sang MB), dung lượng và thời gian.
- **Hoạt động bền bỉ**: Có sẵn các cơ chế xử lý logic nhánh (If) và độ trễ (Wait) giúp hệ thống chạy mượt mà, không sợ quá tải API.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản **Google Drive** và **Google Sheets** (để cấu hình OAuth2 hoặc Google API Credentials).
- API hoặc dịch vụ hỗ trợ tải nhạc Spotify (được tích hợp qua node **HTTP Request**).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này từ nguồn gốc (hoặc tải file JSON) và sử dụng tính năng **Import from JSON** trong giao diện n8n Editor để đưa toàn bộ 12 nodes lên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần chú ý cấu hình các node sau:
- **On form submission**: Node này tạo một giao diện nhập liệu đơn giản. Các sếp có thể tùy chỉnh lại giao diện form (nếu muốn) hoặc sử dụng trực tiếp URL công khai do n8n cung cấp sau khi Active.
- **HTTP Request**: Kiểm tra lại Endpoint của API tải nhạc Spotify (đảm bảo API key hoặc cấu hình request truyền đúng tham số URL bài hát từ form).
- **If & If1 (Link check & Success check)**: Các node điều kiện giúp lọc dữ liệu đầu vào trống và kiểm tra xem API trả về link tải thành công hay không trước khi tiến hành bước tiếp theo.
- **Download music & Code**: Node Code sẽ nhận file nhị phân từ HTTP Request và tự động tính toán, quy đổi kích thước file từ *bytes* sang *MB* để lưu trữ trực quan hơn.
- **Google Drive**: Kết nối tài khoản Google Drive thông qua `googleDriveOAuth2Api`, chọn thư mục đích (Folder ID) trên Drive để lưu các file nhạc tải về.
- **Google Sheets, Google Sheets1, Google Sheets2**: 
  - Kết nối tài khoản Google qua `googleApi`.
  - Chuẩn bị sẵn một Google Sheet với các cột cần thiết (URL bài hát, Link tải, Kích thước MB, Trạng thái thành công/thất bại, Thời gian).
  - Cấu hình thao tác `appendOrUpdate` cho các node ghi log thành công (`Google Sheets`, `Google Sheets1`) và ghi log lỗi (`Google Sheets2`).
- **Wait & Wait1**: Các node tạo khoảng trễ cần thiết giữa các tiến trình tải file nặng, giúp file kịp đồng bộ lên Google Drive trước khi ghi dữ liệu vào bảng tính.

#### 3. Kích hoạt ⚡️
- Nhấp **Execute Workflow** và test thử bằng cách điền một URL bài hát Spotify bất kỳ vào Form để kiểm tra luồng chạy.
- Sau khi kiểm tra dữ liệu trả về Google Drive và Google Sheets chính xác, gạt công tắc sang **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Kết nối thêm node Telegram hoặc Slack ở nhánh thành công/thất bại để nhận thông báo tức thì về điện thoại mỗi khi có bài hát mới được tải về.
- **Tự động tạo thư mục theo nghệ sĩ**: Sử dụng thêm node Code để phân tích tên nghệ sĩ từ link Spotify và tự động tạo thư mục riêng trên Google Drive cho từng ca sĩ.
- **Báo cáo định kỳ**: Thiết lập thêm Schedule Trigger để gửi báo cáo tổng hợp danh sách nhạc đã tải trong tuần qua email.

### 📌 Kết luận
Với workflow n8n này, việc sưu tầm và quản lý kho nhạc Spotify của các sếp nay đã được tự động hóa hoàn toàn gọn gàng trên Google Drive và Google Sheets. Triển khai ngay hôm nay để tối ưu hóa thời gian của mình nhé các sếp!