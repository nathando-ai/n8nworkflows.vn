---
title: "🚀 Tự động Tìm kiếm, Quản lý & Phân tích Podcast với Listen API cho AI Agents"
description: "Giải pháp không-code giúp các sếp nhanh chóng tìm, lưu trữ, phân tích và khai thác podcast bằng Listen API – tiết kiệm thời gian, tăng độ chính xác và hỗ trợ AI RAG."
slug: "tu-dong-tim-kiem-qua-ly-phan-tich-podcast-listen-api"
tags: [n8n, automation, no-code, podcast, AI, market-research]
keywords: [n8n workflow, tự động hóa, podcast, Listen API, AI RAG, market research]
---

# 🚀 Tự động Tìm kiếm, Quản lý & Phân tích Podcast với Listen API cho AI Agents

Bạn đang phải **làm việc thủ công** để tìm kiếm podcast, thu thập metadata, rồi mới mới đưa vào hệ thống AI để trả lời câu hỏi?  
Mỗi lần phải mở trình duyệt, copy‑paste, kiểm tra genre, rồi lại nhập lại vào công cụ RAG – **tốn hàng giờ và dễ sai sót**.  

Workflow này sẽ **tự động hoá 100%** quy trình từ tìm kiếm, lấy chi tiết, lưu trữ, tới phân tích dữ liệu podcast bằng **Listen API** – tất cả trong n8n, không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động lấy hàng trăm podcast trong vài giây.  
- **Độ chính xác cao**: Dữ liệu được lấy trực tiếp từ Listen API, không còn lỗi copy‑paste.  
- **Cá nhân hoá nội dung**: Lưu trữ podcast theo genre, ngôn ngữ, khu vực – dễ dàng tạo bộ dữ liệu cho AI.  
- **Hoạt động liên tục**: Workflow chạy 24/7, luôn cập nhật podcast mới và xu hướng tìm kiếm.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Listen API** và **API Key** (được cấp khi đăng ký trên https://listen-api.com).  
- **n8n** (cài đặt trên VPS hoặc Docker).  
- (Tùy chọn) **Cơ sở dữ liệu** (PostgreSQL, MySQL, hoặc Google Sheets) nếu muốn lưu trữ podcast lâu dài.  
- Kết nối internet ổn định để gọi API.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Đăng nhập vào n8n Dashboard.  
2. Click **"Import"** → **"Upload JSON"** và chọn file JSON của workflow (hoặc copy/paste nội dung JSON).  
3. Nhấn **"Import"**, workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là **các node quan trọng** và cách cấu hình chúng:

| Node | Loại | Cấu hình cần chỉnh |
|------|------|-------------------|
| **Listen API: Podcast Search, Directory, and Insights MCP Server** | `mcpTrigger` | Chọn **Credentials → Listen API** và nhập **API Key**. Đặt **Trigger** thành **HTTP** nếu muốn gọi qua webhook, hoặc **Cron** để chạy định kỳ. |
| **Fetch Best Podcasts by Genre** | `httpRequestTool` | URL: `https://listen-api.com/v2/best_podcasts` <br> Method: **GET** <br> Query Params: `genre_id` (đặt giá trị tùy ý, ví dụ `68` cho Technology). |
| **Fetch Curated Podcast Lists** | `httpRequestTool` | URL: `https://listen-api.com/v2/curated_podcasts` <br> Method: **GET**. |
| **Fetch Curated Podcast List by ID** | `httpRequestTool` | URL: `https://listen-api.com/v2/curated_podcasts/{list_id}` <br> Thay `{list_id}` bằng ID danh sách muốn lấy. |
| **Batch Fetch Episode Metadata** | `httpRequestTool` | URL: `https://listen-api.com/v2/episodes` <br> Method: **POST** <br> Body: JSON chứa mảng `episode_ids`. |
| **Fetch Episode Details by ID** | `httpRequestTool` | URL: `https://listen-api.com/v2/episodes/{episode_id}` <br> Thay `{episode_id}` bằng ID episode. |
| **Fetch Episode Recommendations** | `httpRequestTool` | URL: `https://listen-api.com/v2/episodes/{episode_id}/recommendations`. |
| **Fetch Podcast Genres** | `httpRequestTool` | URL: `https://listen-api.com/v2/genres` (GET). |
| **Fetch Random Podcast Episode** | `httpRequestTool` | URL: `https://listen-api.com/v2/episodes/random` (GET). |
| **Fetch Supported Languages** | `httpRequestTool` | URL: `https://listen-api.com/v2/languages` (GET). |
| **Batch Fetch Podcast Metadata** | `httpRequestTool` | URL: `https://listen-api.com/v2/podcasts` (POST) – body chứa mảng `podcast_ids`. |
| **Fetch Podcast Details by ID** | `httpRequestTool` | URL: `https://listen-api.com/v2/podcasts/{podcast_id}`. |
| **Fetch Podcast Recommendations** | `httpRequestTool` | URL: `https://listen-api.com/v2/podcasts/{podcast_id}/recommendations`. |
| **Fetch Supported Regions** | `httpRequestTool` | URL: `https://listen-api.com/v2/regions` (GET). |
| **Fetch User Playlists** | `httpRequestTool` | URL: `https://listen-api.com/v2/playlists` (GET) – cần **Authorization** (Bearer token). |
| **Fetch Playlist Details by ID** | `httpRequestTool` | URL: `https://listen-api.com/v2/playlists/{playlist_id}`. |
| **Submit Podcast to Database** | `httpRequestTool` | URL: `https://your-db-endpoint.com/podcasts` (POST) – cấu hình **Credentials** tới DB hoặc webhook nội bộ. |
| **Delete Podcast by ID** | `httpRequestTool` | URL: `https://your-db-endpoint.com/podcasts/{podcast_id}` (DELETE). |
| **Fetch Podcast Audience Data** | `httpRequestTool` | URL: `https://listen-api.com/v2/podcasts/{podcast_id}/audience`. |
| **Fetch Related Search Terms** | `httpRequestTool` | URL: `https://listen-api.com/v2/search/related` – query `term`. |
| **Full-Text Search** | `httpRequestTool` | URL: `https://listen-api.com/v2/search/fulltext` – query `q`. |
| **Spell Check Search Term** | `httpRequestTool` | URL: `https://listen-api.com/v2/search/spellcheck` – query `term`. |
| **Fetch Trending Search Terms** | `httpRequestTool` | URL: `https://listen-api.com/v2/search/trending` (GET). |
| **Typeahead Search** | `httpRequestTool` | URL: `https://listen-api.com/v2/search/typeahead` – query `prefix`. |

**Lưu ý chung**  
- Tất cả các node `httpRequestTool` cần **Credentials → HTTP Basic / Bearer** được cấu hình với **API Key** của Listen API.  
- Đối với các node ghi dữ liệu vào DB, hãy tạo **Credentials** phù hợp (PostgreSQL, MySQL, hoặc Google Sheets).  
- Kiểm tra **Response Format** (JSON) và sử dụng **Set** hoặc **Function** node để trích xuất trường cần thiết trước khi lưu.

#### 3. Kích hoạt ⚡️
1. **Test run**: Chạy từng node một với dữ liệu mẫu (ví dụ: genre_id = 68) để xác nhận API trả về dữ liệu hợp lệ.  
2. Khi mọi thứ ổn, bật **Active** ở góc phải của workflow.  
3. Nếu dùng **Cron Trigger**, thiết lập lịch (ví dụ: mỗi 6 giờ một lần) để tự động cập nhật podcast mới.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** để gửi thông báo mỗi khi có podcast mới hoặc khi xuất hiện xu hướng tìm kiếm.  
- **Lưu log chi tiết**: Dùng node **Write Binary File** hoặc **Google Sheets** để ghi lại lịch sử các request, giúp debug nhanh khi API thay đổi.  
- **Tạo báo cáo định kỳ**: Kết hợp **Google Docs** hoặc **PDF Generator** để tự động tạo báo cáo podcast hàng tuần, gửi qua email cho team.  
- **Kết nối RAG**: Sau khi thu thập metadata, dùng **LangChain** hoặc **OpenAI** node để xây dựng knowledge base, cho phép AI trả lời câu hỏi “Podcast nào phù hợp với chủ đề X?”.  

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động hoá toàn bộ vòng đời podcast** – từ tìm kiếm, lưu trữ, tới phân tích – mà không cần viết code. Hãy **import ngay**, cấu hình API Key, bật chạy và để n8n làm việc thay bạn. Khi dữ liệu đã sẵn sàng, AI Agents sẽ có nguồn thông tin phong phú, giúp nâng cao chất lượng trả lời và đưa ra quyết định nhanh hơn.  

**Áp dụng ngay hôm nay, để thời gian của các sếp được dành cho những công việc chiến lược hơn!**