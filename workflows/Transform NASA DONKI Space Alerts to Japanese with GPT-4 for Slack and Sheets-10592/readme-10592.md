---
title: "🚀 Tự động hóa cảnh báo thiên văn NASA bằng GPT-4 và Slack - Workflow n8n"
description: "Hướng dẫn chi tiết cách tự động hóa cảnh báo thiên văn từ NASA bằng n8n, chuyển đổi sang tiếng Nhật bằng GPT-4 và gửi thông báo qua Slack cùng lưu trữ dữ liệu vào Google Sheets"
slug: "tu-dong-hoa-canh-bao-thien-van-nasa-bang-gpt-4-va-slack"
tags: [n8n, automation, no-code, NASA, AI, Slack, Google Sheets]
keywords: [n8n workflow, tự động hóa thiên văn, NASA DONKI, GPT-4, Slack, Google Sheets]
---

# 🚀 Tự động hóa cảnh báo thiên văn NASA bằng GPT-4 và Slack - Workflow n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp trong ngành thiên văn học khi phải theo dõi thủ công các cảnh báo từ NASA. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình theo dõi cảnh báo thiên văn từ NASA
- Chuyển đổi thông báo sang tiếng Nhật bằng công nghệ GPT-4 tiên tiến
- Phân loại và ưu tiên thông báo quan trọng để gửi qua Slack
- Lưu trữ dữ liệu quan trọng vào Google Sheets cho phân tích sau này
- Tiết kiệm thời gian và giảm lỗi thủ công trong quá trình xử lý thông tin thiên văn
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI API (để sử dụng GPT-4)
- Tài khoản Slack với quyền gửi thông báo
- Tài khoản Google với quyền truy cập Google Sheets
- Tài khoản NASA DONKI (nếu cần xác thực)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link sau: https://n8n.io/workflows/10592
3. Hoặc tải file JSON từ link trên và import thủ công

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node Cron**:
   - Thiết lập lịch chạy workflow (mặc định là mỗi 30 phút)
   - Có thể điều chỉnh theo nhu cầu của bạn

2. **Node NASA DONKI Notifications**:
   - Đảm bảo đã cấu hình tài khoản NASA DONKI (nếu cần)
   - Kiểm tra tham số "resource" đã được thiết lập là "donkiNotifications"

3. **Node OpenAI Chat Model**:
   - Cấu hình credentials cho OpenAI API
   - Đảm bảo đã chọn model "gpt-4.1-mini" hoặc model tương đương khác

4. **Node Slack Notify (Critical) và Slack Notify (High)**:
   - Cấu hình credentials cho Slack OAuth2 API
   - Kiểm tra kênh Slack sẽ nhận thông báo

5. **Node Append row in sheet**:
   - Cấu hình credentials cho Google Sheets
   - Điền ID của Google Sheet cần lưu trữ dữ liệu
   - Kiểm tra tên sheet và cấu trúc cột phù hợp

6. **Node Analyze & Prioritize Events**:
   - Kiểm tra mã JavaScript xử lý phân loại và ưu tiên sự kiện
   - Có thể điều chỉnh logic phân loại theo nhu cầu cụ thể

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để kiểm tra toàn bộ workflow
- Bật Active workflow sau khi đã kiểm tra và cấu hình đầy đủ

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để gửi thông báo qua Telegram hoặc Discord cho các kênh khác
- Tạo báo cáo hàng tuần tự động từ dữ liệu trong Google Sheets
- Thiết lập cảnh báo email cho các sự kiện quan trọng
- Tích hợp với hệ thống cảnh báo nội bộ của tổ chức
- Thêm node để lưu log hoạt động của workflow

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa theo dõi và xử lý thông tin thiên văn từ NASA. Bằng cách kết hợp công nghệ AI của GPT-4, tính năng phân loại thông báo và tích hợp với Slack và Google Sheets, các sếp có thể tối ưu hóa quá trình theo dõi thiên văn một cách hiệu quả và chuyên nghiệp. Hãy áp dụng ngay để nâng cao năng suất và giảm thiểu công việc thủ công!