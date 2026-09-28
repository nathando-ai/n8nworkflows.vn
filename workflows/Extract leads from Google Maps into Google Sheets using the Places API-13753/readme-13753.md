---
title: "🚀 Tự động quét Lead từ Google Maps vào Google Sheets với Places API"
description: "Hướng dẫn xây dựng hệ thống tự động cào dữ liệu khách hàng tiềm năng (leads) từ Google Maps sử dụng n8n và Google Places API mới nhất."
slug: "tu-dong-quet-lead-tu-google-maps-vao-google-sheets"
tags: [n8n, automation, google-maps, lead-generation, google-sheets]
keywords: [n8n workflow, google maps scraper, places api, cào lead google maps, tự động hóa n8n]
---

# 🚀 Tự động quét Lead từ Google Maps vào Google Sheets với Places API

Chào các sếp! Việc tìm kiếm khách hàng tiềm năng (lead generation) thủ công trên Google Maps vừa mất thời gian, vừa dễ thiếu sót. Các sếp phải gõ từng từ khóa như *"Quán cà phê Quận 1"*, *"Nha khoa Hà Nội"*, copy từng số điện thoại, website, địa chỉ vào file Excel... Quá cực công phải không nào?

Giải pháp ở đây là tự động hóa 100%! Workflow n8n này sẽ giúp các sếp quét hàng loạt thông tin doanh nghiệp (Tên, SĐT, Website, Địa chỉ...) từ Google Maps thông qua **Google Places API (New)** và lưu trữ gọn gàng vào Google Sheets. Hệ thống hỗ trợ cả chạy tự động theo lịch trình hoặc chạy thủ công qua biểu mẫu (Form) cực kỳ tiện lợi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Gom hàng trăm leads chỉ với một cú click form hoặc theo lịch hẹn sẵn.
- **Chống trùng lặp thông minh:** Sử dụng Google Place ID để lọc và cập nhật lead, không sợ bị trùng dòng trong sheet.
- **Quản lý trạng thái thông minh:** Tự động đánh dấu "đã quét" (Scraped) vào bảng nguồn sau khi chạy xong lịch trình.
- **Tối ưu chi phí:** Dễ dàng kiểm soát số lượng trang kết quả quét (Max Pages) để tránh phát sinh chi phí API ngoài ý muốn từ Google.
:::

### 🔑 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã hoạt động (Cloud hoặc Self-hosted).
- **Google Cloud Console:** Cần kích hoạt **Places API (New)** và tạo một API Key.
- **Google Sheets:** Bản sao của [Google Sheet Template chuẩn](https://docs.google.com/spreadsheets/d/1x_GYw6KHgvhe2dgSw1eKKTimIzQYTsRkkWoxkAJEdD8/copy?usp=sharing) để lưu trữ dữ liệu nguồn (QUERIES) và dữ liệu đích (LEADS).
- **Credentials:** Kết nối tài khoản Google Sheets OAuth2 trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, paste trực tiếp vào giao diện n8n Editor của mình hoặc import file JSON tải về từ kho lưu trữ.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các node sau:

- **Google Places Search (`httpRequest`):** 
  - Cung cấp API Key của Google vào tham số header `X-Goog-Api-Key`.
  - *Mẹo bảo mật:* Đối với môi trường Production, các sếp nên chuyển API Key này thành n8n Environment Variable để bảo mật và dễ quản lý.
  - Có thể điều chỉnh giới hạn **Max Pages** trong body request để kiểm soát số lượng kết quả và chi phí API.
- **Get rows in QUERIES (`googleSheets`):** Chọn kết nối Google Sheets và trỏ tới file Google Sheet template đã nhân bản của các sếp (để lấy danh sách các từ khóa tìm kiếm như *"Bakeries New York USA"*, *"Cafes Berlin Germany"*...).
- **Append or update lead row (`googleSheets`):** Cấu hình tính năng `appendOrUpdate` trỏ tới sheet **LEADS** trong file của các sếp để lưu thông tin doanh nghiệp đồng thời chống trùng lặp dựa trên Place ID.
- **Mark Query as Scraped (`googleSheets`):** Cấu hình tính năng `update` trỏ về sheet **QUERIES** để đánh dấu các từ khóa đã được quét xong (cột `Scraped` chuyển thành `true`).

#### 3. Kích hoạt ⚡️
- **Điểm vào (Entry Points):** Workflow có 2 nhánh bắt đầu:
  - `Scrape on form submission`: Dùng khi các sếp muốn tìm kiếm nhanh thủ công qua Form.
  - `Scrape on schedule`: Dùng để chạy tự động theo lịch (Cron/Schedule) lấy danh sách từ Google Sheets.
- Sau khi test thử nghiệm (Test run) thành công và dữ liệu đổ đúng vào Google Sheets, các sếp hãy gạt công tắc **Active workflow** sang màu xanh để hệ thống tự vận hành.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống xịn sò hơn nữa, các sếp có thể mở rộng workflow này với các ý tưởng sau:
- **Thông báo qua Telegram/Slack:** Thêm node gửi tin nhắn thông báo về số lượng leads vừa quét được vào cuối mỗi đợt chạy lịch trình.
- **Tích hợp AI (OpenAI/Claude):** Dùng LLM node để tự động phân tích và chấm điểm chất lượng lead (Lead Scoring) dựa trên website và mô tả của doanh nghiệp.
- **Làm sạch dữ liệu tự động:** Thêm bước kiểm tra định dạng số điện thoại hoặc email trước khi ghi vào Google Sheets.

### 📌 Kết luận
Với workflow n8n tích hợp Google Places API này, việc xây dựng cơ sở dữ liệu khách hàng tiềm năng từ Google Maps trở nên nhanh chóng, tự động và chuyên nghiệp hơn bao giờ hết. Hãy triển khai ngay hôm nay để tiết kiệm hàng chục giờ làm việc thủ công cho đội ngũ Sales và Marketing của các sếp nhé!