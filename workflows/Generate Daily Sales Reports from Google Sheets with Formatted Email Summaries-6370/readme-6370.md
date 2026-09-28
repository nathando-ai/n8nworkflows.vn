---
title: "🚀 Tự động tạo và gửi báo cáo doanh số hàng ngày từ Google Sheets qua Email"
description: "Hướng dẫn xây dựng workflow n8n tự động đọc dữ liệu từ Google Sheets, xử lý và gửi email báo cáo doanh số hàng ngày một cách chuyên nghiệp và chính xác."
slug: "tu-dong-tao-gui-bao-cao-doanh-so-tu-google-sheets"
tags: [n8n, automation, no-code, google-sheets, crm, email-automation]
keywords: [n8n workflow, tự động hóa doanh số, báo cáo google sheets, gửi email tự động n8n, crm automation]
---

# 🚀 Tự động hóa Báo cáo Doanh số Hàng ngày từ Google Sheets

Các sếp có đang cảm thấy mệt mỏi và mất quá nhiều thời gian mỗi ngày chỉ để tổng hợp số liệu bán hàng từ Google Sheets, định dạng lại bảng biểu rồi thủ công copy-paste vào email gửi cho sếp lớn hoặc đội ngũ quản lý? Việc làm thủ công này không chỉ tẻ nhạt, dễ xảy ra sai sót số liệu mà còn ngốn một lượng lớn thời gian quý giá lẽ ra có thể dùng để chốt sale.

Được thiết kế bởi chuyên gia tự động hóa **Rahul Joshi**, workflow n8n này chính là giải pháp tự động hóa 100% không cần code, giúp các sếp giải phóng hoàn toàn sức lao động, tự động hóa quy trình báo cáo doanh số một cách mượt mà và chuyên nghiệp nhất.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Không còn phải thao tác thủ công mỗi sáng để tổng hợp số liệu.
- **Độ chính xác tuyệt đối:** Dữ liệu được kéo trực tiếp từ Google Sheets và xử lý bằng logic code chuẩn xác, loại bỏ hoàn toàn sai sót do con người.
- **Báo cáo chuyên nghiệp:** Email gửi đi được định dạng đẹp mắt, trực quan, dễ dàng theo dõi các chỉ số kinh doanh cốt lõi.
- **Hoạt động linh hoạt:** Có thể kích hoạt thủ công khi cần hoặc dễ dàng chuyển đổi sang lịch trình chạy tự động mỗi ngày (Schedule Trigger).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt tay vào "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- Một tài khoản **n8n** (Cloud hoặc Self-hosted).
- File **Google Sheets** chứa dữ liệu bán hàng/doanh số.
- Tài khoản kết nối **Google Sheets Credentials** (OAuth2 hoặc Service Account).
- Tài khoản gửi email (**SMTP**, Gmail Node, hoặc SendGrid/Resend) để cấu hình node `Send email`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ n8n (Link gốc: [n8n Workflow #6370](https://n8n.io/workflows/6370)), sau đó copy nội dung JSON và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 6 nodes chính được bố trí cực kỳ khoa học. Các sếp cần cấu hình các điểm sau:

- **When clicking ‘Execute workflow’ (Manual Trigger):** Node khởi chạy thủ công. Các sếp có thể thay thế bằng node *Schedule Trigger* nếu muốn hệ thống tự động chạy vào một khung giờ cố định mỗi ngày (ví dụ: 8:00 sáng).
- **Read Google Sheet:** Kết nối tài khoản Google của các sếp, sau đó trỏ tới file Google Sheets chứa dữ liệu doanh số và chọn đúng Sheet Name / Range cần đọc.
- **Check Data Exists (If):** Node kiểm tra xem Google Sheets có dữ liệu trả về hay không, đảm bảo hệ thống không bị lỗi khi bảng số liệu trống.
- **Format Report & No Data Handler (Code):** Các đoạn mã JavaScript bên trong các node này sẽ giúp định dạng lại dữ liệu thô thành một bản báo cáo hoàn chỉnh, hoặc xử lý thông báo trong trường hợp ngày hôm đó không có dữ liệu phát sinh.
- **Send email (Email Send):** Cấu hình thông tin người gửi, người nhận (To, CC), tiêu đề email và nội dung được truyền từ node *Format Report* sang. Đảm bảo đã điền đúng thông tin SMTP hoặc kết nối dịch vụ email tương ứng.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test Step** hoặc **Execute Workflow** ở từng node để kiểm tra xem dữ liệu có chảy qua mượt mà hay không.
- Sau khi test thành công, gạt công tắc **Active** ở góc trên bên phải để workflow chính thức đi vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa hơn nữa quy trình bán hàng, các sếp có thể mở rộng workflow này bằng cách:
- **Tích hợp thêm kênh chat:** Gửi bản tóm tắt doanh số đồng thời lên nhóm **Telegram** hoặc **Slack** của công ty để ban quản lý nắm bắt nhanh chóng.
- **Lưu lịch sử báo cáo:** Thêm một nhánh ghi log các báo cáo đã gửi vào một Sheet lưu trữ riêng biệt để dễ dàng đối soát theo tuần/tháng.
- **Bổ sung biểu đồ trực quan:** Sử dụng các thư viện tạo ảnh hoặc công cụ BI để đính kèm biểu đồ tăng trưởng doanh số trực tiếp vào nội dung email.

### 📌 Kết luận
Việc tự động hóa báo cáo doanh số với n8n không chỉ giúp tiết kiệm thời gian mà còn tạo sự chuyên nghiệp trong quy trình vận hành doanh nghiệp. Hãy áp dụng ngay workflow này để tối ưu hóa hiệu suất làm việc của đội ngũ ngay hôm nay các sếp nhé!