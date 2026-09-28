---
title: "🚀 Tự động hóa gửi báo cáo tiến độ xây dựng hằng ngày qua Gmail và WhatsApp với n8n"
description: "Hướng dẫn cấu hình workflow n8n tự động đọc Google Sheets, lọc báo cáo công trình trong ngày và gửi thông báo qua Gmail, WhatsApp một cách chính xác."
slug: "tu-dong-hoa-gui-bao-cao-xay-dung-qua-gmail-whatsapp-n8n"
tags: [n8n, automation, no-code, google-sheets, whatsapp, gmail, project-management]
keywords: [n8n workflow, tự động hóa xây dựng, google sheets to whatsapp, gửi email tự động n8n, quản lý dự án xây dựng]
---

# 🚀 Tự động hóa gửi báo cáo tiến độ xây dựng hằng ngày qua Gmail và WhatsApp

Các sếp làm trong ngành xây dựng hoặc quản lý dự án chắc chắn đã quá quen thuộc với cảnh mỗi sáng phải đi "nhắc khéo" các nhà thầu gửi báo cáo, sau đó lại lọ mọ tổng hợp số liệu, copy-paste gửi cho sếp lớn hoặc khách hàng. Vừa tốn thời gian, dễ sót việc, lại cực kỳ áp lực khi số lượng dự án tăng lên.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa toàn bộ quy trình: Tự động kích hoạt vào đầu giờ mỗi ngày, quét dữ liệu từ Google Sheets, lọc ra các báo cáo mới nhất và gửi trực tiếp qua **Gmail** lẫn **WhatsApp** cho các bên liên quan. Không một phút thủ công, không sợ quên việc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian tổng hợp:** Không còn cảnh thủ công copy số liệu từ Excel/Google Sheets mỗi sáng.
- **Minh bạch và tức thời:** Báo cáo tiến độ xây dựng bay thẳng đến điện thoại (WhatsApp) và hòm thư (Gmail) của các bên liên quan đúng giờ hẹn.
- **Giám sát chặt chẽ:** Tự động ghi log (Log Successful Notifications) mọi hoạt động gửi thông báo để dễ dàng kiểm tra khi cần đối soát.
- **Vận hành 24/7 tự động:** Hoạt động trơn tru trên n8n mà không cần sự can thiệp thủ công hằng ngày.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản Google:** Có chứa Google Sheet ghi nhận báo cáo tiến độ của nhà thầu.
- **Tài khoản WhatsApp Business API:** Để gửi tin nhắn tự động đến nhóm hoặc cá nhân.
- **SMTP Server / Gmail Credential:** Để gửi email thông báo chi tiết.
- **Hệ thống n8n:** Đã cài đặt sẵn sàng (Self-hosted hoặc n8n Cloud).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy đoạn mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor, hoặc import file JSON thông qua menu tuỳ chọn của n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không lỗi, các sếp cần cấu hình kỹ các node sau:

- **Daily Trigger (8:00 AM IST):** Node này định giờ chạy tự động. Các sếp có thể đổi lại múi giờ (Timezone) thành `Asia/Ho_Chi_Minh` (GMT+7) và giờ chạy mong muốn (ví dụ 8:00 AM VN).
- **Set Google Sheet Config & Read Google Sheet Data:** 
  - Kết nối tài khoản Google Sheets thông qua `googleSheetsOAuth2Api`.
  - Điền chính xác **Spreadsheet ID** và **Sheet Name** chứa dữ liệu báo cáo của nhà thầu.
- **Filter Today's Reports:** Kiểm tra lại logic lọc ngày tháng (`Date` column) để đảm bảo hệ thống chỉ lấy đúng báo cáo của ngày hiện tại.
- **Check If Reports Found (Node IF):** Xử lý nhánh rẽ: Nếu có báo cáo mới -> tiến hành gửi tin. Nếu không có -> có thể thiết lập cảnh báo hoặc kết thúc.
- **Set Notification Recipients & Create Notification Content:** Khai báo danh sách số điện thoại WhatsApp và email người nhận, đồng thời định dạng lại nội dung bản tóm tắt dự án cho thật chuyên nghiệp.
- **Send WhatsApp Notification & Send Email Notification:** 
  - Gắn Credentials cho WhatsApp (`whatsAppApi`) và Email (`smtp`).
  - Đảm bảo các tham số gửi tin khớp với cấu hình API của nhà mạng WhatsApp và dịch vụ Email các sếp đang dùng.
- **Log Successful Notifications:** Cấu hình lưu vết lại lịch sử gửi thông báo (thời gian, số lượng người nhận, chi tiết dự án) vào một bảng log trên Google Sheets hoặc database nếu muốn.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để chạy thử nghiệm (Test Run) với dữ liệu mẫu xem hệ thống đã bắn tin nhắn và email thành công chưa.
- Sau khi test ngon lành, gạt công tắc sang **Active** để workflow chính thức tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Có thể kết hợp thêm node Telegram hoặc Slack để bắn tin vào nhóm chat chung của công ty.
- **Lưu lịch sử vào Database:** Thay vì chỉ log thông thường, các sếp có thể đẩy dữ liệu log vào Airtable hoặc PostgreSQL để làm báo cáo dashboard trực quan hàng tuần/tháng.
- **Xử lý ngoại lệ (Error Handling):** Thêm Error Trigger vào workflow để nếu nhà thầu quên gửi báo cáo hoặc hệ thống lỗi API, n8n sẽ tự động bắn tin báo cáo sự cố về cho bộ phận vận hành.

### 📌 Kết luận
Tự động hóa quy trình báo cáo xây dựng không chỉ giúp tiết kiệm hàng giờ đồng hồ mỗi tuần mà còn nâng tầm chuyên nghiệp trong mắt đối tác và khách hàng. Hãy triển khai ngay workflow này để tối ưu hóa vận hành doanh nghiệp của các sếp ngay hôm nay!