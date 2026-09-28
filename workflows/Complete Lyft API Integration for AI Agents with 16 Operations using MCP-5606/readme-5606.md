---
title: "🚀 Tích hợp hoàn chỉnh API Lyft cho AI Agents với 16 thao tác sử dụng MCP"
description: "Giải pháp tự động hóa 100% không cần code, giúp AI Agents tương tác với Lyft API nhanh chóng và hiệu quả."
slug: "tich-hop-hon-chinh-api-lyft-cho-ai-agents"
tags: [n8n, automation, no-code, lyft, ai, integration]
keywords: [n8n workflow, tự động hóa, Lyft API, AI agents, MCP, no-code]
---

# 🚀 Tích hợp hoàn chỉnh API Lyft cho AI Agents với 16 thao tác sử dụng MCP

Bạn đang xây dựng một AI Agent muốn có thể đặt xe, lấy thông tin chuyến đi, đánh giá tài xế, hay thậm chí quản lý sandbox rides? Thường thì việc viết mã để gọi từng endpoint của Lyft API sẽ tốn thời gian và dễ lỗi. Workflow này sẽ giúp bạn **tự động hóa toàn bộ quy trình** mà không cần viết một dòng code, chỉ cần cấu hình một vài thông số và chạy.

:::info[Hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 <https://tino.vn/vps-n8n?affid=388> (🎁 Mã giảm giá: **VPSN8N** – giảm tới 39%)  
👉 <https://my.bnix.one/aff.php?aff=172> (VPS Xeon 4GB chỉ 50k/tháng)  
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút viết code xuống vài giây chạy workflow.  
- **Độ chính xác cao**: Mọi request được kiểm tra, lỗi được ghi log ngay lập tức.  
- **Tích hợp linh hoạt**: Dễ dàng mở rộng thêm Slack, Telegram, hoặc gửi báo cáo định kỳ.  
- **Hoạt động liên tục**: Khi chạy trên VPS, workflow luôn sẵn sàng 24/7.  
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
| Dịch vụ / API | Mô tả | Cách lấy |
|---|---|---|
| **Lyft API Key** | Để gọi các endpoint của Lyft. | Đăng ký tại <https://developer.lyft.com/> và tạo ứng dụng. |
| **n8n Credentials** | Đăng nhập vào n8n, tạo credential “Lyft API” (OAuth2). | Trong n8n, vào Credentials → New Credential → Lyft API. |
| **MCP Server** | Để nhận trigger từ AI Agent. | Cài đặt MCP Server (đọc tài liệu tại <https://github.com/mcp-xyz/mcp>) và cấu hình URL trong node `Lyft MCP Server`. |
| **Optional – Slack / Telegram** | Để gửi thông báo. | Tạo bot và lấy token. |
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON từ <https://n8n.io/workflows/5606> hoặc copy toàn bộ JSON.  
2. Mở n8n Editor → `Import` → `Import from JSON` → dán JSON.  
3. Nhấn **Import**. Workflow sẽ xuất hiện trong danh sách.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên Node | Cấu hình cần thiết | Ghi chú |
|---|---|---|---|
| `Lyft MCP Server` | `mcpTrigger` | URL endpoint của MCP, secret key (nếu có). | Đảm bảo MCP Server đang chạy và có thể gửi request tới n8n. |
| `Retrieve Cost Estimate` | `httpRequestTool` | URL: `https://api.lyft.com/v1/cost_estimates`, Method: GET, Headers: `Authorization: Bearer <API_KEY>`. | Thêm query params `start_latitude`, `start_longitude`, `end_latitude`, `end_longitude`. |
| `List Nearby Drivers` | `httpRequestTool` | URL: `https://api.lyft.com/v1/drivers/nearby`, Method: GET, Headers: `Authorization: Bearer <API_KEY>`. | Thêm query params `latitude`, `longitude`. |
| `Retrieve Pickup ETA` | `httpRequestTool` | URL: `https://api.lyft.com/v1/eta`, Method: GET, Headers: `Authorization: Bearer <API_KEY>`. | Thêm query params `latitude`, `longitude`. |
| `List Ride Types` | `httpRequestTool` | URL: `https://api.lyft.com/v1/ride_types`, Method: GET, Headers: `Authorization: Bearer <API_KEY>`. | |
| `Retrieve User Profile` | `httpRequestTool` | URL: `https://api.lyft.com/v1/profile`, Method: GET, Headers: `Authorization: Bearer <API_KEY>`. | |
| `List User Rides` | `httpRequestTool` | URL: `https://api.lyft.com/v1/rides`, Method: GET, Headers: `Authorization: Bearer <API_KEY>`. | |
| `Request New Ride` | `httpRequestTool` | URL: `https://api.lyft.com/v1/rides`, Method: POST, Headers: `Authorization: Bearer <API_KEY>`. | Body: JSON với `ride_type_id`, `start_latitude`, `start_longitude`, `end_latitude`, `end_longitude`. |
| `Retrieve Ride Details` | `httpRequestTool` | URL: `https://api.lyft.com/v1/rides/{ride_id}`, Method: GET, Headers: `Authorization: Bearer <API_KEY>`. | |
| `Cancel Ride Request` | `httpRequestTool` | URL: `https://api.lyft.com/v1/rides/{ride_id}`, Method: DELETE, Headers: `Authorization: Bearer <API_KEY>`. | |
| `Update Ride Destination` | `httpRequestTool` | URL: `https://api.lyft.com/v1/rides/{ride_id}/destination`, Method: PATCH, Headers: `Authorization: Bearer <API_KEY>`. | Body: JSON với `latitude`, `longitude`. |
| `Submit Ride Rating` | `httpRequestTool` | URL: `https://api.lyft.com/v1/rides/{ride_id}/rating`, Method: POST, Headers: `Authorization: Bearer <API_KEY>`. | Body: JSON với `rating`, `comment`. |
| `Retrieve Ride Receipt` | `httpRequestTool` | URL: `https://api.lyft.com/v1/rides/{ride_id}/receipt`, Method: GET, Headers: `Authorization: Bearer <API_KEY>`. | |
| `Set Prime Time Percentage` | `httpRequestTool` | URL: `https://api.lyft.com/v1/prime_time`, Method: PATCH, Headers: `Authorization: Bearer <API_KEY>`. | Body: JSON với `percentage`. |
| `Update Sandbox Ride Status` | `httpRequestTool` | URL: `https://sandbox-api.lyft.com/v1/rides/{ride_id}/status`, Method: PATCH, Headers: `Authorization: Bearer <API_KEY>`. | Body: JSON với `status`. |
| `Set Sandbox Ride Types` | `httpRequestTool` | URL: `https://sandbox-api.lyft.com/v1/ride_types`, Method: PATCH, Headers: `Authorization: Bearer <API_KEY>`. | Body: JSON với `ride_types`. |
| `Update Driver Availability` | `httpRequestTool` | URL: `https://api.lyft.com/v1/drivers/{driver_id}/availability`, Method: PATCH, Headers: `Authorization: Bearer <API_KEY>`. | Body: JSON với `available`. |

> **Lưu ý**: Tất cả các node `httpRequestTool` đều cần credential “Lyft API” đã được cấu hình trong n8n. Nếu chưa có, hãy tạo credential mới và gán vào từng node.

### 3. Kích hoạt ⚡️
1. **Test run**: Chọn một node, click **Execute Node** để kiểm tra kết quả.  
2. Kiểm tra log trong tab **Execution** để xác nhận không có lỗi.  
3. Khi mọi thứ ổn, bật **Active** cho workflow.  
4. Đảm bảo MCP Server gửi trigger đúng định dạng JSON (đọc tài liệu MCP).

## ✍️ Mẹo & gợi ý nâng cao
- **Slack Notification**: Thêm node Slack → “Send Message” sau mỗi hành động quan trọng (đặt xe, hủy, đánh giá).  
- **Telegram Bot**: Sử dụng node Telegram → “Send Message” để gửi thông báo tới nhóm.  
- **Logging**: Thêm node “Write Binary File” để lưu log JSON vào bucket S3 hoặc Google Drive.  
- **Scheduled Reports**: Dùng node “Cron” để chạy workflow hàng ngày và gửi báo cáo tổng hợp (số chuyến, doanh thu, thời gian trung bình).  
- **Error Handling**: Thêm node “Set” để kiểm tra status code, và node “If” để chuyển sang node “Send Email” khi lỗi.  

## 📌 Kết luận
Workflow này là công cụ **đánh dấu** cho các sếp muốn nhanh chóng triển khai AI Agents có khả năng tương tác với Lyft mà không cần viết code. Bạn chỉ cần cấu hình một vài credential, chạy thử, và workflow sẽ tự động thực hiện mọi thao tác từ lấy ước tính giá, đặt xe, đến đánh giá tài xế. Hãy **đặt nó lên VPS** và bắt đầu khai thác sức mạnh của Lyft API ngay hôm nay!