---
title: "📈 Tự động hóa thông tin thị trường chứng khoán với Telegram & GPT-4 Nano"
description: "Hướng dẫn tự động hóa thông tin thị trường chứng khoán bằng n8n, Telegram và GPT-4 Nano - giải pháp hoàn toàn không cần code"
slug: "tu-dong-hoa-thong-tin-thi-truong-chung-khoan-voi-telegram-gpt4-nano"
tags: [n8n, automation, no-code, finance, ai]
keywords: [n8n workflow, tự động hóa chứng khoán, Telegram bot, GPT-4 Nano, Yahoo Finance]
---

# 📈 Tự động hóa thông tin thị trường chứng khoán với Telegram & GPT-4 Nano

[Đoạn mở đầu: Phân tích nỗi đau thực tế của nhà đầu tư khi phải tra cứu thông tin thị trường thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian tra cứu thông tin thị trường lên đến 90%
- Nhận thông tin chính xác và cập nhật liên tục
- Tích hợp hoàn hảo với Telegram - công cụ giao tiếp yêu thích
- Hỗ trợ nhiều loại truy vấn về thị trường chứng khoán
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot token
- API key từ OpenRouter cho GPT-4 Nano
- Tài khoản Yahoo Finance (nếu cần truy cập dữ liệu cụ thể)
- Kiến thức cơ bản về n8n và cách tạo credentials
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/5039](https://n8n.io/workflows/5039)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên
4. Hoàn tất quá trình import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Telegram Trigger**:
   - Tạo bot Telegram mới qua BotFather
   - Thêm bot vào nhóm hoặc kênh Telegram của bạn
   - Cấu hình credentials với bot token và chat ID

2. **OpenRouter Chat Model**:
   - Đăng ký tài khoản tại OpenRouter
   - Tạo API key và cấu hình credentials
   - Đảm bảo tài khoản có đủ credit để sử dụng GPT-4 Nano

3. **Google Search & Yahoo Finance**:
   - Không cần cấu hình riêng, nhưng đảm bảo kết nối internet ổn định
   - Nếu gặp lỗi, kiểm tra lại các node HTTP Request

4. **Simple Memory**:
   - Điều chỉnh số lượng tin nhắn lưu trữ trong bộ nhớ (mặc định 5)

#### 3. Kích hoạt ⚡️
1. Test workflow bằng cách gửi tin nhắn đến bot Telegram với nội dung như:
   - "Thông tin về AAPL"
   - "So sánh MSFT và GOOGL"
   - "Dự báo thị trường trong tuần tới"

2. Kiểm tra kết quả trả về từ bot
3. Nếu mọi thứ hoạt động tốt, bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp thêm Slack**: Thay thế node Telegram bằng Slack để nhận thông báo trên Slack
2. **Lưu log**: Thêm node Google Sheets để lưu lịch sử truy vấn
3. **Báo cáo định kỳ**: Tạo workflow phụ để gửi báo cáo thị trường hàng ngày
4. **Tích hợp với các sàn giao dịch**: Kết nối với các API giao dịch để thực hiện lệnh tự động

### 📌 Kết luận
Workflow này mang lại giải pháp hoàn hảo cho những nhà đầu tư muốn theo dõi thị trường chứng khoán một cách hiệu quả mà không cần phải tra cứu thủ công. Với tích hợp GPT-4 Nano, bạn có thể nhận được thông tin phân tích sâu hơn và các dự đoán thị trường. Hãy thử ngay và nâng cao trải nghiệm đầu tư của bạn!