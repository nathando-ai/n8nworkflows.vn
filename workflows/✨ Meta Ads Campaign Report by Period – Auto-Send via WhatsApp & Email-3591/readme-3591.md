---
title: "✨ Tự động báo cáo chiến dịch Meta Ads theo kỳ hạn và gửi qua WhatsApp & Email"
description: "Workflow n8n giúp tự động tổng hợp dữ liệu quảng cáo Meta Ads theo kỳ hạn, lọc các chiến dịch có hiệu quả và gửi báo cáo qua WhatsApp và Email một cách tự động."
slug: "tu-dong-bao-cao-chien-dich-meta-ads-theo-ky-han-va-gui-qua-whatsapp-email"
tags: [n8n, automation, no-code, marketing, meta-ads]
keywords: [n8n workflow, tự động hóa, báo cáo quảng cáo, meta ads, gửi email tự động]
---

# ✨ Tự động báo cáo chiến dịch Meta Ads theo kỳ hạn và gửi qua WhatsApp & Email

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Khi quản lý nhiều tài khoản quảng cáo Meta Ads, việc theo dõi hiệu suất từng chiến dịch theo kỳ hạn là một công việc tốn thời gian và dễ gây lỗi. Các sếp thường phải:

- Xem từng tài khoản quảng cáo để lấy dữ liệu
- Tổng hợp dữ liệu theo kỳ hạn (tuần, tháng, quý)
- Lọc các chiến dịch có hiệu quả (chuyển đổi)
- Gửi báo cáo qua email và WhatsApp cho các bộ phận liên quan

Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này trong vòng 15 phút, giảm thiểu lỗi và tiết kiệm thời gian đáng kể.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 2-3 giờ mỗi tuần cho việc tổng hợp báo cáo thủ công
- Dữ liệu báo cáo chính xác và cập nhật tự động
- Báo cáo được gửi tự động qua email và WhatsApp cho các bộ phận liên quan
- Hoạt động liên tục 24/7 mà không cần can thiệp
- Dễ dàng mở rộng cho nhiều tài khoản quảng cáo
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Meta Ads với quyền truy cập API
- Tài khoản Google Workspace (để gửi email thông qua Gmail)
- API key của dịch vụ gửi tin nhắn WhatsApp (ví dụ: Twilio, WhatsApp Business API)
- Google Sheet để lưu trữ dữ liệu tạm thời (tùy chọn)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/3591](https://n8n.io/workflows/3591)
2. Nhấn nút "Download" để tải file JSON workflow
3. Trong n8n Editor, nhấn nút "Import from File" và chọn file JSON vừa tải về

Hoặc copy/paste JSON sau vào n8n Editor:

```json
{
  "nodes": [
    // Danh sách các nodes trong workflow
  ],
  "connections": [
    // Danh sách các kết nối giữa các nodes
  ]
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**Node "Start Time" (scheduleTrigger):**
- Cấu hình thời gian chạy workflow (ví dụ: hàng tuần vào thứ Hai lúc 8h sáng)
- Thiết lập múi giờ phù hợp với khu vực của các sếp

**Node "Ad Accounts" (googleSheets):**
- Thiết lập Google Sheet chứa danh sách tài khoản Meta Ads cần theo dõi
- Cấu hình credentials cho Google Sheets
- Đảm bảo Google Sheet có định dạng: `Tên tài khoản | ID tài khoản | Email nhận báo cáo | Số điện thoại nhận báo cáo`

**Node "Ads by Period" (facebookGraphApi):**
- Cấu hình credentials cho Meta Ads API
- Thiết lập các tham số:
  - `time_range`: Thời gian theo dõi (ví dụ: `{"since":"2023-01-01","until":"2023-01-31"}`)
  - `fields`: Các chỉ số cần theo dõi (ví dụ: `impressions, clicks, spend, conversions`)

**Node "Send by Email" (gmail):**
- Cấu hình credentials cho Gmail
- Thiết lập email nhận báo cáo (có thể lấy từ Google Sheet)
- Tùy chỉnh nội dung email bao gồm các chỉ số chính

**Node "Send by WhatsApp" (httpRequest):**
- Cấu hình API endpoint của dịch vụ gửi tin nhắn WhatsApp
- Thiết lập các tham số:
  - `to`: Số điện thoại nhận báo cáo (có thể lấy từ Google Sheet)
  - `body`: Nội dung tin nhắn bao gồm các chỉ số chính

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Execute Workflow" để test với dữ liệu mẫu
2. Kiểm tra kết quả tại các node cuối cùng (Send by Email và Send by WhatsApp)
3. Nếu kết quả đúng, nhấn nút "Activate" để chạy workflow tự động theo lịch trình

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node "Slack" để gửi báo cáo qua Slack channel
- Lưu log báo cáo vào Google Sheet để theo dõi lịch sử
- Tạo báo cáo định kỳ (tuần, tháng, quý) với các chỉ số khác nhau
- Kết hợp với workflow khác để tự động hóa các hành động tiếp theo (ví dụ: điều chỉnh ngân sách quảng cáo)

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình báo cáo hiệu suất quảng cáo Meta Ads, tiết kiệm thời gian và giảm thiểu lỗi. Với việc cấu hình đơn giản và chạy tự động, các sếp có thể tập trung vào các chiến lược quan trọng hơn. Hãy áp dụng ngay để tối ưu hóa hiệu suất quảng cáo của các sếp!