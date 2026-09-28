---
title: "🚀 Tự động phân loại và xử lý yêu cầu liên hệ từ khách hàng bằng GPT-4.1, Gmail và Telegram"
description: "Hướng dẫn tự động hóa xử lý yêu cầu liên hệ từ khách hàng bằng n8n, kết hợp AI phân loại, gửi email tự động và thông báo Telegram"
slug: "tu-dong-phan-loai-yeu-cau-lien-he-khach-hang"
tags: [n8n, automation, no-code, ai, customer-service]
keywords: [n8n workflow, tự động hóa, phân loại yêu cầu, xử lý liên hệ, AI chatbot]
---

# 🚀 Tự động phân loại và xử lý yêu cầu liên hệ từ khách hàng bằng GPT-4.1, Gmail và Telegram

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động phân loại yêu cầu liên hệ thành 3 loại: hợp lệ, seller và spam
- Tự động gửi email xác nhận cá nhân hóa cho khách hàng hợp lệ
- Thông báo ngay cho team qua Telegram khi có yêu cầu mới
- Lưu trữ dữ liệu yêu cầu vào bảng dữ liệu (DataTable)
- Tiết kiệm thời gian xử lý thủ công lên đến 90%
- Tăng trải nghiệm khách hàng với email tự động chuyên nghiệp
- Giảm rủi ro bỏ lỡ yêu cầu quan trọng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail với quyền truy cập API (đã bật Gmail API và OAuth2)
- API Key từ OpenAI (đã đăng ký tài khoản và có credit)
- Bot Telegram và Chat ID để nhận thông báo
- Bảng dữ liệu (DataTable) để lưu trữ thông tin yêu cầu
- Form liên hệ trên website đã cấu hình gửi dữ liệu đến webhook
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [n8n.io/workflows/14593](https://n8n.io/workflows/14593)
2. Nhấn nút "Import" trên trang workflow
3. Trong n8n Editor, chọn "Import from URL" và dán link workflow
4. Hoàn tất import và mở workflow trong Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Webhook Node**:
   - Kiểm tra và cập nhật đường dẫn webhook (path) nếu cần
   - Đảm bảo form liên hệ trên website gửi dữ liệu đến đúng endpoint

2. **Gmail Nodes**:
   - Cấu hình credentials cho Gmail OAuth2
   - Xác minh địa chỉ email gửi trong node "Send message to Client"
   - Kiểm tra cấu hình trong node "Send a notification"

3. **OpenAI Nodes**:
   - Cấu hình credentials cho OpenAI API
   - Đảm bảo tài khoản OpenAI có đủ credit
   - Kiểm tra các node "OpenAI Chat Model" và "OpenAI Chat Model1" đã chọn đúng model (gpt-4.1-mini và gpt-4.1-nano)

4. **Telegram Nodes**:
   - Cấu hình credentials cho Telegram Bot
   - Cập nhật Chat ID để nhận thông báo
   - Kiểm tra các node "Send a text message" và "Send a text message1"

5. **DataTable Nodes**:
   - Cấu hình kết nối đến bảng dữ liệu của bạn
   - Đảm bảo cấu trúc bảng phù hợp với dữ liệu đầu vào

6. **Set Data Node**:
   - Cập nhật thông tin công ty trong trường "Our Company Information"
   - Điều chỉnh tone và mô tả công ty theo nhu cầu

7. **Chain LLM Nodes**:
   - Kiểm tra và điều chỉnh prompt trong node "Analyze intend" nếu cần
   - Tùy chỉnh prompt trong node "Personalized auto respond" để thay đổi tone email xác nhận

#### 3. Kích hoạt ⚡️
1. Thực hiện test run với dữ liệu mẫu để kiểm tra toàn bộ luồng
2. Kiểm tra các thông báo Telegram và email được gửi
3. Kiểm tra dữ liệu đã được lưu vào bảng dữ liệu
4. Bật Active workflow khi đã kiểm tra và xác nhận mọi thứ hoạt động đúng

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack để nhận thông báo thay vì Telegram
2. Thêm node lưu log hoạt động để theo dõi hiệu suất
3. Tạo báo cáo hàng ngày về số lượng yêu cầu đã xử lý
4. Thêm node xử lý lỗi để thông báo khi có vấn đề xảy ra
5. Tùy chỉnh email xác nhận để bao gồm thông tin sản phẩm/dịch vụ liên quan

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình xử lý yêu cầu liên hệ từ khách hàng, từ phân loại đến phản hồi tự động. Với sự kết hợp của AI, Gmail và Telegram, các sếp có thể tiết kiệm thời gian đáng kể và cung cấp trải nghiệm khách hàng chuyên nghiệp hơn. Hãy áp dụng ngay để nâng cao hiệu quả làm việc của đội ngũ!