---
title: "🚀 Tự động lấy địa chỉ IP Public của n8n Instance cực kỳ đơn giản"
description: "Hướng dẫn cài đặt và sử dụng workflow n8n giúp truy vấn nhanh chóng địa chỉ IP Public (IPv4/IPv6) của hệ thống n8n server thông qua Webhook bảo mật."
slug: "lay-ip-public-n8n-instance-tu-dong"
tags: [n8n, automation, devops, webhook, http-request, infrastructure]
keywords: [n8n workflow, lay ip public n8n, n8n instance ip, devops automation n8n, http request n8n]
---

# 🚀 Tự động lấy địa chỉ IP Public của n8n Instance cực kỳ đơn giản

Các sếp chạy hệ thống n8n tự host (Self-hosted) trên VPS đôi khi sẽ gặp tình huống cần biết chính xác địa chỉ IP Public của server mình đang đứng để cấu hình Firewall, whitelist API hoặc tích hợp dịch vụ bên thứ ba. Thay vì phảiSSH vào server rồi gõ lệnh `curl ifconfig.me`, các sếp hoàn toàn có thể dựng một API endpoint ngay trong n8n để làm việc này một cách tự động và chuyên nghiệp 100% không cần code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **API Endpoint riêng:** Tạo sẵn một Webhook Endpoint có bảo mật bằng Header Auth để gọi lấy IP bất cứ lúc nào.
- **Tự động hóa DevOps:** Dễ dàng tích hợp vào các kịch bản CI/CD, script tự động hóa hoặc hệ thống giám sát.
- **Bảo mật tuyệt đối:** Yêu cầu xác thực API Key trước khi trả về thông tin IP của server.
- **Hoạt động liên tục:** Sẵn sàng phục vụ 24/7 trên chính hạ tầng n8n của các sếp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động (Self-hosted trên VPS hoặc Cloud).
- Thiết lập sẵn **Header Auth Credential** (dùng một chuỗi UUID hoặc API token ngẫu nhiên làm khóa bảo vệ).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor, hoặc import file JSON tải từ trang chủ n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 5 nodes chính phối hợp nhịp nhàng với nhau. Các sếp cần chú ý cấu hình các điểm sau:

- **Node Webhook:** 
  - Node này đóng vai trò là điểm nhận request từ bên ngoài.
  - Cần cấu hình **Authentication** bằng cách chọn **Header Auth** và trỏ tới credential chứa API token bảo mật của các sếp (đảm bảo không ai mò ra endpoint này).
  - Đường dẫn (Path) mặc định được thiết lập là `4879bc79-d6f8-48df-bfe4-613366c7f399`, các sếp có thể đổi lại chuỗi này thành một chuỗi bí mật của riêng mình.

- **Node HTTP Request:** 
  - Thực hiện gọi đến các dịch vụ tra cứu IP công cộng (như ipify hoặc tương tự) từ phía server đang chạy n8n.

- **Node Repeat (Set) & Aggregate:** 
  - Xử lý, gom nhóm và định dạng lại dữ liệu IP trả về thành một mảng JSON gọn gàng (Ví dụ: `["88.88.88.66", "88.88.88.88"]`).

- **Node Respond to Webhook:** 
  - Trả kết quả mảng IP trực tiếp về cho người gọi thông qua HTTP Response.

#### 3. Kích hoạt ⚡️
- Test thử câu lệnh `curl` mẫu trên Terminal của các sếp để kiểm tra:
  ```bash
  curl -H "api-key: super-long-api-token" http://localhost:5678/webhook/4879bc79-d6f8-48df-bfe4-613366c7f399
  ```
- Nếu trả về mảng chứa IP chính xác, các sếp bấm nút **Active** để bật workflow chạy chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack Bot:** Kết hợp thêm node gửi thông báo về chat nội bộ mỗi khi n8n instance thay đổi IP mạng (nếu dùng các dịch vụ Cloud có IP động).
- **Lưu log vào Google Sheets:** Ghi lại lịch sử mỗi lần kiểm tra IP để kiểm toán hệ thống.
- **Giám sát Uptime:** Dùng công cụ bên ngoài ping vào Webhook này định kỳ để kiểm tra xem n8n instance có đang "sống" khỏe hay không.

### 📌 Kết luận
Một workflow tuy nhỏ nhưng cực kỳ hữu ích cho các anh em làm DevOps và tự động hóa hệ thống self-hosted. Hãy cài đặt ngay vào n8n của các sếp để làm chủ hoàn toàn hạ tầng mạng của mình nhé!