---
title: "📍 [Tự động hóa] Nhận thông báo về các chợ đồ cũ gần nhà qua Telegram mỗi sáng"
description: "Workflow n8n tự động tìm kiếm và gửi thông báo về các chợ đồ cũ trong bán kính 20km quanh vị trí hiện tại của bạn mỗi sáng lúc 7h qua Telegram. Tiết kiệm thời gian và không bỏ lỡ cơ hội mua sắm."
slug: "tu-dong-hoa-cho-do-cu-qua-telegram-moi-sang"
tags: [n8n, automation, no-code, telegram, home-assistant]
keywords: [n8n workflow, tự động hóa, chợ đồ cũ, telegram, home assistant]
---

# 📍 [Tự động hóa] Nhận thông báo về các chợ đồ cũ gần nhà qua Telegram mỗi sáng

[Các sếp] có biết không? Mỗi ngày bạn phải tốn thời gian tìm kiếm thông tin về các chợ đồ cũ gần nhà để không bỏ lỡ cơ hội mua sắm hấp dẫn? Với workflow này, n8n sẽ tự động tìm kiếm và gửi thông báo về các chợ đồ cũ trong bán kính 20km quanh vị trí hiện tại của bạn mỗi sáng lúc 7h qua Telegram. Không cần phải nhớ hoặc tra cứu thủ công nữa!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải tra cứu thông tin chợ đồ cũ mỗi ngày.
- **Nhận thông tin kịp thời**: Nhận thông báo về các chợ đồ cũ gần nhà mỗi sáng lúc 7h.
- **Tăng cơ hội mua sắm**: Không bỏ lỡ cơ hội mua sắm các mặt hàng hiếm có hoặc giá tốt.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công sau khi cài đặt.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot Telegram đã được tạo.
- Tài khoản Home Assistant với sensor vị trí đã được thiết lập.
- API key của Home Assistant.
- Tài khoản Brocabrac.fr (nếu cần).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/4649](https://n8n.io/workflows/4649).
3. Hoặc tải file JSON từ link trên và import vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Get location"**: Cần cấu hình credentials cho Home Assistant API và chọn resource là "state".
- **Node "Set URL to parse"**: Cần cấu hình URL động dựa trên vị trí hiện tại của bạn.
- **Node "Extract Date & Blocks"**: Cần cấu hình để trích xuất dữ liệu từ trang Brocabrac.fr.
- **Node "Filter on close and bigger events"**: Cần cấu hình để lọc các sự kiện trong bán kính 20km và có rank.
- **Node "Send an Alert"**: Cần cấu hình credentials cho Telegram API và chọn chat ID để gửi thông báo.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow để chạy tự động mỗi sáng lúc 7h.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack**: Thay vì gửi thông báo qua Telegram, các sếp có thể cấu hình để gửi thông báo qua Slack.
- **Lưu log**: Các sếp có thể thêm node để lưu log các sự kiện đã được xử lý.
- **Gửi báo cáo định kỳ**: Các sếp có thể cấu hình để gửi báo cáo định kỳ về các chợ đồ cũ đã được xử lý.
- **Thêm điều kiện lọc**: Các sếp có thể thêm điều kiện lọc để chỉ nhận thông báo về các chợ đồ cũ có giá trị cao.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và không bỏ lỡ cơ hội mua sắm các mặt hàng hiếm có hoặc giá tốt. Với việc tự động hóa hoàn toàn, các sếp có thể tập trung vào những việc quan trọng hơn. Hãy thử ngay và trải nghiệm sự tiện lợi của tự động hóa!