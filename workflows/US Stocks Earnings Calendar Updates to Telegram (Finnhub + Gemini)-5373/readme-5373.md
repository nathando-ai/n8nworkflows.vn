---
title: "🚀 Tự động hóa lịch báo cáo cổ phiếu Mỹ tới Telegram với Finnhub + Gemini"
description: "Hướng dẫn tự động hóa quy trình theo dõi lịch báo cáo tài chính của cổ phiếu Mỹ và gửi thông báo tới Telegram mỗi 3 ngày với n8n, Finnhub và Google Gemini"
slug: "tu-dong-hoa-lich-bao-cao-co-phieu-my-toi-telegram"
tags: [n8n, automation, no-code, finnhub, telegram]
keywords: [n8n workflow, tự động hóa, lịch báo cáo cổ phiếu, Finnhub, Google Gemini]
---

# 🚀 Tự động hóa lịch báo cáo cổ phiếu Mỹ tới Telegram với Finnhub + Gemini

[Các sếp] có biết không? Theo dõi lịch báo cáo tài chính của cổ phiếu Mỹ thủ công là một công việc cực kỳ tốn thời gian và dễ gây lỗi. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ việc lấy dữ liệu tới gửi thông báo tới Telegram mỗi 3 ngày, mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi thủ công lịch báo cáo hàng ngày
- **Chính xác cao**: Dữ liệu được lấy từ nguồn đáng tin cậy (Finnhub)
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công sau khi cài đặt
- **Thông báo tức thì**: Nhận cập nhật mới nhất về lịch báo cáo qua Telegram
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Finnhub (để lấy dữ liệu lịch báo cáo)
- API Key của Google Gemini (để xử lý dữ liệu)
- Bot Telegram và Chat ID (để gửi thông báo)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc](https://n8n.io/workflows/5373)
2. Click vào nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON vừa sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Set API Key for Finhubb & Dates"**:
   - Thêm API Key của Finnhub vào biến `finnhub_api_key`
   - Cấu hình các ngày cần theo dõi (ví dụ: 3 ngày tới)

2. **Node "Google Gemini Chat Model (Formats Output)"**:
   - Thêm API Key của Google Gemini vào credentials
   - Đảm bảo model được chọn hỗ trợ xử lý dữ liệu tài chính

3. **Node "Send Upcoming Earning Updates via Telegram"**:
   - Cấu hình credentials với Bot Token và Chat ID của Telegram
   - Tùy chỉnh nội dung thông báo theo nhu cầu

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra kết quả
2. Bật Active workflow để bắt đầu nhận thông báo hàng ngày

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để lưu log các thông báo đã gửi
- Kết hợp với Slack để nhận thông báo trên cả hai nền tảng
- Tùy chỉnh lịch gửi thông báo (ví dụ: chỉ nhận thông báo vào cuối tuần)
- Thêm node để gửi báo cáo định kỳ (ví dụ: báo cáo hàng tháng về các cổ phiếu có lịch báo cáo sắp tới)

### 📌 Kết luận
Với workflow này, các sếp có thể hoàn toàn tự động hóa quy trình theo dõi lịch báo cáo cổ phiếu Mỹ và nhận thông báo tức thì qua Telegram. Hãy thử ngay để tiết kiệm thời gian và giảm thiểu rủi ro trong đầu tư cổ phiếu!