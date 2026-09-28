---
title: "🚀 Tự động săn việc làm trên Meta Threads với Apify, AI và Telegram"
description: "Hướng dẫn cài đặt workflow n8n tự động quét bài đăng tuyển dụng trên Threads, lọc rác bằng AI Agent, lưu vào Google Sheets và cảnh báo qua Telegram."
slug: "san-viec-lam-threads-apify-ai-telegram"
tags: [n8n, automation, no-code, apify, openai, telegram, google-sheets]
keywords: [n8n workflow, tu dong hoa threads, apify threads scraper, ai filter hiring posts, san viec lam n8n]
---

# 🚀 Tự động săn việc làm trên Meta Threads với Apify, AI và Telegram

Các sếp đang làm freelance, agency hay tìm việc chắc chắn hiểu cảm giác mệt mỏi khi phải lướt mạng xã hội hàng giờ để tìm kiếm cơ hội tuyển dụng, chưa kể đến việc bị ngập lụt bởi các bài đăng quảng cáo dịch vụ ("hire me") thay vì thực sự tuyển người ("we are hiring"). 

Workflow n8n này sinh ra để giải quyết triệt để vấn đề đó! Hệ thống sẽ tự động hóa 100% quy trình: Quét bài viết trên Meta Threads qua **Apify**, dùng **AI Agent (OpenAI)** thông minh để lọc bỏ rác, kiểm tra trùng lặp trên **Google Sheets**, và bắn thông báo nóng hổi về **Telegram** ngay khi có khách hàng tiềm năng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần lướt Threads thủ công, hệ thống tự động làm việc thay các sếp.
- **Lọc chính xác ý định tuyển dụng:** AI Agent phân biệt rõ ràng giữa "We are hiring" (nhà tuyển dụng) và "Hire me" (freelancer tự pr bản thân).
- **Chống trùng lặp thông minh:** Tự động đối chiếu với Google Sheets để không bao giờ gửi 1 job hai lần.
- **Cảnh báo tức thì:** Nhận ngay tin nhắn Telegram khi có cơ hội việc làm mới, giúp tiếp cận khách hàng nhanh nhất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Apify Account & API Token** (Sử dụng Actor `meta-threads-scraper`).
- **OpenAI API Key** (Dùng cho AI Agent và OpenAI Chat Model).
- **Google Sheets API & Credentials** (OAuth2) để lưu trữ dữ liệu.
- **Telegram Bot Token & Chat ID** để nhận thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow hoặc tải file JSON về, sau đó vào giao diện n8n chọn **Add workflow** -> Dấu ba chấm (...) -> **Import from File / Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:
- **Node `3 hours1` (Schedule Trigger):** Cài đặt thời gian chạy tự động (ví dụ: cứ mỗi 3 tiếng hoặc 12 tiếng quét một lần).
- **Các node `HTTP Request` (Quét dữ liệu từ Apify):** 
  - Điền Apify API Token của các sếp vào header/auth của các HTTP Request gọi đến actor [Meta Threads Scraper](https://apify.com/futurizerush/meta-threads-scraper).
  - Tùy chỉnh từ khóa tìm kiếm (keywords) trong phần JSON body của các node này (ví dụ: *n8n expert, automation engineer, video editor, graphic designer*...).
- **Node `OpenAI Chat Model` & `AI Agent`:** Chọn credential OpenAI và cấu hình model `gpt-4.1-mini`. Đảm bảo Prompt trong AI Agent hướng dẫn rõ ràng về tiêu chí tuyển dụng và các quốc gia mục tiêu mà các sếp muốn nhắm tới.
- **Node `Append or update row in sheet` (Google Sheets):** Kết nối tài khoản Google, chọn đúng file Sheet và Sheet Name dùng để lưu trữ danh sách việc làm.
- **Node `Send a text message1` (Telegram):** Kết nối Telegram Bot Credentials và điền Chat ID của các sếp hoặc nhóm Telegram nhận thông báo.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để chạy thử nghiệm (Test run) với dữ liệu mẫu từ Apify xem AI và Google Sheets có hoạt động trơn tru không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa nguồn tin:** Thay đổi từ khóa tìm kiếm liên tục trong các HTTP Request Apify để bắt trọn các xu hướng tuyển dụng ngách (như *AI automation, UI/UX designer, copywriter*...).
- **Mở rộng kênh thông báo:** Kết hợp thêm node **Slack** hoặc **Discord** bên cạnh Telegram để team cùng nhận được cơ hội việc làm.
- **Biến Sheets thành CRM thực thụ:** Thêm các cột trạng thái (*Status: New, Contacted, Interview, Closed*) trong Google Sheets để dễ dàng theo dõi phễu chăm sóc khách hàng.

### 📌 Kết luận
Workflow này là một "vũ khí bí mật" cực kỳ mạnh mẽ giúp các freelancers và agency tự động hóa quy trình tìm kiếm khách hàng tiềm năng mà không tốn một đồng chi phí quảng cáo nào. Hãy cài đặt ngay hôm nay để đón đầu mọi cơ hội việc làm trên mạng xã hội!