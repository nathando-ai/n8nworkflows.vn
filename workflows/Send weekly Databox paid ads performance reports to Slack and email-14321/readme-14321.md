---
title: "🚀 Tự động hóa báo cáo hiệu suất quảng cáo hàng tuần với Databox, Slack và Email"
description: "Hướng dẫn tự động hóa báo cáo hiệu suất quảng cáo hàng tuần từ Databox đến Slack và Email, tiết kiệm thời gian và nâng cao hiệu quả chiến dịch"
slug: "tu-dong-hoa-bao-cao-quang-cao-hang-tuan-databox-slack-email"
tags: [n8n, automation, no-code, databox, marketing]
keywords: [n8n workflow, tự động hóa báo cáo, quảng cáo online, marketing automation]
---

# 🚀 Tự động hóa báo cáo hiệu suất quảng cáo hàng tuần với Databox, Slack và Email

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp marketing thường phải tốn nhiều thời gian và công sức để theo dõi hiệu suất quảng cáo hàng tuần trên nhiều nền tảng khác nhau. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ thu thập dữ liệu đến gửi báo cáo, tiết kiệm thời gian quý giá và tập trung vào những chiến lược quan trọng hơn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quy trình báo cáo hàng tuần
- Tăng cường hiệu quả: Theo dõi 6 chỉ số quan trọng trên nhiều nền tảng quảng cáo
- Tăng tính chuyên nghiệp: Báo cáo được định dạng đẹp mắt với các chỉ số so sánh tuần trước
- Hoạt động liên tục: Nhận báo cáo hàng tuần vào đúng giờ mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Databox với ít nhất một nền tảng quảng cáo đã kết nối (miễn phí: [Đăng ký Databox](https://databox.com/?ref=n8n))
- API key của OpenAI (Claude hoặc ChatGPT)
- Tài khoản Slack (tùy chọn)
- Tài khoản Gmail (tùy chọn)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link sau: [https://n8n.io/workflows/14321](https://n8n.io/workflows/14321)
3. Hoặc tải file JSON về và import từ máy tính

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Every Monday 9 AM"**:
   - Có thể thay đổi lịch trình theo nhu cầu (hàng ngày, ngày khác, giờ khác)
   - Click vào node này và chỉnh sửa Cron Expression

2. **Node "OpenAI Chat Model"**:
   - Thêm API key của OpenAI
   - Có thể thay thế bằng các model khác nếu cần

3. **Node "Databox MCP Tool"**:
   - Đảm bảo đã kết nối ít nhất một nền tảng quảng cáo trong tài khoản Databox
   - Xác thực bằng OAuth2 và kết nối với tài khoản Databox của bạn

4. **Node "Send to Slack"**:
   - Kết nối với tài khoản Slack của bạn
   - Chỉ định kênh nhận báo cáo

5. **Node "Send Email"**:
   - Thêm thông tin xác thực Gmail/SMTP
   - Có thể thay đổi địa chỉ email nhận báo cáo

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, nhấn "Execute Workflow" để test với dữ liệu mẫu
2. Kiểm tra kết quả trên Slack và Email
3. Nếu mọi thứ ổn, nhấn "Activate Workflow" để chạy tự động hàng tuần

### ✍️ Mẹo & gợi ý nâng cao
1. Thêm các kênh thông báo khác như Microsoft Teams, Discord hoặc Telegram
2. Tùy chỉnh nội dung báo cáo theo nhu cầu cụ thể của đội ngũ
3. Thiết lập cảnh báo tự động khi có hiệu suất quảng cáo kém
4. Lưu trữ lịch sử báo cáo để phân tích dài hạn

### 📌 Kết luận
Workflow này giúp các sếp marketing tự động hóa hoàn toàn quy trình báo cáo hiệu suất quảng cáo hàng tuần, tiết kiệm thời gian quý giá và nâng cao hiệu quả chiến dịch. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của bạn!