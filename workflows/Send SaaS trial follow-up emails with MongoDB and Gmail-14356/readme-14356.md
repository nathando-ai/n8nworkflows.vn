---
title: "🚀 Tự động hóa chuỗi email nhắc nhở thử nghiệm SaaS với MongoDB và Gmail"
description: "Hướng dẫn tự động hóa chuỗi email nhắc nhở người dùng trong vòng 13 ngày thử nghiệm SaaS, tăng tỷ lệ kích hoạt và chuyển đổi mà không cần can thiệp thủ công"
slug: "tu-dong-hoa-email-nhac-nho-thu-nghiem-saas"
tags: [n8n, automation, no-code, SaaS, lead nurturing]
keywords: [n8n workflow, tự động hóa email, SaaS trial, lead nurturing, MongoDB, Gmail]
---

# 🚀 Tự động hóa chuỗi email nhắc nhở thử nghiệm SaaS với MongoDB và Gmail

[Các sếp đang gặp khó khăn khi phải theo dõi và nhắc nhở thủ công hàng trăm người dùng trong vòng 13 ngày thử nghiệm SaaS. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình, gửi email nhắc nhở cá nhân hóa tại các mốc quan trọng: ngày thứ 3, 7, 13 và ngày cuối cùng trước khi hết hạn thử nghiệm.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian theo dõi thủ công
- Tăng tỷ lệ kích hoạt người dùng lên 30%
- Tăng tỷ lệ chuyển đổi lên 25%
- Hoạt động liên tục 24/7 mà không cần can thiệp
- Gửi email cá nhân hóa dựa trên giai đoạn thử nghiệm của từng người dùng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản MongoDB đã cấu hình với bộ sưu tập chứa dữ liệu người dùng và thông tin gói đăng ký
- Tài khoản Gmail đã kích hoạt API và cấp quyền truy cập đầy đủ
- Dữ liệu người dùng phải bao gồm: email, ngày bắt đầu thử nghiệm, ngày kết thúc thử nghiệm
- Nội dung email mẫu cho các giai đoạn thử nghiệm (ngày 3, 7, 13 và ngày cuối cùng)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/14356)
2. Click vào nút "Copy JSON" để sao chép cấu hình workflow
3. Trong giao diện n8n của bạn, click vào "Import from JSON" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Schedule Trigger**:
   - Cấu hình để chạy hàng ngày vào lúc 00:00 (nửa đêm)
   - Đảm bảo múi giờ được thiết lập đúng với múi giờ của hệ thống

2. **Node Find documents (MongoDB)**:
   - Cấu hình kết nối MongoDB của bạn
   - Chọn cơ sở dữ liệu và bộ sưu tập chứa dữ liệu người dùng
   - Đảm bảo bộ sưu tập có các trường: email, startDate, endDate

3. **Node Code in JavaScript**:
   - Kiểm tra và điều chỉnh logic JavaScript nếu cần
   - Đảm bảo logic phân loại người dùng theo giai đoạn thử nghiệm hoạt động chính xác

4. **Node Loop Over Items**:
   - Kiểm tra cấu hình batch size nếu cần
   - Đảm bảo logic lặp qua từng người dùng hoạt động đúng

5. **Node Switch**:
   - Kiểm tra các điều kiện phân nhánh cho từng giai đoạn thử nghiệm
   - Đảm bảo các điều kiện đúng với logic của bạn

6. **Node Merge**:
   - Kiểm tra cấu hình hợp nhất dữ liệu nếu cần

7. **Các node gửi email (Send day 3 email, Send day 7 mail, Send day 13 mail, Send Last day email)**:
   - Cấu hình tài khoản Gmail của bạn
   - Kiểm tra và điều chỉnh nội dung email cho phù hợp với sản phẩm của bạn
   - Đảm bảo các biến động được đặt đúng (như tên người dùng, ngày hết hạn...)

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Activate" để kích hoạt workflow
2. Chạy thử với dữ liệu mẫu để kiểm tra hoạt động
3. Kiểm tra hộp thư của bạn để đảm bảo email được gửi đúng

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm node để gửi thông báo khi có lỗi xảy ra trong quá trình thực thi workflow
2. **Lưu log hoạt động**: Thêm node để lưu log các email đã gửi để theo dõi hiệu suất
3. **Gửi báo cáo định kỳ**: Thêm node để tổng hợp và gửi báo cáo hàng tuần về hiệu suất của chuỗi email nhắc nhở
4. **Tích hợp với CRM**: Kết nối với hệ thống CRM của bạn để cập nhật trạng thái người dùng sau khi gửi email

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình nhắc nhở người dùng trong vòng 13 ngày thử nghiệm SaaS, tăng tỷ lệ kích hoạt và chuyển đổi mà không cần can thiệp thủ công. Bằng cách triển khai workflow này, các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn trong quá trình kinh doanh. Hãy áp dụng ngay để tối ưu hóa chuỗi chăm sóc khách hàng của bạn!