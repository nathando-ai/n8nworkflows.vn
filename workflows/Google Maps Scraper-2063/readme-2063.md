---
title: "🚀 Hướng dẫn cào dữ liệu Google Maps tự động không giới hạn với n8n và SerpAPI"
description: "Tự động hóa quy trình trích xuất thông tin doanh nghiệp từ Google Maps (số điện thoại, website, đánh giá, địa chỉ...) vào Google Sheets với chi phí siêu rẻ."
slug: "cao-du-lieu-google-maps-tu-dong-voi-n8n"
tags: [n8n, automation, google-maps, serpapi, google-sheets, web-scraping]
keywords: [n8n workflow, google maps scraper, cào dữ liệu google maps, serpapi n8n, tự động hóa marketing]
---

# 🚀 Tự động hóa cào dữ liệu Google Maps chuyên nghiệp với n8n & SerpAPI

Các sếp đang làm Sales, Marketing hay Nghiên cứu thị trường chắc chắn đã từng đau đầu khi phải copy/paste thủ công từng thông tin doanh nghiệp từ Google Maps. Việc này vừa tốn hàng giờ đồng hồ, vừa dễ sai sót, lại tốn kém nếu dùng các dịch vụ API đắt đỏ. 

Giải pháp ở đây là gì? Hãy để chiếc workflow **Google Maps Scraper** do tác giả *Lucas Perret* xây dựng thay các sếp làm việc đó. Workflow này sẽ tự động hóa 100% quá trình lấy danh sách địa điểm, thông tin chi tiết (số điện thoại, website, đánh giá, địa chỉ...) và lưu thẳng vào Google Sheets một cách mượt mà!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn cảnh tìm kiếm và copy thủ công từng quán ăn, công ty, cửa hàng.
- **Tiết kiệm chi phí:** Sử dụng **SerpAPI** với chi phí rẻ hơn rất nhiều so với việc gọi trực tiếp Google Maps API truyền thống.
- **Dữ liệu chuẩn chỉnh:** Tự động lọc các giá trị trùng lặp, làm sạch dữ liệu và cập nhật trực tiếp vào Google Sheets theo thời gian thực.
- **Hoạt động tự động:** Có thể cấu hình chạy ngầm định kỳ hàng giờ hoặc chạy thủ công tùy nhu cầu.
:::

### ### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **SerpAPI Account:** Đăng ký tài khoản miễn phí tại [serpapi.com](https://serpapi.com) để lấy API Key.
- **Google Sheets Template:** Sao chép mẫu Google Sheets chính thức tại [đường dẫn này](https://docs.google.com/spreadsheets/d/170osqaLBql9M-4RAH3_lBKR7ZMaQqyLUkAD-88xGuEQ/edit?usp=sharing) để làm nguồn dữ liệu đầu vào.
- **Google OAuth2 Credentials:** Kết nối tài khoản Google với n8n để đọc/ghi dữ liệu trên Google Sheets.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy toàn bộ mã JSON của workflow (từ nguồn gốc n8n.io/2063).
- Tại giao diện n8n Editor, chọn **Add workflow** -> Click vào dấu `...` ở góc trên bên phải -> Chọn **Import from File/Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node sau để hệ thống chạy trơn tru:

- **Google Sheets - Get searches to scrap** & **Add rows in Google Sheets**:
  - Chọn `credentials` là tài khoản Google Sheets OAuth2 của các sếp.
  - Trỏ đúng tới file Google Sheets mẫu mà các sếp vừa copy về.
- **SERPAPI - Scrape Google Maps URL**:
  - Thêm `credentials` loại SerpAPI và dán API Key lấy từ tài khoản SerpAPI của các sếp vào.
- **Run workflow every hours** (Schedule Trigger):
  - Mặc định workflow sẽ chạy định kỳ hàng giờ. Các sếp có thể điều chỉnh tần suất này trong phần cài đặt của node tùy theo nhu cầu thực tế (ví dụ: chạy mỗi ngày 1 lần).

#### 3. Kích hoạt ⚡️
- Điền các từ khóa hoặc URL tìm kiếm Google Maps cần cào vào file Google Sheets.
- Nhấn nút **"Execute Workflow"** để test thử mẻ đầu tiên.
- Sau khi kiểm tra dữ liệu trả về trong Google Sheets đã chuẩn chỉnh, hãy gạt công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack vào sau node `Update Status to Success` để nhận thông báo ngay lập tức về điện thoại mỗi khi cào xong một chiến dịch.
- **Quản lý lỗi thông minh:** Tận dụng node `Update Status to Error` sẵn có trong workflow để ghi log trạng thái lỗi thẳng vào Google Sheets, giúp dễ dàng kiểm tra lại các từ khóa bị lỗi.
- **Mở rộng dữ liệu:** Kết hợp thêm các bước AI (OpenAI/Anthropic node) để phân loại ngành nghề hoặc chấm điểm tiềm năng (Lead Scoring) cho các doanh nghiệp vừa cào về.

### 📌 Kết luận
Workflow **Google Maps Scraper** là một vũ khí cực mạnh cho các đội ngũ Sales và Marketing để xây dựng Database khách hàng tiềm năng một cách tự động và tiết kiệm. Hãy triển khai ngay hôm nay để tối ưu hóa hiệu suất công việc của các sếp!