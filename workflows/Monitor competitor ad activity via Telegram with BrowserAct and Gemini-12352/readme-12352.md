---
title: "🚀 Tự động giám sát quảng cáo đối thủ trên Meta & Google qua Telegram với BrowserAct và Gemini"
description: "Hướng dẫn cài đặt workflow n8n giúp theo dõi chiến dịch quảng cáo của đối thủ cạnh tranh trên Meta và Google, phân tích bằng AI Gemini và gửi báo cáo trực tiếp qua Telegram."
slug: "giam-sat-quang-cao-doi-thu-telegram-browseract-gemini"
tags: [n8n, automation, telegram, browseract, gemini, ai-agent, competitor-analysis]
keywords: [n8n workflow, giám sát quảng cáo đối thủ, browseract, gemini ai, telegram bot automation]
---

# 🚀 Tự động giám sát quảng cáo đối thủ trên Meta & Google qua Telegram với BrowserAct và Gemini

Việc theo dõi thủ công các chiến dịch quảng cáo (Ad Library) của đối thủ trên Meta và Google tốn rất nhiều thời gian, dễ bỏ sót thông tin và khó đưa ra đánh giá chiến lược nhanh chóng. 

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa 100%: Nhận yêu cầu qua **Telegram**, sử dụng **BrowserAct** để cào dữ liệu quảng cáo, nhờ **Google Gemini AI** phân tích thông minh và trả về kết quả chiến lược chi tiết ngay lập tức cho các sếp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Không cần mất hàng giờ lướt tìm kiếm thủ công trên Meta Ad Library hay Google Ads Transparency Center.
- **Phân tích chuyên sâu:** AI Gemini tự động thống kê số lượng quảng cáo, phân tích mẫu content (hooks) hiệu quả và đưa ra phán quyết chiến lược (Nên chạy ngay hay chờ đợi).
- **Tương tác thời gian thực:** Nhận báo cáo chiến lược trực tiếp qua chat Telegram bất cứ lúc nào chỉ với một câu lệnh đơn giản.
- **Hoạt động tự động 24/7:** Bot luôn sẵn sàng túc trực để phục vụ nhu cầu nghiên cứu thị trường của đội ngũ Marketing.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Telegram Bot Token** (tạo qua BotFather).
- **BrowserAct Account & API Key** (với template: *Competitor Ad Activity Monitor*).
- **Google Gemini API Key** (Google Palm/Gemini API credentials).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow hoặc import trực tiếp file JSON vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node sau:

- **User Sends Message to Bot & Send Message to User Chat:** Kết nối với **Telegram API Credentials** của bot Telegram mà các sếp đã tạo.
- **Scrape Ads from Meta and Google:** Kết nối với **BrowserAct API Credentials**. Đảm bảo các sếp đã lưu template **Competitor Ad Activity Monitor** trong tài khoản BrowserAct của mình.
- **Validate inputs, Analyze user Input, Process Ad Data & Gemini:** Cấu hình **Google Palm/Gemini API Credentials** để AI có đủ quyền thực hiện bóc tách ý định người dùng và phân tích dữ liệu quảng cáo.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi một tin nhắn thử nghiệm tới bot Telegram của sếp (ví dụ: *"Check ads for [Tên Công Ty]*") để test luồng dữ liệu.
- Sau khi test thành công, gạt công tắc sang **Active** để bật bot chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu lịch sử báo cáo:** Kết nối thêm node Google Sheets hoặc Airtable để lưu lại lịch sử các lần check đối thủ nhằm phục vụ việc theo dõi xu hướng dài hạn.
- **Mở rộng kênh thông báo:** Ngoài Telegram, có thể cấu hình gửi bản tóm tắt sang nhóm Slack hoặc Discord của phòng Marketing.
- **Cảnh báo định động:** Thiết lập lịch chạy tự động (Cron node) hàng tuần để bot chủ động quét đối thủ chính và gửi báo cáo vào đầu tuần.

### 📌 Kết luận
Workflow này là vũ khí cực kỳ mạnh mẽ cho các đội ngũ Marketing và nhà sáng lập muốn nắm bắt nhanh chóng chiến lược của đối thủ cạnh tranh mà không tốn nhiều nhân lực. Hãy import ngay vào n8n và tối ưu hóa quy trình nghiên cứu thị trường của các sếp ngay hôm nay!