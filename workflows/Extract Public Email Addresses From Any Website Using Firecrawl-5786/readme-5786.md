---
title: "🚀 Tự động trích xuất Email công khai từ bất kỳ Website nào với Firecrawl và n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động quét toàn bộ trang web, tìm kiếm và trích xuất địa chỉ email công khai bằng Firecrawl API một cách nhanh chóng."
slug: "trich-xuat-email-website-tu-dong-firecrawl-n8n"
tags: [n8n, automation, no-code, lead-generation, firecrawl, web-scraping, email-extraction]
keywords: [n8n workflow, trích xuất email website, firecrawl n8n, tự động hóa lead generation, web scraping n8n]
---

# 🚀 Tự động trích xuất Email công khai từ bất kỳ Website nào với Firecrawl

Việc tìm kiếm và thu thập thông tin liên hệ (Lead Generation) thủ công từ các website đối thủ hoặc khách hàng tiềm năng luôn ngốn rất nhiều thời gian của các đội ngũ Sales và Marketing. Việc click vào từng trang Liên hệ (Contact), Giới thiệu (About Us) rồi copy từng email rất dễ bị sót và mệt mỏi.

Giải pháp ở đây là gì? Workflow n8n này sẽ tự động hóa 100% quy trình đó! Chỉ với một URL trang chủ được nhập vào Form, hệ thống sẽ sử dụng **Firecrawl API** để map toàn bộ sơ đồ website, tiến hành quét hàng loạt (batch scrape) và trả về danh sách tất cả các địa chỉ email công khai nằm trong mã nguồn HTML của website đó.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Chỉ cần nhập URL website vào Form, nhận kết quả gọn gàng dạng mảng (array).
- **Quét sâu toàn trang**: Không chỉ trang chủ, Firecrawl giúp map và quét các trang con quan trọng chứa thông tin liên hệ.
- **Xử lý thông minh**: Tích hợp cơ chế kiểm tra trạng thái batch scrape, chờ (wait) và giới hạn số lần thử lại (retry) tránh quá tải API.
- **Tiết kiệm 90% thời gian**: Gom toàn bộ email của một doanh nghiệp chỉ trong vài phút chạy ngầm.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đã sẵn sàng hoạt động.
- Tài khoản **Firecrawl** (lấy API Key để xác thực các HTTP Request).
- Credentials loại **HTTP Header Auth** để kết nối n8n với Firecrawl API.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ n8n (Link gốc: [n8n.io/workflows/5786](https://n8n.io/workflows/5786)) và tiến hành Import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 9 nodes chính hoạt động nhịp nhàng, các sếp cần chú ý cấu hình các điểm sau:
- **`form_trigger`**: Nơi người dùng nhập URL trang chủ website cần quét. Các sếp có thể tùy chỉnh giao diện form nếu muốn thu thập thêm thông tin (như tên công ty, người liên hệ...).
- **Các nodes HTTP Request (`map_website`, `start_batch_scrape`, `fetch_scrape_results`)**: 
  - Cần cấu hình **Credentials (`httpHeaderAuth`)** bằng API Key của Firecrawl.
  - Kiểm tra lại Endpoint URL của Firecrawl API (map, batch scrape, status/results) đảm bảo khớp với tài liệu mới nhất của Firecrawl.
- **Logic kiểm tra (`check_retry_count`, `rate_limit_wait`, `check_scrape_completed`)**: Các nodes này giúp điều phối tiến trình chờ kết quả trả về từ Firecrawl vì quá trình scrape diện rộng cần thời gian xử lý bất đồng bộ. Các sếp giữ nguyên logic này để đảm bảo hệ thống không bị lỗi timeout.
- **`set_result`**: Node này định dạng lại kết quả cuối cùng thành một mảng (array) chứa các email sạch sẽ, sẵn sàng để đẩy sang Google Sheets, CRM hoặc gửi về Email/Telegram.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** và test thử bằng một URL website bất kỳ trên Form.
- Sau khi test thành công và dữ liệu trả về chuẩn chỉnh, gạt công tắc sang **Active** để chính thức đưa workflow vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình Lead Generation, các sếp có thể mở rộng workflow này bằng cách:
1. **Lưu trữ tự động**: Thêm node **Google Sheets** hoặc **Airtable** ngay sau node `set_result` để tự động lưu danh sách email thu được kèm theo tên miền website.
2. **Thông báo kết quả**: Tích hợp thêm node **Telegram** hoặc **Slack** để nhận thông báo ngay khi hệ thống quét xong một website kèm theo số lượng email tìm được.
3. **Lọc và làm sạch email**: Thêm một bước kiểm tra cú pháp hoặc tích hợp AI (như OpenAI node) để phân loại email nào là Sales, Support hay Info trước khi lưu vào database.

### 📌 Kết luận
Workflow trích xuất email bằng Firecrawl này là một "vũ khí" cực kỳ lợi hại cho các đội ngũ làm chiến dịch outreach, sales B2B hay nghiên cứu thị trường. Hãy cài đặt ngay lên hệ thống n8n của các sếp để tối ưu hóa hiệu suất công việc ngay hôm nay!