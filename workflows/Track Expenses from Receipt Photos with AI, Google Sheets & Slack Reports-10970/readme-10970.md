---
title: "💰 Tự động theo dõi chi tiêu từ ảnh hóa đơn bằng AI, Google Sheets & Slack"
description: "Hướng dẫn tự động hóa theo dõi chi tiêu gia đình bằng n8n: Nhận dạng hóa đơn bằng AI, lưu vào Google Sheets và báo cáo Slack hàng ngày/tháng."
slug: "tu-dong-theo-doi-chi-tieu-tu-anh-hoa-don"
tags: [n8n, automation, no-code, google-sheets, slack]
keywords: [n8n workflow, tự động hóa chi tiêu, theo dõi ngân sách, AI nhận dạng hóa đơn]
---

# 💰 Tự động theo dõi chi tiêu từ ảnh hóa đơn bằng AI, Google Sheets & Slack

[Các sếp nhà hàng, cửa hàng, hoặc gia đình thường phải ghi chép chi tiêu hàng ngày một cách thủ công. Việc này tốn thời gian, dễ sai sót và không thể phân tích được. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ nhận ảnh hóa đơn đến báo cáo chi tiêu hàng ngày/tháng trên Slack.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhập liệu thủ công cho mỗi hóa đơn.
- **Chính xác cao**: AI nhận dạng thông tin từ ảnh hóa đơn với độ chính xác cao.
- **Báo cáo tự động**: Nhận báo cáo chi tiêu hàng ngày/tháng trên Slack.
- **Phân tích dữ liệu**: Dễ dàng theo dõi xu hướng chi tiêu, các cửa hàng tốn nhiều nhất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Self-hosted hoặc Cloud).
- Google Sheet đã tạo với các cột: "Date", "Store", "Items", "Amount".
- Workspace Slack để nhận báo cáo.
- API key từ OpenRouter để sử dụng các mô hình chat.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc](https://n8n.io/workflows/10970).
2. Chọn "Copy JSON" và lưu file JSON.
3. Trong n8n Editor, chọn "Import from file" và chọn file JSON đã lưu.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Google Sheets Setup**:
   - Tạo Google Sheet với các cột: Date, Store, Items, Amount.
   - Chia sẻ Google Sheet với email của n8n credentials.
   - Trong node "Add to Budget Sheet" và "Get Budget Sheet (Daily)", chọn Google Sheet và Sheet Name đã tạo.

2. **OpenRouter Credentials**:
   - Tạo tài khoản OpenRouter và lấy API key.
   - Tạo credentials trong n8n với API key này.
   - Áp dụng cho tất cả các node OpenRouter Chat Model.

3. **Slack Credentials**:
   - Kết nối workspace Slack trong n8n.
   - Chọn channel mong muốn trong node "Send a message" và "Send monthly report".

4. **Webhook URL**:
   - Sau khi kích hoạt workflow, copy URL từ node "Receipt Photo Upload".
   - Sử dụng URL này để upload ảnh hóa đơn.

5. **Monthly Budget Adjustment**:
   - Trong node "Code in JavaScript2", chỉnh sửa `const budget = 30000;` để đặt ngân sách hàng tháng.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động.
- Bật Active workflow để bắt đầu theo dõi chi tiêu.

### ✍️ Mẹo & gợi ý nâng cao
- **Thay đổi tần suất báo cáo**: Chỉnh sửa cron settings trong node "Daily Report Trigger".
- **Thay đổi mô hình AI**: Chọn các mô hình khác trong các node OpenRouter Chat Model.
- **Tùy chỉnh nội dung báo cáo**: Chỉnh sửa nội dung và tone trong các node "Report Budget" và "Monthly Report".
- **Kết nối thêm dịch vụ**: Thêm các node khác để tích hợp với các phần mềm kế toán khác, gửi thông báo qua Telegram, hoặc phân tích dữ liệu nâng cao.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình theo dõi chi tiêu, từ nhận ảnh hóa đơn đến báo cáo hàng ngày/tháng trên Slack. Hãy áp dụng ngay để tiết kiệm thời gian và có cái nhìn rõ ràng về ngân sách của mình!