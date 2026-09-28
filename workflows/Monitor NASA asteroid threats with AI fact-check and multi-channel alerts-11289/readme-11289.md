---
title: "🚀 Giám sát tiểu hành tinh NASA với AI Fact-Check và Cảnh báo đa kênh"
description: "Tự động quét dữ liệu thiên thạch từ NASA, đối chiếu tin tức truyền thông qua Apify, dùng AI phân tích độ chính xác và gửi cảnh báo thời gian thực."
slug: "giam-sat-tieu-hanh-tinh-nasa-ai-fact-check"
tags: [n8n, automation, ai-summarization, market-research, openAI, nasa]
keywords: [n8n workflow, giám sát tiểu hành tinh, nasa api, ai fact check, apify news scraper, tu dong hoa n8n]
---

# 🚀 Giám sát tiểu hành tinh NASA với AI Fact-Check và Cảnh báo đa kênh

Các sếp có bao giờ tò mò liệu có thiên thạch nào đang bay sượt qua Trái Đất mà truyền thông đang thổi phồng quá mức không? Việc thủ công đi tra cứu dữ liệu từ NASA, sau đó lùng sục tin tức khắp các khu vực (Mỹ, Nhật, Châu Âu) rồi đối chiếu xem báo chí có nói sai sự thật không thực sự là một "cực hình" mất rất nhiều thời gian. 

Workflow n8n này sẽ giải quyết trọn vẹn bài toán đó một cách tự động 100%. Hệ thống sẽ tự động quét dữ liệu Near Earth Object (NEO) của NASA trong 7 ngày tới, quét tin tức quốc tế qua Apify, nhờ AI của OpenAI kiểm chứng độ thật giả, đo lường mức độ hoảng loạn của truyền thông và bắn cảnh báo đa kênh (Slack, Discord, Email) kèm theo Google Sheets log lại toàn bộ lịch sử!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- 🔍 **Tự động hóa hoàn toàn**: Nhận dự báo tiểu hành tinh trong 7 ngày từ NASA API mà không cần thao tác tay.
- ✅ **AI Fact-Check thông minh**: So sánh dữ liệu khoa học chính xác của NASA với thông tin báo chí từ nhiều quốc gia (Mỹ, Nhật, EU) để phát hiện tin đồn thất thiệt, thổi phồng.
- 📊 **Đánh giá đa chiều**: Chấm điểm mối đe dọa thực tế (Actual Threat) đối chiếu với mức độ hoảng loạn của truyền thông (Media Panic).
- 🔔 **Cảnh báo đa kênh tức thì**: Đẩy thông báo trực quan qua Slack (Rich blocks), Discord (Embeds), Email (HTML) và ghi log chi tiết vào Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow vận hành trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **NASA API Key**: Đăng ký miễn phí tại [api.nasa.gov](https://api.nasa.gov/).
- **Apify Account**: Tạo tài khoản tại [apify.com](https://apify.com/) để cào tin tức khu vực.
- **OpenAI API Key**: Lấy khóa API từ [platform.openai.com](https://platform.openai.com/).
- **Kênh thông báo (Tùy chọn)**: Webhook Discord, Slack OAuth app hoặc cấu hình SMTP Email.
- **Google Sheets (Tùy chọn)**: Tạo sẵn một file Google Sheet để lưu log lịch sử.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (hoặc tải file JSON từ n8n template #11289) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các node quan trọng sau:
- **Daily Schedule & Webhook Trigger**: Workflow hỗ trợ chạy tự động lúc 9h sáng mỗi ngày hoặc kích hoạt thủ công qua POST request tới đường dẫn `/webhook/asteroid-alert`.
- **Get NASA Asteroid Data**: Thêm Credential cho NASA API bằng khóa đã đăng ký. Node này sẽ tự động quét 7 ngày dữ liệu tiểu hành tinh.
- **Search Regional News (Apify)**: Kết nối tài khoản Apify qua OAuth trong n8n để hệ thống cào tin tức từ 3 khu vực (Mỹ, Nhật, EU/UK).
- **AI Fact-Check Analysis (OpenAI)**: Cấu hình API Key của OpenAI, node này sẽ đóng vai trò chuyên gia phân tích, đối chiếu dữ liệu khoa học và phát hiện tin giả.
- **Send Slack Alert / Send Discord Alert / Send Email Alert**: Bật/tắt hoặc cấu hình các kênh thông báo tùy theo nhu cầu sử dụng của tổ chức. Các sếp có thể ngắt kết nối kênh không dùng.
- **Log to Google Sheets**: Trỏ tới file Google Sheet của các sếp. Đảm bảo sheet có các cột: `Date`, `Alert Level`, `Hazardous Count`, `Threat Score`, `Media Panic Score`, `Misinformation Detected`, `Top Asteroid`, `Most Accurate Region`.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để chạy thử nghiệm (Test run) với dữ liệu mẫu xem các node có hoạt động mượt mà không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin**: Tích hợp thêm node Telegram để nhận thông báo ngay trên điện thoại cá nhân với định dạng Markdown bắt mắt.
- **Tạo bảng Dashboard**: Kết hợp Google Sheets vừa log dữ liệu để vẽ biểu đồ trực quan trên Looker Studio, tạo bảng theo dõi thiên thạch riêng cho team.
- **Tùy chỉnh ngưỡng cảnh báo**: Tinh chỉnh logic ở node `Check for Hazardous Objects` hoặc `Analyze Asteroid Threats` nếu các sếp chỉ muốn nhận cảnh báo khi có thiên thạch tiến lại gần Trái Đất dưới 5 khoảng cách Mặt Trăng (Lunar Distances).

### 📌 Kết luận
Workflow giám sát tiểu hành tinh tích hợp AI Fact-Check này không chỉ là một ứng dụng thú vị về khoa học vũ trụ mà còn là hình mẫu tuyệt vời cho việc kết hợp dữ liệu API thời gian thực, cào tin tức tự động và khả năng phân tích ngữ nghĩa đỉnh cao của LLM. Hãy "lên đồ" ngay cho hệ thống n8n của các sếp để không bỏ lỡ bất kỳ tin tức vũ trụ quan trọng nào!