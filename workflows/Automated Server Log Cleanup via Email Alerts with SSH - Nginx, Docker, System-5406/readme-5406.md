---
title: "🚀 Tự Động Dọn Log Server Khi Nhận Email Cảnh Báo Đầy Đĩa (Nginx, Docker, System)"
description: "Workflow n8n tự động đọc email cảnh báo đầy đĩa, trích xuất IP server và SSH vào để dọn dẹp log Nginx, Docker, System. Giải pháp DevOps thông minh, không cần code."
slug: "tu-dong-don-log-server-qua-email-ssh"
tags: [n8n, devops, automation, server-management, log-cleanup]
keywords: [n8n workflow, tự động hóa server, dọn log nginx, ssh automation, devops n8n]
---

# 🚀 Tự Động Dọn Log Server Khi Nhận Email Cảnh Báo Đầy Đĩa (Nginx, Docker, System)

Các sếp đang vận hành server có bao giờ rơi vào tình huống "đêm khuya thức dậy vì server đầy đĩa" không? Khi dung lượng disk chạm ngưỡng cảnh báo, hệ thống gửi email báo động. Việc phải mở terminal, SSH vào từng server, tìm lệnh `du -sh` để xem log nào đang "ăn" hết dung lượng, rồi gõ lệnh `truncate` hoặc `rm` thủ công là một quy trình vừa tốn thời gian, vừa dễ gây lỗi do con người.

Workflow này chính là "trợ lý DevOps" 24/7 của các sếp. Nó hoạt động hoàn toàn tự động: khi nhận được email cảnh báo từ hệ thống giám sát (như Zabbix, Nagios, hoặc script cron), n8n sẽ tự động phân tích email, trích xuất địa chỉ IP của server bị sự cố, và SSH vào để thực thi các lệnh dọn dẹp log chuyên dụng cho Nginx, Docker, PM2 và System Logs. Không cần code, không cần lo lắng về việc quên dọn log, mọi thứ diễn ra mượt mà và chính xác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản ứng tức thì:** Loại bỏ hoàn toàn độ trễ do con người xử lý, server được giải phóng dung lượng ngay khi có cảnh báo.
- **Chính xác tuyệt đối:** Các lệnh dọn log được chuẩn hóa, tránh rủi ro xóa nhầm file quan trọng do gõ lệnh thủ công sai.
- **Tiết kiệm chi phí nhân sự:** Giảm tải khối lượng công việc lặp đi lặp lại cho đội ngũ DevOps/IT.
- **Ghi nhận sự kiện:** Mọi lần dọn log đều được kích hoạt bởi email cụ thể, giúp truy vết dễ dàng khi cần kiểm tra lịch sử.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Email (IMAP):** Một hộp thư nhận cảnh báo (ví dụ: `alerts@yourdomain.com`) và thông tin IMAP (Host, Port, Username, Password/App Password).
2. **Quyền SSH:** Tài khoản user có quyền truy cập SSH vào các server cần giám sát (khuyến nghị dùng user có quyền `sudo` hoặc thuộc nhóm `adm` để đọc/xóa log).
3. **Cấu hình cảnh báo:** Hệ thống giám sát của các sếp (Zabbix, Prometheus, Grafana, hoặc script cron) phải được cấu hình để gửi email cảnh báo khi disk usage vượt ngưỡng (ví dụ: >80%).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from File** hoặc **Import from URL**.
3. Dán link workflow gốc hoặc upload file JSON đã export.
4. Workflow sẽ hiển thị 4 node chính: `Check Disk Alert Emails`, `Extract Server IP from Email`, `Prepare SSH Variables`, và `Run Log Cleanup Commands via SSH`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**Node 1: Check Disk Alert Emails (IMAP)**
- **Credentials:** Chọn hoặc tạo credential IMAP mới.
- **Host/Port:** Điền thông tin server mail (ví dụ: `imap.gmail.com`, port `993`).
- **Filter:** Cấu hình bộ lọc để chỉ đọc email có tiêu đề chứa từ khóa cảnh báo (ví dụ: "Disk Usage Alert" hoặc "High Disk Space"). Điều này giúp tránh việc workflow chạy lung tung với email thông thường.
- **Unread Only:** Nên bật để chỉ xử lý email mới.

**Node 2: Extract Server IP from Email (Code)**
- Node này dùng JavaScript để parse nội dung email.
- Các sếp cần kiểm tra lại regex trong node này. Nếu email cảnh báo của các sếp có định dạng IP khác (ví dụ: nằm trong body thay vì subject, hoặc có prefix khác), hãy chỉnh sửa code để khớp với format thực tế.
- *Mẹo:* Chạy thử với một email mẫu để đảm bảo node trả về đúng IP (ví dụ: `192.168.1.10` hoặc `203.0.113.5`).

**Node 3: Prepare SSH Variables (Set)**
- Node này chuẩn bị các biến cần thiết cho bước SSH.
- **Host:** Lấy từ kết quả của node trước (IP đã trích xuất).
- **Username:** Điền user SSH (ví dụ: `root` hoặc `deploy`).
- **Commands:** Đây là phần quan trọng nhất. Các sếp cần điền các lệnh dọn log phù hợp với môi trường của mình. Ví dụ mặc định thường bao gồm:
  - `sudo find /var/log/nginx -name "*.log" -mtime +7 -delete` (Xóa log Nginx cũ hơn 7 ngày)
  - `sudo journalctl --vacuum-time=7d` (Dọn log System)
  - `docker system prune -af` (Dọn Docker, cẩn thận nếu có container đang chạy)
- *Lưu ý:* Đảm bảo các lệnh này an toàn và phù hợp với chính sách backup của công ty.

**Node 4: Run Log Cleanup Commands via SSH (SSH)**
- **Credentials:** Chọn credential SSH Password hoặc SSH Key đã tạo trước đó.
- **Command:** Tham chiếu biến `commands` từ node `Prepare SSH Variables`.
- **Timeout:** Thiết lập timeout hợp lý (ví dụ: 30s) để tránh workflow treo nếu server phản hồi chậm.

#### 3. Kích hoạt ⚡️
1. **Test Run:** Gửi một email giả lập cảnh báo đầy đĩa vào hộp thư IMAP đã cấu hình.
2. Chạy workflow thủ công (Test Workflow).
3. Kiểm tra kết quả:
   - Node IMAP có đọc được email không?
   - Node Code có trích xuất đúng IP không?
   - Node SSH có kết nối thành công và thực thi lệnh không? (Kiểm tra output hoặc log trên server đích).
4. Nếu mọi thứ ổn, bật nút **Active** để workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi thông báo xác nhận:** Thêm node `Slack` hoặc `Telegram` sau bước SSH để gửi tin nhắn "Đã dọn log thành công cho server [IP]" vào kênh nội bộ.
- **Lưu log hoạt động:** Thêm node `Google Sheets` hoặc `Postgres` để ghi lại lịch sử: Thời gian, IP server, dung lượng trước/sau khi dọn (nếu có thể lấy được).
- **Phân loại mức độ nghiêm trọng:** Chỉnh sửa node Code để phân biệt cảnh báo "Warning" (80%) và "Critical" (90%). Với "Critical", có thể thêm bước gửi email cho quản trị viên cấp cao.
- **Backup trước khi xóa:** Nếu lo ngại mất dữ liệu log quan trọng, thêm bước SSH trước đó để `tar` nén log vào thư mục backup trước khi `rm`.

### 📌 Kết luận
Việc quản lý log server là một phần không thể thiếu trong DevOps, nhưng nó không nên là gánh nặng thủ công. Với workflow n8n này, các sếp đã biến một quy trình phản ứng khẩn cấp thành một quy trình tự động, an toàn và hiệu quả. Hãy import, cấu hình và để n8n lo phần "dọn dẹp", còn các sếp tập trung vào việc phát triển sản phẩm và tối ưu hóa hệ thống. Chúc các sếp vận hành server mượt mà, không lo đầy đĩa!