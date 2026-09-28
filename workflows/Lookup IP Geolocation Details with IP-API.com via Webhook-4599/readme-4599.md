---
title: "🚀 Tự động tra cứu vị trí IP (Geolocation) qua Webhook bằng n8n và IP-API"
description: "Hướng dẫn xây dựng API tra cứu vị trí địa lý của địa chỉ IP tự động 100% sử dụng n8n webhook và IP-API.com miễn phí, nhanh chóng."
slug: "tra-cuu-vi-tri-ip-geolocation-voi-n8n-va-ip-api"
tags: [n8n, automation, no-code, webhook, ip-api, it-ops]
keywords: [n8n workflow, tra cứu ip, ip geolocation, tự động hóa api, ip-api n8n, webhook n8n]
---

# 🚀 Tự động tra cứu vị trí IP (Geolocation) qua Webhook bằng n8n và IP-API

Các sếp có bao giờ cần biết vị trí địa lý, nhà mạng (ISP), quốc gia hoặc thành phố của một địa chỉ IP truy cập vào hệ thống nhưng lại phải tra cứu thủ công từng cái trên các trang web? Việc này vừa mất thời gian, vừa khó tích hợp vào các quy trình tự động hóa khác như bảo mật, phân tích hành vi người dùng hay cá nhân hóa nội dung.

Giải pháp ở đây chính là xây dựng một API Endpoint nội bộ siêu tốc bằng **n8n** kết hợp với dịch vụ **IP-API.com**. Workflow này sẽ nhận yêu cầu (POST request) chứa địa chỉ IP, tự động gọi sang dịch vụ tra cứu và trả về toàn bộ thông tin chi tiết chỉ trong tích tắc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và sẵn sàng nhận request từ các ứng dụng bên ngoài, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Biến n8n thành một microservice tra cứu IP riêng biệt qua Webhook.
- **Dữ liệu phong phú:** Nhận ngay thông tin chi tiết bao gồm quốc gia, thành phố, khu vực, múi giờ, nhà mạng (ISP) và tọa độ.
- **Tích hợp linh hoạt:** Dễ dàng kết nối từ website, CRM, bot Telegram hoặc các hệ thống giám sát bảo mật khác.
- **Tiết kiệm chi phí:** Sử dụng IP-API.com miễn phí mà không cần cấu hình API Key phức tạp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Self-hosted hoặc n8n Cloud) có hỗ trợ Webhook công khai (Public URL).
- Không cần tài khoản hay API Key phức tạp nào vì workflow sử dụng dịch vụ công khai từ IP-API.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ cấu trúc JSON từ nguồn cung cấp hoặc dựng lại bằng 3 nodes cơ bản dưới đây:
- **Receive IP Webhook** (`n8n-nodes-base.webhook`)
- **Get IP Geolocation** (`n8n-nodes-base.httpRequest`)
- **Respond with Geolocation Data** (`n8n-nodes-base.respondToWebhook`)

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 3 nodes chính hoạt động nhịp nhàng với nhau:

1. **Node `Receive IP Webhook` (Webhook):**
   - **Path:** Đặt mặc định là `ip-lookup` (hoặc thay đổi tùy ý các sếp).
   - **Method:** `POST`.
   - **Cách gọi:** Node này lắng nghe các request dạng JSON gửi tới. Dữ liệu đầu vào cần có cấu trúc:
     ```json
     {
       "ip": "8.8.8.8"
     }
     ```

2. **Node `Get IP Geolocation` (HTTP Request):**
   - **Method:** `GET`.
   - **URL:** Gọi đến API của IP-API theo cú pháp: `http://ip-api.com/json/{{ $json.body.ip }}` (lấy động giá trị IP từ body của Webhook gửi vào).
   - Node này sẽ trả về một cục dữ liệu JSON chứa toàn bộ thông tin về vị trí địa lý của IP đó.

3. **Node `Respond with Geolocation Data` (Respond to Webhook):**
   - **Response Body:** Trả về dữ liệu nhận được từ node HTTP Request cho ứng dụng/người gọi ban đầu.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và dùng các công cụ như Postman hoặc lệnh `curl` để gửi một POST request mẫu đến Webhook URL của n8n để kiểm tra kết quả.
- Sau khi test thành công, bật công tắc **Active** để đưa workflow vào trạng thái vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
Để workflow trở nên "lợi hại" hơn, các sếp có thể mở rộng thêm các tính năng sau:
- **Lưu log vào Google Sheets / Database:** Mỗi khi có IP gọi đến, tự động lưu lại lịch sử truy vấn kèm thời gian để phục vụ thống kê.
- **Cảnh báo qua Telegram/Slack:** Nếu phát hiện IP truy cập đến từ các quốc gia lạ hoặc nằm trong danh sách cần chú ý, bắn tin nhắn cảnh báo ngay lập tức.
- **Xử lý điều kiện (If Node):** Kiểm tra nếu thiếu trường `ip` trong request thì trả về mã lỗi `400 Bad Request` thay vì để lỗi xảy ra.

### 📌 Kết luận
Chỉ với 3 nodes cực kỳ cơ bản trong n8n, các sếp đã có thể tự dựng cho mình một dịch vụ tra cứu vị trí IP chuyên nghiệp, sẵn sàng tích hợp vào bất kỳ hệ thống nào mà không tốn một đồng chi phí API nào. Chúc các sếp "lên đồ" thành công!