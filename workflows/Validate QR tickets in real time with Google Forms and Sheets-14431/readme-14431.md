---
title: "🚀 Tự động hóa kiểm tra vé QR thời gian thực với Google Forms & Sheets"
description: "Giải pháp tự động hóa 100% không cần code để kiểm tra vé QR trong sự kiện, tiết kiệm thời gian và tránh sai sót thủ công"
slug: "tu-dong-hoa-kiem-tra-ve-qr-thoi-gian-thuc-google-forms-sheets"
tags: [n8n, automation, no-code, google-sheets, event-management]
keywords: [n8n workflow, tự động hóa vé sự kiện, kiểm tra vé QR, google forms, google sheets]
---

# 🚀 Tự động hóa kiểm tra vé QR thời gian thực với Google Forms & Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian kiểm tra vé thủ công
- Giảm 100% sai sót do nhập liệu
- Tự động lưu trữ dữ liệu kiểm tra
- Hoạt động liên tục 24/7 mà không cần can thiệp
- Tích hợp dễ dàng với hệ thống Google Workspace hiện tại
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace với quyền truy cập Google Sheets API
- Google Sheets có 2 bảng:
  1. Bảng chứa dữ liệu vé (được quét từ QR)
  2. Bảng chứa dữ liệu đăng ký sự kiện (dữ liệu từ Google Forms)
- Quyền truy cập vào n8n để import và cấu hình workflow
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/14431)
2. Click vào nút "Copy Workflow" và chọn "Copy JSON"
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã copy

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Sheets Update Trigger** node:
   - Cấu hình Google Sheets API credentials
   - Điền Spreadsheet ID của bảng chứa dữ liệu vé
   - Chọn Sheet Name chứa dữ liệu vé
   - Cấu hình trigger conditions (ví dụ: khi có hàng mới được thêm)

2. **Read Trigger Sheet Rows** node:
   - Đảm bảo sử dụng cùng credentials với node trước
   - Chọn Spreadsheet ID và Sheet Name tương ứng

3. **Append Scan Results** và **Append to Scan Results Sheet** nodes:
   - Cấu hình để ghi kết quả kiểm tra vào bảng kết quả
   - Đảm bảo có đủ quyền ghi vào bảng này

4. **Set Ticket Code Field** node:
   - Cấu hình trường dữ liệu cần kiểm tra (thường là mã vé từ QR)

5. **Select Latest Item** và **Select Latest Form Response** nodes:
   - Kiểm tra và điều chỉnh code nếu cần xử lý dữ liệu khác nhau
   - Đảm bảo logic xử lý phù hợp với cấu trúc dữ liệu của bạn

6. **Read Form Responses Sheet** node:
   - Cấu hình để đọc dữ liệu từ bảng đăng ký sự kiện
   - Đảm bảo sử dụng đúng Spreadsheet ID và Sheet Name

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu để kiểm tra logic
2. Kiểm tra kết quả trong bảng kết quả đã cấu hình
3. Bật Active workflow khi đã xác nhận hoạt động ổn định

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack/Teams để thông báo khi có vé không hợp lệ
2. Thêm chức năng gửi email tự động cho người dùng khi vé được kiểm tra
3. Tích hợp với hệ thống thanh toán để tự động cập nhật trạng thái vé
4. Thêm báo cáo định kỳ về tỷ lệ vé hợp lệ/thất bại

### 📌 Kết luận
Workflow này giúp các sếp tổ chức sự kiện tiết kiệm thời gian đáng kể, giảm sai sót và tự động hóa toàn bộ quá trình kiểm tra vé. Với cấu hình đơn giản và tích hợp liền mạch với Google Workspace, đây là giải pháp hoàn hảo cho các sự kiện quy mô lớn. Hãy áp dụng ngay để nâng cao trải nghiệm cho khách hàng và tối ưu hóa quy trình tổ chức sự kiện!