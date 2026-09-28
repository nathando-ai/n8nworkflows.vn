---
title: "🚀 Tự động lên lịch bài đăng LinkedIn từ Google Sheets với Gemini & DALL·E"
description: "Giải pháp tự động tạo nội dung và hình ảnh, lên lịch đăng bài LinkedIn hoàn toàn không cần code, giúp doanh nghiệp tiết kiệm thời gian và tăng tương tác."
slug: "tang-lap-lich-bai-dang-linkedin-gsheet-gemini-dalle"
tags: [n8n, automation, no-code, google-sheets, linkedin, gemini, dalle-e, scheduling]
keywords: [n8n workflow, tự động hóa, LinkedIn, Google Sheets, Gemini, DALL·E, lên lịch đăng bài]
---

# 🚀 Tự động lên lịch bài đăng LinkedIn từ Google Sheets với Gemini & DALL·E

Bạn đang phải mất hàng giờ để viết nội dung, tạo hình ảnh và lên lịch đăng bài trên LinkedIn? Bạn muốn chuyển toàn bộ quy trình này thành một chuỗi tự động, không cần viết code, chỉ cần nhập dữ liệu vào Google Sheets và để n8n lo phần còn lại? Workflow này chính là giải pháp hoàn hảo cho bạn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút viết nội dung, tạo hình ảnh, lên lịch – thành một chuỗi tự động trong vài giây.
- **Chính xác & nhất quán**: Nội dung và hình ảnh được tạo bởi Gemini & DALL·E dựa trên prompt chuẩn, tránh sai sót khi viết tay.
- **Tăng tương tác**: Lên lịch đăng bài vào thời điểm tối ưu, giúp bài tiếp cận đúng đối tượng.
- **Hoạt động liên tục**: Khi đã kích hoạt, workflow chạy 24/7 mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Google Sheets**: Tài khoản Google, bảng tính chứa dữ liệu (cột tiêu đề, mô tả, ngày đăng, thời gian, v.v.).
- **Gemini API Key**: Đăng ký tại Google Cloud, bật Gemini API.
- **DALL·E API Key**: Đăng ký tại OpenAI, bật DALL·E 3.
- **LinkedIn API Credentials**: Tạo ứng dụng LinkedIn, lấy Client ID, Client Secret, và Access Token (hoặc OAuth 2.0 flow).
- **n8n**: Cài đặt phiên bản mới nhất (Self-hosted hoặc Cloud).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/12663) hoặc sao chép toàn bộ JSON.
2. Mở n8n Editor → **Import** → **Import from JSON** → dán JSON → **Import**.
3. Kiểm tra danh sách nodes đã xuất hiện.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cài đặt cần chỉnh |
|------|-------|-------------------|
| **Google Sheets** | Đọc dữ liệu từ bảng tính | *Spreadsheet ID*, *Sheet Name*, *Range* |
| **Gemini** | Tạo nội dung văn bản | *API Key*, *Prompt* (định dạng prompt tùy chỉnh) |
| **DALL·E** | Tạo hình ảnh | *API Key*, *Prompt* (định dạng prompt hình ảnh) |
| **LinkedIn** | Đăng bài lên LinkedIn | *Client ID*, *Client Secret*, *Access Token* |
| **Schedule** | Lên lịch chạy workflow | *Cron expression* (ví dụ `0 9 * * *` để chạy lúc 9h mỗi ngày) |
| **Webhook** (nếu có) | Nhận trigger từ bên ngoài | *Webhook URL*, *HTTP Method* |

> **Lưu ý**: Nếu workflow chưa có node “Schedule”, bạn có thể thêm node “Cron” để tự động kích hoạt workflow vào thời điểm mong muốn.

#### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (đảm bảo các credentials hoạt động).
2. Kiểm tra log: Đảm bảo không có lỗi, nội dung và hình ảnh được tạo đúng.
3. **Bật Active**: Đánh dấu workflow là *Active* để nó tự động chạy theo lịch.

### ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram notifications**: Thêm node “Slack” hoặc “Telegram” để nhận thông báo khi bài đăng thành công hoặc lỗi xảy ra.
- **Lưu log vào Google Sheets**: Sử dụng node “Google Sheets” để ghi lại ID bài đăng, thời gian, trạng thái.
- **Tùy chỉnh prompt**: Thêm biến động trong prompt Gemini/DALL·E dựa trên cột “Chủ đề” trong Google Sheets.
- **Định kỳ báo cáo**: Thêm node “Email” để gửi báo cáo hàng tuần về số lượng bài đăng, lượt tương tác.

### 📌 Kết luận
Workflow “Create and schedule LinkedIn posts from Google Sheets with Gemini and DALL·E” là công cụ mạnh mẽ giúp các sếp tiết kiệm thời gian, giảm thiểu sai sót và tăng hiệu quả truyền thông trên LinkedIn. Hãy thử ngay, tùy chỉnh theo nhu cầu và chia sẻ trải nghiệm của mình với cộng đồng n8n!