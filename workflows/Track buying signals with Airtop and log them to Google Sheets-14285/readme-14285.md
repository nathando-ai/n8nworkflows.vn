---
title: "🚀 Theo dõi tín hiệu mua hàng với Airtop và lưu vào Google Sheets"
description: "Tự động theo dõi các tài khoản mục tiêu trên LinkedIn và các nguồn tin để phát hiện các tín hiệu mua hàng như tuyển dụng, ra mắt sản phẩm, vòng gọi vốn - và lưu trực tiếp vào Google Sheets."
slug: "theo-doi-tin-hieu-mua-hang-voi-airtop-va-google-sheets"
tags: [n8n, automation, no-code, market-research, ai-summarization]
keywords: [n8n workflow, tự động hóa, theo dõi thị trường, tín hiệu mua hàng, Google Sheets]
---

# 🚀 Theo dõi tín hiệu mua hàng với Airtop và lưu vào Google Sheets

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải theo dõi thủ công các tài khoản mục tiêu trên LinkedIn và các nguồn tin để phát hiện các tín hiệu mua hàng quan trọng? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này chỉ trong vài phút!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi thủ công hàng ngày.
- **Chính xác cao**: Phát hiện các tín hiệu mua hàng quan trọng một cách tự động.
- **Dễ quản lý**: Tất cả dữ liệu được lưu trữ và tổ chức trong Google Sheets.
- **Hoạt động liên tục**: Theo dõi 24/7 mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Airtop với template [Real-Time Buying Signals Agent](https://www.airtop.ai/templates/multi-source-b2b-buying-signal-monitor?utm_source=n8n-template) đã được cài đặt.
- Tài khoản Google với quyền truy cập vào Google Sheets.
- API Key từ Airtop.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL".
3. Dán link sau vào ô nhập liệu: `https://n8n.io/workflows/14285`.
4. Nhấn "Import".

Hoặc, các sếp có thể tải file JSON từ [đây](https://n8n.io/workflows/14285) và import thủ công.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Run 'The Real-Time Buying Signals Agent'"**:
  - Chọn credentials là `airtopApi`.
  - Đảm bảo template [Real-Time Buying Signals Agent](https://www.airtop.ai/templates/multi-source-b2b-buying-signal-monitor?utm_source=n8n-template) đã được cài đặt trong tài khoản Airtop của các sếp.

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút "Execute Workflow" để chạy thử.
2. Kiểm tra kết quả trên Google Sheets.
3. Nếu mọi thứ hoạt động tốt, nhấn vào nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node để gửi thông báo tức thời khi phát hiện tín hiệu mua hàng quan trọng.
- **Lưu log chi tiết**: Thêm node để lưu log chi tiết của các hoạt động phát hiện tín hiệu mua hàng.
- **Gửi báo cáo định kỳ**: Tự động gửi báo cáo hàng tuần/tuần về các tín hiệu mua hàng quan trọng đến email của các sếp.

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa việc theo dõi tín hiệu mua hàng một cách hiệu quả và chính xác. Hãy áp dụng ngay để tiết kiệm thời gian và tăng cường hiệu quả trong việc nghiên cứu thị trường!