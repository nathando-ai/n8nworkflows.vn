---
title: "🚀 Tự động giám sát Uptime Server và cảnh báo qua Email với Google Sheets"
description: "Xây dựng hệ thống giám sát trạng thái server tự động 24/7 bằng n8n, tự động kiểm tra HTTP, ghi log vào Google Sheets và gửi cảnh báo qua Gmail khi server sập."
slug: "giam-sat-server-uptime-va-canh-bao-email-google-sheets"
tags: [n8n, automation, devops, monitoring, google-sheets, gmail]
keywords: [n8n workflow, giám sát server, server uptime, cảnh báo server down, tự động hóa devops, google sheets monitoring]
---

# 🚀 Tự động giám sát Uptime Server và cảnh báo qua Email với Google Sheets

Các sếp đang quản lý hệ thống nhiều website hoặc VPS chắc chắn đã từng trải qua cảm giác "đứng ngồi không yên" khi sợ server sập giữa đêm mà không hay biết. Việc kiểm tra thủ công bằng tay vừa mất thời gian, vừa dễ bỏ sót sự cố, ảnh hưởng trực tiếp đến doanh thu và uy tín. 

Giải pháp là đây! Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình kiểm tra trạng thái server, ghi lại lịch sử hoạt động vào Google Sheets và lập tức bắn email cảnh báo qua Gmail ngay khi có sự cố xảy ra.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Giám sát 24/7 không nghỉ:** Tự động kiểm tra danh sách server liên tục theo lịch trình định sẵn (ví dụ: mỗi phút/lần).
- **Cảnh báo tức thì:** Nhận email ngay lập tức kèm thông tin chi tiết và thời điểm server "gặp nạn".
- **Lưu trữ lịch sử minh bạch:** Mọi trạng thái thành công (Alive) hay thất bại (Down) đều được ghi log tự động vào Google Sheets để phục vụ việc báo cáo uptime.
- **Quản lý linh hoạt:** Thêm hoặc xóa server cực kỳ dễ dàng trực tiếp trên Google Sheets mà không cần chỉnh sửa lại workflow trong n8n.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Google:** Để kết nối Google Sheets (lấy danh sách server và ghi log).
- **Tài khoản Gmail:** Để gửi email cảnh báo khi server sập.
- **File Google Sheets mẫu:** Chuẩn bị sẵn file Google Sheets gồm các cột chứa danh sách URL/IP server cần giám sát, cùng các sheet để ghi log sống/chết.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy mã JSON của workflow này và paste trực tiếp vào n8n Editor của mình, hoặc tải file JSON về và chọn **Import from File** trong giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 6 nodes chính, các sếp cần chú ý cấu hình kỹ các node sau:

- **1. Schedule Trigger:** 
  - Cấu hình tần suất chạy (mặc định chạy mỗi phút). Các sếp có thể điều chỉnh lại thời gian cho phù hợp với nhu cầu (ví dụ: 5 phút/lần để tiết kiệm tài nguyên).
- **2. Web Servers List (Google Sheets):** 
  - Chọn tài khoản kết nối **Google Sheets OAuth2 API**.
  - Trỏ tới file Google Sheets chứa danh sách server và chọn đúng Sheet Name chứa các URL/IP cần theo dõi.
- **3. Servers Alive Check (HTTP):** 
  - Node này thực hiện request HTTP GET tới từng server lấy từ danh sách. Đảm bảo cấu hình đúng biến truyền vào từ bước đọc Google Sheets.
- **4. Web Server Alive Log (Google Sheets):** 
  - Cấu hình kết nối Google Sheets để ghi lại các bản log khi server phản hồi thành công (kèm timestamp).
- **5. Server Down Notification (Gmail):** 
  - Chọn kết nối **Gmail OAuth2**.
  - Điền email nhận cảnh báo, tùy chỉnh tiêu đề và nội dung email thông báo lỗi, địa chỉ server bị sập và thời gian xảy ra sự cố.
- **6. Web Server Down Log (Google Sheets):** 
  - Cấu hình kết nối Google Sheets để ghi nhận các trường hợp server down phục vụ cho việc audit và debug sau này.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm (Test run) với dữ liệu từ Google Sheets xem hệ thống có check và log chuẩn chỉnh chưa.
- Sau khi test ngon lành, gạt công tắc sang **Active** để workflow chính thức gác cổng 24/7 cho các sếp.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm kênh chat:** Ngoài Gmail, các sếp có thể gắn thêm node Telegram Bot hoặc Slack để nhận thông báo ngay lập tức trên điện thoại.
- **Báo cáo định kỳ:** Dùng một nhánh phụ chạy vào cuối tuần để đọc dữ liệu từ Google Sheets Log, tổng hợp tỉ lệ Uptime (%) và gửi email báo cáo sức khỏe hệ thống tổng thể.
- **Tự động retry:** Thêm logic kiểm tra lại lần 2 (Retry on fail) trước khi gửi email cảnh báo để tránh việc báo động giả do rớt mạng chớp nhoáng.

### 📌 Kết luận
Một hệ thống monitoring chuyên nghiệp không nhất thiết phải tốn kém chi phí hàng tháng cho các bên thứ ba đắt đỏ. Chỉ với vài phút thiết lập workflow n8n này kết hợp cùng Google Sheets và Gmail, các sếp đã sở hữu ngay một "lính gác" tận tụy bảo vệ hạ tầng của mình 24/7. Lên đồ ngay thôi các sếp ơi!