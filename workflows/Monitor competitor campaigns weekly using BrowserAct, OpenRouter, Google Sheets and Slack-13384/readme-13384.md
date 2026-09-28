---
title: "🚀 Tự động giám sát chiến dịch đối thủ hàng tuần với BrowserAct, OpenRouter, Google Sheets và Slack"
description: "Hướng dẫn xây dựng hệ thống tự động cào dữ liệu landing page đối thủ, phân tích sự thay đổi chiến lược bằng AI và gửi báo cáo chi tiết qua Slack hàng tuần."
slug: "tu-dong-giam-sat-chien-dich-doi-thu-hang-tuan"
tags: [n8n, automation, no-code, market-research, ai-agent, browseract]
keywords: [n8n workflow, giám sát đối thủ, browseract, openrouter, google sheets, slack automation, market research ai]
---

# 🚀 Tự động giám sát chiến dịch đối thủ hàng tuần với BrowserAct, OpenRouter, Google Sheets và Slack

Các sếp có đang tốn hàng giờ mỗi tuần để thủ công truy cập website đối thủ, soi xem họ thay đổi giá cả, chương trình khuyến mãi hay thông điệp marketing ra sao không? Công việc lặp đi lặp lại này vừa mất thời gian lại dễ bỏ sót các biến động quan trọng trên thị trường.

Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ mạnh mẽ giúp tự động hóa 100% quy trình này: Tự động cào dữ liệu, dùng AI so sánh với lịch sử cũ, cập nhật Google Sheets và gửi báo cáo chiến lược tóm tắt thẳng vào Slack mỗi tuần!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải "lướt dạo" web đối thủ thủ công hàng tuần.
- **Phát hiện thay đổi chớp nhoáng:** Nhận diện ngay lập tức các biến động về giá, gói sản phẩm (bundles) hay câu chữ marketing (copy) của đối thủ.
- **Báo cáo thông minh:** AI tổng hợp thành bản tin (Executive Digest) ngắn gọn, súc tích gửi trực tiếp vào kênh Slack của đội ngũ.
- **Hoạt động tự động 24/7:** Chạy ngầm định kỳ hàng tuần nhờ Trigger thông minh mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **BrowserAct Account & API Key** (Kèm theo Template: *Competitor Campaign Monitoring (Huel)*).
- **OpenRouter API Key** (Sử dụng các mô hình AI cao cấp như GPT-4/GPT-5).
- **Google Sheets** (File chứa danh sách URL đối thủ và lưu trữ dữ liệu lịch sử).
- **Slack Workspace & Bot Token** (Để gửi thông báo báo cáo).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON từ nguồn gốc (ID: `13384`) hoặc copy mã JSON của workflow và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, hệ thống gồm 15 nodes sẽ xuất hiện. Các sếp cần cấu hình chính xác các thành phần sau:

- **Weekly Trigger**: Đặt lịch chạy tự động theo tuần (ví dụ: sáng thứ Hai hàng tuần).
- **Retrieve database items & Extract the target URLs (Google Sheets)**: 
  - Kết nối tài khoản Google Sheets thông qua `googleSheetsOAuth2Api`.
  - Trỏ đến đúng file Google Sheet quản lý URL các trang landing page của đối thủ và dữ liệu lịch sử.
- **Loop Over Items (Split In Batches)**: Xử lý từng URL một cách mượt mà để tránh quá tải API.
- **Scrape the target pages (BrowserAct)**: 
  - Cấu hình credentials `browserActApi`.
  - Đảm bảo template **Competitor Campaign Monitoring (Huel)** đã được lưu sẵn trong tài khoản BrowserAct của các sếp.
- **Analyze the pages & Analyze all the items and generate a report (AI Agent + OpenRouter)**:
  - Cấu hình credentials `openRouterApi` cho **OpenRouter Chat Model** và **OpenRouter Chat Model1**.
  - Thiết lập model (mặc định cấu hình sử dụng `openai/gpt-5` hoặc có thể đổi sang các model linh hoạt khác như Claude 3.5 Sonnet).
  - Kết hợp **Structured Output Parser** để ép AI trả về dữ liệu đúng định dạng mong muốn.
- **Update Database (Google Sheets)**: Cập nhật lại dữ liệu mới nhất vào file Google Sheets để làm mốc so sánh cho tuần sau.
- **Send a message (Slack)**: 
  - Kết nối credentials `slackApi`.
  - Điền ID kênh Slack nhận báo cáo (thông qua node **Split out Slack messages** để tách các đoạn tin nhắn dài nếu cần).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng nút thực thi thủ công trên một vài dòng dữ liệu mẫu để kiểm tra kết quả trả về ở Google Sheets và Slack.
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, hãy bật công tắc **Active** để workflow tự động làm việc thay các sếp!

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống nghiên cứu thị trường này trở nên bá đạo hơn, các sếp có thể tùy biến thêm:
- **Đa kênh thông báo:** Ngoài Slack, tích hợp thêm node Telegram hoặc Email để gửi bản tin tóm tắt cho ban lãnh đạo.
- **Lưu trữ Log lịch sử:** Tạo thêm một sheet "Audit Log" để ghi nhận lại toàn bộ lịch sử biến động giá của từng đối thủ qua các tháng.
- **Cảnh báo khẩn cấp:** Thêm điều kiện lọc nếu phát hiện đối thủ giảm giá sốc (>20%), lập tức bắn thông báo khẩn cấp lên kênh Slack riêng của đội Sales & Pricing.

### 📌 Kết luận
Việc theo dõi đối thủ cạnh tranh chưa bao giờ dễ dàng và tự động hóa đến thế. Chỉ với một workflow n8n kết hợp giữa BrowserAct và AI, các sếp đã có ngay một "gián điệp công nghệ cao" phục vụ 24/7. Hãy setup ngay hôm nay để nắm bắt mọi chuyển động của thị trường trước đối thủ!