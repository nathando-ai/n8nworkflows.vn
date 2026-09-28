---
title: "🚀 Tự động xoay vòng User-Agent và Proxy IP để Cào dữ liệu & Gọi API không giới hạn"
description: "Hướng dẫn xây dựng workflow n8n giúp bypass giới hạn IP và chống chặn khi cào dữ liệu web hoặc gọi API công khai bằng kỹ thuật xoay vòng IP Proxy và User-Agent ngẫu nhiên."
slug: "tao-xoay-vong-user-agents-va-proxy-ips-cho-scraping-api"
tags: [n8n, automation, scraping, proxy, api, web-scraping]
keywords: [n8n workflow, xoay vong proxy, user-agent ngau nhien, scrape api, vuot gioi han ip, decodo proxy]
---

# 🚀 Tự động xoay vòng User-Agent và Proxy IP để Cào dữ liệu & Gọi API không giới hạn

Các sếp có bao giờ đau đầu khi viết tool cào dữ liệu (Web Scraping) hoặc gọi các API công khai nhưng liên tục bị chặn, bị giới hạn số lần gọi (Rate Limit) hay bị khóa địa chỉ IP chưa? Việc sử dụng một IP cố định và một User-Agent duy nhất cho hàng loạt request là nguyên nhân chính khiến hệ thống đích phát hiện và chặn bot.

Workflow n8n này chính là "vũ khí bí mật" giúp các sếp giải quyết triệt để bài toán trên. Hệ thống sẽ tự động cào danh sách các User-Agent mới nhất, kết hợp với dịch vụ Proxy xoay vòng (Rotating Proxy), ghép nối ngẫu nhiên và gán cho mỗi request gọi đến API mục tiêu. Nhờ đó, mỗi lần gọi API sẽ trông giống như được thực hiện bởi một người dùng hoàn toàn khác nhau từ khắp nơi trên thế giới!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Vượt rào cản IP/Rate Limit:** Tránh việc bị ban IP hoặc chặn truy cập khi gọi API với tần suất lớn.
- **Giả lập người dùng thật:** Tự động xoay vòng danh sách User-Agent đa dạng kết hợp địa chỉ IP proxy động.
- **Tích hợp linh hoạt:** Có thể đặt workflow này làm tiền đề (middleware) trước bất kỳ HTTP Request node nào cần cào dữ liệu.
- **Hoạt động hoàn toàn tự động:** Không cần can thiệp thủ công, sẵn sàng mở rộng cho các chiến dịch data scraping quy mô lớn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động ổn định.
- Tài khoản dịch vụ Proxy (ví dụ: Decodo, Bright Data, Oxylabs...) hỗ trợ loại Residential Proxy với tính năng xoay vòng (rotating session type) để mỗi request nhận một IP khác nhau.
- API mục tiêu mà các sếp muốn cào dữ liệu hoặc gọi tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ mã nguồn JSON của workflow (ID: 13637) và dán trực tiếp vào n8n Editor, hoặc import file JSON trực tiếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động trơn tru với môi trường của các sếp, hãy chú ý cấu hình các node quan trọng sau:

- **Node `SET your proxy connection details here` (Set):** Nơi cấu hình thông tin kết nối proxy của nhà cung cấp. Các sếp cần cập nhật các thông số:
  - `proxy_username`: Tên đăng nhập tài khoản proxy.
  - `proxy_password`: Mật khẩu tài khoản proxy.
  - `proxy_port`: Cổng kết nối (Port) của proxy.
  *(Định dạng thường là: `http://username:password@gate.decodo.com:PORT`)*

- **Node `Take X random user-agents` (Limit):** Cho phép các sếp giới hạn số lượng User-Agent ngẫu nhiên muốn lấy và sử dụng trong mỗi đợt chạy.

- **Node `Targeted API` (HTTP Request):** Đây là nơi các sếp gọi API thực tế của mình. Hãy nhớ cấu hình thêm:
  - Thêm Header: `user-agent` với giá trị `{{ $json["clean_user-agent"] }}`
  - Thêm cấu hình Proxy (trong phần Options của HTTP Request node) với giá trị: `http://{{ $json.proxy_username }}:{{ $json.proxy_password }}@gate.decodo.com:{{ $json.proxy_port }}`

- **Node `IP address and user-agent used` (Set):** Node thông tin giúp các sếp theo dõi xem cặp IP và User-Agent nào đang được sử dụng cho request hiện tại.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** thông qua **Manual trigger** để kiểm tra dữ liệu chạy thử xem các User-Agent và IP đã được ghép nối chính xác chưa.
- Sau khi test thành công, bật trạng thái **Active** để workflow sẵn sàng vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Telegram/Slack Alert:** Thêm node thông báo nếu tỷ lệ lỗi (Error Rate) khi gọi API vượt quá ngưỡng cho phép do IP proxy chết.
- **Lưu lịch sử Log:** Đẩy cặp thông tin `IP address / User-Agent` và kết quả trả về của API vào Google Sheets hoặc Database để dễ dàng kiểm tra, audit.
- **Xoay vòng Proxy tự động theo lịch:** Cân nhắc kết hợp Cron node để làm mới danh sách User-Agent định kỳ hàng ngày.

### 📌 Kết luận
Việc cào dữ liệu và gọi API số lượng lớn chưa bao giờ dễ dàng đến thế nếu thiếu đi cơ chế ẩn mình và đổi danh tính liên tục. Hãy áp dụng ngay workflow này vào hệ thống n8n của các sếp để tối ưu hóa hiệu suất cào dữ liệu mà không sợ bị chặn đứng giữa chừng!