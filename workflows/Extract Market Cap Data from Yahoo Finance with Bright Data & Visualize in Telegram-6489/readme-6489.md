---
title: "🚀 Tự Động Cào Dữ Liệu Vốn Hóa Thị Trường Từ Yahoo Finance & Gửi Biểu Đồ Lên Telegram"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động cào dữ liệu tài chính qua Bright Data, lưu trữ vào Google Sheets và trực quan hóa biểu đồ gửi thẳng lên Telegram."
slug: "tu-dong-cao-du-lieu-yahoo-finance-bright-data-telegram"
tags: [n8n, automation, no-code, bright-data, telegram, google-sheets]
keywords: [n8n workflow, cào dữ liệu yahoo finance, bright data api, telegram bot automation, google sheets n8n]
---

# 🚀 Tự Động Cào Dữ Liệu Vốn Hóa Thị Trường Từ Yahoo Finance & Gửi Biểu Đồ Lên Telegram

Các nhà đầu tư, nhà phân tích tài chính hay anh em làm crypto thường xuyên đối mặt với nỗi đau: Mất hàng giờ đồng hồ mỗi ngày để tìm kiếm, tổng hợp dữ liệu vốn hóa (Market Cap) từ Yahoo Finance, thủ công copy paste vào Excel rồi vẽ biểu đồ báo cáo. Việc này vừa tốn thời gian, dễ sai sót lại không thể cập nhật liên tục theo thời gian thực.

Giải pháp ở đây là gì? Workflow n8n tự động hóa 100% không cần code dưới đây sẽ giúp các sếp nhập từ khóa (keyword), hệ thống tự động cào dữ liệu qua Bright Data, lưu vào Google Sheets và sinh ra biểu đồ trực quan gửi thẳng vào Telegram trong tích tắc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Chỉ cần nhập từ khóa (VD: "AI", "Crypto", "MSFT") qua Form, hệ thống tự động làm từ A-Z.
- **Dữ liệu chuẩn xác**: Khai thác dữ liệu mạnh mẽ từ Yahoo Finance thông qua hạ tầng cào dữ liệu chuyên nghiệp Bright Data.
- **Lưu trữ thông minh**: Tự động lọc và lưu lịch sử dữ liệu vào Google Sheets để tiện tra cứu.
- **Trực quan sinh động**: Tự động vẽ biểu đồ vốn hóa (tính bằng tỷ USD) và gửi ảnh PNG trực tiếp qua Telegram bot.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Bright Data** kèm API Token và Dataset ID (`gd_lmrpz3vxmz972ghd7`).
- **Google Sheets Credentials** để kết nối và lưu dữ liệu.
- **Telegram Bot Token** và Chat ID để gửi thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (hoặc tải file JSON từ nguồn gốc) và dán trực tiếp vào n8n Editor của mình. Workflow bao gồm 10 nodes được tổ chức bài bản theo các phân khu rõ ràng.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node quan trọng sau:

- **🟩 Form Trigger**: Nơi người dùng nhập từ khóa cần cào dữ liệu (VD: `"AI"`, `"Crypto"`, `"MSFT"`).
- **🚀 Trigger Scraping1 (HTTP Request to Bright Data)**: Điền API Key của Bright Data và đảm bảo Dataset ID đúng chuẩn (`gd_lmrpz3vxmz972ghd7`) với cấu hình `discover_by: keyword`.
- **🕐 Wait 1 minute1 & 🟡 Check Delivery Status**: Cơ chế chờ và kiểm tra trạng thái snapshot từ Bright Data cho đến khi trả về trạng thái `"ready"`.
- **📊 Filtered Output & Save to Sheet**: Kết nối tài khoản Google Sheets của các sếp, chọn đúng file và sheet để node tiến hành `append` dữ liệu.
- **🧮 Generate Chart Payload & 🌐 Generate PNG from Chart**: Code node chuẩn bị dữ liệu (labels + giá trị market cap tỷ đô) và gọi QuickChart.io API để xuất ra file ảnh PNG.
- **📤 Send Chart on Telegram**: Cấu hình Telegram Bot Credentials, điền Chat ID và gắn file ảnh PNG từ bước trước vào để gửi kèm caption sắc nét.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng cách điền form với một từ khóa bất kỳ.
- Kiểm tra kết quả trên Google Sheets và Telegram.
- Nếu mọi thứ chạy trơn tru, hãy bật công tắc **Active** để hệ thống tự động hóa hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Ngoài Telegram, các sếp có thể kết hợp thêm node Slack hoặc Discord để gửi báo cáo đồng thời cho team kinh doanh.
- **Lưu log chi tiết**: Thiết lập thêm nhánh ghi lỗi vào Google Sheets hoặc bắn alert về Telegram nếu quá trình cào dữ liệu từ Bright Data gặp sự cố.
- **Lên lịch tự động (Cron):** Thay vì dùng Form Trigger thủ công, các sếp có thể đổi thành Schedule Trigger để hệ thống tự động cào dữ liệu thị trường định kỳ mỗi sáng.

### 📌 Kết luận
Workflow này là một cỗ máy tự động hóa cực kỳ mạnh mẽ giúp các sếp tiết kiệm hàng đống thời gian nghiên cứu thị trường tài chính và crypto. Hãy triển khai ngay lên VPS của mình và tận hưởng sức mạnh của No-Code automation!