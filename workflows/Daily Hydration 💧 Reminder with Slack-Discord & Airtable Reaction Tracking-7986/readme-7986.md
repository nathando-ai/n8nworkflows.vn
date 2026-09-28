---
title: "🚀 Nhắc Uống Nước Hàng Ngày 💧 – Tự động Slack, Discord & Ghi nhận trong Airtable"
description: "Giải pháp tự động nhắc uống nước lúc 10h & 15h, gửi GIF vui nhộn, ghi nhận phản hồi ✅ từ Slack và lưu lịch sử vào Airtable – hoàn toàn không cần code."
slug: "daily-hydration-reminder"
tags: [n8n, automation, no-code, slack, discord, airtable, reminder]
keywords: [n8n workflow, tự động hóa, nhắc uống nước, Slack, Discord, Airtable]
---

# 🚀 Nhắc Uống Nước Hàng Ngày 💧 – Tự động Slack, Discord & Ghi nhận trong Airtable

Bạn đang làm việc trong môi trường năng động, luôn quên uống nước? Workflow này sẽ nhắc bạn uống nước lúc 10h và 15h mỗi ngày, gửi GIF vui nhộn tới kênh Slack và Discord, và tự động ghi lại những phản hồi ✅ của bạn trong Airtable. Tất cả đều được thực hiện 100% tự động, không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhắc tay, workflow tự động gửi nhắc.
- **Độ chính xác cao**: Đảm bảo nhắc đúng thời gian, không bỏ lỡ.
- **Tích hợp đa kênh**: Slack + Discord cùng lúc, phù hợp với đội ngũ làm việc đa nền tảng.
- **Ghi nhận lịch sử**: Tất cả phản hồi được lưu trong Airtable, dễ dàng phân tích và báo cáo.
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Slack**: Webhook URL (Incoming Webhook) – tạo trong Slack App > Incoming Webhooks.
- **Discord**: Webhook URL – tạo trong Discord Server > Integrations > Webhooks.
- **Airtable**: API Key, Base ID, Table name (ví dụ: `HydrationLog`).
- **n8n**: Đã cài đặt và chạy (đề nghị Self-hosted trên VPS).
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/7986) hoặc sao chép nội dung JSON.
2. Mở n8n Editor, chọn **Import** → **Import from file** hoặc **Import from clipboard**.
3. Lưu lại workflow với tên “Daily Hydration 💧 Reminder”.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên Node | Hướng dẫn cấu hình |
|------|----------|---------------------|
| **Schedule Trigger** | Every Day at 10 AM & 3 PM | Đặt **Time**: `10:00` và `15:00` (định dạng 24h). Đảm bảo múi giờ đúng (ví dụ: `Asia/Ho_Chi_Minh`). |
| **Set** | Pick Random GIF | Thêm trường `gifUrl` với giá trị: `{{$json["randomGif"]}}`. Trong phần **Values** nhập danh sách URL GIF, sau đó dùng expression `{{$arrayRandom($json["gifList"])}}` để chọn ngẫu nhiên. |
| **HTTP Request** | Send to Slack | **Method**: POST. **URL**: Slack Webhook URL. **Body**: JSON – `{"text":"🌊 Nhắc uống nước!","attachments":[{"image_url":"{{ $json["gifUrl"] }}"}]}`. |
| **HTTP Request** | Send to Discord | **Method**: POST. **URL**: Discord Webhook URL. **Body**: JSON – `{"content":"🌊 Nhắc uống nước!","embeds":[{"image":{"url":"{{ $json["gifUrl"] }}"}}]}`. |
| **Wait** | Wait 24 Hours | **Time**: 24h. Đặt **Type**: `Hours`. |
| **HTTP Request** | Get Slack Reactions | **Method**: GET. **URL**: `https://slack.com/api/reactions.get?channel={{$json["channel"]}}&timestamp={{$json["ts"]}}`. **Headers**: `Authorization: Bearer {{ $credentials.slack.apiToken }}`. |
| **Switch** | Filter ✅ Reactions | **Conditions**: Kiểm tra `reactions[0].name == "white_check_mark"`. Nếu đúng, chuyển sang node “Log in Airtable”. |
| **Airtable** | Log in Airtable | **Operation**: Create. **Base ID**: `{{ $credentials.airtable.baseId }}`. **Table**: `HydrationLog`. **Fields**: `Timestamp`, `User`, `Reaction`, `GIF URL`. |

> **Lưu ý**: Đối với các node HTTP Request, hãy bật **Authentication** và chọn credential tương ứng (Slack, Discord, Airtable). Nếu chưa có credential, tạo mới trong **Credentials** panel.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (đặt thời gian gần nhất) để kiểm tra các bước.
2. Kiểm tra Slack/Discord nhận được GIF và tin nhắn.
3. Kiểm tra Airtable có ghi nhận đúng dữ liệu khi có reaction ✅.
4. Khi mọi thứ ổn, bật **Active** cho workflow.

## ✍️ Mẹo & gợi ý nâng cao
- **Gửi báo cáo hàng tuần**: Thêm node `Schedule Trigger` vào cuối workflow, gửi summary tới Slack/Discord.
- **Lưu log vào Google Sheets**: Thay vì Airtable, dùng node `Google Sheets` để lưu log, dễ chia sẻ trong Google Drive.
- **Tùy chỉnh GIF**: Kết nối với API Giphy để lấy GIF ngẫu nhiên theo từ khóa “water”.
- **Thông báo qua Telegram**: Thêm node `Telegram` để gửi tin nhắn nhắc uống nước cho những người không dùng Slack/Discord.

## 📌 Kết luận
Workflow “Daily Hydration 💧 Reminder” giúp bạn và đội ngũ luôn nhớ uống nước đúng giờ, đồng thời ghi nhận phản hồi một cách tự động và minh bạch. Hãy triển khai ngay trên VPS của mình để tận hưởng lợi ích 24/7 mà không cần lo lắng về việc quên nhắc. Chúc các sếp luôn khỏe mạnh và năng suất!