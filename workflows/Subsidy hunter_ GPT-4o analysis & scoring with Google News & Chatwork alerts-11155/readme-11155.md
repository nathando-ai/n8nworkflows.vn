---
title: "🚀 Tự động hóa tìm kiếm thông tin trợ cấp với GPT-4o: Phân tích và cảnh báo Chatwork"
description: "Workflow n8n tự động thu thập thông tin trợ cấp từ Google News và RSS, phân tích bằng GPT-4o và gửi cảnh báo Chatwork theo mức độ ưu tiên"
slug: "tu-dong-hoa-tim-kiem-thong-tin-tro-cap-gpt-4o"
tags: [n8n, automation, no-code, google-news, chatwork, google-sheets]
keywords: [n8n workflow, tự động hóa, trợ cấp doanh nghiệp, phân tích AI, cảnh báo Chatwork]
---

# 🚀 Tự động hóa tìm kiếm thông tin trợ cấp với GPT-4o: Phân tích và cảnh báo Chatwork

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có thể tưởng tượng được nỗi đau khi phải theo dõi hàng chục nguồn thông tin trợ cấp hàng ngày, từ Google News đến các trang chính phủ. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ thu thập thông tin đến phân tích và cảnh báo, giúp tiết kiệm thời gian quý giá và tập trung vào những cơ hội thực sự quan trọng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian theo dõi thủ công
- Phân tích thông tin trợ cấp một cách chính xác và chuyên nghiệp
- Nhận cảnh báo tức thì về các cơ hội trợ cấp quan trọng
- Lưu trữ dữ liệu có cấu trúc trong Google Sheets
- Tự động lọc và phân loại thông tin theo mức độ ưu tiên
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI với API key
- Tài khoản Google với Google Sheets đã tạo
- Tài khoản Chatwork với API token
- Room ID trong Chatwork để gửi cảnh báo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [trang workflow gốc](https://n8n.io/workflows/11155)
2. Click vào nút "Import" để tải file JSON về máy
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Workflow Configuration"**:
   - Thiết lập các biến môi trường:
     - `CHATWORK_ROOM_ID`: ID của room Chatwork để gửi cảnh báo
     - `CHATWORK_API_TOKEN`: API token của tài khoản Chatwork
     - `GOOGLE_SHEET_ID`: ID của Google Sheet để lưu trữ dữ liệu

2. **Node "OpenAI GPT-4o"**:
   - Kết nối với tài khoản OpenAI của bạn
   - Đảm bảo bạn có đủ credit để sử dụng GPT-4o

3. **Node "Check Duplicate" và "Save to Google Sheets"**:
   - Kết nối với tài khoản Google của bạn
   - Tạo Google Sheet với tên "Subsidies" và các cột sau:
     - `subsidyName`
     - `targetRecipients`
     - `applicationDeadline`
     - `budgetAmount`
     - `urgency`
     - `importanceScore`
     - `priorityTag`
     - `sourceUrl`

4. **Node "Send Chatwork"**:
   - Đảm bảo bạn có quyền gửi tin nhắn vào room Chatwork đã cấu hình

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, chạy test với dữ liệu mẫu
2. Kiểm tra kết quả trong Google Sheets và room Chatwork
3. Nếu mọi thứ hoạt động tốt, bật chế độ Active cho workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh prompt phân tích**: Chỉnh sửa prompt trong node "AI Scoring Agent" để phù hợp với nhu cầu cụ thể của doanh nghiệp
2. **Thêm nguồn thông tin**: Có thể thêm các nguồn RSS khác bằng cách sao chép và sửa đổi các node "Read J-Net21 RSS" và "Read Mirasapo RSS"
3. **Cảnh báo đa kênh**: Kết nối thêm với Slack hoặc Telegram để nhận cảnh báo từ nhiều nguồn
4. **Báo cáo định kỳ**: Thêm node để gửi báo cáo tổng hợp hàng tuần/tháng về các cơ hội trợ cấp quan trọng

### 📌 Kết luận
Workflow này không chỉ giúp các sếp tiết kiệm thời gian mà còn nâng cao hiệu quả trong việc tìm kiếm và lựa chọn các cơ hội trợ cấp phù hợp. Với sự kết hợp của tự động hóa và trí tuệ nhân tạo, các sếp có thể tập trung vào những việc thực sự quan trọng trong kinh doanh của mình. Hãy thử ngay và trải nghiệm cách làm việc thông minh hơn!