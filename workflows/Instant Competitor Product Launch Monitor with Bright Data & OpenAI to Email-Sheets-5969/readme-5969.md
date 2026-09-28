---
title: "🚀 Tự động giám sát sản phẩm mới ra mắt của đối thủ bằng Bright Data & OpenAI"
description: "Hướng dẫn cài đặt workflow n8n tự động cào dữ liệu đánh giá sản phẩm từ The Verge, AI tóm tắt và gửi cảnh báo qua Gmail, lưu log Google Sheets mỗi ngày."
slug: "tu-dong-giam-sat-san-pham-doi-thu-bright-data-openai"
tags: [n8n, automation, bright-data, openai, market-research, ai-agent]
keywords: [n8n workflow, giám sát đối thủ, bright data mcp, cào dữ liệu tự động, openai gpt-4o-mini]
---

# 🚀 Tự động giám sát sản phẩm mới ra mắt của đối thủ bằng Bright Data & OpenAI

Việc theo dõi liên tục các sản phẩm mới ra mắt, bài đánh giá (review) của đối thủ cạnh tranh trên các trang tin lớn (như The Verge, TechCrunch) là sống còn đối với đội ngũ R&D và Marketing. Tuy nhiên, nếu làm thủ công, các sếp sẽ mất hàng giờ mỗi ngày để lướt web, copy thông tin và báo cáo. Chưa kể các trang web lớn thường có hệ thống chặn bot (anti-bot) rất gắt gao.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code. Hệ thống sẽ tự động cào dữ liệu mỗi sáng, sử dụng AI thông minh để trích xuất thông tin, gửi email cảnh báo trực tiếp cho đội ngũ R&D và lưu trữ lịch sử vào Google Sheets một cách gọn gàng!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoàn toàn 24/7**: Không cần thao tác thủ công, đúng 7h sáng mỗi ngày hệ thống tự chạy.
- **Vượt rào cản chống bot**: Nhờ tích hợp Bright Data MCP, cào dữ liệu mượt mà từ các trang web khó tính nhất.
- **Cập nhật tức thì cho đội ngũ**: Gửi email tóm tắt chi tiết (Tiêu đề, ngày phát hành, tóm tắt, link gốc) thẳng vào Gmail của team R&D.
- **Lưu trữ dữ liệu khoa học**: Tự động ghi nhận lịch sử vào Google Sheets để phục vụ việc phân tích xu hướng về lâu dài.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **n8n Instance** (Cloud hoặc Self-hosted).
- Tài khoản **OpenAI** (để lấy OpenAI API Key dùng cho Model `gpt-4o-mini`).
- Tài khoản **Bright Data** (để sử dụng dịch vụ cào dữ liệu và MCP Tool). *(Sếp có thể đăng ký qua link ủng hộ tác giả: [Bright Data](https://get.brightdata.com/1tndi4600b25))*
- Tài khoản **Google Gmail** (để gửi email thông báo).
- Tài khoản **Google Sheets** (để lưu log dữ liệu).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow hoặc tải file JSON từ nguồn cấp.
- Mở giao diện n8n của các sếp, chọn **Workflows** -> **Import from JSON** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các node quan trọng sau:

- **⏰ Daily Check (7AM)**: Node kích hoạt theo lịch. Các sếp có thể đổi giờ chạy tùy ý nếu không muốn cố định lúc 7 giờ sáng.
- **🛠 Set Scrape Target (Verge Reviews)**: Node này chứa URL cần cào (`https://www.theverge.com/reviews`). Các sếp có thể thay đổi URL này thành trang review của đối thủ khác (như TechCrunch, Wired...).
- **🤖 Bright Data Scraper Agent & OpenAI Chat Model**: 
  - Kết nối OpenAI Credential (`openAiApi`) cho các node Chat Model (`gpt-4o-mini`).
  - Cấu hình MCP Client Tool để kết nối với tài khoản Bright Data, giúp AI Agent vượt qua các lớp bảo vệ chống bot để trích xuất: Tiêu đề sản phẩm, Ngày phát hành, Tóm tắt ngắn gọn và URL.
- **🧾 Split & Format Each Review**: Node xử lý code JavaScript có sẵn giúp chuyển đổi các đường dẫn tương đối (relative URL) thành link hoàn chỉnh (`https://www.theverge.com/...`) và tách mảng dữ liệu thành từng dòng riêng biệt.
- **📤 Email R&D: Product Alerts**: Chọn Gmail Credentials (`gmailOAuth2`) và điền địa chỉ email nhận tin của đội ngũ R&D hoặc của chính các sếp.
- **📊 Log to Google Sheet (Review History)**: 
  - Kết nối Google Sheets Credentials (`googleSheetsOAuth2Api`).
  - Chọn file Google Sheet và Sheet Name tương ứng để hệ thống tự động append (thêm dòng) lịch sử review mỗi ngày.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để chạy thử nghiệm thủ công xem dữ liệu có đổ về Google Sheets và Gmail hay không.
- Nếu mọi thứ chạy mượt mà, hãy gạt công tắc sang **Active** để workflow tự động chạy ngầm mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Chatwork/Telegram/Slack**: Ngoài Gmail, các sếp có thể nối thêm node Telegram hoặc Slack để bắn tin nhắn nhanh vào group chat của công ty ngay khi có sản phẩm mới.
- **Thêm bộ lọc thông minh**: Thêm node IF sau phần cào dữ liệu để chỉ gửi cảnh báo khi sản phẩm chứa các từ khóa đặc biệt (ví dụ: "AI", "Smartwatch", tên thương hiệu đối thủ cụ thể...).
- **Báo cáo định kỳ hàng tuần**: Tạo thêm một nhánh workflow tổng hợp dữ liệu từ Google Sheets vào cuối tuần để gửi báo cáo tuần cho Sếp lớn.

### 📌 Kết luận
Với workflow này, việc theo dõi đối thủ cạnh tranh đã trở nên tự động hóa hoàn toàn nhờ sức mạnh của AI và công cụ cào dữ liệu chuyên nghiệp. Hãy áp dụng ngay hôm nay để giúp đội ngũ R&D của các sếp luôn đi trước một bước trên thị trường!