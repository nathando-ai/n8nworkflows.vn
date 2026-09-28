---
title: "📊 Theo dõi lượng calo và cân nặng bằng Gemini, Google Sheets, Gmail và QuickChart"
description: "Hướng dẫn tự động hóa theo dõi sức khỏe cá nhân với n8n: ghi nhận dữ liệu, phân tích AI, tạo biểu đồ và gửi báo cáo tự động qua email."
slug: "theo-doi-suc-khoe-voi-n8n-gemini-googlesheets"
tags: [n8n, automation, no-code, sức khỏe, AI]
keywords: [n8n workflow, tự động hóa sức khỏe, theo dõi cân nặng, phân tích calo, Google Sheets]
---

# 📊 Theo dõi lượng calo và cân nặng bằng Gemini, Google Sheets, Gmail và QuickChart

[Các sếp] có bao giờ cảm thấy việc ghi chép và phân tích dữ liệu sức khỏe hàng ngày lại tốn thời gian và dễ gây nhầm lẫn không? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ ghi nhận dữ liệu đến gửi báo cáo qua email chỉ trong vài phút!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động ghi nhận và phân tích dữ liệu sức khỏe hàng ngày
- **Chính xác cao**: Sử dụng AI Gemini để ước tính lượng calo từ mô tả bữa ăn
- **Hình ảnh hóa dữ liệu**: Tạo biểu đồ xu hướng cân nặng và lượng calo
- **Báo cáo tự động**: Nhận báo cáo sức khỏe hàng ngày qua email
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets, Gmail đã kích hoạt
- API Key từ Google Gemini
- Biết cách tạo và chia sẻ Google Sheet (cần ID của sheet)
- Biết cách tạo và cấu hình OAuth2 cho Google Sheets và Gmail
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/12844)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Configuration"**:
   - Thay đổi tham số `sheetId` bằng ID của Google Sheet của bạn
   - Cập nhật giá trị `bmr` (Basal Metabolic Rate) theo chỉ số của bạn

2. **Node "Gemini: Calc"**:
   - Đảm bảo đã cấu hình credentials cho Google Gemini
   - Kiểm tra prompt trong node để đảm bảo nó phù hợp với nhu cầu phân tích của bạn

3. **Node "Save Today" và "Get History"**:
   - Đảm bảo đã cấu hình credentials cho Google Sheets
   - Kiểm tra tên sheet và phạm vi dữ liệu trong node

4. **Node "Send Email"**:
   - Đảm bảo đã cấu hình credentials cho Gmail
   - Cập nhật địa chỉ email nhận báo cáo

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra kết quả trong Google Sheet và email
3. Bật Active workflow để bắt đầu theo dõi sức khỏe hàng ngày

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm node để gửi báo cáo đến các kênh thông báo khác
2. **Lưu log hoạt động**: Thêm node để lưu nhật ký hoạt động của workflow
3. **Tự động hóa báo cáo tuần/tháng**: Thay đổi tần suất gửi báo cáo từ hàng ngày sang tuần/tháng
4. **Thêm chỉ số sức khỏe khác**: Mở rộng workflow để theo dõi các chỉ số khác như huyết áp, huyết áp,...

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình theo dõi sức khỏe hàng ngày, từ ghi nhận dữ liệu đến gửi báo cáo qua email. Với sự hỗ trợ của AI Gemini, các sếp có thể nhận được phân tích chính xác về lượng calo và cân nặng, giúp cải thiện lối sống lành mạnh hơn. Hãy áp dụng ngay để bắt đầu cuộc hành trình sức khỏe tốt hơn!