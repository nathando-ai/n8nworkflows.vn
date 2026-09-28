---
title: "🚀 Tự động quét Lead Google My Business cực đỉnh theo dịch vụ và khu vực với Bright Data & AI"
description: "Hướng dẫn chi tiết workflow n8n tự động trích xuất thông tin doanh nghiệp từ Google Maps bằng Bright Data, kết hợp Claude AI phân tích thành phố, loại bỏ trùng lặp và lưu trữ vào Google Sheets."
slug: "tu-dong-quet-lead-google-my-business-bright-data-n8n"
tags: [n8n, automation, bright-data, google-my-business, lead-generation, ai]
keywords: [n8n workflow, quét lead google maps, bright data n8n, google my business automation, claude ai n8n]
---

# 🚀 Tự động quét Lead Google My Business cực đỉnh theo dịch vụ và khu vực với Bright Data & AI

Các sếp đang làm Sales, Marketing hay phát triển thị trường chắc chắn hiểu cảm giác "đau đầu" khi phải ngồi thủ công tìm kiếm từng danh sách khách hàng tiềm năng trên Google Maps. Việc này không chỉ tốn hàng chục giờ đồng hồ mà dữ liệu thu về còn dễ bị trùng lặp, thiếu sót thông tin liên hệ và phân loại lộn xộn.

Hiểu được nỗi đau đó, workflow n8n mang tên **"Extract Google My Business Leads by Service or Location with Bright Data"** do tác giả *Dvir Sharon* phát triển sẽ giải quyết triệt để vấn đề này. Workflow tự động hóa 100% từ khâu nhận yêu cầu, sử dụng AI để mở rộng danh sách thành phố/dịch vụ, gọi API cào dữ liệu chuyên sâu từ Bright Data, lọc bỏ dữ liệu trùng lặp thông minh và tự động đẩy toàn bộ lead sạch vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh copy/paste thủ công từng quán ăn, công ty, dịch vụ trên Google Maps.
- **Dữ liệu cực kỳ sạch và chi tiết:** Tự động đối chiếu tên doanh nghiệp và số điện thoại để loại bỏ hoàn toàn các bản ghi trùng lặp (Duplicates).
- **Phủ sóng thông minh bằng AI:** Claude AI sẽ tự động phân rã các khu vực thành phố lớn và chuẩn hóa loại hình dịch vụ để quét dữ liệu toàn diện nhất.
- **Đồng bộ thời gian thực:** Toàn bộ lead chất lượng cao được lưu trữ gọn gàng ngay vào Google Sheets để đội ngũ Sales gọi điện chốt đơn ngay lập tức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance:** Đã cài đặt sẵn (Cloud hoặc Self-hosted).
- **Bright Data Account:** Tài khoản Bright Data và API Key để truy cập dịch vụ cào dữ liệu Google Maps Web Scrapper.
- **Anthropic API Key:** Để sử dụng model *Claude 4 Sonnet* trong các node AI phân tích thành phố và danh mục.
- **Google Sheets Account:** Kết nối OAuth2 với n8n để đọc/ghi dữ liệu lead.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ kho lưu trữ n8n.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** và chọn file JSON vừa tải. Hoặc đơn giản là copy toàn bộ mã JSON của workflow và dán trực tiếp vào màn hình làm việc của n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các credentials và tham số cho các node cốt lõi sau:

- **Form Submission Trigger:** Node khởi chạy dạng Form. Các sếp có thể tùy chỉnh các trường đầu vào (Input fields) như *Service Type* (Loại dịch vụ cần tìm) và *Location* (Khu vực/Thành phố mục tiêu).
- **Claude AI Model for Cities & Categories (Anthropic API):** Chọn credential chứa *Anthropic API Key* của các sếp để kích hoạt model `claude-sonnet-4-20250514`. Node này giúp phân tích và tối ưu hóa từ khóa tìm kiếm theo địa lý và ngành nghề.
- **Scrape Business Data from Google Maps (Bright Data):** Chọn credential loại `brightdataApi`. Node này sẽ gọi trực tiếp dataset Web Scrapper của Bright Data để thu thập thông tin doanh nghiệp từ Google Maps.
- **Fetch Scraped Data & Check Data Collection Status (HTTP Request):** Sử dụng HTTP Header Auth kết hợp với API của Bright Data để theo dõi tiến trình cào dữ liệu và tải kết quả về khi hoàn tất.
- **Get Existing Business Data, Find Duplicate Row Number, Delete Duplicate Row & Save Business Data to Sheet (Google Sheets):** 
  - Kết nối tài khoản Google Sheets thông qua OAuth2.
  - Trỏ đường dẫn đến file Google Sheets chuẩn bị sẵn của các sếp.
  - Đảm bảo cấu trúc cột trong Sheet khớp với dữ liệu trả về từ workflow (Tên doanh nghiệp, Số điện thoại, Địa chỉ, Website, Đánh giá...).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và điền thử một form mẫu để test quá trình cào dữ liệu từ Bright Data qua Claude AI và đẩy vào Google Sheets.
- Kiểm tra kết quả trên Google Sheets xem dữ liệu đã đổ về chuẩn chỉnh chưa.
- Sau khi test thành công, gạt công tắc sang **Active** để đưa workflow vào vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm một node Telegram hoặc Slack vào cuối workflow để gửi thông báo ngay cho sếp hoặc đội ngũ Sales mỗi khi có một mẻ lead mới được cào và lưu thành công.
- **Lên lịch chạy định kỳ (Cron/Schedule):** Thay vì dùng Form Trigger, các sếp có thể kết hợp thêm Schedule Trigger để tự động quét lead theo tuần/tháng cho các từ khóa dịch vụ chiến lược.
- **Lọc điểm đánh giá (Rating Filter):** Thêm một node IF để chỉ giữ lại các doanh nghiệp có số sao trên Google Maps từ 4.0 trở lên hoặc có số lượng review vượt mức cho phép, giúp lọc ra các đối tượng tiềm năng chất lượng nhất.

### 📌 Kết luận
Workflow tự động hóa quét lead Google My Business bằng Bright Data và Claude AI là vũ khí cực kỳ lợi hại giúp tối ưu hóa quy trình tìm kiếm khách hàng. Thay vì tốn nhân sự làm tay chân, hãy để hệ thống tự động làm việc thay các sếp 24/7. Bắt tay vào cài đặt ngay thôi nào!