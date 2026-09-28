---
title: "✈️ Tự động hóa tính toán CO2 cho chuyến bay doanh nghiệp với Carbon Interface API và GPT-4o"
description: "Hướng dẫn tự động hóa tính toán lượng CO2 phát thải từ chuyến bay doanh nghiệp bằng n8n, Carbon Interface API và GPT-4o. Tiết kiệm thời gian và nâng cao tính bền vững cho doanh nghiệp."
slug: "tu-dong-hoa-tinh-toan-co2-chuyen-bay-doanh-nghiep"
tags: [n8n, automation, no-code, carbon, sustainability, ai]
keywords: [n8n workflow, tự động hóa, carbon interface, gpt-4o, tính toán co2]
---

# ✈️ Tự động hóa tính toán CO2 cho chuyến bay doanh nghiệp với Carbon Interface API và GPT-4o

[Các sếp] có biết rằng mỗi chuyến bay của nhân viên doanh nghiệp lại phát thải lượng CO2 đáng kể không? Với workflow này, các sếp có thể tự động hóa quy trình tính toán lượng CO2 phát thải từ các chuyến bay doanh nghiệp một cách nhanh chóng và chính xác, giúp doanh nghiệp tuân thủ các quy định về bền vững và tiết kiệm chi phí.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quy trình tính toán CO2 phát thải từ chuyến bay doanh nghiệp.
- Chính xác: Sử dụng Carbon Interface API để tính toán lượng CO2 phát thải một cách chính xác.
- Cá nhân hóa: Tùy chỉnh prompt cho AI Agent để phù hợp với định dạng email của doanh nghiệp.
- Hoạt động liên tục: Workflow chạy tự động 24/7, không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail để thiết lập Gmail Trigger.
- API Key từ Carbon Interface để tính toán lượng CO2 phát thải.
- API Key từ OpenAI để sử dụng GPT-4o.
- Tài khoản Google Sheets để lưu trữ dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào [n8n.io/workflows/4756](https://n8n.io/workflows/4756) để tải file JSON của workflow.
2. Trong n8n Editor, nhấn vào **Import from File** và chọn file JSON đã tải về.
3. Hoặc, copy toàn bộ nội dung JSON và paste vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Gmail Trigger Node**: Thiết lập credentials cho Gmail API.
- **OpenAI Chat Model2 Node**: Thiết lập credentials cho OpenAI API và chọn model là `gpt-4o-mini`.
- **AI Agent Parser Node**: Tùy chỉnh prompt để phù hợp với định dạng email của doanh nghiệp.
- **Collect CO2 Emissions Node**: Thiết lập API Key từ Carbon Interface.
- **Record Flights Information Node**: Thiết lập credentials cho Google Sheets API và chọn file, sheet để lưu trữ dữ liệu.
- **Load Results Node**: Thiết lập credentials cho Google Sheets API và chọn file, sheet để lưu trữ kết quả.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật Active workflow để chạy tự động khi có email mới.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để thông báo kết quả tính toán CO2 phát thải.
- Lưu log các lần chạy workflow để theo dõi hiệu suất.
- Gửi báo cáo định kỳ về lượng CO2 phát thải của doanh nghiệp.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình tính toán lượng CO2 phát thải từ chuyến bay doanh nghiệp một cách nhanh chóng và chính xác. Với việc sử dụng Carbon Interface API và GPT-4o, các sếp có thể đảm bảo tính chính xác và tính bền vững cho doanh nghiệp. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất làm việc!