---
title: "🛍️ Tự động hóa tìm kiếm sản phẩm Amazon qua Telegram với n8n và AI"
description: "Hướng dẫn tạo bot Telegram tự động tìm kiếm sản phẩm Amazon bằng n8n, Apify và OpenRouter AI - giải pháp tiết kiệm thời gian cho nghiên cứu thị trường và mua sắm"
slug: "tu-dong-hoa-tim-kiem-san-pham-amazon-qua-telegram-voi-n8n-va-ai"
tags: [n8n, automation, no-code, telegram, apify, openrouter, ai, market-research]
keywords: [n8n workflow, tự động hóa tìm kiếm sản phẩm, bot telegram, apify amazon, openrouter ai, nghiên cứu thị trường]
---

# 🛍️ Tự động hóa tìm kiếm sản phẩm Amazon qua Telegram với n8n và AI

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải tự tay tìm kiếm thông tin sản phẩm trên Amazon? Với workflow này, các sếp có thể tạo ngay một bot Telegram thông minh giúp tự động tìm kiếm sản phẩm Amazon chỉ với vài cú nhấn phím.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động tìm kiếm sản phẩm Amazon chỉ với tin nhắn Telegram
- **Nghiên cứu thị trường hiệu quả**: Lấy thông tin sản phẩm nhanh chóng và chính xác
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công sau khi cài đặt
- **Tích hợp AI thông minh**: Phân biệt giữa tìm kiếm sản phẩm và trò chuyện thông thường
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot token (tạo tại [BotFather](https://t.me/BotFather))
- API key từ [OpenRouter](https://openrouter.ai/) (đăng ký tài khoản và lấy API key)
- Tài khoản Apify (đăng ký tại [Apify](https://apify.com/))
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/6319](https://n8n.io/workflows/6319)
2. Click vào nút "Import" để tải file JSON
3. Hoặc copy toàn bộ JSON và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Recieve Message"**:
   - Chọn credentials "telegramApi"
   - Điền bot token đã tạo từ BotFather

2. **Node "OpenRouter Chat Model" và "OpenRouter Chat Model2"**:
   - Chọn credentials "openRouterApi"
   - Đảm bảo đã điền đúng API key từ OpenRouter
   - Model được cấu hình sẵn là "openai/gpt-3.5-turbo-instruct"

3. **Node "Send Post request and get datset items"**:
   - Đảm bảo URL API Apify là chính xác
   - Có thể cần điều chỉnh tham số nếu Apify thay đổi cấu trúc API

4. **Node "Send Response" và "Send Amazone Products"**:
   - Chọn credentials "telegramApi"
   - Đảm bảo bot token đã được cấu hình đúng

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu để đảm bảo workflow hoạt động
2. Bật Active workflow để bắt đầu sử dụng
3. Gửi tin nhắn đến bot Telegram với nội dung tìm kiếm sản phẩm (ví dụ: "Điện thoại Samsung")

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack**: Thêm node Slack để nhận thông báo khi có sản phẩm mới
- **Lưu log tìm kiếm**: Thêm node Google Sheets để lưu lịch sử tìm kiếm
- **Mở rộng phạm vi tìm kiếm**: Thêm các node để tìm kiếm trên các trang thương mại khác
- **Tự động gửi báo cáo**: Lập lịch gửi báo cáo hàng ngày về các sản phẩm được tìm kiếm nhiều nhất

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc tìm kiếm thông tin sản phẩm Amazon. Với tích hợp AI thông minh, bot có thể phân biệt giữa tìm kiếm sản phẩm và trò chuyện thông thường, mang lại trải nghiệm sử dụng tốt hơn. Hãy thử ngay và nâng cao hiệu suất làm việc của mình!