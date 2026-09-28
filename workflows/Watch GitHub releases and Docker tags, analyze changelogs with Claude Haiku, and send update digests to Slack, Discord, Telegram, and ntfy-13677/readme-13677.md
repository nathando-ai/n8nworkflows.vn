---
title: "🚀 Theo dõi tự động cập nhật phần mềm với AI và thông báo đa kênh"
description: "Giải pháp tự động hóa theo dõi cập nhật phần mềm từ GitHub và Docker, phân tích changelog bằng AI và gửi thông báo đến Discord, Telegram, Slack và ntfy"
slug: "theo-doi-cap-nhat-phan-mem-tu-dong-voi-ai"
tags: [n8n, automation, no-code, devops, ai]
keywords: [n8n workflow, tự động hóa, theo dõi cập nhật, AI phân tích, thông báo đa kênh]
---

# 🚀 Theo dõi tự động cập nhật phần mềm với AI và thông báo đa kênh

[Các sếp] có bao giờ phải tự tay kiểm tra cập nhật phần mềm hàng ngày không? Hay phải chờ đợi email thông báo từ nhà cung cấp? Với workflow này, các sếp có thể tự động hóa hoàn toàn quá trình theo dõi cập nhật phần mềm từ GitHub và Docker, phân tích changelog bằng AI và gửi thông báo đến nhiều kênh khác nhau như Discord, Telegram, Slack và ntfy.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải tự tay kiểm tra cập nhật hàng ngày.
- **Chính xác**: Phân tích changelog bằng AI để xác định các thay đổi quan trọng.
- **Đa kênh thông báo**: Gửi thông báo đến nhiều kênh khác nhau để đảm bảo không bỏ lỡ cập nhật nào.
- **Hoạt động liên tục**: Theo dõi cập nhật 24/7 mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Anthropic API Key**: Để sử dụng AI phân tích changelog.
- **GitHub Token** (tùy chọn): Để tăng giới hạn API rate.
- **URL Webhook Discord**: Để gửi thông báo đến Discord.
- **Token Bot Telegram**: Để gửi thông báo đến Telegram.
- **Token Bot Slack**: Để gửi thông báo đến Slack.
- **Topic ntfy**: Để gửi thông báo đến ntfy.
- **PostgreSQL Database**: Để lưu trữ lịch sử cập nhật.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow](https://n8n.io/workflows/13677).
2. Click vào nút **Download** để tải file JSON.
3. Trong n8n Editor, click vào **Import from File** và chọn file JSON đã tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Configure Watcher**:
   - Thêm **Anthropic API Key** vào credentials.
   - Cấu hình các kênh thông báo (Discord, Telegram, Slack, ntfy).
   - Thiết lập `test_mode` thành `true` để kiểm tra workflow trước khi chạy thực tế.

2. **Build Repo Watchlist**:
   - Thêm danh sách các repo cần theo dõi.
   - Cấu hình các thiết lập riêng cho từng repo (nếu cần).

3. **Claude Haiku**:
   - Chọn credentials đã cấu hình Anthropic API Key.
   - Đảm bảo model được chọn là `claude-haiku-4-5-20251001`.

4. **Send Discord**:
   - Thêm URL Webhook Discord vào credentials.

5. **Send Telegram**:
   - Thêm Token Bot Telegram và Chat ID vào credentials.

6. **Send Slack**:
   - Thêm Token Bot Slack và Channel ID vào credentials.

7. **Send ntfy**:
   - Thêm URL ntfy và Topic vào credentials.

8. **Save to DB**:
   - Cấu hình kết nối PostgreSQL để lưu trữ lịch sử cập nhật.

#### 3. Kích hoạt ⚡️
1. Click vào nút **Test workflow** để kiểm tra workflow với dữ liệu mẫu.
2. Sau khi kiểm tra thành công, đặt `test_mode` thành `false` trong node **Configure Watcher**.
3. Toggle **Active** để chạy workflow hàng ngày lúc 8 AM.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack**: Thêm node Slack để gửi thông báo đến kênh Slack.
- **Lưu log**: Thêm node để lưu log các cập nhật để theo dõi lịch sử.
- **Gửi báo cáo định kỳ**: Cấu hình gửi báo cáo định kỳ về các cập nhật quan trọng.
- **Kết hợp với Telegram**: Thêm node Telegram để gửi thông báo đến nhóm Telegram.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình theo dõi cập nhật phần mềm, phân tích changelog bằng AI và gửi thông báo đến nhiều kênh khác nhau. Với việc cấu hình đúng các credentials và thiết lập các kênh thông báo, các sếp có thể tiết kiệm thời gian và đảm bảo không bỏ lỡ cập nhật quan trọng nào. Hãy áp dụng ngay để tối ưu hóa quá trình quản lý cập nhật phần mềm của các sếp!