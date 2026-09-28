---
title: "🚀 Theo dõi danh mục crypto đa chuỗi & phân tích rủi ro bằng Gemini + QuickNode"
description: "Tự động thu thập số dư ví, giá gas & giá token trên nhiều chuỗi, tính toán giá trị danh mục và nhận báo cáo AI thông minh qua Slack."
slug: "theo-doi-danh-muc-crypto-da-chuoi-gemini-quicknode"
tags: [n8n, automation, no-code, crypto, AI, blockchain]
keywords: [n8n workflow, tự động hóa crypto, Gemini AI, QuickNode, phân tích rủi ro]
---

# 🚀 Theo dõi danh mục crypto đa chuỗi & phân tích rủi ro bằng Gemini + QuickNode

Các sếp đang phải **đối mặt với việc kiểm tra thủ công** số dư ví trên nhiều blockchain, tính toán giá trị danh mục, theo dõi phí gas và cuối cùng còn phải tự viết báo cáo.  
Quá trình này tốn hàng giờ, dễ sai sót và không thể cung cấp **các góc nhìn chiến lược** ngay lập tức.  

**Workflow này** giải quyết toàn bộ vấn đề bằng một chuỗi tự động hoá 100 % – không cần viết code – từ việc lấy dữ liệu blockchain, giá token, phí gas, tới việc phân tích bằng AI Gemini và gửi báo cáo ngay vào Slack.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn phải mở nhiều explorer, API, hay tính toán bằng tay.  
- **Độ chính xác 100 %**: Dữ liệu lấy trực tiếp từ QuickNode & CoinGecko, không có sai sót do nhập liệu.  
- **Cá nhân hoá**: AI Gemini đưa ra phân tích rủi ro, gợi ý cân bằng danh mục dựa trên ví của từng sếp.  
- **Hoạt động liên tục**: Có thể lên lịch chạy hàng ngày, báo cáo tự động gửi vào Slack hoặc Telegram.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Ví EVM** (Ethereum, Polygon, …) – địa chỉ công khai.  
- **QuickNode API key** (để truy cập RPC của các chuỗi).  
- **Google Gemini (Palm) API key** – dùng cho node `Google Gemini Chat Model`.  
- **Slack OAuth2 token** + kênh Slack nơi muốn nhận báo cáo.  
- **API giá token** (CoinGecko được dùng mặc định, không cần key).  
- **Instance n8n** (Self‑hosted hoặc n8n.cloud) có cài các node: QuickNode, LangChain, Slack.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow (từ link gốc hoặc đính kèm).  
2. Vào **n8n → Workflows → Import** → Chọn file JSON → **Import**.  
3. Hoặc mở **n8n Editor**, nhấn **+** → **Import from Clipboard**, dán toàn bộ JSON và **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌  
Dưới đây là danh sách **node quan trọng** và cách cấu hình chúng:

| Node | Loại | Cấu hình cần chỉnh |
|------|------|--------------------|
| **When clicking ‘Execute workflow’** | `manualTrigger` | Không cần thay đổi, dùng để test hoặc gắn Cron sau. |
| **Set Wallet & Coins** | `set` | - **walletAddress**: địa chỉ ví của sếp.<br>- **coins**: mảng token (ví dụ: `["ETH","MATIC","USDC"]`). |
| **Polygon blockchain** | `quicknodeRpc` | Chọn **Credential** `quicknodeApi` → nhập **Endpoint URL** cho Polygon. |
| **Ethereum blockchain** | `quicknodeRpc` | Tương tự, nhập **Endpoint URL** cho Ethereum. |
| **Polygon Gas Price** | `quicknodeRpc` | Credential `quicknodeApi` + **Operation** = `getGasPrice`. |
| **ETH Gas Price** | `quicknodeRpc` | Credential `quicknodeApi` + **Operation** = `getGasPrice`. |
| **Fetch Crypto Prices (USD)** | `httpRequest` | URL: `https://api.coingecko.com/api/v3/simple/price?ids=ethereum,polygon&vs_currencies=usd` (hoặc tùy chỉnh token). Phương thức **GET**. |
| **Google Gemini Chat Model** | `lmChatGoogleGemini` | Chọn **Credential** `googlePalmApi`. Prompt mặc định đã được thiết kế để nhận dữ liệu danh mục và trả về insight. |
| **Structured Output Parser** | `outputParserStructured` | Định nghĩa **Schema** (JSON) cho kết quả AI: `insights`, `riskScore`, `suggestions`, … (được workflow cung cấp sẵn). |
| **Generate AI Portfolio Insights** | `agent` (LangChain) | Kết nối **Model** = `Google Gemini Chat Model`, **Parser** = `Structured Output Parser`. |
| **Merge Portfolio & AI Data** | `merge` | Đảm bảo **Mode** = `Append` để gộp dữ liệu portfolio với kết quả AI. |
| **Format Slack Report** | `code` | Script JavaScript chuẩn format markdown cho Slack (không cần chỉnh nếu muốn giữ nguyên). |
| **Send Slack Alert** | `slack` | Chọn **Credential** `slackOAuth2Api`, nhập **Channel ID** hoặc **Channel Name** nơi muốn nhận báo cáo. |

> **Lưu ý:**  
> - Các node **QuickNode RPC** phải dùng **cùng một Credential** (`quicknodeApi`) nhưng endpoint khác nhau cho mỗi chuỗi.  
> - Nếu muốn mở rộng sang **chuỗi khác** (BSC, Avalanche…), chỉ cần thêm node `quicknodeRpc` mới và cập nhật phần **Merge Blockchain Data**.  
> - Kiểm tra **Scope** của Slack token: cần quyền `chat:write` và `channels:read`.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn nút **Execute Workflow** → kiểm tra log từng node, đặc biệt node `Generate AI Portfolio Insights` và `Send Slack Alert`.  
2. Nếu mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải).  
3. (Tùy chọn) Thêm **Cron node** trước `manualTrigger` để tự động chạy hàng ngày (ví dụ: `0 9 * * *` → 9 AM mỗi ngày).

### ✍️ Mẹo & gợi ý nâng cao
- **Lên lịch Cron**: Đặt Cron node trước `manualTrigger` để nhận báo cáo mỗi sáng, giúp sếp luôn nắm bắt tình hình danh mục.  
- **Mở rộng chuỗi**: Thêm node `quicknodeRpc` cho bất kỳ EVM chain nào, chỉ cần endpoint và cập nhật phần merge.  
- **Lưu log**: Dùng node **Google Sheets** hoặc **PostgreSQL** để ghi lại lịch sử báo cáo, tiện cho phân tích xu hướng dài hạn.  
- **Thông báo đa kênh**: Thêm node **Telegram** hoặc **Email** song song với Slack để không bỏ lỡ khi Slack offline.  
- **Tùy chỉnh Prompt AI**: Sửa nội dung trong `Google Gemini Chat Model` để nhận thêm phân tích kỹ thuật, tin tức thị trường hoặc đề xuất tái cân bằng danh mục.

### 📌 Kết luận
Với workflow này, các sếp sẽ **không còn phải mất hàng giờ** để thu thập dữ liệu, tính toán và viết báo cáo. Tất cả được tự động hoá, chính xác và được **AI Gemini** phân tích sâu, đưa ra những gợi ý chiến lược ngay trong Slack. Hãy **import ngay**, cấu hình các credential cần thiết và để n8n làm việc cho bạn – biến việc quản lý danh mục crypto thành một việc “bấm một nút”. 🚀