---
title: "🚀 Tự động trích xuất Email doanh nghiệp từ Google Maps bằng n8n"
description: "Hướng dẫn chi tiết cách sử dụng workflow n8n để tìm kiếm từ khóa, cào dữ liệu Google Maps, lọc website và tự động lưu danh sách email chất lượng vào Google Sheets."
slug: "trich-xuat-email-google-maps-bang-n8n"
tags: [n8n, automation, lead-generation, google-maps, google-sheets, web-scraping]
keywords: [n8n workflow, trích xuất email google maps, tự động hóa lead generation, cào email doanh nghiệp, google sheets automation]
---

# 🚀 Tự động trích xuất Email doanh nghiệp từ Google Maps bằng n8n

Việc tìm kiếm khách hàng tiềm năng (Lead Generation) theo phương pháp thủ công bằng cách lên Google Maps, tìm từng doanh nghiệp, click vào website và mò mẫm tìm email liên hệ thực sự là một cơn ác mộng tốn thời gian. Quy trình này vừa chậm chạp, vừa dễ sai sót và cực kỳ nhàm chán cho đội ngũ sale.

Được phát triển bởi **Agent Circle**, workflow n8n này sẽ tự động hóa toàn bộ từ A-Z quy trình: Nhập từ khóa $\rightarrow$ Truy vấn Google Maps $\rightarrow$ Lọc website hợp lệ $\rightarrow$ Cào và chuẩn hóa email $\rightarrow$ Loại bỏ trùng lặp và lưu thẳng vào Google Sheets. Giúp các sếp tiết kiệm hàng chục giờ làm việc thủ công!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Chỉ cần nhập từ khóa và bấm nút, hệ thống tự lo phần còn lại.
- **Dữ liệu sạch & chuẩn xác:** Tự động lọc bỏ các URL rác, loại bỏ các email trùng lặp nhờ các node xử lý thông minh.
- **Tiết kiệm thời gian nhân sự:** Thay vì mất hàng tuần để tìm data, workflow xử lý hàng loạt chỉ trong vài phút.
- **Ứng dụng đa dạng:** Phù hợp cho đội ngũ Sales chạy Cold Email, Agency Marketing tìm kiếm khách hàng mục tiêu, nhà tuyển dụng hoặc nghiên cứu thị trường.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản Google Cloud Console (để cấu hình API/OAuth cho **Google Sheets**).
- Bản sao Google Sheets template: [Google Maps - Crawl Emails By Keyword Google Sheets Template](https://docs.google.com/spreadsheets/d/17y_MmRHfBbW67bVyRuep1hkpoh2BV3yF5_Woxt0W9kk/edit?gid=0#gid=0).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc sao chép đoạn mã JSON, sau đó dán trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà, các sếp cần chú ý cấu hình các node sau:
- **Fields - Set Keyword / Phrase**: Nhập từ khóa hoặc cụm từ mục tiêu muốn tìm kiếm (ví dụ: `"coffee shop in Hanoi"`, `"digital marketing agency"`).
- **HTTP Request - Get Sites**: Đảm bảo phương thức GET được cấu hình chính xác để truy vấn dữ liệu từ Google Maps.
- **Google Sheets - Update Data**: Kết nối tài khoản Google thông qua `googleSheetsOAuth2Api`, chọn đúng file Google Sheets template đã sao chép ở phần chuẩn bị và trỏ tới đúng Sheet nhận dữ liệu.
- Các node phụ trợ như **Loop Websites**, **Loop Emails**, **Code - Matching URL**, **Code - Match Email**, **Remove Site Duplicates**, **Remove Email Duplicates**: Giữ nguyên logic cấu hình sẵn có trong template để đảm bảo việc bóc tách và lọc trùng lặp diễn ra hoàn hảo.

#### 3. Kích hoạt ⚡️
- Bấm **Test workflow** trên node `When clicking ‘Test workflow’` để chạy thử nghiệm và kiểm tra dòng dữ liệu.
- Sau khi kiểm tra dữ liệu đổ về Google Sheets thành công, gạt công tắc sang chế độ **Active** để hoàn tất.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp tự động gửi Email**: Nối thêm node Gmail hoặc Resend ngay sau bước lưu Google Sheets để tự động gửi chuỗi email chăm sóc (Cold Outreach) tới danh sách vừa thu thập.
- **Thông báo qua Chat**: Thêm node Telegram hoặc Slack để nhận thông báo ngay khi workflow chạy xong và tổng hợp số lượng email tìm được.
- **Lên lịch chạy định kỳ (Cron/Schedule)**: Thay thế `manualTrigger` bằng `Schedule Trigger` để tự động cào data theo tuần hoặc theo tháng cho các từ khóa mới.

### 📌 Kết luận
Workflow **Extract Business Emails from Google Maps Search Results to Google Sheets** là vũ khí cực kỳ mạnh mẽ giúp tự động hóa quá trình tìm kiếm khách hàng tiềm năng. Hãy áp dụng ngay hôm nay để tối ưu hóa nguồn lực và bứt phá doanh thu cho doanh nghiệp của các sếp!