---
title: "🚀 Tự động tạo và gửi khảo sát sau cuộc họp từ ghi chú Google Meet với OpenAI và Weavely"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình tạo khảo sát sau họp bằng AI dựa trên ghi chú Gemini, phê duyệt qua Slack và gửi email cho người tham gia."
slug: "tu-dong-tao-khao-sat-sau-cuop-hop-google-meet-openai-weavely"
tags: [n8n, automation, ai-summarization, google-meet, openai, slack, weavely]
keywords: [n8n workflow, tự động hóa cuộc họp, google meet notes, openai ai agent, weavely mcp, khảo sát tự động]
---

# 🚀 Tự động tạo và gửi khảo sát sau cuộc họp từ Google Meet với AI & Weavely

Việc thủ công viết câu hỏi khảo sát, thiết kế form và gửi cho người tham gia sau mỗi cuộc họp dài dòng tốn rất nhiều thời gian của các sếp. Thường thì chúng ta dễ bị quên hoặc làm qua loa, dẫn đến chất lượng feedback thu về không cao.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa 100%: Lắng nghe sự kiện kết thúc họp, lấy ghi chú từ Gemini, dùng OpenAI AI Agent để phân tích và tạo 5-7 câu hỏi khảo sát phù hợp với nội dung thảo luận, tự động tạo form qua Weavely MCP, gửi yêu cầu duyệt qua Slack và tự động gửi email cho toàn bộ người tham gia khi được phê duyệt!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian thủ công**: Không cần tự soạn câu hỏi hay tạo form thủ công sau mỗi cuộc họp.
- **Khảo sát cá nhân hóa cực cao**: AI đọc trực tiếp ghi chú cuộc họp (Gemini notes) để tạo ra các câu hỏi bám sát thực tế nội dung đã thảo luận.
- **Kiểm soát chặt chẽ**: Gửi yêu cầu duyệt qua Slack DM trước khi form được gửi chính thức đến người tham gia.
- **Vận hành liền mạch 24/7**: Tự động hóa hoàn toàn từ lúc kết thúc cuộc họp đến khi gửi email khảo sát.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Google Workspace Business Standard hoặc cao hơn (để Gemini tự động tạo ghi chú cuộc họp).
- Tài khoản OpenAI (với API Key).
- Tài khoản Weavely (miễn phí tại [weavely.ai](https://weavely.ai)).
- Slack Workspace (để nhận thông báo và phê duyệt).
- Tài khoản Google Calendar, Google Docs và Gmail.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow này và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình các thành phần quan trọng sau:

- **Node ⚙️ Configuration**: Cập nhật 2 giá trị quan trọng trước khi kích hoạt:
  - `calendarId`: Địa chỉ email Google Calendar của các sếp.
  - `slackUserId`: Member ID trên Slack của người quản lý (Vào Slack profile -> chọn `···` -> *Copy member ID*).
- **Credentials**: Kết nối đầy đủ tài khoản cho các node:
  - **Google Calendar Trigger** & **Get an event**: Kết nối `googleCalendarOAuth2Api`.
  - **Get a document**: Kết nối `googleDocsOAuth2Api`.
  - **OpenAI Chat Model**: Nhập OpenAi API Key.
  - **Send message and wait for response (Slack)**: Kết nối `slackOAuth2Api`.
  - **Send a message (Gmail)**: Kết nối `gmailOAuth2`.
- **Cấu hình Slack Interactivity**: Tại node Slack, nhớ bật tính năng Interactivity trong Slack App settings và trỏ Request URL về webhook-waiting URL của n8n, nếu không các nút bấm Approve/Reject sẽ mở trên trình duyệt thay vì tương tác trực tiếp trong Slack.
- **Model LLM**: Node **OpenAI Chat Model** mặc định dùng `gpt-4.1-mini`. Các sếp có thể đổi thành `gpt-4o` nếu muốn chất lượng câu hỏi khảo sát sâu sắc hơn.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test run) với một sự kiện cuộc họp mẫu có sẵn ghi chú từ Gemini.
- Bật công tắc **Active** để workflow chính thức tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Thay thế Google Calendar**: Có thể đổi nguồn trigger sang Calendly hoặc công cụ đặt lịch khác nếu các sếp không dùng Google Meet.
- **Kênh thông báo linh hoạt**: Thay thế hoặc bổ sung node gửi thông báo qua Telegram hoặc Microsoft Teams thay vì chỉ dùng Slack/Gmail.
- **Lưu trữ dữ liệu**: Thêm node Google Sheets hoặc Airtable ngay sau bước hoàn thành khảo sát để lưu log lịch sử các form đã tạo.

### 📌 Kết luận
Workflow này là một "vũ khí" tối tân giúp tự động hóa khâu thu thập feedback sau họp, vừa chuyên nghiệp vừa tiết kiệm thời gian tuyệt đối. Hãy cài đặt ngay để tối ưu hóa đội ngũ của các sếp!