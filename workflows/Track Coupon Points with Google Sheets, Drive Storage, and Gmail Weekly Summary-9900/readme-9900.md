---
title: "🚀 Theo dõi điểm thưởng từ coupon với Google Sheets, Drive và Gmail - Tự động hóa hoàn toàn"
description: "Hướng dẫn chi tiết cách tự động lưu trữ coupon, điểm thưởng và nhận báo cáo tuần tự với n8n, Google Sheets và Gmail. Tiết kiệm thời gian và tránh bỏ lỡ điểm thưởng."
slug: "theo-doi-diem-thuong-coupon-google-sheets-gmail"
tags: [n8n, automation, no-code, google-sheets, gmail, productivity]
keywords: [n8n workflow, tự động hóa, theo dõi điểm thưởng, coupon, google sheets, gmail]
---

# 🚀 Theo dõi điểm thưởng từ coupon với Google Sheets, Drive và Gmail - Tự động hóa hoàn toàn

[Các sếp] có biết không? Việc theo dõi điểm thưởng từ các chương trình coupon thường là một công việc nhàm chán và dễ bỏ sót. Mỗi lần mua sắm, các sếp phải ghi chép chi tiết, chụp ảnh hóa đơn và sau đó chờ đợi thời gian để điểm thưởng được ghi nhận. Quá trình này không chỉ tốn thời gian mà còn dễ gây nhầm lẫn khi có nhiều giao dịch cùng lúc.

Với workflow này, các sếp có thể tự động hóa hoàn toàn quy trình theo dõi điểm thưởng từ coupon. Workflow sẽ tự động lưu trữ thông tin coupon, chụp ảnh hóa đơn lên Google Drive và ghi nhận vào Google Sheets. Ngoài ra, các sếp còn nhận được báo cáo tuần tự về các điểm thưởng sắp đến hạn, giúp các sếp không bỏ sót bất kỳ điểm thưởng nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động lưu trữ thông tin coupon và chụp ảnh hóa đơn.
- **Tránh bỏ sót điểm thưởng**: Nhận báo cáo tuần tự về các điểm thưởng sắp đến hạn.
- **Dễ dàng quản lý**: Tất cả thông tin được lưu trữ và quản lý trên Google Sheets và Google Drive.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công, workflow chạy tự động 24/7.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive để lưu trữ ảnh hóa đơn.
- Tài khoản Google Sheets để lưu trữ thông tin coupon.
- Tài khoản Gmail để nhận báo cáo tuần tự.
- Tài khoản n8n để chạy workflow.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow, các sếp có thể tải file JSON từ [đây](https://n8n.io/workflows/9900) và import vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Tracking Form**: Node này tạo form để các sếp nhập thông tin coupon. Các sếp cần cấu hình đường dẫn cho form (ví dụ: `CouponTracker`).
- **Upload file**: Node này tải ảnh hóa đơn lên Google Drive. Các sếp cần cấu hình tài khoản Google Drive và thư mục lưu trữ.
- **Append row in sheet**: Node này ghi thông tin coupon vào Google Sheets. Các sếp cần cấu hình tài khoản Google Sheets, tên sheet và các cột dữ liệu.
- **Send a message**: Node này gửi báo cáo tuần tự về các điểm thưởng sắp đến hạn. Các sếp cần cấu hình tài khoản Gmail và địa chỉ email nhận báo cáo.
- **Schedule Trigger**: Node này cấu hình thời gian gửi báo cáo tuần tự. Các sếp có thể điều chỉnh thời gian gửi báo cáo theo nhu cầu.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể kết hợp với Slack hoặc Telegram để nhận báo cáo tuần tự.
- Các sếp có thể lưu log các hoạt động của workflow để theo dõi và kiểm tra.
- Các sếp có thể gửi báo cáo định kỳ (hàng tháng, hàng quý) để theo dõi tiến độ theo dõi điểm thưởng.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình theo dõi điểm thưởng từ coupon. Với workflow này, các sếp không còn phải lo lắng về việc bỏ sót điểm thưởng hay quản lý thông tin coupon một cách thủ công. Hãy áp dụng ngay để tiết kiệm thời gian và tăng hiệu quả làm việc!