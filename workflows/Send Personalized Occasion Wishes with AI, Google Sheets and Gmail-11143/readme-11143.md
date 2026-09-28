---
title: "🎉 Tự động gửi lời chúc cá nhân hóa cho ngày đặc biệt với AI, Google Sheets và Gmail"
description: "Hướng dẫn tự động hóa gửi lời chúc sinh nhật, kỷ niệm, ngày lễ với thông điệp cá nhân hóa thông qua AI và Google Sheets"
slug: "tu-dong-gui-loi-chuc-ca-nhan-hoa-voi-ai-google-sheets-gmail"
tags: [n8n, automation, no-code, ai, google-sheets]
keywords: [n8n workflow, tự động hóa, gửi email cá nhân hóa, ai chúc mừng, google sheets]
---

# 🎉 Tự động gửi lời chúc cá nhân hóa cho ngày đặc biệt với AI, Google Sheets và Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quá trình gửi lời chúc hàng ngày
- Cá nhân hóa cao: Thông điệp chúc mừng được tạo riêng cho từng người
- Chính xác: Chỉ gửi lời chúc cho những người có ngày đặc biệt
- Hoạt động liên tục: Gửi lời chúc tự động mỗi ngày lúc 8h sáng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (cho Google Sheets và Gmail)
- API Key từ OpenAI (cho dịch vụ AI tạo thông điệp)
- Google Sheet chứa danh sách người nhận với các cột: Name, Occasion_Date, Email, Occasion_Type, Relationship, Personal_Note
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/11143](https://n8n.io/workflows/11143)
2. Chọn "Import" và sao chép JSON workflow vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Every Day at 8 AM"**:
   - Đảm bảo múi giờ được đặt chính xác
   - Kiểm tra lịch trình chạy đúng lúc 8h sáng hàng ngày

2. **Node "Get row(s) in sheet in Google Sheets"**:
   - Tạo credentials cho Google Sheets OAuth 2.0 API
   - Điền ID của Google Sheet chứa danh sách người nhận
   - Đảm bảo các cột dữ liệu đúng định dạng: Name, Occasion_Date, Email, Occasion_Type, Relationship, Personal_Note

3. **Node "OpenAI Chat Model"**:
   - Tạo credentials cho OpenAI API
   - Chọn model "gpt-4.1-mini" hoặc model tương thích khác
   - Đảm bảo API key có đủ credit để sử dụng

4. **Node "Send a message"**:
   - Cấu hình tài khoản Gmail để gửi email
   - Đảm bảo tài khoản không bị khóa bởi Google
   - Kiểm tra thư mục "Sent" để xác nhận email đã được gửi

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra workflow
2. Kích hoạt workflow sau khi xác nhận hoạt động bình thường

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack để nhận thông báo khi có sự kiện đặc biệt
- Lưu lịch sử gửi email vào Google Sheet để theo dõi
- Tùy chỉnh prompt AI để thay đổi phong cách thông điệp
- Thêm chức năng gửi thông báo sớm (ví dụ: 1 ngày trước ngày đặc biệt)

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc gửi lời chúc hàng ngày. Với sự kết hợp của AI và Google Sheets, thông điệp chúc mừng sẽ luôn được cá nhân hóa và gửi đúng lúc. Hãy thử ngay và trải nghiệm sự tiện lợi của tự động hóa!