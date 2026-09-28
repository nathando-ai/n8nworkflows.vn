---
title: "🚀 Tự động tìm kiếm khách hàng tiềm năng chất lượng cao bằng cách cào Glassdoor với Bright Data & GPT"
description: "Khám phá workflow n8n tự động hóa quy trình tìm kiếm khách hàng tiềm năng (Sales Leads) từ Glassdoor sử dụng Bright Data API và OpenAI GPT-4o-mini."
slug: "tim-kiem-khach-hang-tiem-nang-glassdoor-bright-data-gpt"
tags: [n8n, automation, no-code, sales, ai, bright-data]
keywords: [n8n workflow, sales leads, bright data scraping, glassdoor scraper, openai gpt, tự động hóa sales]
keywords: [n8n workflow, sales leads, bright data scraping, glassdoor scraper, openai gpt, tự động hóa sales]
---

# 🚀 Tự động tìm kiếm khách hàng tiềm năng chất lượng cao bằng cách cào Glassdoor với Bright Data & GPT

Việc tìm kiếm khách hàng tiềm năng (Sales Leads) theo phương pháp thủ công bằng cách lướt qua hàng trăm tin tuyển dụng trên Glassdoor là một cực hình: mất thời gian, dễ bỏ sót và tốn quá nhiều công sức để phân tích xem công ty đó có thực sự cần dịch vụ của bạn hay không. 

Đừng lo, các sếp hoàn toàn có thể tự động hóa 100% quy trình này! Workflow n8n siêu việt này sẽ kết hợp **Bright Data** để cào dữ liệu tuyển dụng từ Glassdoor theo từ khóa, sau đó dùng sức mạnh của **OpenAI GPT-4o-mini** để tự động phân tích và viết nội dung tiếp cận (pitching) cực kỳ cá nhân hóa cho từng khách hàng, rồi lưu trữ gọn gàng vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải thủ công tìm kiếm công ty đang có nhu cầu tuyển dụng nhân sự liên quan đến sản phẩm/dịch vụ của bạn.
- **Dữ liệu chính xác thời gian thực:** Khai thác dữ liệu tuyển dụng mới nhất từ Glassdoor thông qua công cụ chuyên nghiệp Bright Data.
- **Cá nhân hóa tự động:** AI (GPT-4o-mini) tự động phân tích mô tả công việc và soạn sẵn nội dung tiếp cận (pitch) phù hợp nhất cho từng lead.
- **Quản lý tập trung:** Toàn bộ danh sách việc làm và nội dung pitch được đồng bộ trực tiếp vào Google Sheets, sẵn sàng cho đội sales chốt đơn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Bright Data** kèm API Token/Key để sử dụng dịch vụ Web Scraping.
- Tài khoản **OpenAI** kèm API Key (sử dụng model `gpt-4o-mini`).
- Tài khoản **Google** để kết nối Google Sheets.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow này, vào giao diện n8n chọn **Add workflow** -> **Import from File** và tải file lên là xong!

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình kỹ các node sau:

- **On form submission - Discover Jobs (`formTrigger`):** Đây là điểm khởi đầu nơi các sếp nhập các thông tin tìm kiếm như Vị trí (Location), Từ khóa (Keyword), và Quốc gia (Country) thông qua một biểu mẫu web trực quan.
- **HTTP Request- Post API call to Bright Data (`httpRequest`) & Snapshot Progress / Getting data:** Cấu hình API Key của Bright Data vào các node HTTP Request này để gửi yêu cầu cào dữ liệu, kiểm tra trạng thái snapshot (`If - Checking status...`, `Wait - Polling...`) và lấy dữ liệu trả về.
- **Google Sheets - Adding All Job Posts & Update Pitches (`googleSheets`):** Kết nối tài khoản Google Sheets của các sếp. Có thể sử dụng [Google Sheets Template mẫu tại đây](https://docs.google.com/spreadsheets/d/1ZYRk83hNIQCyQNaKpchdnbTiapVxE4aG6ZFIQlwEoWM/edit?usp=sharing) để đồng bộ cấu trúc cột dữ liệu cho chuẩn xác.
- **OpenAI Chat Model (`lmChatOpenAi`) & Basic LLM Chain (`chainLlm`):** Thêm OpenAI API Credentials và cấu hình model `gpt-4o-mini`. Node này sẽ nhận danh sách việc làm từ node `Split Out` và tiến hành phân tích, tạo nội dung pitch tự động.

#### 3. Kích hoạt ⚡️
- Chạy thử (Test run) bằng cách điền thông tin vào form trigger để kiểm tra xem dữ liệu có đổ về Google Sheets và được AI xử lý mượt mà không.
- Bật công tắc **Active** để đưa workflow vào trạng thái hoạt động tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node **Slack** hoặc **Telegram** ngay sau bước AI tạo pitch để bắn thông báo nóng về điện thoại cho đội sales ngay khi có khách hàng tiềm năng chất lượng cao xuất hiện.
- **Lọc thông minh hơn:** Tinh chỉnh Prompt trong node `Basic LLM Chain` để AI chỉ chọn lọc các công ty phù hợp với tiêu chí quy mô hoặc ngân sách của doanh nghiệp các sếp.
- **Tự động gửi email:** Kết nối thêm node Gmail hoặc Resend để tự động gửi bản pitch do AI soạn thảo trực tiếp đến HR hoặc Hiring Manager của công ty đó (cần có thêm dữ liệu email).

### 📌 Kết luận
Tự động hóa tìm kiếm khách hàng tiềm năng từ dữ liệu tuyển dụng chưa bao giờ dễ dàng và hiệu quả đến thế. Hãy áp dụng ngay workflow này để tối ưu hóa phễu bán hàng và bứt phá doanh thu cho doanh nghiệp của các sếp ngay hôm nay!