---
title: "🚀 Tự động hóa báo cáo kinh doanh hàng tuần với AI, Google Sheets, Slack và Gmail"
description: "Hướng dẫn xây dựng workflow n8n tự động tổng hợp dữ liệu từ Google Sheets, sử dụng GPT-4o phân tích chỉ số kinh doanh và gửi báo cáo chuyên nghiệp qua Slack, Gmail."
slug: "tu-dong-hoa-bao-cao-kinh-doanh-hang-tuans-ai-google-sheets-slack-gmail"
tags: [n8n, automation, no-code, ai-summarization, google-sheets, open-ai]
keywords: [n8n workflow, tu dong hoa bao cao, google sheets ai, gpt-4o business digest, slack email automation]
---

# 🚀 Tự động hóa báo cáo kinh doanh hàng tuần với AI, Google Sheets, Slack và Gmail

Mỗi đầu tuần, các sếp lại mất hàng giờ đồng hồ để tổng hợp số liệu từ Google Sheets, tính toán tỷ lệ tăng trưởng, so sánh tuần qua và viết báo cáo gửi team? Việc làm thủ công này không chỉ tốn thời gian mà còn dễ xảy ra sai sót trong tính toán.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa 100% quy trình: tự động lấy dữ liệu, dùng AI (GPT-4o) phân tích xu hướng, chỉ ra điểm sáng, rủi ro và gửi thẳng báo cáo chuyên nghiệp đến kênh Slack và Email của team vào đúng 8 giờ sáng thứ Hai hàng tuần.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Không cần thủ công copy-paste số liệu hay tính toán tỷ lệ tăng trưởng.
- **Phân tích sâu từ AI:** GPT-4o tự động đưa ra nhận định, điểm nổi bật (wins), mối lo ngại (concerns) và định hướng ưu tiên (priorities) cho tuần tới.
- **Đa kênh đồng thời:** Báo cáo được gửi trực tiếp đến cả Slack channel của team và hòm thư Gmail cá nhân/đội ngũ.
- **Hoạt động tự động 24/7:** Chạy đều đặn vào mỗi sáng thứ Hai mà không cần sự can thiệp thủ công.
:::

### 📦 Các Nodes chính trong Workflow
Workflow gồm 8 nodes được bố trí tối ưu:
1. **Trigger every Monday at 8am** (`scheduleTrigger`): Lên lịch chạy tự động hàng tuần.
2. **Set report config variables** (`set`): Lưu trữ cấu hình (Sheet ID, tên sheet, kênh Slack, email nhận...).
3. **Fetch metrics from Google Sheets** (`googleSheets`): Đọc 14 ngày dữ liệu gần nhất từ Google Sheets.
4. **Calculate weekly comparisons** (`code`): Xử lý dữ liệu, tính toán so sánh tuần này với tuần trước, tỷ lệ chuyển đổi (conversion rate) và ROAS.
5. **Generate AI performance digest** (`openAi` - GPT-4o-mini): Phân tích dữ liệu và viết báo cáo dạng văn bản tự nhiên.
6. **Format digest for Slack and email** (`code`): Định dạng lại nội dung cho phù hợp với hiển thị của Slack và Email HTML.
7. **Post digest to Slack channel** (`slack`): Đẩy báo cáo lên kênh Slack định sẵn.
8. **Email digest to team** (`gmail`): Gửi email báo cáo cho đội ngũ.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Google:** Cấp quyền truy cập Google Sheets và Gmail.
- **Tài khoản OpenAI:** Có API Key tích hợp mô hình GPT-4o / GPT-4o-mini.
- **Tài khoản Slack:** Đã kết nối Bot/App để gửi tin nhắn vào channel mong muốn.
- **Google Sheet chuẩn bị sẵn:** Có các cột cơ bản như: `Date`, `Revenue`, `Leads`, `Conversions`, `Ad Spend`, `Support Tickets`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trống trên n8n, sau đó copy toàn bộ JSON của workflow này và dán trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `Set report config variables`**: Mở node này và điền chính xác các biến cấu hình của doanh nghiệp:
  - `Sheet ID`: Mã định danh của Google Sheet chứa dữ liệu kinh doanh.
  - `Sheet Name`: Tên tab chứa dữ liệu.
  - `Slack Channel`: Tên hoặc ID kênh Slack nhận tin nhắn.
  - `Email Recipients`: Địa chỉ email nhận báo cáo.
  - `Company Name`: Tên công ty để AI cá nhân hóa báo cáo.
- **Credentials**: Kết nối tài khoản của các dịch vụ tương ứng tại các node:
  - `Fetch metrics from Google Sheets`: Chọn Google Sheets OAuth2 API.
  - `Generate AI performance digest`: Chọn OpenAI API.
  - `Post digest to Slack channel`: Chọn Slack API.
  - `Email digest to team`: Chọn Gmail OAuth2.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** chạy thủ công lần đầu để kiểm tra dữ liệu và kết nối các dịch vụ có mượt mà không.
- Nếu mọi thứ xanh mướt, hãy bật công tắc **Active** ở góc trên bên phải để n8n tự động chạy định kỳ.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Webhook cảnh báo khẩn cấp:** Kết hợp điều kiện (If Node), nếu doanh thu giảm quá X% so với tuần trước, hãy bắn tin nhắn cảnh báo ngay lập tức vào Telegram hoặc Slack.
- **Lưu lịch sử báo cáo:** Thêm một bước ghi lại kết quả báo cáo của AI vào một tab lịch sử riêng trên Google Sheets để dễ dàng theo dõi theo quý/năm.
- **Đa ngôn ngữ:** Tinh chỉnh System Prompt trong node OpenAI để yêu cầu AI viết báo cáo bằng tiếng Việt hoặc tiếng Anh tùy theo nhu cầu của ban quản lý.

### 📌 Kết luận
Workflow này là một "vũ khí" tự động hóa cực kỳ lợi hại giúp các sếp nắm bắt toàn bộ bức tranh kinh doanh mỗi đầu tuần chỉ trong một nốt nhạc. Hãy triển khai ngay hôm nay để tiết kiệm thời gian và tối ưu hóa hiệu suất vận hành doanh nghiệp!