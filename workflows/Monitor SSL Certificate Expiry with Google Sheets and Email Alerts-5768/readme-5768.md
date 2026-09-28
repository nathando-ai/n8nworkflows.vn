---
title: "🚀 Tự Động Kiểm Tra Và Cảnh Báo Hạn Chứng Chỉ SSL Với n8n, Google Sheets & Email"
description: "Hướng dẫn xây dựng workflow n8n tự động kiểm tra thời hạn chứng chỉ SSL hàng tuần, cập nhật Google Sheets và gửi email cảnh báo khi sắp hết hạn."
slug: "tu-dong-kiem-tra-va-canh-bao-han-chung-chi-ssl"
tags: [n8n, automation, secops, google-sheets, email-alert, ssl-monitoring]
keywords: [n8n workflow, kiểm tra ssl tự động, giám sát chứng chỉ ssl, google sheets automation, cảnh báo ssl hết hạn]
---

# 🚀 Tự Động Giám Sát Và Cảnh Báo Hạn Chứng Chỉ SSL Toàn Diện

Quên đi nỗi ám ảnh website sập hoặc trình duyệt hiển thị cảnh báo bảo mật nguy hiểm chỉ vì quên gia hạn chứng chỉ SSL! Việc kiểm tra thủ công hàng chục hay hàng trăm tên miền là một cơn ác mộng đối với đội ngũ quản trị hệ thống (SecOps/IT). 

Với workflow n8n này, các sếp sẽ tự động hóa hoàn toàn quy trình: định kỳ quét trạng thái SSL, cập nhật thông tin chi tiết vào Google Sheets và ngay lập tức gửi email cảnh báo nếu có chứng chỉ nào sắp hết hạn (dưới 14 ngày). Giải pháp 100% không cần code, hoạt động bền bỉ 24/7!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Không cần tự tay kiểm tra từng domain hay ghi nhớ lịch hết hạn.
- **Phòng ngừa rủi ro chủ động:** Cảnh báo trước 14 ngày giúp đội ngũ kỹ thuật có dư dả thời gian gia hạn SSL, tránh downtime website.
- **Quản lý tập trung:** Toàn bộ thông tin ngày cấp, ngày hết hạn và trạng thái SSL của các trang web được đồng bộ hóa tự động vào Google Sheets.
- **Hoạt động tự động 24/7:** Chạy ngầm định kỳ mỗi tuần một lần mà không cần sự can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Sheets:** Một file Google Sheet chứa danh sách các website cần theo dõi.
- **Google API Credentials** (OAuth2 hoặc Service Account) để n8n đọc/ghi dữ liệu trên Google Sheets.
- **SMTP Server / Email Account:** Để cấu hình node gửi email cảnh báo (Gmail, SendGrid, Mailgun hoặc SMTP riêng của doanh nghiệp).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow trống trong n8n, sau đó copy toàn bộ mã JSON của workflow này và dán trực tiếp vào giao diện n8n Editor, hoặc import file JSON tải về từ kho lưu trữ.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 8 nodes chính hoạt động nhịp nhàng với nhau. Các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Trigger Every Monday (`scheduleTrigger`):**
  - Mặc định workflow được lên lịch chạy vào **mỗi thứ Hai hàng tuần lúc 7:00 sáng**. Các sếp có thể thay đổi thời gian này tùy theo nhu cầu vận hành của doanh nghiệp.
- **Get Website List (`googleSheets`):**
  - Kết nối với tài khoản Google của sếp và chọn đúng file Google Sheets quản lý danh sách website.
  - Chuẩn bị sẵn các cột trong Sheet bao gồm: `No`, `Name`, `Link`, `SSL Issued On`, `SSL Expired On`, `SSL Status`.
- **Get SSL (`httpRequest`):**
  - Node này sử dụng API công khai từ `ssl-checker.io` để truy vấn thông tin SSL của từng URL chạy qua vòng lặp. Không cần chỉnh sửa phức tạp, nhưng cần đảm bảo server n8n có kết nối internet ổn định.
- **Loop (`splitInBatches`) & Code (`code`):**
  - Xử lý danh sách từng website và lọc ra các chứng chỉ có thời hạn sử dụng còn lại **dưới 14 ngày**.
- **Update SSL in Spreadsheet (`googleSheets`):**
  - Cấu hình lại Operation là `update` để ghi đè hoặc bổ sung thông tin ngày cấp, ngày hết hạn và trạng thái SSL mới nhất vào đúng hàng tương ứng trong Google Sheets.
- **SSL Not Good? (`if`) & Send Email Alert (`emailSend`):**
  - Kết nối credentials SMTP của sếp vào node `Send Email Alert`. 
  - Đảm bảo điền đúng địa chỉ email nhận cảnh báo (Email của quản trị viên hoặc đội ngũ IT).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để chạy thử nghiệm thủ công với dữ liệu mẫu và kiểm tra xem Google Sheets đã được cập nhật chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để n8n tự động vận hành theo lịch hẹn.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp đa kênh:** Ngoài email, các sếp có thể bổ sung thêm node Telegram, Slack hoặc Discord để nhận thông báo tức thì ngay trên điện thoại khi có SSL sắp hết hạn.
- **Lưu lịch sử Audit:** Thiết lập thêm một bảng log riêng trong Google Sheets để ghi lại lịch sử các lần quét SSL thành công nhằm phục vụ cho báo cáo kiểm toán bảo mật (Security Audit).
- **Tùy chỉnh thời gian cảnh báo:** Thay vì mốc 14 ngày, các sếp có thể đổi thông số trong đoạn mã Code thành 30 ngày đối với các chứng chỉ SSL doanh nghiệp cần quy trình phê duyệt dài ngày.

### 📌 Kết luận
Việc quản lý chứng chỉ SSL chưa bao giờ trở nên dễ dàng và tự động hóa đến thế. Chỉ với vài phút thiết lập workflow n8n này, các sếp đã có thể hoàn toàn yên tâm ngủ ngon vào ban đêm mà không sợ website bị lỗi chứng chỉ bất ngờ. Áp dụng ngay thôi nào!