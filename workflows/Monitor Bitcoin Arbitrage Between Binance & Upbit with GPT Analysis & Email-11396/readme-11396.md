---
title: "🚀 Tự động giám sát chênh lệch giá Bitcoin (Kimchi Premium) giữa Binance & Upbit bằng n8n & GPT"
description: "Hướng dẫn xây dựng workflow n8n tự động theo dõi giá Bitcoin trên Binance và Upbit, phân tích tỷ giá Forex, sử dụng AI GPT-4o-mini để đánh giá cơ hội arbitrage và gửi báo cáo qua Gmail."
slug: "tu-dong-giam-sat-chenh-lech-gia-bitcoin-binance-upbit-n8n-gpt"
tags: [n8n, automation, crypto, openai, gmail, arbitrage]
keywords: [n8n workflow, kimchi premium, binance upbit arbitrage, ai crypto analysis, tu dong hoa crypto]
keywords: [n8n workflow, chênh lệch giá bitcoin, kimchi premium, tự động hóa crypto, openai n8n]
---

# 🚀 Tự động giám sát chênh lệch giá Bitcoin (Kimchi Premium) giữa Binance & Upbit bằng n8n & GPT

Các sếp làm trong lĩnh vực giao dịch tiền mã hóa (Crypto) chắc hẳn đều biết đến hiện tượng **Kimchi Premium** – sự chênh lệch giá Bitcoin thường thấy giữa các sàn quốc tế (như Binance) và các sàn Hàn Quốc (như Upbit). Việc theo dõi thủ công biến động này từng phút là bất khả thi và cực kỳ tốn thời gian. 

Giải pháp là gì? Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n tự động hoàn toàn: thu thập giá, quy đổi tiền tệ qua tỷ giá ngoại hối (Forex), sử dụng AI (GPT-4o-mini) phân tích cơ hội Arbitrage và tự động gửi báo cáo chiến lược qua Gmail mỗi khi có biến động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 săn cơ hội kiếm lời từ thị trường crypto không ngủ, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Hệ thống tự quét dữ liệu định kỳ mà không cần con người can thiệp.
- **Phân tích thông minh bằng AI:** Sử dụng AI Agent (GPT-4o-mini) để tính toán độ chênh lệch, đánh giá tính khả thi và rủi ro của cơ hội arbitrage.
- **Báo cáo tức thời:** Nhận ngay bản phân tích chiến lược chi tiết gửi thẳng vào hòm thư Gmail cá nhân.
- **Tối ưu hóa lợi nhuận:** Nắm bắt thời điểm vàng mua thấp bán cao giữa thị trường quốc tế và Hàn Quốc một cách nhanh chóng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance **n8n** đang hoạt động (Cloud hoặc Self-hosted).
- **OpenAI API Key** (dùng cho các node LangChain OpenAI).
- **Tài khoản Google/Gmail** (để cấu hình node gửi email tự động).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ kho lưu trữ n8n (Template ID: `11396`).
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc paste trực tiếp mã JSON vào).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 13 nodes được chia thành 3 giai đoạn chính. Các sếp cần cấu hình kỹ các điểm sau:

- **Schedule Trigger:** Mặc định workflow được thiết lập chạy định kỳ (ví dụ: mỗi 30 phút). Các sếp có thể điều chỉnh tần suất này tùy theo chiến lược giao dịch ngắn hạn hay dài hạn.
- **Get price from Binance**, **Get price from Upbit**, **Get price from Forex** (`httpRequest` nodes): Các node này gọi API công khai để lấy giá BTC thời gian thực và tỷ giá USD/KRW. Thường không cần cấu hình API key riêng nhưng cần kiểm tra kết nối mạng của VPS.
- **Edit Fields For Binance Data**, **Edit Fields For Upbit Data**, **Edit Fields For Forex Data** (`set` nodes): Dùng để chuẩn hóa tên trường dữ liệu trước khi gộp chung.
- **Merge Data** (`merge` node): Gộp dữ liệu từ 3 nguồn (Binance, Upbit, Forex) thành một dataset duy nhất.
- **OpenAI Chat Model for Analyzer** & **OpenAI Chat Model for Format** (`lmChatOpenAi`): 
  - Chọn model: `gpt-4o-mini`.
  - Nhập **OpenAI API Key** của các sếp vào phần Credentials.
- **Analyzer** (`agent`) & **Structured Output Parser** (`outputParserStructured`): AI Agent sẽ xử lý dữ liệu đầu vào đã gộp, tính toán "Kimchi Premium", chạy prompt phân tích và ép kiểu đầu ra theo cấu trúc định sẵn.
- **Send a Message for Traders** (`gmail`): 
  - Kết nối tài khoản Google của các sếp qua OAuth2.
  - Điền địa chỉ email nhận báo cáo (`To`) tại node này.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thủ công một lần và kiểm tra kết quả trả về ở node Gmail / AI Agent.
- Nếu mọi thứ chạy mượt mà, gạt công tắc sang trạng thái **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Ngoài Gmail, các sếp có thể nối thêm node Telegram hoặc Slack để nhận thông báo tức thời ngay trên điện thoại khi có chênh lệch giá vượt ngưỡng cho phép (ví dụ > 3%).
- **Lưu trữ lịch sử:** Thêm node Google Sheets hoặc Airtable để lưu lại lịch sử biến động giá qua từng khung giờ, phục vụ cho việc backtest hoặc phân tích kỹ thuật sau này.
- **Cảnh báo rủi ro:** Tùy chỉnh prompt trong AI Agent để đưa ra cảnh báo về phí giao dịch giữa các sàn và biến động tỷ giá hối đoái.

### 📌 Kết luận
Workflow giám sát Arbitrage Bitcoin kết hợp AI là một công cụ cực kỳ mạnh mẽ giúp các sếp tiết kiệm hàng giờ theo dõi biểu đồ. Hãy cài đặt ngay lên hệ thống n8n của mình và bắt đầu "săn" những cơ hội chênh lệch giá tiềm năng ngay hôm nay!