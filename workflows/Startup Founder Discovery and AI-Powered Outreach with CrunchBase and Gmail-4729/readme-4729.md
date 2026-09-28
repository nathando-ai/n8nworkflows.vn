---
title: "🚀 Tự động hóa tìm kiếm nhà đầu tư và gửi email liên hệ với CrunchBase và Gmail"
description: "Hướng dẫn tự động hóa quy trình tìm kiếm nhà đầu tư tiềm năng từ CrunchBase, tổng hợp thông tin bằng AI và gửi email liên hệ tự động qua Gmail"
slug: "tu-dong-hoa-tim-kiem-nha-dau-tu-va-gui-email"
tags: [n8n, automation, no-code, crunchbase, gmail, ai, marketing]
keywords: [n8n workflow, tự động hóa, crunchbase, gmail, ai, marketing]
---

# 🚀 Tự động hóa tìm kiếm nhà đầu tư và gửi email liên hệ với CrunchBase và Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian tìm kiếm và tổng hợp thông tin nhà đầu tư
- Tự động hóa quá trình gửi email liên hệ với nhà đầu tư tiềm năng
- Tăng hiệu quả tiếp cận và tăng cơ hội đầu tư
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
- Tích hợp AI để tạo nội dung email chuyên nghiệp và cá nhân hóa
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản CrunchBase API (để truy cập dữ liệu công ty và nhà đầu tư)
- Tài khoản Gmail (để gửi email tự động)
- API key của OpenAI (để sử dụng dịch vụ AI tổng hợp thông tin)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import from URL" và dán link sau: https://n8n.io/workflows/4729
3. Hoặc tải file JSON từ trang n8n.io và import thủ công

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "OpenAI Chat Model"**:
   - Cần cấu hình credentials cho OpenAI API
   - Đảm bảo chọn model phù hợp (gpt-4o-mini hoặc các model khác)

2. **Node "Updated profiles List"**:
   - Cần cấu hình URL và tham số truy vấn cho CrunchBase API
   - Có thể thay đổi tham số `page` để lấy dữ liệu từ các trang khác nhau
   - Có thể điều chỉnh tham số `updated_since` để lọc theo thời gian cập nhật

3. **Node "Founder Profiles by UUID"**:
   - Cần cấu hình URL và tham số truy vấn cho CrunchBase API
   - Có thể thay đổi chỉ số mảng (ví dụ từ `[0]` sang `[1]`) để lấy thông tin của nhà đầu tư khác

4. **Node "Send email for outreach"**:
   - Cần cấu hình credentials cho Gmail OAuth2
   - Có thể thay đổi địa chỉ email nhận, chủ đề và nội dung email

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Test workflow" để kiểm tra dữ liệu mẫu
2. Sau khi kiểm tra thành công, nhấn "Activate workflow" để kích hoạt tự động hóa

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi thông báo qua Slack hoặc Telegram khi có nhà đầu tư mới
- Lưu log các email đã gửi để theo dõi hiệu quả liên hệ
- Tự động hóa quá trình gửi báo cáo hàng tuần về các nhà đầu tư mới
- Kết hợp với các công cụ CRM khác để lưu trữ thông tin nhà đầu tư
- Tùy chỉnh nội dung email dựa trên ngành nghề của nhà đầu tư

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và công sức trong việc tìm kiếm và liên hệ với nhà đầu tư tiềm năng. Bằng cách tự động hóa quy trình này, các sếp có thể tập trung vào các hoạt động quan trọng hơn và tăng cơ hội đầu tư thành công. Hãy thử ngay và trải nghiệm hiệu quả của tự động hóa!