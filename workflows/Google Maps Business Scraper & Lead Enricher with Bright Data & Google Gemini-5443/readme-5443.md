---
title: "🚀 Tự động quét Google Maps & Làm giàu dữ liệu khách hàng tiềm năng với Bright Data & Google Gemini"
description: "Hướng dẫn chi tiết workflow n8n giúp cào dữ liệu doanh nghiệp từ Google Maps, kết hợp AI Google Gemini và MCP để làm giàu thông tin và lưu trữ tự động."
slug: "google-maps-business-scraper-bright-data-gemini"
tags: [n8n, automation, lead-generation, bright-data, google-gemini, ai]
keywords: [n8n workflow, google maps scraper, bright data, google gemini, lead generation automation]
---

# 🚀 Tự động quét Google Maps & Làm giàu dữ liệu khách hàng tiềm năng với Bright Data & Google Gemini

Việc đi tìm kiếm khách hàng tiềm năng (Lead Generation) bằng tay trên Google Maps cực kỳ tốn thời gian: vừa phải copy, paste thông tin từng doanh nghiệp, vừa phải kiểm tra website, mạng xã hội, số điện thoại... Quy trình thủ công này không chỉ làm giảm năng suất của đội ngũ sales mà dữ liệu thu về lại thiếu đồng bộ.

Giải pháp cho các sếp đây! Workflow n8n tự động hóa 100% này sẽ kết hợp sức mạnh của **Bright Data**, **Google Gemini AI**, và **MCP (Model Context Protocol)** để tự động cào dữ liệu từ Google Maps/Yelp, cấu trúc hóa thông tin và lưu thẳng vào Google Sheets hoặc ghi ra ổ cứng. Không cần tốn một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 (đặc biệt khi xử lý các tác vụ cào dữ liệu lớn), các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Cào hàng loạt thông tin doanh nghiệp từ từ khóa tìm kiếm trên Google Maps và Yelp.
- **Dữ liệu chuẩn hóa thông minh:** Sử dụng Google Gemini AI để bóc tách và trả về cấu trúc JSON sạch sẽ, chính xác.
- **Làm giàu dữ liệu (Data Enrichment):** Tự động tìm kiếm thêm thông tin bổ trợ thông qua MCP Search Client và Web Scraping.
- **Đồng bộ đa kênh:** Tự động ghi dữ liệu vào Google Sheets, lưu file local trên ổ cứng và bắn Webhook thông báo.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Self-hosted instance** (Workflow này sử dụng node cộng đồng MCP Client nên bắt buộc chạy bản Self-hosted).
- Tài khoản **Bright Data** (Lấy API Key/Token và cấu hình Zone name).
- Tài khoản/API Key **Google Gemini** (Google Palm API credentials).
- Tài khoản **Google Sheets** (Để lưu trữ database leads).
- Tài khoản **MCP Client API** (Dùng cho các node `MCP Search Client` và `MCP Client for Web Scraping`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào n8n Editor của mình, hoặc import file JSON đã tải từ trang chủ n8n (ID: 5443).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các điểm sau:

- **Node `Set input fields`**: Điền các thông số tìm kiếm của các sếp vào đây:
  - `url`: `https://www.google.com/maps/search/`
  - `search`: Từ khóa tìm kiếm (ví dụ: `dentists+in+texas/?q=dentists+in+texas`)
  - `zone`: Tên zone của Bright Data (ví dụ: `serp_api1`)
  - `num`: Số lượng kết quả muốn cào (ví dụ: `20`)
  - `webhook notification url`: URL nhận thông báo (có thể dùng webhook.site để test).
- **Thiết lập Credentials**:
  - `Perform Bright Data Web Request`: Chọn Http Header Auth với token Bright Data.
  - `Google Gemini Chat Model` & `Google Gemini Chat Model for Google Search`: Cấu hình Google Palm API.
  - `Update Google Sheets for Structured Data`: Kết nối tài khoản Google Sheets OAuth2 và trỏ tới file Sheet chuẩn bị sẵn.
  - `MCP Search Client` & `MCP Client for Web Scraping`: Cấu hình thông tin kết nối `mcpClientApi`.
- **Node lưu file (`Write the structured content to disk` & `Write the Yelp content to disk`)**: Kiểm tra lại đường dẫn thư mục lưu trữ file trên ổ cứng VPS của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn **‘Test workflow’** để chạy thử với dữ liệu mẫu trong `Set input fields`.
- Kiểm tra kết quả trên Google Sheets, ổ cứng và Webhook xem dữ liệu đã đổ về chuẩn chưa.
- Nếu mọi thứ xanh mướt, hãy gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot thông báo:** Thêm node Telegram hoặc Slack ở cuối workflow để bắn tin nhắn thông báo mỗi khi quét xong danh sách leads mới.
- **Tự động gửi Email tiếp cận:** Kết hợp thêm node Gmail để tự động gửi email giới thiệu dịch vụ tới các lead vừa thu thập được sau bước làm giàu dữ liệu.
- **Lên lịch chạy định kỳ (Cron):** Thay thế node `Manual Trigger` bằng `Schedule Trigger` để tự động cào dữ liệu hàng tuần/hàng tháng theo nhu cầu marketing.

### 📌 Kết luận
Với sự kết hợp đỉnh cao giữa Bright Data, Google Gemini AI và n8n, việc tìm kiếm khách hàng tiềm năng quy mô lớn chưa bao giờ dễ dàng đến thế. Hãy triển khai ngay trên VPS của mình và tối ưu hóa quy trình sales ngay hôm nay các sếp nhé!