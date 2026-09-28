---
title: "🚀 Theo dõi và Trực quan hóa tâm trạng hàng ngày với GPT-4o, Wolfram Alpha, Sheets và Slack"
description: "Hướng dẫn tự động hóa theo dõi tâm trạng hàng ngày, phân tích bằng AI, tạo biểu đồ và lưu vào Google Sheets - hoàn toàn không cần code"
slug: "theo-doi-tam-trang-hang-ngay-voi-ai"
tags: [n8n, automation, no-code, google-sheets, ai, wolfram-alpha, slack]
keywords: [n8n workflow, tự động hóa, tâm trạng hàng ngày, AI phân tích, biểu đồ, Google Sheets]
---

# 🚀 Theo dõi và Trực quan hóa tâm trạng hàng ngày với GPT-4o, Wolfram Alpha, Sheets và Slack

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có biết không? Theo dõi tâm trạng hàng ngày là một thói quen tuyệt vời để tự nhận thức bản thân, nhưng khi làm thủ công thì tốn thời gian và dễ bị bỏ qua. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình: từ ghi nhận tâm trạng đến phân tích bằng AI, tạo biểu đồ và lưu trữ dữ liệu - chỉ với vài bước cấu hình đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình theo dõi tâm trạng hàng ngày
- **Phân tích chính xác**: Sử dụng AI GPT-4o để chuyển đổi tâm trạng thành chỉ số valence và energy
- **Trực quan hóa dữ liệu**: Tạo biểu đồ thời gian bằng Wolfram Alpha để theo dõi xu hướng tâm trạng
- **Lưu trữ an toàn**: Tất cả dữ liệu được lưu vào Google Sheets với cấu trúc rõ ràng
- **Nhận phản hồi cá nhân hóa**: AI tạo phản hồi động dựa trên dữ liệu tâm trạng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI với API key (để sử dụng GPT-4o)
- Tài khoản Google với Google Sheets API đã kích hoạt
- Tài khoản Slack với quyền gửi file
- App ID từ Wolfram Alpha Developer Portal
- Google Sheet mới với các cột tiêu đề sau: `userId`, `moodText`, `valence`, `energy`, `createdAt`, `wolframQuery`, `feedback`
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/10922](https://n8n.io/workflows/10922)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "OK" để hoàn tất import

Hoặc có thể copy/paste JSON workflow vào n8n Editor bằng cách:
1. Mở n8n Editor
2. Click vào nút "Import from Clipboard"
3. Dán nội dung JSON workflow vào và click "OK"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Webhook: Mood Input** và **Webhook: History Request**:
   - Đảm bảo các path `/mood` và `/history` chưa được sử dụng bởi workflow khác
   - Có thể thay đổi path nếu cần thiết

2. **OpenAI Chat Model** và **OpenAI Chat Model1**:
   - Cấu hình credentials cho OpenAI
   - Đảm bảo model "gpt-4o-mini" được kích hoạt trong tài khoản OpenAI

3. **Generate Mood Graph** và **Generate History Graph**:
   - Nhập App ID từ Wolfram Alpha Developer Portal vào trường `appid`
   - Có thể điều chỉnh các tham số khác như `width`, `height` để phù hợp với nhu cầu

4. **Log Mood to Google Sheet** và **Get History from Sheet**:
   - Cấu hình credentials cho Google Sheets
   - Nhập ID của Google Sheet đã tạo vào trường `spreadsheetId`
   - Đảm bảo Sheet có các cột tiêu đề như yêu cầu

5. **Upload a file**:
   - Cấu hình credentials cho Slack
   - Chọn channel hoặc người nhận file trong trường `channel`

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Chỉnh sửa node "Set Test Data" với dữ liệu mẫu
   - Click "Execute Workflow" để kiểm tra toàn bộ quy trình
2. Bật Active workflow:
   - Sau khi kiểm tra thành công, click vào nút "Active" ở góc trên bên phải của workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack**: Có thể thêm node Slack để gửi thông báo khi có dữ liệu mới được ghi nhận
2. **Tạo báo cáo định kỳ**: Sử dụng node "Schedule Trigger" để tạo báo cáo tâm trạng hàng tuần
3. **Phân tích sâu hơn**: Kết nối với các dịch vụ phân tích dữ liệu khác như Tableau hoặc Power BI
4. **Tích hợp với các nền tảng khác**: Có thể thêm các node để kết nối với các nền tảng khác như Notion, Trello...

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện để theo dõi và phân tích tâm trạng hàng ngày một cách tự động, chính xác và trực quan. Với việc kết hợp AI, Wolfram Alpha và Google Sheets, các sếp có thể dễ dàng theo dõi xu hướng tâm trạng của mình và nhận được phản hồi cá nhân hóa. Hãy thử ngay và biến theo dõi tâm trạng hàng ngày thành một thói quen hiệu quả!