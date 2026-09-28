---
title: "🚀 Theo dõi các hồ sơ Form D của SEC và gửi dữ liệu nhà đầu tư lên Google Sheets"
description: "Tự động hóa theo dõi các giao dịch niêm yết cổ phiếu riêng tư (Form D) từ SEC, trích xuất dữ liệu nhà đầu tư và lưu vào Google Sheets để phân tích thị trường hiệu quả."
slug: "theo-doi-form-d-sec-google-sheets"
tags: [n8n, automation, no-code, sec, google-sheets, market-research]
keywords: [n8n workflow, tự động hóa, sec form d, phân tích thị trường, dữ liệu đầu tư]
---

# 🚀 Theo dõi các hồ sơ Form D của SEC và gửi dữ liệu nhà đầu tư lên Google Sheets

[Các sếp đang làm việc trong lĩnh vực đầu tư, phân tích thị trường hay theo dõi thị trường chứng khoán thường gặp khó khăn khi phải theo dõi thủ công các giao dịch niêm yết cổ phiếu riêng tư (Form D) từ SEC. Quá trình này tốn thời gian, dễ bỏ sót và không thể tự động hóa. Workflow này sẽ giúp các sếp tiết kiệm thời gian và tập trung vào phân tích dữ liệu quan trọng hơn.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động theo dõi và xử lý dữ liệu từ SEC mà không cần can thiệp thủ công.
- **Dữ liệu chính xác**: Trích xuất thông tin chi tiết về nhà đầu tư, công ty và giao dịch từ các hồ sơ Form D.
- **Phân tích thị trường hiệu quả**: Dữ liệu được lưu vào Google Sheets, giúp các sếp dễ dàng phân tích và đưa ra quyết định đầu tư.
- **Tự động hóa liên tục**: Workflow chạy định kỳ (mỗi 10 phút) để đảm bảo dữ liệu luôn cập nhật.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Google Sheets**: Tạo một bảng tính với các cột cần thiết (xem mô tả trong workflow).
- **Google Sheets OAuth Credentials**: Cấu hình xác thực OAuth2 để n8n có quyền truy cập vào Google Sheets.
- **Thay đổi email**: Thay thế `nchoudhary110792@gmail.com` trong các node HTTP bằng email của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/12851).
2. Nhấn nút **Download** để tải file JSON.
3. Trong n8n Editor, nhấn **Import from File** và chọn file JSON đã tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node Schedule Trigger**: Đảm bảo thời gian chạy phù hợp với lịch làm việc của các sếp (mặc định: 6 AM - 9 PM, thứ 2 - thứ 6).
- **Node Google Sheets**: Cấu hình credentials và chỉ định đúng tên bảng tính và sheet cần ghi dữ liệu.
- **Node HTTP Request**: Thay thế email `nchoudhary110792@gmail.com` bằng email của các sếp trong các node HTTP.
- **Node Remove Duplicates**: Đảm bảo cấu hình đúng để loại bỏ các hồ sơ đã xử lý trước đó.

#### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu để kiểm tra tính năng.
2. **Bật Active workflow**: Sau khi kiểm tra thành công, bật workflow để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo khi có giao dịch mới hoặc khi dữ liệu được cập nhật.
- **Lưu log**: Thêm node ghi log để theo dõi quá trình xử lý và xử lý lỗi.
- **Gửi báo cáo định kỳ**: Tự động gửi báo cáo tổng hợp dữ liệu qua email hoặc Slack vào cuối ngày.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và tập trung vào phân tích dữ liệu quan trọng hơn. Bằng cách tự động hóa quá trình theo dõi và xử lý dữ liệu từ SEC, các sếp có thể đưa ra quyết định đầu tư nhanh chóng và chính xác hơn. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của mình!