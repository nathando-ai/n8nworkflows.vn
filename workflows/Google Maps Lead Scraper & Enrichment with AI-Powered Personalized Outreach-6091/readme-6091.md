---
title: "🚀 Tự Động Quét Lead Google Maps & Tiếp Cận Cá Nhân Hóa Bằng AI trong n8n"
description: "Hướng dẫn chi tiết xây dựng hệ thống tự động quét data từ Google Maps, làm giàu thông tin website và tạo nội dung tiếp cận bằng AI Agent."
slug: "google-maps-lead-scraper-enrichment-ai-n8n"
tags: [n8n, lead-generation, ai-agent, openai, google-sheets, automation]
keywords: [n8n workflow, google maps scraper, apify n8n, ai lead generation, lam giau du lieu lead]
---

# 🚀 Tự Động Quét Lead Google Maps & Tiếp Cận Cá Nhân Hóa Bằng AI

Việc tìm kiếm khách hàng tiềm năng (Lead Generation) thủ công trên Google Maps tốn rất nhiều thời gian: từ việc copy tên doanh nghiệp, địa chỉ, số điện thoại, cho đến việc vào từng website để mò mẫm thông tin mạng xã hội và soạn email chào hàng. 

Đừng làm việc đó bằng tay nữa các sếp ạ! Bài viết này sẽ hướng dẫn các sếp thiết lập một siêu workflow n8n giúp tự động hóa 100% quy trình: **Quét data Google Maps ➔ Làm giàu dữ liệu thông minh (Enrichment) ➔ Xử lý website thiếu thông tin bằng AI/Code ➔ Tạo nội dung outreach cá nhân hóa bằng OpenAI**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Thu thập hàng loạt data doanh nghiệp từ Google Maps chỉ với một cú click hoặc lịch trình tự động.
- **Làm giàu dữ liệu thông minh:** Tự động crawl website để bóc tách thông tin liên hệ, mạng xã hội (LinkedIn, Facebook, Twitter...) đối với các lead thiếu thông tin ban đầu.
- **Cá nhân hóa đỉnh cao:** Sử dụng **AI Agent** và **OpenAI Chat Model** để viết thông điệp tiếp cận (outreach message) cực kỳ tự nhiên cho từng khách hàng dựa trên dữ liệu thu thập được.
- **Lưu trữ khoa học:** Tự động đồng bộ và cập nhật trạng thái vào Google Sheets để đội ngũ Sales dễ dàng chăm sóc.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Apify Account & API Key:** Dùng cho Actor quét Google Maps.
- **OpenAI API Key:** Cho node AI Agent tạo nội dung cá nhân hóa.
- **Firecrawl API Key:** Dùng để crawl nội dung website đối với các lead chưa đủ thông tin.
- **Google Sheets Account:** Để lưu trữ danh sách lead (có tích hợp OAuth2).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, vào giao diện n8n, chọn **Add workflow** -> **Import from JSON** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 21 nodes kết hợp chặt chẽ với nhau. Các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Node `HTTP Request` (Apify Integration):** 
  - Cấu hình endpoint chạy Actor đồng bộ của Apify theo hướng dẫn trên canvas.
  - Đưa JSON Input vào phần Body Field (chứa từ khóa tìm kiếm, vị trí...).
  - Thêm Header Bearer Token sử dụng Apify API Key (`<token>`).
- **Node `OpenAI Chat Model`:** 
  - Chọn model (`gpt-4.1-mini` hoặc tùy chọn).
  - Kết nối credentials tài khoản OpenAI của các sếp.
- **Các node `Append or update row in sheet` (Google Sheets):** 
  - Kết nối tài khoản Google Sheets qua OAuth2.
  - Trỏ đúng đến file Google Sheet và Sheet Name mà các sếp muốn lưu data lead.
- **Node `Scrape Website Content` (Firecrawl):** 
  - Thay thế token xác thực bằng Firecrawl API Key để hệ thống tự động cào dữ liệu website cho các lead bị thiếu thông tin.

#### 3. Kích hoạt ⚡️
- Bấm nút `When clicking ‘Execute workflow’` để chạy thử nghiệm với một vài bản ghi mẫu.
- Kiểm tra lại các bảng Google Sheets xem data đã đổ về chuẩn chưa.
- Sau khi test ngon lành, các sếp gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Nối thêm node Telegram hoặc Slack ngay sau khi AI Agent tạo xong nội dung outreach để bắn thông báo nóng về cho đội sales.
- **Mở rộng CRM:** Thay vì chỉ lưu Google Sheets, các sếp có thể đẩy thẳng lead vào HubSpot, Salesforce hoặc Close CRM.
- **Lên lịch chạy định kỳ (Schedule Trigger):** Thay thế node `manualTrigger` bằng `Schedule Trigger` để hệ thống tự động quét lead mới hàng tuần/hàng tháng mà không cần can thiệp thủ công.

### 📌 Kết luận
Workflow này là một "vũ khí bí mật" giúp tối ưu hóa toàn bộ phễu tìm kiếm khách hàng B2B. Hãy thiết lập ngay hôm nay để tiết kiệm hàng chục giờ làm việc thủ công cho đội ngũ của các sếp!