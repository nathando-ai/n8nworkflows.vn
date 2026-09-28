---
title: "🚀 Tạo Kịch Bản Meta Ads Chuyển Đổi Cao Với GPT & Gemini Dựa Trên Dữ Liệu Hiệu Suất"
description: "Tự động tạo kịch bản quảng cáo Meta chuẩn conversion bằng AI, tích hợp Notion, Telegram và OpenAI chỉ trong vài giây."
slug: "tao-kich-ban-meta-ad-gan-chi-voi-gpt-gemini"
tags: [n8n, automation, no-code, AI, marketing, productivity]
keywords: [n8n workflow, tự động hóa, meta ads, GPT, Gemini, script generation]
---

# 🚀 Tạo Kịch Bản Meta Ads Chuyển Đổi Cao Với GPT & Gemini Dựa Trên Dữ Liệu Hiệu Suất

Bạn đã từng tốn hàng giờ đồng hồ để viết **kịch bản quảng cáo Meta** (Facebook/Instagram) sao cho thật “đỉnh” và **đạt tỷ lệ chuyển đổi cao**?  
Quá trình này thường bao gồm:

* Thu thập dữ liệu hiệu suất (CTR, CPC, ROAS…)  
* Phân tích, rút ra insight  
* Viết tiêu đề, mô tả, lời kêu gọi hành động (CTA) sao cho phù hợp với từng audience  

Nếu làm thủ công, bạn sẽ gặp:

* **Mệt mỏi** vì lặp đi lặp lại cùng một mẫu câu.  
* **Sai sót** khi sao chép dữ liệu, dẫn tới quảng cáo không tối ưu.  
* **Mất thời gian** quý báu có thể dùng để tối ưu chiến dịch khác.  

💡 **Giải pháp:** Workflow n8n này tự động **thu thập dữ liệu hiệu suất**, **đưa vào GPT & Gemini** để tạo dàn ý và kịch bản quảng cáo, rồi **lưu vào Notion** và **gửi qua Telegram** để bạn và team nhanh chóng duyệt và triển khai. Hoàn toàn **không cần viết code** – chỉ cần cấu hình vài trường.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm 70‑80% thời gian** so với viết thủ công.  
- **Độ chính xác cao** nhờ AI phân tích dữ liệu thực tế, giảm lỗi copy‑paste.  
- **Cá nhân hoá từng ad set** dựa trên performance data, tăng ROAS.  
- **Hoạt động liên tục 24/7**, luôn sẵn sàng tạo script mới khi có dữ liệu mới.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản OpenAI** (API Key) – dùng cho các node `OpenAI`, `Transcribe Audio`, `Generate Script Outline`.  
- **Tài khoản Notion** + **Integration Token** và ID của database nơi lưu script.  
- **Bot Telegram** (Bot Token) và **Chat ID** để nhận thông báo.  
- **(Tùy chọn) Microsoft Outlook** credentials nếu muốn gửi email báo cáo.  
- **n8n** đã cài đặt (đề nghị chạy trên VPS như trên).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở **n8n Editor**.  
2. Click **Import** → **Upload JSON** và chọn file workflow (hoặc copy toàn bộ JSON vào ô).  
3. Nhấn **Import**, workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌  
Dưới đây là **các node quan trọng** và cách cấu hình chúng:

| Node | Loại | Mô tả ngắn | Cấu hình cần thay đổi |
|------|------|------------|-----------------------|
| **Manual Trigger** | manualTrigger | Bắt đầu workflow thủ công (hoặc dùng webhook). | Không cần thay đổi, chỉ dùng để test. |
| **Telegram Trigger** | telegramTrigger | Nhận lệnh từ Telegram (ví dụ: “/run”). | Chọn **Telegram Credentials** (Bot Token). |
| **Transcribe Audio** | openAi | Chuyển đổi file audio (nếu có) thành text. | Điền **OpenAI API Key**, chọn **Model** (whisper‑1). |
| **Generate Script Outline** | openAi | Dùng GPT/Gemini tạo dàn ý kịch bản dựa trên performance data. | - **Prompt**: chèn biến dữ liệu (CTR, CPC…) <br> - **Model**: `gpt‑4o` hoặc `gemini‑1.5‑flash` <br> - **API Key**: OpenAI. |
| **Code** | code | Xử lý dữ liệu (định dạng JSON, tính toán KPI). | Thêm đoạn JavaScript để chuẩn hoá dữ liệu, ví dụ: `items.map(i => ({...}))`. |
| **Filter** | filter | Lọc các ad set có ROAS > ngưỡng. | Đặt **Condition**: `{{$json["roas"]}} > 2`. |
| **Aggregate** | aggregate | Tổng hợp các insight quan trọng (top 3 ad). | Chọn **Operation**: `Group By` → `adSetId`, **Aggregation**: `max` cho `roas`. |
| **Save to Notion** | notion | Lưu dàn ý và script vào database Notion. | - **Credentials**: Notion Integration Token <br> - **Database ID**: ID của database mục tiêu. |
| **Save to Notion1** | notion | Lưu bản sao (phiên bản đã duyệt) vào Notion. | Tương tự node trên, nhưng **Page Title** có suffix “_Approved”. |
| **Telegram** | telegram | Gửi script qua Telegram cho team. | - **Credentials**: Bot Token <br> - **Chat ID**: ID nhóm/kênh. <br> - **Message**: `{{ $json["script"] }}`. |
| **Microsoft Outlook** (nếu có) | microsoftOutlook | Gửi email báo cáo. | Cấu hình **OAuth2** hoặc **SMTP** credentials. |

> **Lưu ý:**  
> - Đảm bảo **định dạng dữ liệu** từ `Code` node khớp với yêu cầu của node `Notion` (đối tượng JSON với các trường `title`, `content`).  
> - Kiểm tra **quota** API của OpenAI để tránh bị giới hạn khi chạy nhiều lần.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn nút **Execute Workflow** trên node `Manual Trigger` và kiểm tra log từng node.  
2. Nếu mọi thứ ổn, bật **Active** (toggle ở góc phải).  
3. Đặt **Cron** hoặc **Webhook** nếu muốn tự động chạy khi có dữ liệu mới.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack**: Thêm node Slack để đồng thời gửi script tới kênh marketing.  
- **Lưu log vào Google Sheets**: Dùng node Google Sheets để lưu lịch sử các script đã tạo, tiện theo dõi hiệu suất.  
- **Báo cáo định kỳ**: Dùng node **Schedule** + **Email** để gửi bản tổng hợp các script đã duyệt mỗi tuần.  
- **Tối ưu Prompt**: Thử nghiệm các prompt khác nhau (ví dụ: “Viết tiêu đề ngắn gọn, 30 ký tự”) để đạt style phù hợp với brand.

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động hoá toàn bộ quy trình tạo kịch bản Meta Ads** chỉ trong vài giây, giảm thiểu sai sót và tập trung vào việc **tối ưu chiến dịch**. Hãy **import ngay**, cấu hình các credentials cần thiết và để AI làm việc cho bạn! 🚀