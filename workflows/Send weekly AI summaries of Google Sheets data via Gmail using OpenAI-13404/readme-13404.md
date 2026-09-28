---
title: "📊 Tự động hóa báo cáo tuần tự động với Google Sheets + OpenAI + Gmail"
description: "Hướng dẫn chi tiết cách tự động tổng hợp dữ liệu từ Google Sheets, tạo báo cáo AI hàng tuần và gửi qua Gmail - giải pháp tiết kiệm thời gian 100% không cần code"
slug: "tu-dong-hoa-bao-cao-tu-dong-google-sheets-openai-gmail"
tags: [n8n, automation, no-code, google-sheets, openai, gmail]
keywords: [n8n workflow, tự động hóa báo cáo, AI summary, Google Sheets, Gmail]
---

# 📊 Tự động hóa báo cáo tuần tự động với Google Sheets + OpenAI + Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 2-3 giờ mỗi tuần cho việc tổng hợp dữ liệu thủ công
- Báo cáo hàng tuần được tạo tự động với nội dung chính xác, chuyên nghiệp
- Dữ liệu được lưu trữ an toàn trong Google Sheets
- Hoạt động liên tục 24/7 mà không cần can thiệp
- Tự động ghi log báo cáo đã gửi để theo dõi lịch sử
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (cho Google Sheets và Gmail)
- Tài khoản OpenAI với API key
- Google Sheets chứa dữ liệu cần tổng hợp (đã chia sẻ quyền truy cập cho n8n)
- Email nhận báo cáo (có thể là email cá nhân hoặc email nhóm)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang workflow gốc: [n8n.io/workflows/13404](https://n8n.io/workflows/13404)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "Import" để hoàn tất

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Schedule Trigger** (Kích hoạt theo lịch):
   - Chỉnh sửa ngày/giờ chạy (mặc định là 9am thứ Hai hàng tuần)
   - Có thể thay đổi theo nhu cầu (ví dụ: 9am thứ Năm)

2. **Read Google Sheets Data** (Đọc dữ liệu từ Google Sheets):
   - Thiết lập credentials Google Sheets
   - Nhập **Spreadsheet ID** (tìm trong URL của Google Sheets)
   - Nhập **Sheet Name** chứa dữ liệu cần tổng hợp

3. **OpenAI Chat Model** (Cấu hình mô hình AI):
   - Thiết lập credentials OpenAI
   - Chọn mô hình (mặc định là gpt-4.1-mini)
   - Có thể thay đổi nếu cần độ chính xác cao hơn

4. **Send Report Email** (Gửi email báo cáo):
   - Thiết lập credentials Gmail
   - Nhập địa chỉ email nhận báo cáo
   - Có thể thêm CC nếu cần

5. **Log Report Sent** (Ghi log báo cáo đã gửi):
   - Thiết lập credentials Google Sheets
   - Nhập **Spreadsheet ID** của sheet log
   - Đảm bảo sheet log có cấu trúc: date, subject, sent_at

#### 3. Kích hoạt ⚡️
1. Click vào nút "Activate" ở góc trên bên phải
2. Chọn "Activate" để kích hoạt workflow
3. Test run bằng cách click vào nút "Execute Workflow" để kiểm tra

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh nội dung báo cáo**: Chỉnh sửa prompt trong node "Generate Summary with AI" để phù hợp với nhu cầu cụ thể
2. **Thêm nhận xét**: Sử dụng node "Sticky Note" để ghi chú các bước quan trọng trong workflow
3. **Kết hợp với Slack**: Thêm node Slack để thông báo khi báo cáo được gửi thành công
4. **Lập lịch báo cáo khác**: Sao chép workflow và thay đổi lịch trình cho các báo cáo định kỳ khác

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian quý giá trong việc tổng hợp dữ liệu hàng tuần. Với sự kết hợp của Google Sheets, OpenAI và Gmail, báo cáo được tạo tự động, chính xác và gửi đến đúng người nhận. Hãy thử ngay và trải nghiệm sự khác biệt của tự động hóa!