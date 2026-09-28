---
title: "🚀 Tự động gửi Email thông báo cập nhật gói phần mềm Server qua SSH với n8n"
description: "Hướng dẫn xây dựng workflow tự động kiểm tra các gói phần mềm cần cập nhật trên VPS/Server qua SSH mỗi ngày và gửi email cảnh báo chi tiết."
slug: "tu-dong-gui-email-thong-bao-cap-nhat-server-qua-ssh"
tags: [n8n, automation, devops, ssh, smtp, server-monitoring]
keywords: [n8n workflow, tu dong hoa devops, kiem tra update server, ssh n8n, gui email canh bao server]
---

# 🚀 Tự động gửi Email thông báo cập nhật gói phần mềm Server qua SSH với n8n

Các sếp làm kỹ thuật, DevOps hay quản trị hệ thống chắc hẳn đã quá quen thuộc với việc phải thủ công đăng nhập vào từng VPS/Server để kiểm tra các bản cập nhật bảo mật và gói phần mềm (apt upgrade/update). Việc quên cập nhật định kỳ có thể dẫn đến các lỗ hổng bảo mật nghiêm trọng. 

Giải pháp là gì? Workflow n8n này sẽ tự động hóa 100% quy trình đó: mỗi ngày tự động kết nối vào server qua SSH, quét danh sách các gói có thể nâng cấp, xử lý định dạng thành một bảng HTML gọn gàng và gửi email cảnh báo trực tiếp cho các sếp. Không cần code phức tạp, hoàn toàn rảnh tay!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo mật tuyệt đối:** Chủ động nắm bắt các bản cập nhật bảo mật của hệ điều hành ngay khi phát hành.
- **Tiết kiệm thời gian:** Thay vì phải gõ lệnh kiểm tra thủ công mỗi tuần, hệ thống tự động làm việc này mỗi ngày.
- **Báo cáo trực quan:** Danh sách các gói phần mềm cần nâng cấp được format thành dạng bảng HTML dễ nhìn ngay trong hộp thư đến.
- **Hoạt động 24/7:** Chạy ngầm liên tục nhờ Schedule Trigger và giao thức SSH bảo mật.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **SSH Credentials:** Thông tin truy cập SSH vào Server/VPS (Host, Port, Username, Password/SSH Key).
- **SMTP Credentials:** Thông tin tài khoản gửi email (Gmail SMTP, SendGrid, Amazon SES, hoặc Mailgun...) để gửi thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này hoặc sử dụng tính năng copy/paste trực tiếp JSON vào n8n Editor để tạo nhanh chóng.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm các nodes chính sau đây cần được cấu hình chuẩn xác:

- **Run workflow every day (`scheduleTrigger`):** 
  - Mặc định workflow được cấu hình chạy định kỳ mỗi ngày. Các sếp có thể chỉnh lại múi giờ (Timezone) và tần suất (ví dụ: chạy 8h sáng mỗi ngày) cho phù hợp với nhu cầu.
- **List upgradable packages (`ssh`):** 
  - Cần tạo credentials loại **SSH** với thông tin IP/Domain, Port (thường là 22), Username và Password hoặc Private Key của Server.
  - Node này sẽ thực hiện câu lệnh kiểm tra gói cập nhật trên hệ điều hành Linux (ví dụ: `apt list --upgradable`).
- **Check if there are updates (`if`):** 
  - Node điều kiện kiểm tra xem lệnh SSH trả về có bản cập nhật nào mới hay không. Nếu có (`true`), workflow sẽ tiếp tục tiến trình; nếu không, quy trình sẽ kết thúc để tránh làm phiền hộp thư.
- **Format as HTML list (`code`):** 
  - Node JavaScript xử lý dữ liệu thô từ SSH trả về, chuyển đổi và sắp xếp lại thành định dạng HTML sạch đẹp, dễ đọc trên email.
- **Send Email through SMTP (`emailSend`):** 
  - Cấu hình thông tin **SMTP Credentials**.
  - **Lưu ý quan trọng:** Cập nhật chính xác địa chỉ email người gửi (`From`) và người nhận (`To`) trong node này để chắc chắn nhận được thông báo về máy.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thủ công xem kết nối SSH và gửi email có hoạt động trơn tru không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài gửi Email, các sếp có thể nối thêm node **Telegram** hoặc **Slack** để nhận cảnh báo ngay lập tức trên điện thoại.
- **Lưu Log vào Google Sheets:** Thêm một node Google Sheets để lưu lại lịch sử mỗi lần server có yêu cầu update, giúp theo dõi lịch sử bảo trì hệ thống dễ hơn.
- **Tự động hóa nâng cấp luôn:** Nếu tự tin, các sếp có thể bổ sung thêm một câu lệnh SSH chạy `apt upgrade -y` sau khi kiểm tra (cân nhắc kỹ lưỡng trước khi áp dụng cho môi trường Production nhé!).

### 📌 Kết luận
Một workflow DevOps cực kỳ nhỏ gọn nhưng mang lại giá trị bảo mật to lớn cho hệ thống của các sếp. Hãy triển khai ngay để không bao giờ bỏ lỡ bất kỳ bản cập nhật quan trọng nào từ server!