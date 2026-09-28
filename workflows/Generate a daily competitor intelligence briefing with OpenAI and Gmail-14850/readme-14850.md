---
title: "🚀 Tự động hóa Báo cáo Tình báo Đối thủ Cạnh tranh Hàng ngày với n8n và OpenAI"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu website đối thủ, phân tích bằng AI và gửi bản tin tổng hợp qua Gmail mỗi sáng."
slug: "tu-dong-hoa-bao-cao-doi-thu-canh-tranh-n8n-openai"
tags: [n8n, automation, ai-agents, openai, gmail, google-sheets, market-research]
keywords: [n8n workflow, tự động hóa tình báo đối thủ, ai phân tích đối thủ cạnh tranh, openai n8n, gmail automation]
---

# 🚀 Tự động hóa Báo cáo Tình báo Đối thủ Cạnh tranh Hàng ngày với n8n và OpenAI

Các sếp có bao giờ tò mò đối thủ cạnh tranh đang thay đổi giá, ra mắt tính năng gì mới hay chạy chiến dịch gì mà không có thời gian lướt website của từng ông mỗi ngày? Việc theo dõi thủ công vừa tốn thời gian, dễ bỏ sót thông tin quan trọng, lại chẳng thể duy trì đều đặn.

Giải pháp đây rồi! Workflow n8n này sẽ thay đội ngũ của các sếp "vi hành" các trang web đối thủ mỗi sáng, dùng AI phân tích tín hiệu chiến lược, và gửi một bản báo cáo tổng hợp (Executive Briefing) cực kỳ sắc sảo vào hòm thư Gmail trước khi cuộc họp đầu ngày bắt đầu. 

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Nắm bắt thị trường tức thì:** Nhận báo cáo chiến lược đối thủ lúc 8h sáng hàng ngày ngay trong Gmail.
- **Tiết kiệm hàng chục giờ:** Thay vì mất thời gian lướt web thủ công, AI sẽ đọc, chắt lọc và đánh giá mức độ đe dọa (threat level).
- **Ra quyết định nhanh chóng:** Bản tin được tổng hợp gọn gàng, chuyên nghiệp, chỉ tập trung vào những thay đổi cốt lõi ảnh hưởng trực tiếp đến doanh nghiệp của bạn.
- **Lưu trữ lịch sử minh bạch:** Mọi báo cáo đều được tự động đồng bộ vào Google Sheets để tra cứu bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Hạ tầng n8n:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản OpenAI:** Lấy API Key tại [platform.openai.com](https://platform.openai.com).
- **Tài khoản Gmail:** Để gửi email báo cáo tự động cho team.
- **Google Sheets:** Tạo sẵn một Google Sheet để lưu log dữ liệu báo cáo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể lấy mã nguồn từ [n8n Workflow #14850](https://n8n.io/workflows/14850), sau đó copy toàn bộ JSON và Paste trực tiếp vào n8n Editor của mình.

Workflow bao gồm 11 nodes chính được bố trí thông minh:
- **Daily 8AM Trigger (`scheduleTrigger`):** Lên lịch chạy tự động mỗi sáng lúc 8 giờ.
- **Configure Competitors and Settings (`code`):** Nơi khai báo danh sách URL đối thủ và từ khóa cần theo dõi.
- **Fetch Competitor Page (`httpRequest`):** Tải mã nguồn trang web đối thủ.
- **Extract Text and Build AI Prompt (`code`):** Lọc sạch HTML, lấy nội dung văn bản thuần túy.
- **AI Analyze Competitor (`httpRequest`):** Gọi OpenAI để phân tích từng đối thủ.
- **Parse AI Response & Aggregate (`code`):** Xử lý và tổng hợp dữ liệu từ các đối thủ.
- **AI Generate Final Briefing (`httpRequest`):** Dùng AI viết bản tin tổng hợp cuối cùng.
- **Format HTML Email & Send Email Briefing (`gmail`):** Định dạng và gửi email qua Gmail.
- **Log to Google Sheets (`googleSheets`):** Lưu vết toàn bộ lịch sử phân tích.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `Configure Competitors and Settings`**: 
  - Thay thế các URL mẫu bằng website thật của đối thủ cạnh tranh.
  - Cập nhật các trường `watch_for` để định hướng AI tìm kiếm thông tin gì (VD: thay đổi giá, tính năng mới, bài đăng blog...).
  - Thiết lập `YOUR_COMPANY` (Tên công ty bạn) và `YOUR_FOCUS` (Ngành hàng/Thị trường mục tiêu).
  - Cập nhật email nhận báo cáo tại `REPORT_EMAIL`.
- **Node `AI Analyze Competitor` & `AI Generate Final Briefing`**: 
  - Chọn Credentials là tài khoản OpenAI API của các sếp.
- **Node `Send Email Briefing`**: 
  - Kết nối tài khoản Gmail cá nhân hoặc Gmail doanh nghiệp của các sếp.
- **Node `Log to Google Sheets`**: 
  - Tạo Google Sheet với các cột: `Date`, `Company`, `Competitors Analyzed`, `Briefing Summary`.
  - Dán ID của Google Sheet vào node và cấu hình operation là `append`.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử một lần (Test run) để kiểm tra xem email có được gửi đi và dữ liệu có ghi vào Google Sheet hay không.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot:** Thay vì chỉ gửi Gmail, các sếp có thể bổ sung node **Slack** hoặc **Telegram** để đẩy thông báo nhanh vào group chat nội bộ công ty.
- **Nâng cấp Model AI:** Có thể đổi từ `GPT-4o-mini` sang `GPT-4o` ở node phân tích chi tiết nếu đối thủ của các sếp có lượng nội dung quá lớn và phức tạp.
- **Tùy chỉnh lịch chạy:** Thay đổi thời gian kích hoạt trong node `Daily 8AM Trigger` nếu team của các sếp họp sớm hơn (VD: 6h30 sáng).

### 📌 Kết luận
Với workflow n8n này, việc "soi" đối thủ cạnh tranh mỗi sáng không còn tốn một giọt mồ hôi nào nữa. Hãy thiết lập ngay hôm nay để luôn đi trước một bước trên thương trường các sếp nhé!