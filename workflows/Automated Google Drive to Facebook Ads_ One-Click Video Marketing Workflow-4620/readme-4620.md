---
title: "🚀 Tự Động Đăng Video Từ Google Drive Lên Facebook Ads - One‑Click Video Marketing"
description: "Workflow tự động lấy tất cả video MP4 trong thư mục Google Drive, tải lên Facebook Ads và tạo Ad Creative chỉ trong một cú click, không cần viết code."
slug: "tu-dong-google-drive-to-facebook-ads"
tags: [n8n, automation, no-code, marketing, facebook-ads, google-drive]
keywords: [n8n workflow, tự động hóa, video marketing, facebook ads, google drive]
---

# 🚀 Tự Động Đăng Video Từ Google Drive Lên Facebook Ads - One‑Click Video Marketing

Bạn có bao giờ phải **làm thủ công**: mở Google Drive, tải video xuống, đăng lên Facebook Ads, rồi tạo Creative?  
Quá nhiều bước, dễ sai sót và tiêu tốn **giờ đồng** mỗi tuần.  

**Workflow này** sẽ **tự động** thực hiện toàn bộ quy trình chỉ bằng một cú click, không cần viết bất kỳ dòng code nào. Bạn chỉ cần chuẩn bị một vài thông tin đăng nhập, rồi để n8n chạy 24/7.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Từ vài phút/ video xuống chỉ còn vài giây.  
- **Độ chính xác 100 %**: Không còn lỗi “đăng sai file” hay “định dạng không hỗ trợ”.  
- **Tự động hoá liên tục**: Khi có video mới trong Drive, workflow sẽ tự động xử lý ngay.  
- **Không cần lập trình**: Tất cả được cấu hình bằng giao diện kéo‑thả của n8n.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản Google** với **Google Drive OAuth2** đã tạo credential trong n8n.  
- **Access Token** của **Facebook Graph API** (có quyền `ads_management` và `pages_read_engagement`).  
- **Facebook Ad Account ID** và **Page ID** nơi muốn đăng video.  
- Thư mục Google Drive chứa video **MP4** (cần ID của thư mục).  
- n8n phiên bản **≥0.200** (để hỗ trợ node `httpRequest` upload binary).  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Mở n8n → **Workflows** → **Import**.  
2. Chọn **Upload JSON** và tải file `automated-google-drive-to-fb-ads.json` (hoặc copy toàn bộ JSON vào ô **Paste JSON**).  
3. Nhấn **Import** → Workflow sẽ xuất hiện trên canvas.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cấu hình quan trọng | Hướng dẫn chi tiết |
|------|--------------------|--------------------|
| **Manual Trigger** | Không cần thay đổi, dùng để khởi chạy thủ công hoặc kết hợp với **Cron** nếu muốn tự động định kỳ. | - |
| **List Drive Videos** | - **Credentials**: `googleDriveOAuth2Api` <br> - **Folder ID**: ID của thư mục chứa video <br> - **Query**: `mimeType='video/mp4'` | Mở tab **Parameters** → **Folder** → nhập ID. Đặt **Query** để chỉ lấy file MP4. |
| **Download Video** | - **Operation**: `download` (đã được set) <br> - **File ID**: `{{$json["id"]}}` (lấy từ node trước) | Trong **File ID**, dùng biểu thức `{{$json["id"]}}`. |
| **Upload Video to FB** | - **Method**: `POST` <br> - **URL**: `https://graph.facebook.com/v17.0/{{adAccountId}}/advideos` <br> - **Headers**: `Authorization: Bearer <ACCESS_TOKEN>` <br> - **Body**: **Binary** → **File**: `{{$binary["data"]}}` | 1. Thêm **Header** `Authorization`. <br>2. Chọn **Body Type** → **Binary**. <br>3. Đặt **Binary Property** là `data` (được truyền từ node Download). |
| **Extract Video ID** | Node **Function** dùng JavaScript để lấy `video_id` từ response của Facebook. | ```js\nconst response = items[0].json;\nreturn [{ json: { videoId: response.id } }];\n``` (đảm bảo trả về `videoId`). |
| **Create Ad Creative** | - **Method**: `POST` <br> - **URL**: `https://graph.facebook.com/v17.0/{{adAccountId}}/adcreatives` <br> - **Headers**: `Authorization: Bearer <ACCESS_TOKEN>` <br> - **Body (JSON)**: <br>```json\n{\n  \"name\": \"{{ $json[\"name\"] }}\",\n  \"object_story_spec\": {\n    \"page_id\": \"{{pageId}}\",\n    \"video_data\": {\n      \"video_id\": \"{{ $json[\"videoId\"] }}\",\n      \"title\": \"{{ $json[\"title\"] }}\",\n      \"message\": \"{{ $json[\"description\"] }}\"\n    }\n  }\n}\n``` | Thay **adAccountId**, **pageId**, và **ACCESS_TOKEN** bằng giá trị thực. Bạn có thể truyền `name`, `title`, `description` từ một node **Set** (nếu muốn tùy chỉnh). |

> **Lưu ý:** Các biến `{{adAccountId}}`, `{{pageId}}`, `{{ACCESS_TOKEN}}` có thể được lưu trong **Credentials** hoặc **Environment Variables** để bảo mật.

### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn nút **Execute Workflow** → Kiểm tra log từng node, đặc biệt là `Upload Video to FB` và `Create Ad Creative`.  
2. Nếu mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải).  
3. Đối với tự động định kỳ, thêm node **Cron** trước `Manual Trigger` và cấu hình lịch (ví dụ: mỗi ngày 02:00).

## ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** sau `Create Ad Creative` để báo cáo ID Creative vừa tạo.  
- **Lưu log vào Google Sheets**: Dùng node **Google Sheets** để ghi lại `video name`, `video_id`, `creative_id`, và thời gian chạy.  
- **Xử lý lỗi**: Bọc các node `httpRequest` trong **Error Workflow** để gửi email cảnh báo khi API trả về lỗi (quota, token hết hạn…).  
- **Tự động làm sạch**: Thêm node **Delete File** (Google Drive) để xóa video đã upload nếu không cần giữ lại trên Drive.  

## 📌 Kết luận
Với workflow **Automated Google Drive to Facebook Ads**, các sếp có thể biến việc **đăng video quảng cáo** thành một thao tác “**one‑click**” hoàn toàn tự động, giảm thiểu sai sót và tối ưu chi phí nhân lực. Hãy **import**, **cấu hình** nhanh chóng và để n8n làm việc cho bạn 24/7!  

Nếu gặp bất kỳ khó khăn nào, đừng ngại **liên hệ Yaron Been** qua LinkedIn hoặc xem thêm các video hướng dẫn trên kênh YouTube của anh. Chúc các sếp thành công!