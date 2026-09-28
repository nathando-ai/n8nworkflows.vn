---
title: "🚀 Kết Nối AI Agents với API Deal eBay qua MCP Server – Tự Động Hóa Quản Lý Giao Dịch"
description: "Giải pháp tự động 100% không cần code giúp doanh nghiệp lấy dữ liệu deal, sự kiện và chi tiết từ eBay, đồng bộ với AI Agents qua MCP Server."
slug: "ket-noi-ai-agents-voi-api-deal-ebay-qua-mcp-server"
tags: [n8n, automation, no-code, eBay, AI, MCP]
keywords: [n8n workflow, tự động hóa, eBay API, MCP server, AI agents]
---

# 🚀 Kết Nối AI Agents với API Deal eBay qua MCP Server – Tự Động Hóa Quản Lý Giao Dịch

Bạn đang phải làm thủ công nhập dữ liệu deal, sự kiện và chi tiết từ eBay vào hệ thống AI của mình? Mỗi lần cập nhật mới, bạn phải copy‑paste, kiểm tra lỗi, và lo lắng về độ trễ.  
Workflow này sẽ **tự động** lấy dữ liệu từ eBay Deal API, gửi lên MCP Server, và ngay lập tức kích hoạt AI Agents để xử lý, phân tích hoặc đưa ra quyết định. Bạn không cần viết dòng code, chỉ cần cấu hình một vài credential và bật workflow.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn thao tác thủ công, dữ liệu cập nhật ngay khi có sự kiện mới.  
- **Độ chính xác cao**: Truyền dữ liệu trực tiếp từ API, giảm thiểu lỗi nhập liệu.  
- **Tích hợp AI ngay lập tức**: MCP Server gửi dữ liệu ngay cho AI Agents, giúp phản hồi nhanh hơn.  
- **Hoạt động liên tục 24/7**: Khi có deal mới, hệ thống tự động xử lý mà không cần can thiệp.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
| Dịch vụ / Credential | Mô tả | Địa chỉ / Tài khoản |
|-----------------------|-------|----------------------|
| **eBay API Key** | Key để truy cập Deal API. | https://developer.ebay.com/ |
| **MCP Server URL & API Key** | Địa chỉ server và key để nhận trigger. | Tùy chỉnh trong node `Deal MCP Server`. |
| **n8n Self-hosted** | VPS hoặc Docker container chạy n8n. | Tùy chọn của bạn. |
| **Internet** | Kết nối ổn định tới eBay và MCP Server. | N/A |
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON của workflow từ link gốc:  
   <https://n8n.io/workflows/5564> (hoặc copy nội dung JSON).  
2. Mở **n8n Editor**, chọn **Import** → **Import from File** hoặc **Import from Clipboard**.  
3. Chọn file JSON hoặc dán nội dung, rồi nhấn **Import**.  
4. Workflow sẽ xuất hiện trong danh sách workflow của bạn.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên Node | Hướng dẫn cấu hình |
|------|----------|---------------------|
| 1 | **Deal MCP Server** | - Chọn **Credential**: MCP Server (URL + API Key). <br>- Đặt **Trigger Interval** (nếu cần). |
| 2 | **List Deal Items** | - **HTTP Method**: GET <br>- **URL**: `https://api.ebay.com/commerce/deals/v1/deal` <br>- **Headers**: `Authorization: Bearer <eBay API Key>` |
| 3 | **List eBay Events** | - **HTTP Method**: GET <br>- **URL**: `https://api.ebay.com/commerce/deals/v1/event` <br>- **Headers**: `Authorization: Bearer <eBay API Key>` |
| 4 | **Get Event Details** | - **HTTP Method**: GET <br>- **URL**: `https://api.ebay.com/commerce/deals/v1/event/{{ $json["eventId"] }}` <br>- **Headers**: `Authorization: Bearer <eBay API Key>` |
| 5 | **List Event Items** | - **HTTP Method**: GET <br>- **URL**: `https://api.ebay.com/commerce/deals/v1/event/{{ $json["eventId"] }}/items` <br>- **Headers**: `Authorization: Bearer <eBay API Key>` |

> **Lưu ý**:  
> - Đảm bảo **eBay API Key** có quyền truy cập Deal API.  
> - Nếu API yêu cầu pagination, bạn có thể thêm node **Pagination** hoặc xử lý trong **Set** node.  
> - Kiểm tra **Response** của từng node trong tab **Execute Workflow** để xác nhận dữ liệu.

### 3. Kích hoạt ⚡️

1. **Test run**: Chạy workflow với nút **Execute Workflow** để xem dữ liệu mẫu.  
2. Kiểm tra **Output** của mỗi node, đảm bảo không có lỗi.  
3. Khi mọi thứ ổn, bật **Active** toggle ở góc trên bên phải.  
4. Workflow sẽ tự động chạy khi MCP Server gửi trigger.

## ✍️ Mẹo & gợi ý nâng cao

- **Gửi báo cáo qua Slack**: Thêm node **Slack** sau node **List Event Items** để thông báo khi có deal mới.  
- **Lưu log vào Google Sheets**: Dùng node **Google Sheets** để ghi lại lịch sử deal, giúp phân tích sau này.  
- **Tích hợp Telegram**: Thêm node **Telegram** để nhận tin nhắn nhanh chóng khi có deal quan trọng.  
- **Xử lý lỗi**: Thêm node **If** để kiểm tra `statusCode` của HTTP request, gửi email cảnh báo nếu lỗi.  

## 📌 Kết luận

Workflow “Connect AI Agents to eBay Deal API with MCP Server” là giải pháp **đơn giản, mạnh mẽ** cho các doanh nghiệp muốn tự động hóa quy trình lấy dữ liệu deal từ eBay và truyền ngay tới AI Agents.  
Bạn chỉ cần một vài credential, vài lần cấu hình, và workflow sẽ làm việc 24/7, giúp bạn tập trung vào chiến lược kinh doanh thay vì thao tác thủ công.  

**Hãy thử ngay** – cài đặt n8n, import workflow, và cảm nhận sự khác biệt!