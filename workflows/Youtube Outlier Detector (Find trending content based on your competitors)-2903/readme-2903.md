---
title: "🚀 Phát hiện Video Xu hướng trên YouTube từ Đối thủ - Youtube Outlier Detector"
description: "Tự động thu thập, lọc và lưu các video YouTube đang gây bão của đối thủ vào PostgreSQL, giúp các sếp nhanh chóng nắm bắt xu hướng nội dung."
slug: "phat-hien-video-xu-huong-youtube-doi-thu"
tags: [n8n, automation, no-code, youtube, postgres, ai]
keywords: [n8n workflow, tự động hóa, youtube analytics, phát hiện xu hướng, database postgres]
---

# 🚀 Phát hiện Video Xu hướng trên YouTube từ Đối thủ

Bạn có bao giờ phải **làm thủ công** để dò tìm video đang “bùng nổ” của các kênh đối thủ?  
- Dò qua hàng trăm video, lọc Shorts, sao chép link…  
- Ghi lại trong bảng tính, cập nhật liên tục, luôn lo lắng dữ liệu bị trùng hoặc lỗi.  

**Youtube Outlier Detector** là workflow n8n giải quyết 100 % công việc này **không cần viết một dòng code nào**. Nó tự động:

1. Lấy danh sách video mới nhất của các kênh đối thủ (2 tuần gần nhất).  
2. Loại bỏ Shorts và các video không đạt tiêu chí.  
3. Lưu trữ chi tiết video (title, view, like, comment, publish date…) vào PostgreSQL.  
4. Tự động tạo bảng nếu chưa có, đồng thời cho phép xem nhanh dữ liệu qua query.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: không còn phải mở từng kênh, sao chép link, nhập dữ liệu.  
- **Độ chính xác cao**: lọc Shorts, loại trừ video trùng lặp, chỉ lưu những video thực sự “outlier”.  
- **Cập nhật liên tục**: workflow có thể chạy hàng ngày/giờ, dữ liệu luôn mới nhất.  
- **Dễ dàng phân tích**: dữ liệu trong PostgreSQL cho phép dùng BI tools (Metabase, Superset…) để tạo báo cáo.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản YouTube** với **OAuth2 API** (đăng ký tại Google Cloud Console, bật YouTube Data API v3).  
- **PostgreSQL** server (có quyền `CREATE TABLE`, `INSERT`, `SELECT`).  
- **n8n** (cài trên VPS hoặc Docker).  
- **API Key** cho các request HTTP phụ trợ (nếu workflow dùng `httpRequest` để lấy dữ liệu phụ).  
- **Credentials** trong n8n:  
  - `youTubeOAuth2Api` → kết nối YouTube.  
  - `postgres` → thông tin kết nối DB (host, port, database, user, password).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập link gốc: <https://n8n.io/workflows/2903>.  
2. Nhấn **“Export JSON”** → tải file `youtube-outlier-detector.json`.  
3. Mở n8n → **Workflows → Import** → kéo thả file JSON hoặc dán nội dung.  
4. Đặt tên cho workflow (mặc định là *Youtube Outlier Detector*).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là **điểm danh các node** và **hướng dẫn cấu hình chi tiết**:

| Node | Loại | Mô tả & Cấu hình cần chỉnh |
|------|------|-----------------------------|
| **When clicking ‘Test workflow’** | `manualTrigger` | Dùng để khởi chạy thử. Không cần cấu hình. |
| **Execute Workflow Trigger** | `executeWorkflowTrigger` | Nếu bạn muốn gọi workflow phụ (ví dụ: gửi báo cáo Slack). Đặt **Workflow ID** của workflow mục tiêu. |
| **fetch_last_registered** | `postgres` (executeQuery) | Query để lấy `video_id` cuối cùng đã lưu. <br>**SQL mẫu:** <br>`SELECT video_id FROM youtube_videos ORDER BY published_at DESC LIMIT 1;` |
| **get_videos** | `youTube` (resource: video) | - **Operation**: `Search` hoặc `List`. <br>- **Channel IDs**: nhập danh sách kênh đối thủ (có thể dùng biến môi trường). <br>- **Published After**: `{{ $now.subtract(14, "days").toISOString() }}` (2 tuần). |
| **if_is_empty** | `if` | Kiểm tra `{{ $json["items"].length === 0 }}` → nếu không có video mới, workflow sẽ dừng. |
| **Loop Over Items** | `splitInBatches` | Đặt **Batch Size** (ví dụ 10) để xử lý video theo nhóm, tránh limit API. |
| **find_video_data1** | `httpRequest` | Gọi API phụ (ví dụ: lấy thống kê chi tiết). <br>**URL**: `https://www.googleapis.com/youtube/v3/videos` <br>**Query Params**: `part=statistics,contentDetails&id={{ $json["id"] }}&key={{ $credentials["youTubeOAuth2Api"].apiKey }}` |
| **remove_shorts** | `code` | JavaScript lọc video có `duration` < 60s (Shorts). <br>```js\nreturn items.filter(item => parseInt(item.contentDetails.duration.replace('PT','').replace('S','')) > 60);\n``` |
| **create_query** | `code` | Tạo câu lệnh INSERT cho PostgreSQL. <br>```js\nreturn items.map(item => ({\n  query: `INSERT INTO youtube_videos (video_id, title, views, likes, comments, published_at) VALUES ('${item.id}', '${item.snippet.title.replace(/'/g, \"''\")}', ${item.statistics.viewCount}, ${item.statistics.likeCount}, ${item.statistics.commentCount}, '${item.snippet.publishedAt}') ON CONFLICT (video_id) DO NOTHING;`\n}));\n``` |
| **structure_data** | `code` | Định dạng lại dữ liệu thành object phù hợp với bảng. |
| **if_empty** | `if` | Kiểm tra bảng DB có tồn tại chưa. Nếu chưa, chạy **create_table**. |
| **create_table** | `postgres` (executeQuery) | SQL tạo bảng (run 1 lần): <br>`CREATE TABLE IF NOT EXISTS youtube_videos ( video_id TEXT PRIMARY KEY, title TEXT, views BIGINT, likes BIGINT, comments BIGINT, published_at TIMESTAMP );` |
| **already_populated** | `set` | Đánh dấu flag `alreadyPopulated = true` khi bảng đã có dữ liệu. |
| **map_data** | `set` | Đặt lại key cho dữ liệu (ví dụ: `videoId`, `title`, …). |
| **sanitize_data** | `code` | Loại bỏ ký tự gây lỗi SQL (escape `'`). |
| **insert_items** | `postgres` (executeQuery) | Chạy **query** được tạo ở `create_query`. Đặt **Query** = `{{$json["query"]}}`. |
| **see table** | `postgres` (executeQuery) | Tùy chọn: `SELECT * FROM youtube_videos ORDER BY published_at DESC LIMIT 20;` để xem nhanh. |
| **drop table** | `postgres` (executeQuery) | Tùy chọn: xóa bảng khi muốn “reset” dữ liệu. <br>`DROP TABLE IF EXISTS youtube_videos;` |

> **Lưu ý quan trọng**  
> - Đảm bảo **Credentials** (`youTubeOAuth2Api`, `postgres`) đã được tạo và gán cho các node tương ứng.  
> - Kiểm tra **quota** của YouTube API; nếu chạy hàng ngày, cân nhắc giảm `Batch Size` hoặc sử dụng **API Key** thay cho OAuth nếu chỉ cần dữ liệu công khai.  
> - Khi sử dụng node `httpRequest`, bật **“Allow Unauthorized SSL”** nếu server DB của bạn dùng self‑signed cert.

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, nhấn **“Execute Workflow”** → chọn **“Run”** để kiểm tra với dữ liệu mẫu.  
2. Kiểm tra bảng PostgreSQL (`see table` node) để xác nhận dữ liệu đã được chèn.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên‑phải) để workflow tự động chạy theo lịch (có thể dùng **Cron** node nếu muốn chạy định kỳ).

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` sau `insert_items` để gửi tin “🟢 Đã lưu X video mới” tới kênh nội bộ.  
- **Lịch chạy tự động**: Dùng node `Cron` (ví dụ: mỗi ngày 02:00) để tự động kích hoạt `manualTrigger`.  
- **Dashboard BI**: Kết nối PostgreSQL với Metabase hoặc Superset, tạo biểu đồ “Top 10 video có view tăng nhanh nhất”.  
- **Phân tích sentiment**: Thêm node `OpenAI` hoặc `LLM` để phân tích mô tả video, gắn thẻ nội dung (tutorial, review, vlog…).  
- **Backup**: Thêm node `Google Drive` hoặc `S3` để xuất CSV hàng tuần từ bảng `youtube_videos`.

### 📌 Kết luận
Với **Youtube Outlier Detector**, các sếp không còn phải “đào bới” thủ công trên YouTube nữa – mọi dữ liệu xu hướng được thu thập, lọc sạch và lưu trữ tự động, sẵn sàng cho phân tích và quyết định chiến lược nội dung. Hãy **import ngay**, **cấu hình credentials**, và **bật workflow** để bắt đầu nắm bắt xu hướng video của đối thủ chỉ trong vài phút! 🚀