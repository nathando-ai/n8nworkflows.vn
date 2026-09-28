---
title: "🚀 Tự động chụp ảnh màn hình Website theo yêu cầu qua Webhook với n8n và ScreenshotMachine"
description: "Hướng dẫn xây dựng hệ thống tự động chụp ảnh màn hình website (screenshot) on-demand sử dụng n8n, ScreenshotMachine API và cơ chế bảo mật SSRF an toàn."
slug: "tu-dong-chup-anh-man-hinh-website-voi-n8n-va-screenshotmachine"
tags: [n8n, automation, screenshot, webhook, security, api]
keywords: [n8n workflow, chụp ảnh màn hình website, screenshotmachine api, webhook n8n, chống ssrf, tự động hóa no-code]
---

# 🚀 Tự động chụp ảnh màn hình Website theo yêu cầu qua Webhook

Trong quá trình vận hành hệ thống, việc phải chụp ảnh màn hình (screenshot) các trang web một cách thủ công để làm báo cáo, kiểm tra giao diện hay lưu trữ dữ liệu tốn rất nhiều thời gian và công sức. Nếu các sếp đang tìm kiếm một giải pháp tự động hóa 100% không cần code để tích hợp tính năng này vào ứng dụng riêng, thì đây chính là workflow hoàn hảo!

Workflow này giúp tự động nhận yêu cầu qua Webhook, xác thực tính hợp lệ và bảo mật của URL (chống tấn công SSRF), gọi ScreenshotMachine API để chụp ảnh màn hình và trả kết quả ngay lập tức cho người gọi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Nhận URL và trả về ảnh chụp màn hình thông qua API/Webhook chỉ trong vài giây.
- **Bảo mật tối ưu:** Tích hợp tầng kiểm tra chống giả mạo yêu cầu phía máy chủ (SSRF), chặn các URL truy cập nội bộ hoặc localhost độc hại.
- **Linh hoạt tích hợp:** Dễ dàng kết nối với CRM, hệ thống quản trị, chatbot hoặc các ứng dụng web riêng của doanh nghiệp.
- **Hoạt động bền bỉ:** Chạy 24/7 trên nền tảng n8n self-hosted, không giới hạn tác vụ thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **ScreenshotMachine API Key:** Tài khoản và API Key từ [ScreenshotMachine](https://www.screenshotmachine.com/) để thực hiện tính năng chụp ảnh.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ thư viện n8n (Link gốc: [n8n.io/workflows/4594](https://n8n.io/workflows/4594)) và import trực tiếp vào n8n Editor của mình, hoặc sử dụng tính năng copy/paste JSON node.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 7 nodes chính hoạt động nhịp nhàng. Các sếp cần chú ý cấu hình các điểm sau:

- **Receive URL Webhook (`webhook`):** Node này lắng nghe yêu cầu POST từ bên ngoài. Nó mong đợi một định dạng JSON body chứa thuộc tính `url` (đường dẫn website cần chụp). Hãy lấy Production URL của webhook này để tích hợp vào ứng dụng của các sếp.
- **Resolve URL (HEAD Request) (`httpRequest`):** Thực hiện một HTTP HEAD request tới URL nhận được để kiểm tra tính khả dụng, xem website có thể truy cập được không và xử lý các đường chuyển hướng (redirects).
- **Validate URL for SSRF (`code`):** Node JavaScript tùy chỉnh giúp phân tích cú pháp chuỗi URL, đảm bảo giao thức HTTP/HTTPS hợp lệ và ngăn chặn các lỗ hổng SSRF (chặn truy cập vào dải IP nội bộ hoặc localhost).
- **IF URL Valid (`if`):** Phân nhánh luồng xử lý dựa trên kết quả kiểm tra bảo mật ở node trước.
  - Nếu hợp lệ 👉 Chuyển sang bước chụp ảnh màn hình.
  - Nếu không hợp lệ 👉 Trả về thông báo lỗi.
- **Take Screenshot (`httpRequest`):** Node gửi HTTP GET request đến ScreenshotMachine API với URL đã được xác thực. **Lưu ý quan trọng:** Các sếp nhớ thay thế chuỗi `'YOUR_API_KEY'` trong tham số URL bằng API Key thực tế của tài khoản ScreenshotMachine.
- **Respond with Screenshot Data / Respond with Validation Error (`respondToWebhook`):** Trả kết quả dữ liệu ảnh chụp màn hình hoặc thông báo lỗi về cho ứng dụng gọi webhook ban đầu.

#### 3. Kích hoạt ⚡️
- Thực hiện một vài request test (ví dụ dùng Postman hoặc cURL) bắn vào Webhook URL để kiểm tra dữ liệu trả về.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow chính thức vận hành.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống tối ưu hơn, các sếp có thể mở rộng workflow này với các ý tưởng sau:
- **Lưu trữ tự động:** Tích hợp thêm node Google Drive hoặc AWS S3 để lưu lại file ảnh chụp màn hình thay vì chỉ trả về dữ liệu thô qua webhook.
- **Gửi thông báo:** Kết hợp gửi kết quả hoặc thông báo lỗi về kênh Telegram hoặc Slack nội bộ để đội ngũ kỹ thuật dễ dàng theo dõi.
- **Log lịch sử:** Lưu lại danh sách các URL đã được yêu cầu chụp vào Google Sheets hoặc Airtable để phục vụ việc thống kê.

### 📌 Kết luận
Workflow tự động chụp ảnh màn hình website qua Webhook này là một mảnh ghép tuyệt vời giúp tối ưu hóa các tác vụ tự động hóa liên quan đến xử lý hình ảnh và kiểm tra giao diện web. Hãy triển khai ngay lên hệ thống n8n của các sếp để nâng tầm tự động hóa doanh nghiệp!