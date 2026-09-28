---
title: "🚀 Tự động tổng hợp và phân phối tin tức công nghệ hàng ngày lên Slack và Telegram với n8n, BrowserAct và OpenRouter"
description: "Hướng dẫn xây dựng workflow n8n tự động cào tin tức công nghệ từ The Verge và Product Hunt, sử dụng AI Agents qua OpenRouter để định dạng và gửi bản tin tóm tắt hàng ngày lên Slack và Telegram."
slug: "tu-dong-tong-hop-tin-tuc-cong-nghe-slack-telegram-n8n"
tags: [n8n, automation, no-code, ai-agent, browseract, openrouter, slack, telegram]
keywords: [n8n workflow, tự động hóa tin tức, browseract n8n, openrouter ai agent, slack automation, telegram bot n8n]
---

# 🚀 Tự động tổng hợp và phân phối tin tức công nghệ hàng ngày lên Slack và Telegram

Các sếp có đang tốn hàng giờ mỗi ngày để lướt các trang tin công nghệ như The Verge, Product Hunt hay TechCrunch để cập nhật xu hướng? Việc tổng hợp thủ công này vừa tốn thời gian, vừa dễ bỏ lỡ các thông tin quan trọng cho team. 

Giải pháp ư? Workflow n8n này sẽ tự động hóa toàn bộ quy trình: từ cào dữ liệu web (Web Scraping) thông minh bằng **BrowserAct**, xử lý và viết nội dung tối ưu riêng cho từng nền tảng nhờ **AI Agents (OpenRouter)**, cho đến việc tự động xuất bản bản tin chuyên nghiệp lên kênh **Slack** và **Telegram** mỗi ngày mà các sếp không cần phải nhấc một ngón tay!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Tự động hóa hoàn toàn việc điểm tin công nghệ mỗi sáng.
- **Cá nhân hóa nội dung thông minh:** AI tự động phân loại, tóm tắt và điều chỉnh văn phong phù hợp với đặc thù của Slack và Telegram.
- **Vượt giới hạn ký tự tự động:** Các bài viết dài được chia nhỏ mượt mà bằng node `Split Data` nhờ sự hỗ trợ phân đoạn của AI.
- **Hoạt động tự động 24/7:** Chạy đều đặn mỗi ngày theo lịch trình cố định thông qua `Daily Schedule`.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- **BrowserAct Account & API Key:** Cần thiết cho node `Extract Latest News and Products` (Sử dụng template **Automated Multi-Site Morning Brief**).
- **OpenRouter API Key:** Dành cho các node AI sử dụng model `google/gemini-2.5-pro` và `anthropic/claude-sonnet-4.5`.
- **Slack Bot Token / Credentials:** Để đẩy tin lên kênh Slack thông qua node `Publish to Slack Channel`.
- **Telegram Bot Token:** Để gửi bản tin tới nhóm/channel Telegram thông qua node `Publish to Telegram Channel`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ n8n (hoặc tải file JSON từ nguồn gốc) và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các thành phần cốt lõi sau:

- **Daily Schedule (`scheduleTrigger`):** Thiết lập khung giờ chạy bản tin hàng ngày (mặc định thường là 10:00 sáng).
- **Extract Latest News and Products (`n8n-nodes-browseract.browserAct`):** 
  - Kết nối `browserActApi` credentials.
  - Đảm bảo các sếp đã lưu template **Automated Multi-Site Morning Brief** trong tài khoản BrowserAct của mình để tool có nguồn cào dữ liệu chính xác từ The Verge và Product Hunt.
- **AI Content Generation cho Slack & Telegram (`Slack Content Generation` & `Telegram Content Generation`):**
  - Cấu hình các node AI Agent kết hợp với **Open Router** (sử dụng model mạnh như `google/gemini-2.5-pro` hoặc `anthropic/claude-sonnet-4.5`).
  - Thiết lập các node **Structured Output** để đảm bảo dữ liệu trả về đúng định dạng JSON chuẩn bị cho việc tách luồng.
- **Split & Publish Nodes (`Split Data for Slack`, `Split Data for Telegram`, `Publish to Slack Channel`, `Publish to Telegram Channel`):**
  - Kiểm tra lại ID kênh Slack và Chat ID của Telegram để bản tin gửi đến đúng địa chỉ.
  - Các node `Split Out` sẽ giúp cắt nhỏ nội dung nếu bản tin vượt quá giới hạn ký tự của nền tảng.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** để kiểm tra thủ công dữ liệu từ bước cào web đến khi bắn tin thử nghiệm lên Slack/Telegram.
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, hãy chuyển trạng thái workflow sang **Active**.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng nguồn tin:** Các sếp có thể tùy chỉnh template trên BrowserAct để cào thêm các trang báo công nghệ khác như TechCrunch, Hacker News hoặc Medium.
- **Lưu trữ lịch sử:** Thêm một node Google Sheets hoặc Notion vào cuối luồng để lưu lại toàn bộ lịch sử bản tin đã phát hành phục vụ việc tra cứu sau này.
- **Thông báo lỗi:** Kết hợp thêm nhánh Error Trigger để bắn cảnh báo về Telegram cá nhân nếu quá trình cào dữ liệu hoặc gọi API OpenRouter gặp sự cố.

### 📌 Kết luận
Với workflow n8n kết hợp sức mạnh của BrowserAct và các mô hình AI đỉnh cao từ OpenRouter, việc cập nhật tin tức công nghệ nóng hổi mỗi ngày cho team chưa bao giờ dễ dàng đến thế. Hãy cài đặt ngay hôm nay để tối ưu hóa năng suất làm việc cho đội ngũ của các sếp!