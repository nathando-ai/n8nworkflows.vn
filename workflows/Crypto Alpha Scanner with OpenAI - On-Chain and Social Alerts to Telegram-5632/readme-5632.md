---
title: "🚀 Crypto Alpha Scanner: Tự động quét On-Chain, Reddit, Twitter và phân tích AI gửi cảnh báo Telegram"
description: "Hướng dẫn cài đặt workflow n8n tự động săn cơ hội đầu tư crypto (Alpha) từ Whale, Reddit, DexScreener và dùng OpenAI tóm tắt gửi thẳng vào Telegram."
slug: "crypto-alpha-scanner-openai-telegram-n8n"
tags: [n8n, automation, crypto, openai, telegram, ai-summarization]
keywords: [n8n workflow crypto, crypto alpha scanner, tóm tắt crypto bằng ai, bot telegram crypto, theo dõi cá voi crypto n8n]
---

# 🚀 Tự động săn cơ hội Crypto Alpha với OpenAI & Telegram bằng n8n

Các sếp trong làng đầu tư Crypto chắc chắn hiểu cảm giác "FOMO" và việc bỏ lỡ các con sóng tăng trưởng chỉ vì không kịp cập nhật thông tin từ cá voi (Whale), mạng xã hội (Reddit, Twitter) hay các token mới nổi. Việc ngồi canh mỏi mắt trên DexScreener hay Twitter vừa tốn thời gian, vừa dễ bỏ lỡ cơ hội vàng.

Đừng lo, bài toán đó sẽ được giải quyết gọn gàng với workflow **Crypto Alpha Scanner with OpenAI - On-Chain and Social Alerts to Telegram**. Đây là trợ lý ảo tự động 100% không cần code, giúp các sếp gom toàn bộ dữ liệu on-chain, mạng xã hội, dùng AI phân tích độ tiềm năng và bắn thẳng thông tin "thơm" về Telegram của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow quét dữ liệu crypto chạy ổn định 24/7 mà không sợ gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chạy định kỳ theo lịch trình (Schedule Trigger) mà không cần can thiệp thủ công.
- **Tổng hợp đa nguồn:** Quét dữ liệu từ cá voi (Whale Moves), Reddit Crypto, Twitter (X), và DexScreener (Token mới/Trending).
- **Phân tích thông minh bằng AI:** Tận dụng OpenAI (ChatGPT) để lọc nhiễu, đánh giá và tóm tắt những thông tin Alpha thực sự chất lượng.
- **Cảnh báo tức thì:** Bắn tin nhắn tóm tắt sắc bén trực tiếp qua Telegram cá nhân hoặc Channel nhóm.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** Đã cài đặt sẵn sàng (khuyến nghị bản mới nhất).
- **OpenAI API Key:** Để chạy node phân tích AI (`AI Alpha Analysis1`).
- **Telegram Bot Token & Chat ID:** Để bot gửi thông báo (`Send to Telegram1`).
- **Reddit API Credentials:** Kết nối lấy bài đăng hot từ các subreddit crypto (`Reddit Crypto Scanner`).
- **Các API / Endpoints phụ:** Cho DexScreener, Twitter (X) và dữ liệu ví cá voi (`Fetch Whale Moves1`, `Get Tweets`, `DexScreener My Tokens Monitor`,...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow hoặc tải file JSON về máy.
- Mở giao diện n8n, chọn **Workflows** -> **Import from File** (hoặc dán trực tiếp vào Editor).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không lỗi, các sếp cần cấu hình chính xác các node trọng điểm sau:
- **Schedule Trigger:** Thiết lập chu kỳ quét (ví dụ: chạy mỗi 30 phút hoặc 1 tiếng một lần tùy nhu cầu).
- **Reddit Crypto Scanner:** Kết nối tài khoản Reddit của các sếp để quét các bài post/comment từ các cộng đồng crypto nổi tiếng.
- **Fetch Whale Moves1 / Get Tweets / DexScreener Nodes (HTTP Request):** Kiểm tra lại các endpoint API, thêm Bearer Token hoặc API Key nếu các bên cung cấp yêu cầu xác thực.
- **AI Alpha Analysis1 (OpenAI):** Chọn credential OpenAI, thiết lập model (khuyến nghị `gpt-4o-mini` hoặc `gpt-4o`) và tinh chỉnh System Prompt để AI đóng vai trò là một chuyên gia phân tích tài chính crypto, chỉ lọc ra các cơ hội có tỷ lệ thắng cao.
- **Should Send Message? (If) & Format for Telegram (Code):** Tinh chỉnh điều kiện lọc ở node `If` (ví dụ: điểm AI score > 8 mới gửi) và format nội dung hiển thị cho đẹp mắt tại node `Code`.
- **Send to Telegram1 (Telegram):** Điền chính xác Bot Token và Chat ID nơi các sếp muốn nhận thông báo.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thủ công lần đầu, kiểm tra xem dữ liệu từ Reddit, Whale, DexScreener có đổ về đúng không và OpenAI có trả về kết quả không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Nhân bản node Telegram để bắn tin nhắn đồng thời lên nhóm Telegram cộng đồng và nhắn riêng vào Telegram cá nhân của các sếp.
- **Lưu lịch sử Alpha:** Kết nối thêm node **Google Sheets** hoặc **Notion** sau bước phân tích AI để lưu trữ toàn bộ các cơ hội đã phát hiện, tiện cho việc backtest và theo dõi hiệu suất token sau đó.
- **Bộ lọc thông minh:** Tinh chỉnh prompt của OpenAI để yêu cầu AI cảnh báo rõ mức độ rủi ro (Risk Level: Low/Medium/High) trước khi gửi về điện thoại.

### 📌 Kết luận
Với workflow **Crypto Alpha Scanner**, các sếp không còn phải "cày cuốc" hàng giờ trên mạng xã hội hay dò tìm ví cá voi thủ công nữa. Hãy để AI và n8n làm việc đó thay các sếp 24/7. Chúc các sếp săn được nhiều kèo "x5, x10" chất lượng!