---
title: "🚀 Tự động dự báo tồn kho và tạo đơn hàng với Google Sheets, GPT-4o mini và Slack"
description: "Hướng dẫn xây dựng workflow n8n tự động phân tích lịch sử bán hàng, dự báo nhu cầu bằng AI, cảnh báo tồn kho nguy cấp qua Slack và tạo đơn đặt hàng mua sắm."
slug: "tu-dong-du-bao-ton-kho-va-tao-don-hang-n8n"
tags: [n8n, automation, ai, google-sheets, slack, inventory-management]
keywords: [n8n workflow, tự động hóa kho hàng, forecast inventory, gpt-4o mini, google sheets automation, slack alert]
useCases: [Quản lý kho hàng, Tự động hóa chuỗi cung ứng, Cảnh báo tồn kho AI]
---

# 🚀 Tự động dự báo tồn kho và tạo đơn hàng với Google Sheets, GPT-4o mini và Slack

Các sếp làm trong ngành vận hành, quản lý chuỗi cung ứng hay bán lẻ chắc hẳn luôn đau đầu với bài toán kiểm kê tồn kho: Làm sao biết sản phẩm nào sắp hết để nhập thêm trước khi quá muộn? Tính toán số lượng đặt hàng thế nào cho chuẩn xác mà không bị tồn đọng vốn? 

Việc xử lý thủ công bằng tay trên Excel tốn rất nhiều thời gian, dễ sai sót và thường xuyên dẫn đến tình trạng hết hàng đột xuất (stockout). 

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code (No-code automation) giúp các sếp: tự động đọc lịch sử bán hàng, tính toán chỉ số tồn kho, nhờ **GPT-4o mini** dự báo nhu cầu, cảnh báo nguy cấp qua **Slack** và tự động sinh bản ghi Đơn đặt hàng (Purchase Orders) vào **Google Sheets**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Loại bỏ hoàn toàn công sức thủ công**: Hệ thống tự động gom dữ liệu, phân tích và đưa ra quyết định nhập hàng mỗi ngày.
- **Dự báo thông minh bằng AI**: Kết hợp sức mạnh của GPT-4o mini để đánh giá rủi ro chuỗi cung ứng và phân tích xu hướng 30 ngày tới.
- **Cảnh báo tức thời**: Bắn thông báo ngay lập tức lên Slack khi có sản phẩm chạm mức tồn kho nguy cấp (< 7 ngày).
- **Tối ưu dòng tiền**: Tự động tạo các bản ghi Purchase Orders (PO) với số lượng tối ưu, tránh tình trạng ôm hàng quá nhiều hoặc thiếu hụt.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Account**: Đã chuẩn bị sẵn Google Sheet chứa 3 tab: `Sales_History`, `Current_Inventory`, và `Forcast_Analysis`.
- **OpenAI API Key**: Để kết nối với mô hình GPT-4o mini.
- **Slack Workspace**: Tài khoản Slack và quyền kết nối Bot để gửi tin nhắn cảnh báo vào kênh bán hàng/kho vận.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sao chép mã JSON từ n8n (Link gốc: [Workflow #15706](https://n8n.io/workflows/15706)) và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các node sau:
- **Set Forecast Configuration**: Cập nhật lại `spreadsheet_id` của Google Sheet chính xác vào tham số cấu hình, đồng thời tinh chỉnh khung thời gian phân tích (lookback period, forecast horizon) nếu cần.
- **Fetch Sales History**, **Fetch Current Inventory**, **Write Forecast to Sheet**: Kết nối tài khoản `Google Sheets OAuth2 API` và đảm bảo tên các tab sheet khớp với tên chuẩn (`Sales_History`, `Current_Inventory`, `Forcast_Analysis`).
- **OpenAI Chat Model**: Thêm Credentials OpenAI và chọn đúng model `gpt-4o-mini`.
- **Send a message**: Kết nối tài khoản `Slack OAuth2 API` và điền đúng Channel ID (ví dụ `#sales-team` hoặc `#inventory-alerts`) để bot bắn tin cảnh báo.

#### 3. Kích hoạt ⚡️
- Bấm nút **When clicking 'Execute workflow'** để test thủ công lần đầu, kiểm tra luồng chạy qua các node `Build Forecast Dataset`, `Demand Forecast Agent` và `Generate Purchase Orders`.
- Sau khi kiểm tra dữ liệu trả về trên Google Sheets và Slack đã chính xác, bật nút **Active** để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Thay đổi Trigger**: Thay thế node `When clicking 'Execute workflow'` bằng node `Schedule Trigger` để hệ thống tự động chạy chạy dự báo vào 8:00 sáng mỗi ngày.
- **Mở rộng kênh thông báo**: Kết hợp thêm node Telegram hoặc Email để gửi báo cáo tóm tắt tổng hợp cho ban giám đốc.
- **Lưu trữ Log nâng cao**: Tích hợp thêm cơ sở dữ liệu như PostgreSQL hoặc Airtable để lưu lịch sử các lần chạy dự báo phục vụ việc phân tích xu hướng dài hạn.

### 📌 Kết luận
Việc tự động hóa quy trình dự báo tồn kho không chỉ giúp các sếp tiết kiệm hàng chục giờ làm việc mỗi tháng mà còn bảo vệ dòng tiền doanh nghiệp khỏi những sự cố đứt gãy nguồn hàng. Hãy import workflow này ngay hôm nay và tối ưu hóa chuỗi cung ứng của mình nhé!