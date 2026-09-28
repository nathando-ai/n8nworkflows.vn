---
title: "🚀 Kiểm tra email liên hệ mới trong Mautic tự động bằng n8n"
description: "Hướng dẫn tự động hóa kiểm tra email hợp lệ của liên hệ mới trong Mautic và thông báo qua Slack khi phát hiện email nghi ngờ"
slug: "kiem-tra-email-moi-mautic-n8n"
tags: [n8n, automation, no-code, mautic, slack]
keywords: [n8n workflow, tự động hóa, mautic, email validation, slack notification]
---

# 🚀 Kiểm tra email liên hệ mới trong Mautic tự động bằng n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi phải kiểm tra thủ công email của liên hệ mới trong Mautic. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động kiểm tra email hợp lệ của liên hệ mới trong Mautic
- Nhận thông báo tức thì qua Slack khi phát hiện email nghi ngờ
- Giảm thiểu rác email không hợp lệ trong hệ thống
- Tiết kiệm thời gian và công sức kiểm tra thủ công
- Đảm bảo chất lượng dữ liệu liên hệ
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Mautic với quyền truy cập API
- Tài khoản Slack với quyền gửi tin nhắn
- API Key từ OneSimpleApi (dịch vụ kiểm tra email)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/1462](https://n8n.io/workflows/1462)
2. Click vào nút "Download" để tải file JSON workflow
3. Trong n8n Editor, click vào "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "On Contact Identified"**:
   - Chọn credentials "mauticOAuth2Api" đã được cấu hình
   - Đảm bảo tài khoản Mautic có quyền truy cập API

2. **Node "validate email"**:
   - Chọn credentials "oneSimpleApi" đã được cấu hình
   - Điền API Key từ OneSimpleApi vào trường tương ứng
   - Đảm bảo tài khoản OneSimpleApi có đủ credit để kiểm tra email

3. **Node "Send to Slack"**:
   - Chọn credentials "slackApi" đã được cấu hình
   - Chỉnh sửa thông điệp Slack theo nhu cầu (có thể thêm thông tin liên hệ, thời gian, v.v.)

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra Slack để xác nhận thông báo
3. Bật Active workflow để chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node "Google Sheets" để lưu trữ log các email nghi ngờ
- Kết hợp với workflow gửi email tự động để thông báo cho đội ngũ bán hàng
- Thiết lập báo cáo định kỳ về tỷ lệ email hợp lệ trong hệ thống
- Tích hợp với các dịch vụ CRM khác để cập nhật trạng thái liên hệ

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình kiểm tra email hợp lệ của liên hệ mới trong Mautic, giảm thiểu rác email và tăng chất lượng dữ liệu liên hệ. Hãy áp dụng ngay để nâng cao hiệu quả làm việc của đội ngũ marketing và bán hàng!