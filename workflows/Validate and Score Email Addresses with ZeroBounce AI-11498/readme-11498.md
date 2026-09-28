---
title: "🚀 Xác thực và Đánh giá Email với ZeroBounce AI - Workflow n8n Tự động hóa 100% Không Code"
description: "Hướng dẫn chi tiết cách tự động xác thực email và đánh giá chất lượng bằng ZeroBounce AI trong n8n. Tiết kiệm thời gian, tăng độ chính xác và bảo vệ danh tiếng người gửi."
slug: "xac-thuc-danh-gia-email-voi-zerobounce-ai"
tags: [n8n, automation, no-code, email-marketing, ai-validation]
keywords: [n8n workflow, tự động hóa email, xác thực email, đánh giá email, ZeroBounce AI]
---

# 🚀 Xác thực và Đánh giá Email với ZeroBounce AI - Workflow n8n Tự động hóa 100% Không Code

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Xử lý hàng nghìn email chỉ trong vài phút
- Tăng độ chính xác: Xác thực và đánh giá email với độ chính xác 99.6%
- Bảo vệ danh tiếng người gửi: Lọc bỏ email rác và spam trap
- Tự động hóa hoàn toàn: Không cần can thiệp thủ công
- Tích hợp dễ dàng: Kết nối với các công cụ email marketing khác
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản ZeroBounce với API Key (đăng ký [tại đây](https://www.zerobounce.net/members/API))
- Danh sách email cần xử lý (có thể từ Google Sheets, CSV, hoặc bất kỳ nguồn nào)
- Kiến thức cơ bản về n8n (không cần lập trình)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [ZeroBounce Email Validation and Scoring](https://n8n.io/workflows/11498)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import into new workflow" và click "OK"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "When clicking ‘Execute workflow’"**:
   - Không cần cấu hình gì, chỉ cần click "Execute workflow" khi đã sẵn sàng

2. **Node "Check credits for validation"**:
   - Chọn credentials "zeroBounceApi" đã được tạo trước đó
   - Đảm bảo tài khoản ZeroBounce có đủ credits

3. **Node "Check credits for scoring"**:
   - Tương tự như node trên, chọn credentials "zeroBounceApi"
   - Có thể để trống "Credits required" nếu muốn kiểm tra credits trước khi thực hiện

4. **Node "Validate email"**:
   - Chọn credentials "zeroBounceApi"
   - Điền email cần xác thực vào trường "Email"

5. **Node "Score email"**:
   - Chọn credentials "zeroBounceApi"
   - Điền email cần đánh giá vào trường "Email"

6. **Node "Sandbox emails"**:
   - Thay thế các email mẫu bằng danh sách email thực tế của bạn
   - Hoặc kết nối với nguồn dữ liệu khác (Google Sheets, CSV, v.v.)

#### 3. Kích hoạt ⚡️
1. Test run với 1-2 email mẫu trước khi chạy toàn bộ danh sách
2. Sau khi kiểm tra kết quả, click vào nút "Activate" để kích hoạt workflow
3. Workflow sẽ tự động xử lý danh sách email theo các bước đã được cấu hình

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo kết quả qua Slack hoặc Telegram
2. **Lưu log hoạt động**: Kết nối với Google Sheets hoặc Notion để lưu lại lịch sử xử lý
3. **Gửi báo cáo định kỳ**: Tự động gửi báo cáo tổng hợp kết quả qua email hàng ngày
4. **Xử lý email không hợp lệ**: Tự động chuyển email không hợp lệ vào danh sách chặn

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc xác thực và đánh giá email. Với độ chính xác cao và tự động hóa hoàn toàn, nó giúp bảo vệ danh tiếng người gửi và tối ưu hóa chiến dịch email marketing. Hãy thử ngay và trải nghiệm sự khác biệt!