---
title: "🚀 Tự động hóa tóm tắt văn bản với RapidAPI và lưu kết quả vào Google Sheets"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình tóm tắt văn bản sử dụng API RapidAPI và ghi kết quả vào Google Sheets với n8n"
slug: "tu-dong-hoa-tom-tat-van-ban-voi-rapidapi-va-google-sheets"
tags: [n8n, automation, no-code, AI, Google Sheets]
keywords: [n8n workflow, tự động hóa, tóm tắt văn bản, RapidAPI, Google Sheets]
---

# 🚀 Tự động hóa tóm tắt văn bản với RapidAPI và lưu kết quả vào Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có thể đã từng gặp phải tình huống này: cần tóm tắt nhanh một đoạn văn bản dài, nhưng phải làm thủ công qua các công cụ tóm tắt truyền thống. Quá trình này tốn thời gian, không chính xác và không thể tự động hóa. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ nhập liệu đến lưu kết quả vào Google Sheets chỉ trong vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc tóm tắt văn bản
- Tự động hóa toàn bộ quy trình từ nhập liệu đến lưu kết quả
- Ghi log chi tiết các lần tóm tắt thành công và thất bại
- Tích hợp dễ dàng với các công cụ khác trong hệ sinh thái n8n
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets
- API Key từ RapidAPI cho dịch vụ tóm tắt văn bản
- Biết cách tạo và cấu hình Credentials trong n8n cho Google Sheets và RapidAPI
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của bạn, các sếp có thể thực hiện theo các bước sau:

1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import" ở góc trên bên phải
3. Chọn tùy chọn "From JSON" và dán nội dung JSON của workflow vào ô nhập liệu
4. Nhấn "Import" để hoàn tất quá trình

Hoặc các sếp có thể tải file JSON workflow từ [đây](https://n8n.io/workflows/6304) và import trực tiếp vào n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "On form submission"**:
   - Cấu hình form với các trường: Title, Content, Mode (Paragraph/Bullet), Length (Short/Medium/Long)
   - Đảm bảo các trường này được đặt tên chính xác để workflow hoạt động đúng

2. **Node "Mapping"**:
   - Kiểm tra các mapping rules để đảm bảo chuyển đổi dữ liệu đúng cách
   - Đặc biệt chú ý đến việc chuyển đổi Mode thành lowercase và Length thành số tương ứng

3. **Node "HTTP Request"**:
   - Cấu hình credentials cho RapidAPI
   - Đảm bảo URL API và các header được cấu hình chính xác
   - Kiểm tra các tham số gửi đi (title, content, mode, length)

4. **Node "If"**:
   - Kiểm tra điều kiện kiểm tra summary có tồn tại và không rỗng
   - Đảm bảo logic điều kiện đúng để phân luồng thành công/thất bại

5. **Node "Google Sheets" và "Google Sheets1"**:
   - Cấu hình credentials cho Google Sheets
   - Kiểm tra Spreadsheet ID và Sheet Name
   - Đảm bảo các trường dữ liệu được ánh xạ đúng với các cột trong Google Sheets

6. **Node "Wait" và "Wait1"**:
   - Điều chỉnh thời gian chờ nếu cần thiết
   - Có thể bỏ qua nếu không cần độ trễ

#### 3. Kích hoạt ⚡️
Sau khi đã cấu hình đầy đủ các node quan trọng:

1. Thực hiện test run với dữ liệu mẫu để kiểm tra toàn bộ workflow
2. Kiểm tra kết quả trong Google Sheets để đảm bảo dữ liệu được ghi đúng
3. Nếu mọi thứ hoạt động tốt, bật chế độ Active cho workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp với Slack/Telegram**: Các sếp có thể thêm node gửi thông báo qua Slack hoặc Telegram khi tóm tắt hoàn thành
2. **Lưu log chi tiết**: Có thể mở rộng để lưu thêm thông tin chi tiết hơn vào Google Sheets
3. **Tự động gửi báo cáo**: Thiết lập gửi báo cáo định kỳ qua email với các tóm tắt mới nhất
4. **Xử lý lỗi nâng cao**: Thêm các bước xử lý lỗi phức tạp hơn để tự động khắc phục các vấn đề thường gặp

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa tóm tắt văn bản với RapidAPI và lưu kết quả vào Google Sheets. Với các bước cấu hình đơn giản và kết quả đáng tin cậy, các sếp có thể áp dụng ngay vào các dự án của mình mà không cần viết code. Hãy thử ngay và tiết kiệm thời gian quý giá của bạn!