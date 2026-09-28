---
title: "🚀 Tự động hóa tóm tắt video YouTube mới gửi về Slack bằng n8n, Google Sheets & GPT-4o-mini"
description: "Hướng dẫn xây dựng hệ thống n8n tự động quét kênh YouTube, lấy phụ đề, tóm tắt thông minh bằng GPT-4o-mini và bắn thông báo trực tiếp lên Slack cực kỳ chuyên nghiệp."
slug: "tu-dong-hoa-tom-tat-video-youtube-slack-gpt-4o-mini"
tags: [n8n, automation, youtube, slack, openai, google-sheets]
keywords: [n8n workflow, tự động hóa youtube, tóm tắt video ai, gpt-4o-mini slack, n8n google sheets]
---

# 🚀 Tự động hóa tóm tắt video YouTube mới gửi về Slack bằng AI

Chào các sếp! Việc cập nhật liên tục các kiến thức, xu hướng hay video mới từ các kênh YouTube yêu thích trong ngành mất rất nhiều thời gian thủ công. Thay vì phải ngồi xem hết video dài cổ hoặc đọc transcript rối rắm, workflow n8n này sẽ thay các sếp làm tất cả: tự động phát hiện video mới, cào phụ đề, nhờ **GPT-4o-mini** tóm tắt súc tích và gửi thẳng vào kênh **Slack** của team, đồng thời cho phép quản lý danh sách kênh YouTube ngay trực tiếp từ Slack qua AI Agent!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian**: Không cần xem video dài, nắm bắt trọn vẹn ý chính thông qua bản tóm tắt cực kỳ chất lượng từ AI.
- **Cập nhật thời gian thực**: Tự động kiểm tra feed định kỳ mỗi 10 phút, đảm bảo không bỏ lỡ bất kỳ video hot nào.
- **Quản lý linh hoạt qua Slack**: Dễ dàng thêm hoặc xóa nguồn kênh YouTube bằng cách @mention bot trực tiếp trên Slack.
- **Loại bỏ trùng lặp**: Hệ thống tự động ghi log vào Google Sheets, không bao giờ gửi một video tới hai lần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Bản Cloud hoặc Self-hosted (phiên bản hỗ trợ LangChain/AI Agents).
- **Tài khoản Google Sheets**: Để lưu trữ danh sách RSS feed và log video đã xử lý.
- **RapidAPI Key**: Sử dụng API trích xuất phụ đề (Subtitles) từ YouTube.
- **OpenAI API Key**: Sử dụng mô hình `gpt-4o-mini` để tạo nội dung tóm tắt và xử lý câu lệnh Slack.
- **Slack Workspace**: Cài đặt Slack App để nhận tin nhắn thông báo và tương tác bot.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow hoặc import file JSON vào n8n Editor giao diện chính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các thành phần sau:

- **Google Sheets Template & Credentials**:
  - Tạo bản sao từ mẫu chuẩn tại: [Google Sheets Template](https://docs.google.com/spreadsheets/d/1i3jZ_0npsEVtrMUSzGPV3Lbta3q7sArHHeNomlAuSMg/edit?usp=sharing)
  - Kết nối node `Get RSS Links`, `Filter for New Video`, `Log New Videos`, `Get Rows`, `Delete Row`, `Append Row` với tài khoản **Google Sheets OAuth2**.
- **RapidAPI - Subtitles Endpoint**:
  - Đăng ký tài khoản tại RapidAPI với gói Subtitles (`https://yt-api.p.rapidapi.com/subtitles`, miễn phí 300 lần gọi/tháng).
  - Lưu `X-RapidAPI-Key` vào **Header Auth** credential và gán vào node `Fetch Subtitles URL` và `Get Channel ID`.
- **OpenAI API Key**:
  - Tạo API Key từ OpenAI Platform và tạo credential kiểu **OpenAI** liên kết với các node `Generate Summary` và `OpenAI Chat Model` (`gpt-4o-mini`).
- **Slack OAuth & Event Subscriptions**:
  - Tạo Slack App tại `api.slack.com/apps` với các Scope: `chat:write`, `channels:read`, `groups:read`.
  - Bật **Event Subscriptions**, trỏ URL về webhook của n8n và lắng nghe sự kiện `app_mention`.
  - Cấu hình node `Post to Slack` và `Slack Trigger` bằng **Slack OAuth2 API**.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test workflow) với một vài bản ghi thủ công để kiểm tra luồng dữ liệu từ RSS sang OpenAI và đẩy lên Slack.
- Bật công tắc **Active** để hệ thống tự động chạy ngầm theo lịch (Schedule Trigger).

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Ngoài Slack, các sếp có thể clone nhánh cuối để gửi đồng thời bản tóm tắt vào nhóm Telegram hoặc Discord.
- **Tùy biến prompt AI**: Chỉnh sửa System Prompt trong node `OpenAI Chat Model` để yêu cầu AI tóm tắt theo phong cách hài hước, chuyên gia tài chính hoặc ngắn gọn dưới 3 ý chính tùy nhu cầu doanh nghiệp.
- **Lưu trữ dữ liệu phân tích sâu**: Kết hợp thêm node Notion hoặc Airtable để lưu trữ kho tàng kiến thức từ các video đã tóm tắt phục vụ cho việc tra cứu sau này.

### 📌 Kết luận
Với workflow n8n cực kỳ thông minh này, việc nghiên cứu đối thủ hay cập nhật kiến thức từ YouTube đã trở nên hoàn toàn tự động hóa. Hãy triển khai ngay hôm nay để tối ưu hóa hiệu suất làm việc cho cả đội ngũ các sếp nhé!