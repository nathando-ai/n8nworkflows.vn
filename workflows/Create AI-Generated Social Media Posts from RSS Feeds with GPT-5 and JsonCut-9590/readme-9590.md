---
title: "🚀 Tự động tạo bài đăng Instagram từ RSS bằng GPT‑5 & JsonCut"
description: "Workflow n8n đọc nguồn RSS, dùng GPT‑5 tạo nội dung & prompt ảnh, xử lý ảnh qua JsonCut và đăng tự động lên Instagram chỉ trong vài giây."
slug: "tu-dong-tao-bai-dang-instagram-tu-rss-gpt5-jsoncut"
tags: [n8n, automation, no-code, instagram, ai, rss]
keywords: [n8n workflow, tự động hóa, AI content, Instagram posting, JsonCut]
---

# 🚀 Tự động tạo bài đăng Instagram từ RSS bằng GPT‑5 & JsonCut

Bạn đã từng phải **chép‑chép nội dung, tạo hình ảnh, chỉnh sửa và đăng lên Instagram** mỗi khi có một bài viết mới trên blog?  
Công việc này tốn hàng giờ, dễ sai sót và không đồng nhất về phong cách.  

**Workflow này** sẽ **đọc RSS Feed**, **tự động sinh nội dung và prompt ảnh bằng GPT‑5**, **cắt ghép ảnh qua JsonCut**, rồi **đăng ngay lên Instagram** – **không cần viết một dòng code nào**.  

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: 1 bài đăng chỉ mất vài giây, không còn thao tác thủ công.  
- **Độ chính xác & nhất quán**: Nội dung và hình ảnh luôn tuân theo style đã định.  
- **Tự động hoá 24/7**: Khi RSS cập nhật, bài đăng mới tự động xuất hiện trên Instagram.  
- **Mở rộng đa kênh**: Dễ dàng thêm Facebook, LinkedIn, TikTok chỉ bằng một node.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản n8n** (Self‑hosted hoặc n8n.cloud).  
- **API Key OpenAI** (có quyền truy cập GPT‑5).  
- **API Key JsonCut** (đăng ký tại https://jsoncut.com).  
- **API Key Blotato** (để upload media & tạo post Instagram).  
- **RSS Feed URL** của blog hoặc nguồn tin muốn chia sẻ.  
- **Logo / hình ảnh thương hiệu** (URL hoặc file) để chèn vào ảnh nền.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. **Tải file JSON** của workflow (được cung cấp ở cuối README) hoặc **copy toàn bộ JSON**.  
2. Vào **n8n Editor → Import → From File / Clipboard** và dán/đưa file vào.  
3. Nhấn **Import** → Workflow sẽ xuất hiện với 19 nodes.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌  
Dưới đây là **điểm cần cấu hình** cho từng node quan trọng:

| Node | Mô tả | Cấu hình cần thay đổi |
|------|------|-----------------------|
| **RSS Feed Trigger** | Đọc RSS mới | - `Feed URL`: URL RSS của bạn.<br>- `Polling Interval`: tùy chọn (mặc định 15 phút). |
| **Generate content and Image Prompt** (OpenAI) | Dùng GPT‑5 tạo nội dung bài viết + prompt ảnh | - Chọn **Credentials → openAiApi**.<br>- Prompt mẫu: “Viết mô tả ngắn gọn cho bài viết {{ $json.title }} và tạo prompt ảnh nền phù hợp”. |
| **Generate Background Image** (OpenAI – Image) | Tạo ảnh nền dựa trên prompt | - Credentials: **openAiApi**.<br>- `resource` = **image**.<br>- `prompt` = `{{ $json.message.content.image_prompt }}` (được truyền từ node trên). |
| **Download Image** (HTTP Request) | Tải ảnh nền từ URL trả về của OpenAI | - Credentials: **httpHeaderAuth** (nếu cần header Authorization).<br>- `URL` = `{{ $json.data[0].url }}`. |
| **Upload logo** (HTTP Request) | Upload logo lên JsonCut để dùng trong cắt ghép | - Credentials: **httpHeaderAuth** (JsonCut API Key).<br>- `Method` = **POST**.<br>- Body: `form-data` chứa file logo. |
| **Create JsonCut Job** (HTTP Request) | Tạo job cắt ghép ảnh (nền + logo) | - Credentials: **httpHeaderAuth**.<br>- `Method` = **POST**.<br>- Body: JSON chứa `background_image_url` và `logo_image_url`. |
| **Check JsonCut job Status** (HTTP Request) | Kiểm tra trạng thái job cho tới khi hoàn thành | - Credentials: **httpHeaderAuth**.<br>- `Method` = **GET**.<br>- URL: `{{ $json.job_id }}`.<br>- Sử dụng **If Success / If Error** để quyết định tiếp tục hoặc dừng. |
| **Download Background** (HTTP Request) | Tải ảnh đã được cắt ghép từ JsonCut | - `URL` = `{{ $json.result_image_url }}`. |
| **Merge** (Merge) | Gộp dữ liệu (text, image URL, metadata) thành một payload | - Chọn **Mode** = **Pass‑Through** hoặc **Combine** tùy nhu cầu. |
| **Upload Background** (HTTP Request) | Upload ảnh đã cắt lên Blotato (để lấy media ID) | - Credentials: **blotatoApi**.<br>- `Method` = **POST**.<br>- Body: `form-data` với file ảnh. |
| **Upload media** (Blotato) | Lưu media vào Blotato và nhận `media_id` | - Credentials: **blotatoApi**.<br>- `resource` = **media**. |
| **Create Instagram Text** (OpenAI) | Tạo caption Instagram dựa trên nội dung RSS | - Credentials: **openAiApi**.<br>- Prompt: “Viết caption ngắn gọn, hấp dẫn cho Instagram dựa trên {{ $json.title }} và {{ $json.excerpt }}”. |
| **Create Instagram post** (Blotato) | Đăng bài lên Instagram | - Credentials: **blotatoApi**.<br>- `media_id` = output của **Upload media**.<br>- `caption` = output của **Create Instagram Text**. |
| **If Success / If Error** | Kiểm tra kết quả các bước quan trọng (JsonCut, OpenAI) | - Đặt điều kiện `statusCode = 200` hoặc `error != null`. |
| **Wait** | Đợi một khoảng thời gian (ví dụ 30 giây) trước khi kiểm tra lại job JsonCut | - `Time to wait` = **30** seconds (có thể tăng nếu job chậm). |
| **Aggregate** | Gom lại các kết quả để truyền cho node cuối | - Chọn **Mode** = **Append**. |
| **Stop And Error** | Dừng workflow khi có lỗi nghiêm trọng | - Đặt thông báo lỗi chi tiết để dễ debug. |
| **Sticky Note** | Ghi chú hướng dẫn trên canvas (không cần cấu hình). | — |

> **Lưu ý:** Mọi node có trường `Credentials` **phải** được liên kết với API key tương ứng. Nếu chưa tạo credential, vào **Settings → Credentials → New Credential** và nhập key.

#### 3. Kích hoạt ⚡️
1. **Run** workflow một lần với dữ liệu mẫu (có thể tạm thời thay RSS URL bằng một feed test).  
2. Kiểm tra **Execution Log**: mọi node phải trả về `statusCode 200`.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên‑phải). Workflow sẽ tự động chạy mỗi khi RSS cập nhật.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm kênh khác**: Sao chép node **Create Instagram post** và thay `resource` thành **facebook**, **twitter**, hoặc **tiktok** (cần credential tương ứng).  
- **Lưu log vào Google Sheet**: Thêm node **Google Sheets → Append** để ghi lại `title`, `post_url`, `timestamp`.  
- **Gửi báo cáo hàng ngày**: Dùng node **Email** hoặc **Slack** để gửi danh sách các bài đã đăng.  
- **Tối ưu prompt**: Thử nghiệm các prompt GPT‑5 để tạo caption phong cách thương hiệu, hoặc thêm hashtag tự động.  
- **Cache JsonCut**: Nếu cùng một logo và nền được dùng nhiều lần, lưu `media_id` để tránh tạo job mới mỗi lần.

### 📌 Kết luận
Với workflow này, **các sếp** có thể biến bất kỳ RSS Feed nào thành **bài đăng Instagram chất lượng cao** chỉ trong vài giây, hoàn toàn không cần viết code. Hãy **import**, **cấu hình credential**, **bật Active** và để n8n làm việc cho bạn 24/7!  

---  

## 📂 File JSON của Workflow
```json
{
  "nodes": [
    { "name": "Wait", "type": "wait", "position": [0,0] },
    { "name": "If Success", "type": "if", "position": [0,0] },
    { "name": "If Error", "type": "if", "position": [0,0] },
    { "name": "Download Image", "type": "httpRequest", "credentials": ["httpHeaderAuth"], "position": [0,0] },
    { "name": "Error Stop", "type": "stopAndError", "position": [0,0] },
    { "name": "Aggregate", "type": "aggregate", "position": [0,0] },
    { "name": "Create JsonCut Job", "type": "httpRequest", "credentials": ["httpHeaderAuth"], "position": [0,0] },
    { "name": "Check JsonCut job Status", "type": "httpRequest", "credentials": ["httpHeaderAuth"], "position": [0,0] },
    { "name": "RSS Feed Trigger", "type": "rssFeedReadTrigger", "position": [0,0] },
    { "name": "Generate content and Image Prompt", "type": "openAi", "credentials": ["openAiApi"], "position": [0,0] },
    { "name": "Generate Background Image", "type": "openAi", "credentials": ["openAiApi"], "keyParameters": { "resource": "image", "prompt": "={{ $json.message.content.image_prompt }}" }, "position": [0,0] },
    { "name": "Upload logo", "type": "httpRequest", "credentials": ["httpHeaderAuth"], "position": [0,0] },
    { "name": "Download Logo", "type": "httpRequest", "position": [0,0] },
    { "name": "Download Background", "type": "httpRequest", "position": [0,0] },
    { "name": "Merge", "type": "merge", "position": [0,0] },
    { "name": "Upload Background", "type": "httpRequest", "credentials": ["httpHeaderAuth"], "position": [0,0] },
    { "name": "Upload media", "type": "@blotato/n8n-nodes-blotato.blotato", "credentials": ["blotatoApi"], "keyParameters": { "resource": "media" }, "position": [0,0] },
    { "name": "Create Instagram Text", "type": "openAi", "credentials": ["openAiApi"], "position": [0,0] },
    { "name": "Create Instagram post", "type": "@blot