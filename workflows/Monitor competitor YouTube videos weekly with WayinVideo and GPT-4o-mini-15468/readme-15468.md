---
title: "🚀 Tự động theo dõi YouTube đối thủ hàng tuần với WayinVideo và GPT-4o-mini"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy danh sách video YouTube của đối thủ từ Google Sheets, tóm tắt bằng WayinVideo, phân tích chiến lược thông minh qua GPT-4o-mini và lưu trữ vào Airtable mỗi thứ Hai hàng tuần."
slug: "tu-dong-theo-doi-youtube-doi-thu-voi-wayinvideo-gpt-4o-mini"
tags: [n8n, automation, no-code, youtube-monitoring, ai-summarization, airtable, openai]
keywords: [n8n workflow, theo dõi đối thủ youtube, tóm tắt video ai, wayinvideo, gpt-4o-mini, airtable automation, google sheets n8n]
---

# 🚀 Tự động theo dõi YouTube đối thủ hàng tuần với WayinVideo và GPT-4o-mini

Các sếp làm marketing, quản lý sản phẩm (Product Managers) hay đội ngũ Growth chắc chắn hiểu rõ nỗi đau: Việc ngồi hàng giờ xem video YouTube của đối thủ cạnh tranh để phân tích thông điệp, điểm mạnh, điểm yếu hay chiến lược giá thực sự tốn rất nhiều thời gian và công sức. 

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một **n8n workflow hoàn toàn tự động** giải quyết trọn vẹn bài toán trên. Cứ mỗi sáng thứ Hai lúc 8:00, hệ thống sẽ tự động quét danh sách video, tóm tắt nội dung, phân tích chiến lược bằng AI và lưu kết quả gọn gàng vào Airtable mà không cần con người nhúng tay vào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần xem hàng giờ video đối thủ, nhận ngay báo cáo tóm tắt cấu trúc.
- **Phân tích chiều sâu tự động:** GPT-4o-mini tự động bóc tách 10 trường thông tin chiến lược (góc thông điệp, điểm yếu, cơ hội cho đội ngũ, điểm khẩn cấp...).
- **Lưu trữ khoa học:** Tự động đồng bộ báo cáo chi tiết vào Airtable và cập nhật trạng thái trên Google Sheets.
- **Vận hành 24/7:** Lịch chạy tự động mỗi thứ Hai hàng tuần, sẵn sàng khi đội ngũ bắt tay vào tuần mới.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Google Sheets:** Nơi lưu danh sách hàng chờ video đối thủ cần phân tích.
- **API Key WayinVideo:** Dùng để gọi API tóm tắt video YouTube.
- **Tài khoản OpenAI:** Lấy API Key để kết nối với mô hình `gpt-4o-mini`.
- **Tài khoản Airtable:** Tạo Personal Access Token (phạm vi: `data.records:write`) để lưu trữ dữ liệu phân tích.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ trang chủ n8n (Link gốc: [n8n.io/workflows/15468](https://n8n.io/workflows/15468)), sau đó chọn **Import from File** hoặc copy trực tiếp mã JSON dán vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công, các sếp cần cấu hình chính xác các thông số quan trọng sau trong 12 nodes của workflow:

- **1. Schedule — Every Monday 8AM:** Giữ nguyên lịch chạy định kỳ hoặc tuỳ chỉnh lại múi giờ và thời gian nếu muốn.
- **2. Google Sheets — Read Pending Videos & 12. Google Sheets — Mark as Processed:** Kết nối tài khoản Google Sheets (OAuth2), thay thế `YOUR_COMPETITOR_SHEET_ID` bằng ID Google Sheet thực tế.
  - *Cấu trúc Google Sheet:* Tạo sheet tên `Competitor Monitor` với tab `Video Queue` gồm các cột: `Video URL`, `Video Title`, `Competitor Name`, `Your Product / Brand`, `Status`, `Processed Date`.
- **3. WayinVideo — Submit Summarization & 5. WayinVideo — Get Summary Results:** Điền API Key của WayinVideo vào phần Header Authentication (`YOUR_WAYINVIDEO_API_KEY`).
- **9. OpenAI — GPT-4o-mini Model:** Kết nối OpenAI Credential và đảm bảo model được chọn là `gpt-4o-mini`.
- **11. HTTP — Save to Airtable:** Thay thế `YOUR_AIRTABLE_API_KEY`, `YOUR_AIRTABLE_BASE_ID`, và `YOUR_AIRTABLE_TABLE_NAME`.
  - *Cấu trúc Airtable:* Tạo bảng tên `Competitor Intelligence` với các trường: `Week (Date)`, `Competitor Name`, `Video Title`, `Video URL`, `Content Type`, `Messaging Angle`, `Key Claims Made`, `Target Audience Signals`, `Pricing / Offer Signals`, `Strengths Identified`, `Weaknesses / Gaps`, `Opportunity for Us`, `Urgency Score (Number)`, `Tags`, `Summary`, `Status` (mặc định: `New`).

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để test thủ công một bản ghi mẫu từ Google Sheets xem dữ liệu có chạy suôn sẻ sang Airtable hay không.
- Nếu mọi thứ xanh mướt (success), các sếp bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy mỗi tuần.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Slack hoặc Telegram ngay sau node lưu Airtable để bắn thông báo tóm tắt chiến lược nóng hổi trực tiếp lên group chat của team Product/Marketing.
- **Mở rộng nguồn dữ liệu:** Thay vì chỉ đọc Google Sheet, các sếp có thể kết nối thêm webhook từ RSS Feed hoặc Twitter/X để theo dõi đa kênh đối thủ.
- **Tự động hóa log lỗi:** Thêm nhánh xử lý lỗi (Error Trigger) để cảnh báo về Telegram nếu quá trình gọi API WayinVideo hoặc OpenAI gặp sự cố.

### 📌 Kết luận
Việc tự động hóa quy trình nghiên cứu đối thủ cạnh tranh chưa bao giờ dễ dàng đến thế với sức mạnh kết hợp giữa n8n, WayinVideo và AI. Hãy cài đặt ngay workflow này để tối ưu hóa thời gian và giúp đội ngũ của các sếp luôn đi trước đối thủ một bước!