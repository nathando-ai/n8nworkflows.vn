---
title: "🚀 Tự động cập nhật xu hướng tiền mã hoá từ CoinGecko tới Telegram"
description: "Workflow n8n kéo danh sách coin đang hot từ CoinGecko và gửi tin nhắn định kỳ vào nhóm/channel Telegram, không cần API key."
slug: "tu-dong-cap-nhat-coin-gecko-telegram"
tags: [n8n, automation, no-code, crypto, telegram, coin-gecko]
keywords: [n8n workflow, tự động hóa, crypto, telegram bot, CoinGecko]
---

# 🚀 Tự động cập nhật xu hướng tiền mã hoá từ CoinGecko tới Telegram

Bạn có bao giờ phải mở nhiều tab, sao chép‑dán danh sách coin đang “hot” mỗi ngày chỉ để chia sẻ với cộng đồng Telegram?  
Việc này không chỉ tốn thời gian mà còn dễ sai sót, khiến các thành viên bỏ lỡ cơ hội giao dịch quan trọng.  

**Workflow này** sẽ tự động lấy dữ liệu trending từ CoinGecko (API công cộng, không cần key) và gửi ngay một tin nhắn định dạng đẹp mắt tới nhóm hoặc kênh Telegram của bạn – **100 % không cần viết code**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn thao tác thủ công mỗi ngày.  
- **Độ chính xác 100 %**: Dữ liệu lấy trực tiếp từ API CoinGecko.  
- **Cá nhân hoá**: Tin nhắn được định dạng theo phong cách nhóm của bạn.  
- **Hoạt động liên tục**: Tự động chạy 2 lần/ngày (8:30 sáng & tối) mà không cần can thiệp.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n instance** (self‑hosted hoặc n8n.cloud).  
- **Telegram Bot Token** (tạo bot qua BotFather).  
- **Telegram Chat ID** của nhóm hoặc kênh muốn nhận tin (có thể lấy bằng bot).  
- Không cần API key nào khác vì CoinGecko cung cấp API công cộng.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow từ trang gốc: https://n8n.io/workflows/8271  
2. Vào **n8n Editor → Import** → Chọn file JSON → **Import**.  
3. Workflow sẽ xuất hiện với 5 node: `Get Trending`, `Format Message`, `Send Telegram Message`, `When clicking ‘Execute workflow’`, `8:30 AM/PM IST`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cấu hình quan trọng | Hướng dẫn chi tiết |
|------|--------------------|--------------------|
| **Get Trending** (httpRequest) | URL: `https://api.coingecko.com/api/v3/search/trending` <br> Method: **GET** | Không cần authentication. Đảm bảo **Response Format** là **JSON**. |
| **Format Message** (function) | Mã JavaScript để định dạng tin nhắn | ```js\nconst items = $json.coins.map(c => c.item);\nlet msg = '*🔥 Top Trending Coins (CoinGecko) 🔥*\\n\\n';\nitems.forEach((c, i) => {\n  msg += `${i+1}. *${c.name}* (${c.symbol.toUpperCase()})\\n`; \n  msg += `   Market Cap Rank: ${c.market_cap_rank}\\n`;\n  msg += `   Link: https://www.coingecko.com/en/coins/${c.id}\\n\\n`;\n});\nreturn [{ json: { text: msg } }];\n``` |
| **Send Telegram Message** (telegram) | **Credentials**: chọn `telegramApi` (Bot Token) <br> **Chat ID**: thay `{{YOUR_CHAT_ID}}` bằng ID thực tế | Trong **Credentials**, nhập Bot Token từ BotFather. Trong **Chat ID**, dán số ID nhóm/kênh (định dạng `-100xxxxxxxx`). |
| **When clicking ‘Execute workflow’** (manualTrigger) | Dùng để **test** nhanh. Không cần thay đổi. | Khi muốn kiểm tra, nhấn **Execute Workflow** trên node này. |
| **8:30 AM/PM IST** (scheduleTrigger) | Cron expression: `30 8,20 * * *` (IST) | Nếu muốn thay đổi thời gian, chỉnh **Cron** hoặc **Timezone** trong node. |

#### 3. Kích hoạt ⚡️
1. **Test**: Nhấn nút **Execute Workflow** trên node `When clicking ‘Execute workflow’`. Kiểm tra tin nhắn có xuất hiện trong Telegram chưa.  
2. Nếu mọi thứ ổn, bật **Active** ở góc phải của editor. Workflow sẽ tự động chạy vào 8:30 sáng và 8:30 tối (IST) mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm giá hiện tại**: Gọi thêm endpoint `/coins/markets` để lấy giá USD và chèn vào tin nhắn.  
- **Gửi đa kênh**: Nhân bản node `Send Telegram Message` và thay `Chat ID` để đồng thời thông báo tới nhiều nhóm.  
- **Lưu log**: Dùng node **Google Sheets** hoặc **Airtable** để ghi lại danh sách coin mỗi ngày, tiện cho phân tích xu hướng dài hạn.  
- **Xử lý lỗi**: Thêm node **Error Trigger** để nhận thông báo qua Slack/Telegram khi API CoinGecko trả về lỗi.  

### 📌 Kết luận
Với chỉ một vài bước cấu hình, các sếp đã có một công cụ **tự động** cập nhật xu hướng tiền mã hoá, giúp cộng đồng Telegram luôn “đón đầu” thị trường mà không tốn công sức. Hãy triển khai ngay hôm nay, tùy biến lịch chạy và mở rộng tính năng để phù hợp với nhu cầu thực tế của nhóm! 🚀