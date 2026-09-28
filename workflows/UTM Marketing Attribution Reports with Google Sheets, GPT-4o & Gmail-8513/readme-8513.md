---
title: "📊 Tự động hóa báo cáo UTM Marketing với Google Sheets, GPT-4o & Gmail"
description: "Hướng dẫn tự động hóa báo cáo UTM Marketing với n8n, Google Sheets, GPT-4o và Gmail. Tiết kiệm thời gian và nâng cao hiệu quả marketing của bạn."
slug: "tu-dong-hoa-bao-cao-utm-marketing-voi-google-sheets-gpt-4o-gmail"
tags: [n8n, automation, no-code, marketing, google-sheets]
keywords: [n8n workflow, tự động hóa marketing, báo cáo UTM, GPT-4o, Google Sheets]
---

# 📊 Tự động hóa báo cáo UTM Marketing với Google Sheets, GPT-4o & Gmail

[Các sếp marketing] đang gặp khó khăn khi phải thủ công tổng hợp dữ liệu từ nhiều nguồn khác nhau để tạo báo cáo UTM Marketing hàng tuần. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ lấy dữ liệu đến gửi báo cáo qua email, giúp tiết kiệm thời gian và nâng cao hiệu quả marketing.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quy trình báo cáo hàng tuần.
- Chính xác: Dữ liệu được tổng hợp và phân tích một cách chính xác.
- Cá nhân hóa: Báo cáo được tạo ra dựa trên dữ liệu thực tế của doanh nghiệp.
- Hoạt động liên tục: Workflow chạy tự động mỗi giờ, đảm bảo dữ liệu luôn cập nhật.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets.
- Tài khoản Gmail để gửi báo cáo.
- API Key từ Azure OpenAI để sử dụng GPT-4o.
- Google Sheet chứa dữ liệu lead (Form responses 1).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấn vào nút "Import from URL" và nhập URL: [https://n8n.io/workflows/8513](https://n8n.io/workflows/8513).
3. Hoặc, bạn có thể tải file JSON từ link trên và import trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Schedule Trigger**:
   - Cấu hình thời gian chạy workflow (mặc định là mỗi giờ).

2. **Get row(s) in sheet**:
   - Chọn credentials Google Sheets.
   - Điền thông tin Sheet ID và tên Sheet (Form responses 1).

3. **Azure OpenAI Chat Model1**:
   - Chọn credentials Azure OpenAI.
   - Đảm bảo model được cấu hình là `gpt-4o-mini`.

4. **Send Follow-up Email1**:
   - Chọn credentials Gmail.
   - Cấu hình địa chỉ email nhận báo cáo.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật Active workflow để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để thông báo khi báo cáo được gửi.
- Lưu log báo cáo vào Google Sheets để theo dõi lịch sử.
- Gửi báo cáo định kỳ theo tuần/tháng để đánh giá hiệu quả marketing.

### 📌 Kết luận
Workflow này giúp các sếp marketing tự động hóa toàn bộ quy trình báo cáo UTM Marketing, tiết kiệm thời gian và nâng cao hiệu quả marketing. Hãy áp dụng ngay để thấy kết quả ngay lập tức!