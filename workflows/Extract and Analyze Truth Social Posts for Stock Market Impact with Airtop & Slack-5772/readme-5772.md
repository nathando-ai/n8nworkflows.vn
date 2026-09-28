---
title: "🚀 Tự động trích xuất và phân tích bài đăng Truth Social tác động đến thị trường chứng khoán với Airtop & Slack"
description: "Hướng dẫn xây dựng workflow n8n tự động cào bài đăng Truth Social của Donald Trump, phân tích tác động tài chính bằng AI và gửi cảnh báo ngay vào Slack."
slug: "trich-xuat-phan-tich-truth-social-airtop-slack"
tags: [n8n, automation, airtop, slack, ai-summarization, trading-signals]
keywords: [n8n workflow, truth social automation, airtop api, slack integration, phan tich chung khoan ai, tu dong hoa n8n]
---

# 🚀 Tự động trích xuất và phân tích bài đăng Truth Social tác động đến thị trường chứng khoán với Airtop & Slack

Các nhà giao dịch (traders) và nhà phân tích tài chính luôn phải đối mặt với áp lực thời gian cực lớn khi theo dõi các thông tin từ các tài khoản mạng xã hội có sức ảnh hưởng lớn, ví dụ như tài khoản Truth Social của Donald Trump. Việc canh me từng bài đăng, đánh giá nhanh tác động của nó lên thị trường chứng khoán thủ công vừa tốn thời gian, vừa dễ bỏ lỡ cơ hội vàng.

Đừng lo, workflow n8n này sẽ giải quyết triệt để bài toán đó! Nó tự động hóa 100% quy trình: cào dữ liệu qua trình duyệt thông minh của Airtop, dùng AI phân tích mức độ tác động đến thị trường Mỹ, lọc bỏ nhiễu và đẩy thẳng cảnh báo chất lượng cao vào kênh Slack của team.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bắt kịp tin tức tốc độ chớp nhoáng**: Tự động lấy bài đăng mới nhất mà không cần canh me màn hình.
- **Phân tích tài chính thông minh**: AI tự động đánh giá hướng tác động (tích cực, tiêu cực, trung lập) và mức độ ảnh hưởng đến thị trường.
- **Thông báo tập trung**: Gửi thẳng kết quả phân tích kèm hình ảnh, nội dung và đường dẫn vào kênh Slack chuyên dụng.
- **Tiết kiệm 100% thời gian thủ công**: Hoạt động hoàn toàn tự động theo lịch trình (Schedule) hoặc chạy thủ công khi cần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Airtop API Key**: Lấy miễn phí tại [Airtop Portal](https://portal.airtop.ai/api-keys).
- **Airtop Browser Profile**: Đã kết nối và đăng nhập sẵn vào tài khoản Truth Social của bạn [Airtop Browser Profiles](https://portal.airtop.ai/browser-profiles).
- **Slack Workspace**: Đã cấp quyền tích hợp app để bot có thể gửi tin nhắn vào channel chỉ định.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này, sau đó vào giao diện n8n chọn **Add workflow** -> **Import from JSON** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 9 nodes, trong đó các sếp cần lưu ý cấu hình kỹ các node sau:

- **Create Airtop Session** & **Create Airtop Browser**:
  - Chọn `airtopApi` credentials bằng API Key đã lấy từ Airtop.
  - Điền tên Profile Airtop đã đăng nhập sẵn Truth Social vào tham số cấu hình của node.
- **Extract and Analyze Posts** (Node Airtop quan trọng nhất):
  - Node này sử dụng prompt tiếng Anh được thiết lập sẵn để cào tối đa 6 bài đăng từ `@realDonaldTrump`, trích xuất tên tác giả, URL hình ảnh, nội dung text, URL bài viết và dự đoán tác động thị trường (Direction & Magnitude).
  - Đảm bảo kết nối đúng credentials của Airtop.
- **Split Out**: Dùng để tách mảng bài viết lớn thành các items riêng biệt để dễ dàng xử lý từng post một.
- **Filter**: Lọc ra các bài viết thực sự có nội dung và có chỉ số tác động thị trường khác 0 để tránh gửi tin rác.
- **Slack**: 
  - Chọn `slackOAuth2Api` credentials.
  - Chọn kênh Slack (Channel) nhận cảnh báo thông tin tài chính.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử thủ công lần đầu để kiểm tra kết quả trả về từ Airtop và Slack.
- Nếu mọi thứ mượt mà, hãy gạt nút **Active** ở góc trên bên phải để workflow tự động chạy ngầm theo lịch (Schedule Trigger).

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Telegram/Discord**: Ngoài Slack, các sếp có thể nhân bản nhánh output để bắn tin đồng thời sang nhóm Telegram cá nhân hoặc phòng chat riêng của team.
- **Lưu trữ dữ liệu vào Google Sheets / Airtable**: Thêm một node Google Sheets ở cuối luồng để lưu lại lịch sử các bài đăng và mức độ tác động dùng cho việc backtest chiến lược giao dịch sau này.
- **Mở rộng nguồn theo dõi**: Nhân bản workflow để cào thêm các tài khoản có sức ảnh hưởng khác như các CEO công nghệ lớn hoặc các quan chức ngân hàng trung ương.

:::note[Lưu ý pháp lý quan trọng]
Công cụ này chỉ mang tính chất tham khảo và phục vụ phân tích thông tin. Các đánh giá tác động thị trường chỉ là phỏng đoán từ AI, **tuyệt đối không được coi là lời khuyên tài chính (Financial Advice)**. Hãy luôn tham vấn chuyên gia trước khi xuống tiền đầu tư!
:::

### 📌 Kết luận
Một workflow cực kỳ thông minh kết hợp giữa sức mạnh tự động hóa trình duyệt của Airtop và sự linh hoạt của n8n. Hãy thiết lập ngay hôm nay để không bỏ lỡ bất kỳ biến động thị trường nào bắt nguồn từ mạng xã hội!