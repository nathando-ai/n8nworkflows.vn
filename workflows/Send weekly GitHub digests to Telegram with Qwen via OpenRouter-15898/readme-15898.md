---
title: "🚀 Tự động hóa báo cáo GitHub hàng tuần tới Telegram với Qwen thông qua OpenRouter"
description: "Giải pháp tự động hóa hoàn toàn không cần code giúp các sếp theo dõi hoạt động GitHub hàng tuần một cách hiệu quả, tiết kiệm thời gian và tối ưu hóa quy trình làm việc."
slug: "tu-dong-hoa-bao-cao-github-hang-tuan-toi-telegram"
tags: [n8n, automation, no-code, github, telegram]
keywords: [n8n workflow, tự động hóa, github, telegram, báo cáo tự động]
---

# 🚀 Tự động hóa báo cáo GitHub hàng tuần tới Telegram với Qwen thông qua OpenRouter

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải theo dõi nhiều repository GitHub và phải tạo báo cáo thủ công hàng tuần. Giới thiệu workflow như giải pháp tự động hóa hoàn toàn không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động tổng hợp báo cáo hàng tuần mà không cần can thiệp thủ công.
- **Chính xác**: Dữ liệu được lấy trực tiếp từ GitHub, đảm bảo độ tin cậy cao.
- **Cá nhân hóa**: Có thể tùy chỉnh báo cáo theo nhu cầu cụ thể (issues, pull requests, status).
- **Hoạt động liên tục**: Báo cáo được gửi tự động hàng tuần hoặc theo yêu cầu qua Telegram.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản GitHub với Fine-grained Personal Access Token (Quyền đọc nội dung).
- Tài khoản Telegram và một bot Telegram.
- Tài khoản OpenRouter với API key.
- Instance n8n đã được cài đặt và cấu hình.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow, các sếp có thể làm theo các bước sau:

1. Truy cập vào trang [n8n.io/workflows/15898](https://n8n.io/workflows/15898).
2. Nhấp vào nút "Import" để tải xuống file JSON của workflow.
3. Trong n8n Editor, nhấp vào nút "Import from File" và chọn file JSON đã tải xuống.

Hoặc, các sếp có thể copy/paste JSON vào n8n Editor bằng cách:

1. Copy toàn bộ nội dung JSON từ trang workflow.
2. Trong n8n Editor, nhấp vào nút "Import from Clipboard".
3. Dán nội dung JSON vào hộp thoại và nhấp vào "Import".

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Weekly Digest Trigger**: Cấu hình lịch trình hàng tuần (mặc định là 9 AM UTC).
- **Fetch GitHub Repositories**: Cấu hình Header Auth credential với Fine-grained Personal Access Token của GitHub.
- **Retrieve GitHub Events**: Cấu hình Header Auth credential giống với node trước.
- **OpenAI Report Model**: Cấu hình OpenAI API credential với Base URL là `https://openrouter.ai/api/v1` và API Key là OpenRouter key.
- **Send Messages to Telegram** và **Send Error Alert**: Cấu hình `chatId` với ID của Telegram chat.
- **Telegram Message Trigger**: Cấu hình Telegram Bot API credential với token của bot Telegram.

#### 3. Kích hoạt ⚡️
Sau khi đã cấu hình các node quan trọng, các sếp cần thực hiện các bước sau để kích hoạt workflow:

1. **Test run dữ liệu mẫu**: Chạy workflow với dữ liệu mẫu để đảm bảo mọi thứ hoạt động đúng.
2. **Bật Active workflow**: Nhấp vào nút "Activate" để kích hoạt workflow.
3. **Kiểm tra Telegram**: Gửi lệnh `/report` tới bot Telegram để kiểm tra xem workflow có hoạt động đúng không.

### ✍️ Mẹo & gợi ý nâng cao
- **Thay đổi lịch trình**: Chỉnh sửa node Weekly Digest Trigger để thay đổi tần suất và thời gian gửi báo cáo.
- **Lọc repository**: Thêm một bước lọc sau node Fetch GitHub Repositories để loại bỏ các repository không cần thiết.
- **Thay đổi mô hình AI**: Chỉnh sửa node OpenAI Report Model để sử dụng các mô hình khác như GPT-4o, Claude, hoặc Gemini.
- **Thay đổi kênh xuất**: Thay thế các node Telegram bằng các node Discord, Slack, hoặc Email để gửi báo cáo tới các kênh khác.
- **Chế độ báo cáo đơn giản**: Loại bỏ logic tách báo cáo theo `|||` trong node Format Telegram Messages để gửi báo cáo dưới dạng một tin nhắn duy nhất.

### 📌 Kết luận
Workflow này cung cấp một giải pháp tự động hóa hoàn toàn không cần code để theo dõi hoạt động GitHub hàng tuần và gửi báo cáo tới Telegram. Với các tính năng tùy chỉnh và khả năng mở rộng, workflow này giúp các sếp tiết kiệm thời gian và tối ưu hóa quy trình làm việc một cách hiệu quả. Hãy áp dụng ngay để trải nghiệm sự tiện lợi và hiệu quả của tự động hóa!