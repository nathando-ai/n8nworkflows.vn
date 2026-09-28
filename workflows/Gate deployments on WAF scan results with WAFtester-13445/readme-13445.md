---
title: "🚀 Tự động chặn deployment khi quét WAF thất bại với WAFtester và n8n"
description: "Hướng dẫn xây dựng cổng kiểm soát bảo mật (Security Gate) cho CI/CD pipeline tự động quét WAF và chặn deploy nếu phát hiện lỗ hổng."
slug: "tu-dong-chan-deployment-waf-scan-waftester-n8n"
tags: [n8n, automation, devops, security, waf, cicd]
keywords: [n8n workflow, WAFtester, CI/CD security gate, tự động hóa devops, bảo mật ứng dụng web]
---

# 🚀 Tự động chặn deployment khi quét WAF thất bại với WAFtester

Trong quy trình CI/CD hiện đại, việc đẩy code lên môi trường production diễn ra rất nhanh chóng. Tuy nhiên, tốc độ thường đi kèm với rủi ro bảo mật nếu các ứng dụng web chưa được cấu hình tường lửa (WAF) đúng cách. Việc kiểm tra thủ công bằng tay vừa tốn thời gian, vừa dễ bỏ sót.

Workflow n8n này sinh ra để giải quyết triệt để vấn đề đó: tự động đóng vai trò là một **Security Gate** trong CI/CD pipeline, tiến hành nhận diện WAF, chạy quét bảo mật thông qua công cụ **WAFtester**, phân tích kết quả và tự động chặn (block) việc deploy nếu không đạt ngưỡng an toàn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và kết nối mượt mà với các hệ thống CI/CD, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Tích hợp trực tiếp vào CI/CD pipeline mà không cần nhân sự can thiệp thủ công.
- **Bảo mật chủ động:** Chặn đứng các bản deployment kém an toàn, chưa vượt qua bài kiểm tra WAF.
- **Phản hồi minh bạch:** Trả về mã trạng thái HTTP chuẩn (200 cho Pass, 422 cho Fail) kèm chi tiết lý do chặn trong response body.
- **Hoạt động liên tục 24/7:** Xử lý bất đồng bộ (async scan) thông qua cơ chế polling thông minh.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- WAFtester MCP server (được chạy sẵn qua Docker).
- CI/CD Pipeline (GitHub Actions, GitLab CI, Jenkins...) có khả năng bắn HTTP POST request.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy toàn bộ mã nguồn JSON của workflow n8n này, sau đó paste trực tiếp vào n8n Editor của các sếp (chọn **Import from JSON**).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 9 nodes chính hoạt động nhịp nhàng với nhau. Các sếp cần chú ý cấu hình kỹ các phần sau:

- **Deploy Webhook (`webhook`):** Node nhận tín hiệu từ CI/CD pipeline. Endpoint mặc định là `/waf-security-gate` với phương thức `POST`. Payload gửi lên cần có cấu trúc JSON dạng:
  ```json
  {
    "target": "https://your-staging-url.com",
    "categories": ["sqli", "xss"]
  }
  ```
- **Detect WAF (`httpRequest`) & Start Scan (`httpRequest`):** Hai node này gọi tới WAFtester MCP server. Các sếp cần cấu hình biến môi trường (`WAFTESTER_MCP_URL`) trong n8n để trỏ đúng địa chỉ của WAFtester server.
- **Wait for Scan (`wait`) & Poll Task Status (`httpRequest`):** Thực hiện quét bất đồng bộ với độ trễ (polling delay) khoảng 30 giây để chờ kết quả từ WAFtester trả về.
- **Parse Results (`code`):** Node JavaScript xử lý tính toán tỷ lệ phát hiện (detection rate) dựa trên kết quả quét.
- **Pass or Fail? (`if`):** So sánh tỷ lệ phát hiện với ngưỡng cho phép (`WAF_PASS_THRESHOLD`). 
- **Respond Pass / Respond Fail (`respondToWebhook`):** Trả về HTTP `200` để pipeline tiếp tục deploy, hoặc HTTP `422` để ngắt kết nối và báo lỗi.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test run) bằng một request mẫu từ Postman hoặc curl tới Webhook URL.
- Kiểm tra các nhánh Pass/Fail hoạt động chính xác.
- Bật công tắc **Active** để đưa workflow vào trạng thái vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp cảnh báo:** Thêm node gửi thông báo qua **Slack** hoặc **Telegram** mỗi khi có một deployment bị chặn (Fail) để đội ngũ DevOps nắm bắt kịp thời.
- **Lưu lịch sử:** Lưu kết quả quét vào **Google Sheets** hoặc **Database** để làm báo cáo bảo mật định kỳ hàng tuần/tháng.
- **Tinh chỉnh ngưỡng quét:** Tùy chỉnh biến `WAF_PASS_THRESHOLD` linh hoạt theo từng môi trường (Staging có thể nới lỏng, Production áp dụng cấu hình khắt khe nhất).

### 📌 Kết luận
Việc tích hợp Security Gate vào CI/CD bằng n8n và WAFtester giúp doanh nghiệp tự động hóa khâu kiểm tra bảo mật mà không tốn nhiều công sức vận hành thủ công. Hãy triển khai ngay hôm nay để nâng cấp sự an toàn cho các ứng dụng web của các sếp!