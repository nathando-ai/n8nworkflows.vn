---
title: "🚀 Tạo URL Thông Minh với BioURL.link – Định Hướng Geo, Thiết Bị & Ngôn Ngữ"
description: "Giải pháp tự động tạo URL ngắn thông minh, tùy chỉnh theo vị trí, thiết bị và ngôn ngữ, giúp doanh nghiệp tối ưu chiến dịch marketing mà không cần viết code."
slug: "tao-url-thong-minh-bio-url-link-geo-device-language"
tags: [n8n, automation, no-code, bioURL, url-shortener, targeting]
keywords: [n8n workflow, tự động hóa, URL ngắn, targeting, BioURL, geo targeting]
---

# 🚀 Tạo URL Thông Minh với BioURL.link – Định Hướng Geo, Thiết Bị & Ngôn Ngữ

Bạn đang phải thủ công tạo các liên kết ngắn, phân phối chúng qua nhiều kênh marketing, và lo lắng về việc mỗi liên kết có thể không hiển thị đúng nội dung cho người dùng dựa trên vị trí, thiết bị hay ngôn ngữ?  
Workflow này sẽ **tự động** nhận link gốc, gửi tới API của BioURL.link để tạo URL ngắn **định hướng** (geo, device, language) và trả về ngay link ngắn cho bạn – hoàn toàn không cần code, chỉ cần một vài bước cấu hình.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động tạo URL ngắn trong vài giây thay vì thủ công.  
- **Chính xác & tùy chỉnh**: Định hướng theo địa lý, thiết bị, ngôn ngữ ngay từ nguồn.  
- **Tăng hiệu quả marketing**: Link luôn đưa người dùng tới nội dung phù hợp, nâng cao tỷ lệ chuyển đổi.  
- **Liên tục hoạt động**: Không cần giám sát, workflow chạy 24/7.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Tài khoản BioURL.link**: Đăng ký và lấy **API Key**.  
- **N8n**: Cài đặt phiên bản mới nhất (>= v0.200).  
- **Webhook URL**: Được n8n cung cấp khi tạo node Webhook.  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Mở n8n, vào **Workflows** → **Import**.  
2. Chọn **Import from file** và tải file JSON của workflow (điểm 3 trong danh sách nodes).  
3. Hoặc copy toàn bộ JSON vào khung **Paste JSON** và nhấn **Import**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên node | Cấu hình cần chỉnh | Ghi chú |
|------|----------|--------------------|---------|
| 1 | **Receive Link Webhook** | `path` = `shorten-link` (đã được thiết lập sẵn) <br> `httpMethod` = `POST` | Đảm bảo endpoint này được expose qua HTTPS (người dùng sẽ POST link gốc). |
| 2 | **HTTP Request** | - `URL` = `https://api.biourl.link/v1/shorten` <br> - `Method` = `POST` <br> - `Authentication` = `API Key` (đặt trong Credentials) <br> - `Body Parameters` = `{"url":"{{ $json["url"] }}","geo":"{{ $json["geo"] }}","device":"{{ $json["device"] }}","language":"{{ $json["language"] }}"}` | - Nếu không muốn tùy chỉnh, bỏ các trường `geo`, `device`, `language`. <br> - Đảm bảo `Content-Type` là `application/json`. |
| 3 | **Respond with Shortened URL** | - `Response Body` = `{{ $json["shortUrl"] }}` | Trả về link ngắn cho client. |

> **Tip**: Để tránh lỗi, hãy kiểm tra API Key trong Credentials trước khi chạy workflow.

### 3. Kích hoạt ⚡️

1. **Test run**: Nhấn **Execute Workflow** trong n8n, gửi payload mẫu qua Postman:
   ```json
   {
     "url": "https://example.com",
     "geo": "US",
     "device": "mobile",
     "language": "en"
   }
   ```
2. Kiểm tra kết quả: Response body sẽ là URL ngắn.  
3. Khi mọi thứ ổn, bật **Active** cho workflow.

## ✍️ Mẹo & gợi ý nâng cao

- **Tích hợp Slack**: Thêm node Slack để gửi link ngắn ngay khi được tạo.  
- **Lưu log**: Sử dụng node Google Sheets hoặc Airtable để ghi lại tất cả các link đã được tạo.  
- **Báo cáo định kỳ**: Thêm node “Cron” + “HTTP Request” để lấy thống kê từ BioURL và gửi email báo cáo.  
- **Xử lý lỗi**: Thêm node “If” để kiểm tra `status` của API và gửi cảnh báo khi có lỗi.  

## 📌 Kết luận

Workflow “Create Smart URLs with BioURL.link's Geo, Device & Language Targeting” giúp các sếp nhanh chóng triển khai hệ thống URL ngắn thông minh, giảm thiểu công việc thủ công và tối ưu trải nghiệm người dùng.  
Hãy **cài đặt ngay** và trải nghiệm sự tiện lợi mà n8n mang lại!