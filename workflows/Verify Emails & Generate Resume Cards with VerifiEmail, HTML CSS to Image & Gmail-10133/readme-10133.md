---
title: "🚀 Tự động hóa HR: Xác thực Email & Tạo Thẻ Hồ Sơ với n8n"
description: "Giải pháp tự động hóa hoàn toàn không cần code giúp xác thực email ứng viên và tạo thẻ hồ sơ đẹp mắt, tiết kiệm thời gian và nâng cao trải nghiệm ứng tuyển."
slug: "tu-dong-hoa-xac-thuc-email-tao-the-ho-so-n8n"
tags: [n8n, automation, no-code, HR, email-verification]
keywords: [n8n workflow, tự động hóa HR, xác thực email, tạo thẻ hồ sơ, no-code]
---

# 🚀 Tự động hóa HR: Xác thực Email & Tạo Thẻ Hồ Sơ với n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý hồ sơ ứng viên từ 70-90%
- Tăng độ chuyên nghiệp với thẻ hồ sơ đẹp mắt và được xác thực
- Giảm rủi ro nhận hồ sơ với email không tồn tại
- Tự động hóa toàn bộ quy trình từ nhận dữ liệu đến gửi email
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail với quyền truy cập API (OAuth2)
- API Key từ VerifiEmail (https://verifi.email)
- Tài khoản và API Key từ HTML/CSS to Image (https://htmlcsstoimg.com)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/10133](https://n8n.io/workflows/10133)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "OK" để hoàn tất import

Hoặc bạn có thể copy JSON workflow và paste vào n8n Editor bằng cách:
1. Mở n8n Editor
2. Click vào nút "+" để tạo workflow mới
3. Click vào biểu tượng "Import from Clipboard" (biểu tượng mũi tên hướng vào)
4. Paste JSON workflow và click "OK"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Webhook Node**:
   - Đảm bảo đường dẫn "resume-verifier" là duy nhất trong hệ thống của bạn
   - Giữ phương thức HTTP là POST

2. **Gmail Nodes**:
   - Tạo và chọn credentials Gmail OAuth2
   - Cấu hình email template cho cả hai node Gmail (valid và invalid)

3. **VerifiEmail Node**:
   - Tạo và chọn credentials VerifiEmail API
   - Đảm bảo tài khoản VerifiEmail có đủ credit để xử lý lượng yêu cầu dự kiến

4. **HTML/CSS to Image Node**:
   - Tạo và chọn credentials HTML/CSS to Image
   - Cấu hình template HTML/CSS cho thẻ hồ sơ

5. **Set Node**:
   - Kiểm tra và cập nhật các field mappings nếu cần:
     - `name` ← `$json.body.name`
     - `email` ← `$json.body.email`
     - `role` ← `$json.body.role`
     - `skills` ← `$json.body.skills`

#### 3. Kích hoạt ⚡️
1. Test workflow với dữ liệu mẫu:
   ```json
   {
     "name": "Nguyễn Văn A",
     "email": "nguyenvana@gmail.com",
     "role": "Lập trình viên Frontend",
     "skills": "React, JavaScript, Tailwind, Git"
   }
   ```
2. Kiểm tra email để xác nhận nhận được thẻ hồ sơ hoặc thông báo lỗi
3. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Teams**: Thêm node để gửi thông báo vào kênh Slack/Teams khi có hồ sơ mới
2. **Lưu log**: Thêm node để lưu log các hồ sơ đã xử lý vào Google Sheets hoặc cơ sở dữ liệu
3. **Gửi báo cáo định kỳ**: Tạo workflow phụ để gửi báo cáo hàng tuần về số lượng hồ sơ đã xử lý
4. **Xử lý email bị từ chối**: Thêm logic để tự động gửi email nhắc nhở ứng viên khi email bị từ chối

### 📌 Kết luận
Workflow này giúp các sếp HR tự động hóa hoàn toàn quy trình xác thực email và tạo thẻ hồ sơ đẹp mắt, tiết kiệm thời gian quý giá và nâng cao trải nghiệm ứng tuyển. Hãy áp dụng ngay để tối ưu hóa quy trình tuyển dụng của bạn!