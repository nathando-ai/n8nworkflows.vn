---
title: "🚀 Tự động quét khách hàng tiềm năng trên Google Maps với Apify và Firecrawl"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu doanh nghiệp từ Google Maps, trích xuất thông tin liên hệ và lưu trữ vào Google Sheets."
slug: "tu-dong-quet-khach-hang-google-maps-apify-firecrawl"
tags: [n8n, automation, no-code, apify, firecrawl, google-maps, sales]
keywords: [n8n workflow, cào dữ liệu google maps, apify n8n, firecrawl n8n, tự động hóa sales, lead generation]
---

# 🚀 Tự động quét khách hàng tiềm năng trên Google Maps với Apify và Firecrawl

Các sếp làm sales hay marketing chắc chắn hiểu cảm giác "nản" thế nào khi phải ngồi thủ công tìm kiếm từng quán ăn, cửa hàng trên Google Maps, copy số điện thoại, email và website rồi dán vào Excel. Vừa tốn hàng giờ đồng hồ, vừa dễ bỏ sót khách hàng tiềm năng.

Đừng lo, bài toán đó sẽ được giải quyết triệt để với workflow n8n **Google Maps business scraper with contact extraction via Apify and Firecrawl**. Đây là hệ thống tự động hóa 100% giúp các sếp gom data chất lượng cao từ Google Maps, tự động duyệt website của họ để moi sạch thông tin liên hệ (email, mạng xã hội) và lưu thẳng vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh copy-paste thủ công hàng trăm doanh nghiệp mỗi ngày.
- **Data phong phú, chính xác:** Kết hợp sức mạnh của Google Maps (thông tin cơ bản) và Firecrawl (quét sâu website lấy email, mạng xã hội).
- **Tự động hóa hoàn toàn:** Chạy định kỳ nhờ Schedule Trigger, tự động kiểm tra trạng thái và xử lý theo từng lô (batch).
- **Quản lý tập trung:** Toàn bộ dữ liệu doanh nghiệp và thông tin liên hệ chi tiết được phân loại gọn gàng trong Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Google Sheets:** Để lưu trữ truy vấn tìm kiếm và dữ liệu thu thập được.
- **Tài khoản Apify:** Lấy API Token để kích hoạt trình cào Google Maps.
- **Tài khoản Firecrawl:** Lấy API Key để trích xuất nội dung website doanh nghiệp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor, hoặc sử dụng tính năng Import từ file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 14 nodes hoạt động theo 3 giai đoạn chính. Các sếp cần chú ý cấu hình các node sau:

- **Read Pending Queries (`googleSheets`):** Kết nối với tài khoản Google Sheets của các sếp, trỏ tới file Google Sheet chứa danh sách từ khóa/khu vực cần quét (ví dụ: "nhà hàng tại Quận 1").
- **Start Apify Scraping Job (`httpRequest`):** Cần cấu hình Apify API Token thông qua `httpQueryAuth` hoặc `httpHeaderAuth` để gọi Actor cào Google Maps.
- **Check Scraping Status & Fetch Scraped Results (`httpRequest`):** Đảm bảo các tham số kiểm tra trạng thái job của Apify đồng bộ với node `Wait for Job Succeed` (thường đợi khoảng 30-60 giây cho mỗi lần check).
- **Save Business Data & Save Contact Details (`googleSheets`):** Trỏ đúng vào các sheet (ví dụ: sheet "Data" và sheet "Details") trong file Google Sheets mẫu để hệ thống ghi nhận kết quả.
- **Scrape Website Content (`httpRequest`):** Cấu hình API Key của Firecrawl (`httpBearerAuth`) để hệ thống tiến hành cào nội dung từ các website doanh nghiệp hợp lệ.
- **Extract Contact Information (`code`):** Node Javascript này sẽ tự động bóc tách email và mạng xã hội từ dữ liệu HTML mà Firecrawl trả về.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) thủ công từng cụm node để đảm bảo kết nối API Apify, Firecrawl và Google Sheets không bị lỗi Authentication.
- Sau khi test thành công, bật công tắc **Active workflow** ở góc trên bên phải để hệ thống tự động chạy ngầm theo lịch hẹn.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Nối thêm node Telegram hoặc Slack ở cuối workflow để nhận tin nhắn báo cáo ngay khi hệ thống quét xong một batch dữ liệu mới.
- **Gửi email tự động (Cold Outreach):** Kết hợp thêm node Gmail hoặc Resend để tự động gửi email giới thiệu dịch vụ tới các email vừa trích xuất được từ website doanh nghiệp.
- **Lọc trùng lặp thông tin:** Thêm một bước kiểm tra (If/Filter) trước khi lưu vào Google Sheets để tránh việc ghi đè hoặc lưu trùng các doanh nghiệp đã quét ở các lần chạy trước.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ lợi hại cho đội ngũ Sales và Marketing muốn tiếp cận thị trường nhanh chóng bằng Data-driven. Hãy thiết lập ngay hôm nay để tối ưu hóa hiệu suất làm việc và bứt phá doanh thu cho các sếp nhé!