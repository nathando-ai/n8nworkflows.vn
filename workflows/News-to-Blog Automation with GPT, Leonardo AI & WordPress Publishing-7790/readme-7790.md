---  
title: "🚀 Tự động hóa bài viết tin tức lên Blog với GPT, Leonardo AI & WordPress"  
description: "Tự động kéo tin tức từ Google News, tạo nội dung, hình ảnh và đăng lên WordPress chỉ trong vài phút mà không cần viết code."  
slug: "tuyendung-bai-viet-tin-tuc-len-blog-gpt-leonardo-wordpress"  
tags: [n8n, automation, no-code, content-creation, ai, wordpress, rss, leonardo-ai]  
keywords: [n8n workflow, tự động hóa, GPT, Leonardo AI, WordPress, nội dung, tin tức, blog]  
---  

# 🚀 Tự động hóa bài viết tin tức lên Blog với GPT, Leonardo AI & WordPress  

Bạn đang phải mất hàng giờ để thu thập tin tức, viết bài, tạo hình ảnh và đăng lên blog?  
Workflow này sẽ giúp bạn **đẩy nhanh quy trình**:  
- **Kéo dữ liệu** từ Google News RSS và GDELT Docs API.  
- **Lọc, phân loại** và **đánh dấu** những tiêu đề hot nhất.  
- **Tạo nội dung** bằng GPT, điều chỉnh tone, định dạng và kiểm tra độ dài.  
- **Sinh hình ảnh** tiêu đề bằng Leonardo AI, tải lên WordPress và gắn ALT.  
- **Đăng bài** lên WordPress một cách tự động, 100% không cần code.  

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 <https://tino.vn/vps-n8n?affid=388> (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 <https://my.bnix.one/aff.php?aff=172> (VPS Xeon 4GB chỉ 50k/tháng)  
:::

## 🎯 Kết quả các sếp nhận được  

:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: từ 8 giờ → 30 phút mỗi bài.  
- **Chính xác & nhất quán**: nội dung, tone, hình ảnh đều được kiểm soát bởi AI.  
- **Tự động 24/7**: chạy theo lịch hàng ngày, không cần can thiệp.  
- **Tăng traffic**: bài viết chất lượng, hình ảnh hấp dẫn, SEO-friendly.  
:::

## 🔧 Yêu cầu cần thiết  

:::info[CHUẨN BỊ]  
| Dịch vụ / API | Credential cần thiết | Mô tả |
|---|---|---|
| **OpenAI** | `openAiApi` | GPT cho nghiên cứu, tone, mở rộng draft. |
| **WordPress** | `oAuth2Api`, `httpBasicAuth` | Đăng bài, tải ảnh, thêm ALT. |
| **Leonardo AI** | `httpBearerAuth` | Tạo và lấy hình ảnh. |
| **Google News RSS** | Không cần credential | Feed URL: `https://news.google.com/rss`. |
| **GDELT Docs API** | `httpRequest` | Lấy dữ liệu bổ sung (tùy chọn). |
| **n8n** | - | Đảm bảo phiên bản mới nhất. |
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥  
1. Tải file JSON của workflow từ <https://n8n.io/workflows/7790>.  
2. Trong n8n Editor, chọn **Import** → **Upload** → chọn file JSON.  
3. Hoặc copy toàn bộ JSON và dán vào tab **Raw** → **Import**.  

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌  

| Node | Tên node | Cấu hình cần chỉnh | Ghi chú |
|---|---|---|---|
| `Schedule Trigger` | `Schedule Trigger` | Lịch chạy (ví dụ: 00:00 mỗi ngày) | Đảm bảo múi giờ đúng. |
| `Google News RSS` | `Google News RSS` | URL feed (đã mặc định) | Kiểm tra độ tin cậy. |
| `GDELT Docs API` | `GDELT Docs API` | URL, headers, params | Nếu không dùng, bỏ node. |
| `Merge News` | `Merge News` | Định dạng dữ liệu | Đảm bảo dữ liệu từ RSS & GDELT hợp nhất. |
| `Within dedupe` | `Within dedupe` | Logic dedupe | Thay đổi nếu cần. |
| `Top Headlines` | `Top Headlines` | Số lượng tiêu đề | Thay đổi số lượng. |
| `Classify Headlines` | `Classify Headlines` | Prompt GPT | Tùy chỉnh thể loại. |
| `Build GPT body` | `Build GPT body` | Prompt GPT | Tùy chỉnh nội dung. |
| `Tone & Format Revision – GPT` | `Tone & Format Revision – GPT` | Prompt GPT | Định dạng, tone. |
|