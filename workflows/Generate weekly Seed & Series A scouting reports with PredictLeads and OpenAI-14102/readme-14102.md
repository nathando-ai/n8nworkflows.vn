---
title: "🚀 Tự động hóa báo cáo gọi vốn Seed & Series A hàng tuần với PredictLeads và OpenAI trên n8n"
description: "Xây dựng hệ thống tự động quét danh sách theo dõi doanh nghiệp, lọc các vòng gọi vốn Seed/Series A qua PredictLeads và tổng hợp báo cáo bằng AI gửi về Gmail và Slack."
slug: "tu-dong-hoa-bao-cao-goi-von-seed-series-a-predictleads-openai"
tags: [n8n, automation, ai-agents, predictleads, openai, market-research]
keywords: [n8n workflow, tu dong hoa bao cao goi vốn, predictleads api, openai scout report, vc automation]
---

# 🚀 Tự động hóa báo cáo gọi vốn Seed & Series A hàng tuần với PredictLeads và OpenAI

Đối với các nhà đầu tư mạo hiểm (VC), nhà phân tích thị trường hay đội ngũ phát triển kinh doanh, việc theo dõi hàng trăm công ty mục tiêu xem họ có gọi vốn thành công hay không là một cơn ác mộng tốn hàng giờ đồng hồ mỗi tuần. Việc thủ công tra cứu từng domain, kiểm tra tin tức gọi vốn dễ dẫn đến bỏ sót thông tin quan trọng.

Workflow n8n này sẽ giải quyết hoàn toàn bài toán trên bằng cách tự động hóa 100%: Quét danh sách theo dõi, lấy dữ liệu sự kiện tài chính qua PredictLeads API, lọc các vòng gọi vốn Seed & Series A mới nhất, nhờ AI (OpenAI) tổng hợp thành báo cáo chuyên nghiệp và gửi thẳng đến Gmail và Slack của bạn vào mỗi thứ Hai hàng tuần.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải thủ công search Google hay check Crunchbase từng công ty.
- **Không bỏ lỡ cơ hội:** Tự động lọc chính xác các vòng gọi vốn Seed & Series A trong 7 ngày qua.
- **Báo cáo thông minh từ AI:** Nhận bảng markdown chi tiết (Tên công ty, Loại vòng, Số tiền, Ngày, Nhà đầu tư) kèm phân tích xu hướng thị trường.
- **Đa kênh thông báo:** Nhận báo cáo chi tiết qua Gmail và tóm tắt nhanh chóng trên Slack.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Sheets:** File chứa danh sách domain các công ty cần theo dõi.
- **PredictLeads API:** Tài khoản và API key để lấy thông tin sự kiện tài chính.
- **OpenAI API Key:** Để phân tích và viết báo cáo scouting.
- **Gmail Account / OAuth2:** Để gửi email tự động.
- **Slack Webhook:** Để gửi thông báo tóm tắt lên kênh Slack của đội ngũ.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc copy trực tiếp mã JSON từ n8n.io và paste vào n8n Editor của bạn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số và credentials sau cho từng node:
- ⏰ **Weekly Schedule**: Đặt lịch chạy định kỳ (mặc định vào sáng Thứ Hai hàng tuần).
- 📋 **Read Watchlist (Google Sheets)**: Kết nối tài khoản Google Sheets của bạn (`googleSheetsOAuth2Api`), chọn đúng file Spreadsheet và Sheet chứa danh sách các domain công ty.
- 🔄 **Loop Companies (Split In Batches)**: Xử lý danh sách công ty theo từng lô để tránh quá tải API.
- 🔍 **Fetch Financing Events (HTTP Request)**: Điền Endpoint và API Key của PredictLeads để lấy dữ liệu tài chính của từng domain.
- ⚙️ **Filter Seed & Series A (Code)**: Node JavaScript giúp lọc các sự kiện gọi vốn thuộc loại Seed hoặc Series A diễn ra trong 7 ngày gần nhất.
- ⚙️ **Aggregate Results (Code)**: Tổng hợp tất cả dữ liệu đã lọc thành một tập dữ liệu duy nhất.
- 🤖 **Generate Scouting Report (HTTP Request / OpenAI)**: Kết nối OpenAI API, thiết lập prompt yêu cầu AI phân tích và trả về định dạng bảng Markdown cùng phân tích xu hướng.
- 📧 **Send Report Email (Gmail)**: Cấu hình tài khoản Gmail OAuth2 (`gmailOAuth2`) để gửi báo cáo hoàn chỉnh đến email của bạn hoặc đội ngũ.
- 💬 **Slack Summary (HTTP Request)**: Dán Slack Webhook URL của bạn để bắn tin nhắn thông báo nhanh.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm thủ công với dữ liệu mẫu từ Google Sheets.
- Kiểm tra kết quả trả về ở Gmail và Slack xem đã đúng ý chưa.
- Gạt công tắc sang **Active** để workflow tự động chạy ngầm hàng tuần.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Có thể bổ sung thêm node Telegram hoặc Microsoft Teams để đội ngũ nhận tin ở nền tảng chat khác.
- **Lưu lịch sử:** Thêm một node Google Sheets ở cuối luồng để tự động ghi lại lịch sử các báo cáo đã gửi nhằm lưu trữ dữ liệu theo thời gian.
- **Tùy biến Prompt AI:** Điều chỉnh prompt trong node OpenAI để tập trung vào các tiêu chí ngành nghề cụ thể (ví dụ: chỉ lọc AI/SaaS startups).

### 📌 Kết luận
Workflow tự động hóa này là "vũ khí bí mật" giúp các nhà đầu tư và chuyên gia phát triển thị trường luôn đi trước một bước trong việc tiếp cận các startup tiềm năng ngay từ những vòng gọi vốn đầu tiên. Hãy triển khai ngay hôm nay để tối ưu hóa năng suất làm việc của đội ngũ các sếp!