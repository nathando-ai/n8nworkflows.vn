---
title: "🚀 Theo dõi Siêu Ưu đãi Game đa nền tảng với Deku Deals & Gmail Alerts"
description: "Tự động quét trang Deku Deals mỗi ngày, lưu vào SQLite và gửi email thông báo các ưu đãi mới cho bạn."
slug: "theo-doi-uu-dai-game-deku-deals-gmail-alerts"
tags: [n8n, automation, no-code, game-deals, gmail, sqlite]
keywords: [n8n workflow, tự động hóa, theo dõi ưu đãi game, Deku Deals, Gmail alerts]
---

# 🚀 Theo dõi Siêu Ưu đãi Game đa nền tảng với Deku Deals & Gmail Alerts

Bạn có bao giờ lỡ mất một đợt giảm giá “đỉnh” chỉ vì không kịp kiểm tra trang Deku Deals mỗi sáng?  
Việc mở trình duyệt, copy‑paste link, so sánh giá… tiêu tốn thời gian và dễ bỏ sót.  

**Workflow này** sẽ tự động:

1. **Kiểm tra** trang Deku Deals vào 8 h sáng mỗi ngày.  
2. **Trích xuất** các thẻ ưu đãi mới, lưu vào SQLite để tránh thông báo trùng.  
3. **Gửi email** ngay lập tức tới Gmail của bạn với danh sách ưu đãi mới nhất.  

> Không cần viết một dòng code nào – chỉ cần import workflow và cấu hình vài thông tin.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Không còn mở trình duyệt mỗi sáng.  
- **Đảm bảo không bỏ lỡ**: SQLite lưu lịch sử, chỉ thông báo ưu đãi mới.  
- **Cá nhân hoá**: Email được format đẹp, chứa link trực tiếp.  
- **Hoạt động liên tục**: Cron tự động chạy 24/7, không cần can thiệp.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản Gmail** (đã bật Gmail API) – sẽ dùng credential `gmailApi`.  
- **SQLite database** (file `.sqlite` trên server n8n, ví dụ `deku_deals.db`).  
- **Quyền truy cập internet** để gọi `https://deku.deals`.  
- **n8n** (cài đặt trên VPS hoặc Docker).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở **n8n Editor**.  
2. Nhấn **Import** → **From File** → chọn file JSON của workflow (được cung cấp ở cuối README) **hoặc** Copy/Paste toàn bộ JSON vào ô **Paste JSON**.  
3. Nhấn **Import** → workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌  

| Node | Cấu hình cần thay đổi | Ghi chú |
|------|----------------------|---------|
| **Daily Check (8 AM)** (cron) | - **Trigger Time**: `08:00` (UTC hoặc timezone của bạn). | Đảm bảo múi giờ đúng để nhận email vào sáng sớm. |
| **Fetch Deku Deals Page** (httpRequest) | - **Method**: `GET` <br> - **URL**: `https://deku.deals` <br> - **Response Format**: `String` | Nếu Deku thay đổi domain, cập nhật URL tương ứng. |
| **Extract Each Deal Card** (htmlExtract) | - **CSS Selector**: `.deal-card` (hoặc selector thực tế trên trang). <br> - **Attributes to Extract**: `innerHTML` hoặc `data-id`, `title`, `price`, `href`. | Kiểm tra selector bằng công cụ Inspect của trình duyệt. |
| **Parse Deal Details (Function Code)** (function) | - **Code**: (được cung cấp trong workflow). Đảm bảo biến `items` trả về mảng object `{ id, title, price, link }`. | Không cần thay đổi nếu cấu trúc HTML chưa thay đổi. |
| **SQLite: Ensure Table Exists** (sqlite) | - **Database File**: `deku_deals.db` (đường dẫn đầy đủ trên server). <br> - **Query**: `CREATE TABLE IF NOT EXISTS deals (id TEXT PRIMARY KEY, title TEXT, price TEXT, link TEXT, notified INTEGER DEFAULT 0);` | Tạo bảng nếu chưa có. |
| **SQLite: Check if Notified** (sqlite) | - **Database File**: `deku_deals.db`. <br> - **Query**: `SELECT id FROM deals WHERE id = $id;` <br> - **Parameters**: `id` lấy từ output của node trước. | Kiểm tra xem ưu đãi đã được thông báo chưa. |
| **Split into Notified/New** (itemLists) | - **Mode**: `Split In Items`. <br> - **Condition**: dựa vào kết quả của node Check if Notified. | Tạo hai danh sách: `notified` và `new`. |
| **If (New Deals Found)** (if) | - **Condition**: `{{$json["new"].length > 0}}` (hoặc tương tự). | Chỉ tiếp tục nếu có ưu đãi mới. |
| **SQLite: Insert New Deals** (sqlite) | - **Database File**: `deku_deals.db`. <br> - **Query**: `INSERT INTO deals (id, title, price, link, notified) VALUES ($id, $title, $price, $link, 1);` <br> - **Parameters**: lấy từ danh sách `new`. | Lưu ưu đãi mới và đánh dấu đã thông báo. |
| **Format Notification Message** (function) | - **Code**: Tạo chuỗi HTML hoặc plain‑text, ví dụ: ```\nreturn {\n  subject: `🕹️ ${items.length} ưu đãi game mới từ Deku Deals`,\n  body: items.map(i => `• ${i.title} - ${i.price}\\n  ${i.link}`).join('\\n')\n};\n``` | Thay đổi mẫu email nếu muốn. |
| **Send Email Notification** (gmail) | - **Credentials**: chọn `gmailApi` (đã tạo trong n8n). <br> - **To**: địa chỉ Gmail của bạn. <br> - **Subject** & **Body**: dùng output của node trên (`{{ $json.subject }}`, `{{ $json.body }}`). | Kiểm tra quota Gmail API nếu gửi nhiều email. |

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn nút **Execute Workflow** → chọn **Run Once** → kiểm tra log ở mỗi node, đặc biệt node `Send Email Notification`.  
2. Nếu email tới, **bật** workflow bằng cách chuyển **Active** sang **On**.  
3. Kiểm tra hộp thư vào 8 h sáng hôm sau để xác nhận cron hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack/Telegram**: Dùng node **Slack** hoặc **Telegram** để nhận thông báo ngay trên kênh nhóm.  
- **Lưu log chi tiết**: Thêm node **SQLite** hoặc **Google Sheets** để ghi lại thời gian nhận, số lượng ưu đãi mỗi ngày.  
- **Báo cáo tuần**: Dùng **Cron** (ví dụ mỗi Chủ Nhật) để tổng hợp và gửi báo cáo tổng hợp các ưu đãi đã nhận trong tuần.  
- **Đa nguồn**: Nhân rộng workflow, thêm **httpRequest** cho các trang ưu đãi khác (SteamDB, Humble Bundle) và hợp nhất kết quả trước khi gửi email.

### 📌 Kết luận
Với chỉ một workflow n8n, các sếp có thể **tự động** quét, lưu trữ và nhận thông báo về mọi ưu đãi game mới trên Deku Deals mà không tốn một giây phút nào cho việc kiểm tra thủ công. Hãy **import**, **cấu hình** nhanh chóng và để n8n làm việc thay bạn – để bạn có thể tập trung vào việc chơi game và săn deal!

---  

**File JSON của workflow** (để import):  

```json
{
  "name": "Automated Multi-Platform Game Deals Tracker with Deku Deals & Gmail Alerts",
  "nodes": [
    {
      "parameters": {
        "cronExpression": "0 8 * * *"
      },
      "name": "Daily Check (8 AM)",
      "type": "n8n-nodes-base.cron",
      "typeVersion": 1,
      "position": [250, 300]
    },
    {
      "parameters": {
        "url": "https://deku.deals",
        "responseFormat": "string",
        "options": {}
      },
      "name": "Fetch Deku Deals Page",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 1,
      "position": [450, 300]
    },
    {
      "parameters": {
        "selector": ".deal-card",
        "attribute": "innerHTML",
        "multiple": true
      },
      "name": "Extract Each Deal Card",
      "type": "n8n-nodes-base.htmlExtract",
      "typeVersion": 1,
      "position": [650, 300]
    },
    {
      "parameters": {
        "functionCode": "return items.map(item => {\n  const $ = cheerio.load(item.json);\n  const id = $('.deal-id', $).text().trim();\n  const title = $('.deal-title', $).text().trim();\n  const price = $('.deal-price', $).text().trim();\n  const link = $('.deal-link', $).attr('href');\n  return { json: { id, title, price, link } };\n});"
      },
      "name": "Parse Deal Details (Function Code)",
      "type": "n8n-nodes-base.function",
      "typeVersion": 1,
      "position": [850, 300]
    },
    {
      "parameters": {
        "operation": "executeQuery",
        "query": "CREATE TABLE IF NOT EXISTS deals (id TEXT PRIMARY KEY, title TEXT, price TEXT, link TEXT, notified INTEGER DEFAULT 0);