---
title: "🚀 Tự động hóa sáng tạo quảng cáo từ ảnh sản phẩm bằng Gemini Vision và Claude qua Telegram"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình tạo nội dung quảng cáo từ ảnh sản phẩm bằng công nghệ AI Gemini Vision và Claude, gửi kết quả qua Telegram"
slug: "tu-dong-hoa-tao-quang-cao-tu-anh-san-pham-bang-gemini-vision-va-claude-qua-telegram"
tags: [n8n, automation, no-code, AI, content creation]
keywords: [n8n workflow, tự động hóa, AI tạo quảng cáo, Gemini Vision, Claude, Telegram]
---

# 🚀 Tự động hóa sáng tạo quảng cáo từ ảnh sản phẩm bằng Gemini Vision và Claude qua Telegram

[Các sếp] có bao giờ phải mất hàng giờ để tạo nội dung quảng cáo từ những bức ảnh sản phẩm đơn giản? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ phân tích sản phẩm đến tạo hình ảnh quảng cáo hoàn chỉnh, chỉ với một bức ảnh gửi qua Telegram.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tạo nội dung quảng cáo trong vài phút thay vì hàng giờ
- **Chính xác cao**: Phân tích sản phẩm và tạo nội dung theo tiêu chuẩn chuyên nghiệp
- **Cá nhân hóa**: Tạo nhiều phiên bản quảng cáo khác nhau từ một ảnh sản phẩm
- **Hoạt động liên tục**: Tạo nội dung bất cứ lúc nào trong ngày, 24/7
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot token (tạo qua BotFather)
- User ID Telegram của các sếp (lấy qua @userinfobot)
- Google Gemini API Key
- OpenRouter API Key (để sử dụng Claude)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/11190](https://n8n.io/workflows/11190)
2. Click vào nút "Import" ở góc trên bên phải
3. Trong n8n Editor, chọn "Import from URL" và dán link trên
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node CONFIG**:
   - Mở node "CONFIG" (màu xanh lá)
   - Thêm tham số `authorized_user_id` với giá trị là User ID Telegram của các sếp

2. **Node On New Message**:
   - Thêm credentials "telegramApi" với token bot của các sếp

3. **Node Gemini Vision: Analyze**:
   - Thêm credentials "googlePalmApi" với Google Gemini API Key

4. **Node OpenRouter Chat Model**:
   - Thêm credentials "openRouterApi" với OpenRouter API Key

5. **Node Telegram: Send Result**:
   - Thêm credentials "telegramApi" với token bot của các sếp

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu:
   - Gửi một bức ảnh sản phẩm bất kỳ đến bot Telegram của các sếp
   - Kiểm tra kết quả trả về trong Telegram
2. Bật Active workflow sau khi đã kiểm tra thành công

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack**: Thay thế node Telegram bằng node Slack để nhận kết quả qua Slack
2. **Lưu log hoạt động**: Thêm node lưu log hoạt động vào workflow để theo dõi lịch sử tạo nội dung
3. **Tạo báo cáo định kỳ**: Thiết lập gửi báo cáo tổng hợp nội dung đã tạo hàng tuần qua email
4. **Tích hợp với CRM**: Kết nối với hệ thống CRM để lưu trữ các phiên bản quảng cáo đã tạo

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc tạo nội dung quảng cáo. Với sự kết hợp của Gemini Vision và Claude, các sếp có thể tạo ra những nội dung quảng cáo chuyên nghiệp, cá nhân hóa và phù hợp với từng sản phẩm. Hãy thử ngay và trải nghiệm cách làm việc hiệu quả hơn với công nghệ AI!