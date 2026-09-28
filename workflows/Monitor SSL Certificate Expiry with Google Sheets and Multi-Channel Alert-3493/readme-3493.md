---
title: "🚀 Tự động giám sát hạn sử dụng SSL và cảnh báo đa kênh với n8n"
description: "Hướng dẫn xây dựng hệ thống tự động kiểm tra SSL hàng tuần từ Google Sheets, phân loại trạng thái và gửi cảnh báo qua Email, Telegram, Ntfy."
slug: "tu-dong-giam-sat-han-su-dung-ssl-n8n"
tags: [n8n, automation, devops, security, google-sheets, telegram]
keywords: [n8n workflow, giám sát ssl, ssl expiry alert, tự động hóa devops, kiểm tra ssl tự động]
---

# 🚀 Tự động giám sát hạn sử dụng SSL và cảnh báo đa kênh với n8n

Các sếp làm IT hay quản trị hệ thống chắc hẳn đã từng có ít nhất một lần "thót tim" vì chứng chỉ SSL của website hết hạn mà quên gia hạn, dẫn đến việc website bị trình duyệt chặn truy cập hoặc sập hệ thống đột ngột. Việc kiểm tra thủ công hàng chục domain là một cực hình và rất dễ sót việc.

Giải pháp là đây: Workflow n8n tự động 100% giúp các sếp gom toàn bộ danh sách website vào Google Sheets, tự động check hạn sử dụng SSL qua API, cập nhật trạng thái vào sheet và bắn cảnh báo tức thì qua Email, Telegram hoặc Ntfy trước khi quá muộn!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Lên lịch quét hàng tuần mà không cần đụng tay.
- **Phân loại thông minh**: Tự động chia nhóm: Không hợp lệ (Invalid), Sắp hết hạn <30 ngày (Warning), Lưu ý <60 ngày (Notice), và Trạng thái bình thường (Info).
- **Cảnh báo đa kênh**: Gửi thông báo chi tiết qua Gmail, Telegram, hoặc Ntfy để team kỹ thuật nắm bắt ngay lập tức.
- **Quản lý tập trung**: Mọi thông tin trạng thái SSL được cập nhật ngược lại Google Sheets để tra cứu bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Sheets (chứa danh sách URL cần theo dõi).
- Tài khoản Gmail (để gửi email cảnh báo).
- Bot Telegram (tuỳ chọn nếu muốn nhận tin qua Telegram).
- Dịch vụ Ntfy (tuỳ chọn cho thông báo đẩy push notification).
- Workflow sử dụng API từ `SSL-Checker.io` thông qua HTTP Request node.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy đoạn mã JSON của workflow này và dán trực tiếp vào n8n Editor của các sếp, hoặc import file JSON tải từ trang chủ n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình kỹ các node sau để workflow chạy mượt mà:
- **Weekly Trigger**: Node lịch chạy mặc định là hàng tuần. Các sếp có thể đổi sang chạy hàng ngày nếu quản lý các hệ thống lớn.
- **Fetch URLs** & **URLs to Monitor**: Kết nối với tài khoản Google Sheets OAuth2 API của các sếp. Hãy chuẩn bị một Google Sheet với cột `URL` (ví dụ: `n8n.io`, `google.com`) và trỏ ID của sheet vào 2 node này.
- **Check SSL**: Node HTTP Request gọi tới `SSL-Checker.io` để lấy thông tin chi tiết (host, thời gian hiệu lực, số ngày còn lại).
- **Switch**: Bộ lọc phân loại chứng chỉ thành 4 nhóm (`invalid`, `warning`, `notice`, `info`) dựa trên kết quả trả về.
- **Send Alert Email1 / 2 / 4 / 6** & **Telegram** & **Ntfy4**: Cấu hình credentials cho Gmail, Telegram Bot Token và Ntfy server để nhận thông báo tương ứng cho từng mức độ cảnh báo.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử nghiệm với danh sách URL mẫu trong Google Sheets.
- Kiểm tra xem dữ liệu đã được cập nhật vào Sheet và tin nhắn/email đã bắn về chưa.
- Nếu mọi thứ xanh mướt, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Discord**: Thay vì chỉ dùng Telegram và Gmail, các sếp có thể thêm node Slack để bắn tin thẳng vào kênh `#devops` của công ty.
- **Ghi log lịch sử**: Mở rộng Google Sheets thêm các cột lịch sử kiểm tra để vẽ biểu đồ theo dõi xu hướng bảo mật của hệ thống.
- **Rút ngắn chu kỳ**: Đối với các chứng chỉ sắp hết hạn trong vòng 7 ngày, hãy cấu hình trigger chạy mỗi ngày một lần thay vì mỗi tuần một lần để tăng độ an toàn.

### 📌 Kết luận
Một hệ thống DevOps chuyên nghiệp không thể thiếu bước giám sát SSL tự động này. Chỉ mất 10 phút cài đặt, các sếp đã có thể loại bỏ hoàn toàn rủi ro sập web do quên gia hạn SSL. Triển khai ngay thôi các sếp ơi!