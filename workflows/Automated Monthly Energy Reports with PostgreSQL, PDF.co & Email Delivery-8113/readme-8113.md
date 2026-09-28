---
title: "🚀 Tự động tạo Báo cáo Năng lượng Tháng - Postgres → PDF → Email"
description: "Giải pháp tự động gửi báo cáo năng lượng hàng tháng, lấy dữ liệu từ PostgreSQL, chuyển thành PDF và gửi qua Gmail, hoàn toàn không cần code."
slug: "bao-cao-nang-luong-thang"
tags: [n8n, automation, no-code, postgres, pdf, gmail]
keywords: [n8n workflow, tự động hóa, báo cáo năng lượng, PDF, email]
---

# 🚀 Tự động tạo Báo cáo Năng lượng Tháng

Bạn đang phải mất hàng giờ mỗi tháng để trích xuất dữ liệu, tạo báo cáo PDF và gửi email? Đừng lo, workflow này sẽ giúp bạn **tự động hoàn thành mọi bước** chỉ trong vài phút, không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ → vài phút.
- **Độ chính xác cao**: Dữ liệu lấy trực tiếp từ DB, tránh lỗi nhập liệu thủ công.
- **Tự động hóa 24/7**: Báo cáo được gửi đúng thời gian, không cần nhắc nhở.
- **Tích hợp dễ dàng**: Chỉ cần cấu hình credentials, workflow sẵn sàng.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
| Tài khoản / Dịch vụ | Mô tả | Lưu ý |
|----------------------|-------|-------|
| **PostgreSQL** | Cơ sở dữ liệu chứa bảng `energy_data`. | Cần có `host`, `port`, `database`, `user`, `password`. |
| **PDF.co** | API chuyển JSON thành PDF. | Đăng ký API Key tại <https://pdf.co/>. |
| **Gmail** | Gửi email. | Cấu hình OAuth2 (đăng nhập Google, cấp quyền). |
| **n8n** | Platform tự động hóa. | Đảm bảo n8n chạy ổn định, có kết nối internet. |
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON từ <https://n8n.io/workflows/8113> hoặc sao chép nội dung JSON.
2. Mở **n8n Editor**, chọn **Import** → **Import from Clipboard** hoặc **Import from File**.
3. Dán JSON và nhấn **Import**. Workflow sẽ xuất hiện trong danh sách.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên | Cấu hình cần chỉnh | Mô tả |
|------|-----|---------------------|-------|
| **Monthly Trigger** | `Monthly Trigger` | `Month`, `Day`, `Time` | Đặt thời gian gửi báo cáo (ví dụ: 1/1/00:00). |
| **Get energy data** | `Get energy data` | `Connection` (PostgreSQL), `Query` | Ví dụ: `SELECT * FROM energy_data WHERE date >= DATE_TRUNC('month', CURRENT_DATE) AND date < DATE_TRUNC('month', CURRENT_DATE) + INTERVAL '1 month';` |
| **Transform data** | `Transform data` | `Code` | Đảm bảo `items[0].json` chứa dữ liệu từ Postgres. Code mẫu: <br>`return items.map(item => { const data = item.json; return { json: { date_range: data.date_range, note: data.note, records: data.records } }; });` |
| **Convert data to pdf** | `Convert data to pdf` | `URL` (PDF.co endpoint), `API Key`, `Body` (JSON) | Endpoint: `https://api.pdf.co/v1/pdf/convert/from/json`. Body: `{{ $json }}`. |
| **Send Report** | `Send Report` | `Credentials` (gmailOAuth2), `To`, `Subject`, `Body` | Body: `Báo cáo năng lượng tháng {{ $json.date_range }} đã được tạo. <a href="{{ $json.pdfUrl }}">Tải PDF</a>`. |

> **Tip**: Kiểm tra `Output` của từng node trong **n8n Editor** để đảm bảo dữ liệu chảy đúng.

### 3. Kích hoạt ⚡️

1. **Test run**: Nhấn **Execute Workflow** với dữ liệu mẫu (có thể dùng `Mock` data trong Postgres node).
2. Kiểm tra **Logs**: Đảm bảo không có lỗi.
3. Khi OK, bật **Active** (đánh dấu nút xanh).
4. Workflow sẽ chạy tự động theo lịch đã đặt.

## ✍️ Mẹo & gợi ý nâng cao

- **Gửi PDF đính kèm**: Thay vì gửi link, dùng `Send Report` node để đính kèm file PDF (`pdfUrl` → download → attach).
- **Lưu trữ PDF**: Thêm node `S3` hoặc `Google Drive` để lưu trữ bản PDF sau khi tạo.
- **Thông báo Slack**: Thêm node `Slack` để gửi tin nhắn khi báo cáo đã gửi thành công.
- **Định kỳ báo cáo**: Thêm node `Schedule Trigger` khác để gửi báo cáo tuần hoặc hàng ngày.

## 📌 Kết luận

Workflow “Automated Monthly Energy Reports with PostgreSQL, PDF.co & Email Delivery” là công cụ **đơn giản nhưng mạnh mẽ** giúp các sếp tiết kiệm thời gian, giảm sai sót và tăng tính chuyên nghiệp trong báo cáo năng lượng. Hãy thử triển khai ngay hôm nay, và cảm nhận sự khác biệt!

---