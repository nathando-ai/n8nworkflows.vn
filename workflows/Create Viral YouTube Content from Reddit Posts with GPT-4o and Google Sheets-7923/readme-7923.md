---
title: "🚀 Tạo Nội Dung YouTube Viral Từ Reddit Với GPT‑4o & Google Sheets"
description: "Quy trình tự động thu thập, lọc và đánh giá các bài đăng AskReddit có tiềm năng lan truyền, sau đó ghi vào Google Sheets – chuẩn bị dữ liệu cho nội dung YouTube Shorts."
slug: "tao-noi-dung-youtube-viral-reddit-gpt4o-sheets"
tags: [n8n, automation, no-code, reddit, youtube, google-sheets, ai]
keywords: [n8n workflow, tự động hóa, AskReddit, YouTube Shorts, GPT‑4o, Google Sheets]
---

# 🚀 Tạo Nội Dung YouTube Viral Từ Reddit Với GPT‑4o & Google Sheets

Bạn đang phải mất hàng giờ để tìm kiếm, lọc và đánh giá các bài đăng AskReddit có tiềm năng trở thành viral? Bạn muốn chuyển nhanh dữ liệu này thành nội dung YouTube Shorts mà không cần viết code? Workflow này chính là “điểm hẹn” của bạn – tự động 100% từ scraping Reddit, lọc, tính điểm virality, đến ghi dữ liệu vào Google Sheets, sẵn sàng cho các bước tiếp theo như viết kịch bản, tạo video AI và đăng tải.

:::info[Hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ thủ công xuống chỉ vài phút tự động.  
- **Độ chính xác cao**: Lọc duplicate, lọc theo tiêu chí virality một cách nhất quán.  
- **Dữ liệu chuẩn**: Ghi vào Google Sheets ngay, sẵn sàng cho các bước tiếp theo (kịch bản, video, đăng tải).  
- **Không cần code**: Tất cả các thao tác được thực hiện qua giao diện n8n.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Reddit API**: Client ID, Client Secret, User Agent.  
- **OpenAI API**: API Key (để tính điểm virality).  
- **Google Sheets**: OAuth2 credentials, ID của bảng tính cần ghi dữ liệu.  
- **n8n instance**: Đã cài đặt và có quyền truy cập các node cần thiết.  
:::

## 🚀 Cách import & Lưu ý khi “lên đồ”

### 1. Import Workflow 📥

1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/7923).  
2. Trong n8n Editor, chọn **Import** → **Upload JSON** → chọn file vừa tải.  
3. Nhấn **Import** để hoàn tất.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Mô tả | Tham số cần cấu hình | Credentials |
|------|-------|----------------------|-------------|
| **When clicking ‘Test workflow’** | Trigger thủ công | Không cần tham số | - |
| **Get AskReddit Posts** | Gọi Reddit API lấy bài đăng | `URL: https://www.reddit.com/r/AskReddit/top.json?limit=100`<br>`Auth: OAuth2 (Reddit)` | Reddit API |
| **Filter AskReddit Data** | Code node để chọn trường cần giữ (title, url, upvotes, comments) | `return items.map(i => ({ json: { title: i.json.data.children[0].data.title, ... } }))` | - |
| **Filter for Virality Potential** | Code node lọc bài có upvotes > 5000, comments > 200 | `return items.filter(i => i.json.upvotes > 5000 && i.json.comments > 200)` | - |
| **Merge** | Kết hợp dữ liệu từ các nguồn (nếu có) | - | - |
| **Filter Duplicates** | Code node loại bỏ duplicate theo tiêu đề | `const seen = new Set(); return items.filter(i => !seen.has(i.json.title) && !seen.add(i.json.title));` | - |
| **Add Numbering** | Code node thêm chỉ số thứ tự | `return items.map((i, idx) => ({ json: { ...i.json, index: idx + 1 } }))` | - |
| **Merge1** | Kết hợp lại dữ liệu đã được đánh số | - | - |
| **GIVE VIRALITY SCORE** | Node OpenAI (LLM) tính điểm virality | Prompt: “Đánh giá mức độ viral của bài đăng: {{title}} – upvotes: {{upvotes}} – comments: {{comments}}. Trả về điểm từ 0-100.” | OpenAI API |
| **Add Virality Score** | Code node thêm điểm vào dữ liệu | `return items.map(i => ({ json: { ...i.json, viralityScore: i.json.viralityScore } }))` | - |
| **Filter by Score** | Code node lọc bài có điểm >= 70 | `return items.filter(i => i.json.viralityScore >= 70)` | - |
| **Write confession DETAILS** | Google Sheets – Append rows | `Sheet ID: <ID>`, `Range: Sheet1!A:D` (hoặc tùy chỉnh) | Google Sheets OAuth2 |
| **Get row(s) in sheet** | Google Sheets – Read rows (để kiểm tra) | `Sheet ID: <ID>`, `Range: Sheet1!A:D` | Google Sheets OAuth2 |

> **Lưu ý**:  
> - Đảm bảo các credentials đã được cấu hình trong **Credentials** của n8n.  
> - Kiểm tra **URL** và **Parameters** của node `Get AskReddit Posts` để tránh lỗi 429 (điều kiện rate‑limit).  
> - Trong node `GIVE VIRALITY SCORE`, chọn mô hình GPT‑4o (hoặc GPT‑4) và điều chỉnh `Temperature` thành 0.7 để có kết quả đa dạng.  

### 3. Kích hoạt ⚡️

1. **Test run**: Nhấn nút **Execute Workflow** trên n8n Editor, xem kết quả trong tab **Execution**.  
2. Kiểm tra Google Sheet: dữ liệu đã được ghi vào đúng sheet chưa?  
3. Khi mọi thứ ổn, bật **Active** cho workflow.  
4. Nếu muốn tự động chạy, thêm node **Cron** hoặc **Webhook** tùy nhu cầu.

## ✍️ Mẹo & gợi ý nâng cao

- **Thông báo Slack**: Thêm node Slack → “Send Message” sau khi ghi dữ liệu thành công.  
- **Lưu log vào Google Docs**: Dùng node Google Docs để ghi lại lịch sử chạy.  
- **Export CSV**: Thêm node “Write Binary Data” → “Write to File” để lưu bản sao CSV.  
- **Tích hợp với AI Video**: Gửi dữ liệu tới workflow khác (ví dụ “Generate YouTube Shorts”) để tự động tạo video.  
- **Cấu hình Cron**: Chạy workflow hàng ngày lúc 02:00 để luôn cập nhật nội dung mới nhất.  

## 📌 Kết luận

Workflow “Create Viral YouTube Content from Reddit Posts with GPT‑4o and Google Sheets” giúp các sếp tiết kiệm thời gian, giảm sai sót và chuẩn bị dữ liệu chất lượng cao cho nội dung YouTube Shorts. Hãy thử ngay, điều chỉnh các tham số phù hợp với niche của mình, và mở rộng thêm các bước tiếp theo để hoàn thiện quy trình tự động từ A → Z. 🚀