---
title: "🚀 Tự động hóa Gmail với Gemini: Nhãn tự động và soạn nháp trả lời"
description: "Hướng dẫn tự động hóa quản lý hộp thư Gmail với n8n và Gemini AI. Tự động nhãn email, kiểm tra lịch và soạn nháp trả lời một cách thông minh."
slug: "tu-dong-hoa-gmail-voi-gemini"
tags: [n8n, automation, no-code, gmail, ai]
keywords: [n8n workflow, tự động hóa gmail, gemini ai, quản lý email, soạn nháp tự động]
---

# 🚀 Tự động hóa Gmail với Gemini: Nhãn tự động và soạn nháp trả lời

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động nhãn và phân loại email trong vài giây
- Tăng hiệu suất: Nhận nháp trả lời thông minh từ AI Gemini
- Cá nhân hóa: Hệ thống học hỏi từ lịch sử email của bạn
- Hoạt động liên tục: Theo dõi hộp thư 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail với quyền truy cập đầy đủ
- API Key từ Google Gemini
- Các nhãn Gmail đã được thiết lập trước
- Quyền truy cập Google Calendar (tùy chọn)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/10664](https://n8n.io/workflows/10664)
2. Nhấn nút "Import" trên trang workflow
3. Trong n8n Editor, chọn "Import from URL" và dán link trên
4. Hoặc tải file JSON về và chọn "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Gmail Trigger**:
   - Thiết lập credentials Gmail OAuth2
   - Chọn các nhãn email bạn muốn theo dõi

2. **Gemini Node**:
   - Thiết lập credentials Google Palm API
   - Đảm bảo tài khoản Gemini có đủ credit

3. **Google Calendar Tool** (tùy chọn):
   - Thiết lập credentials Google Calendar OAuth2
   - Chỉ cần thiết lập nếu muốn kiểm tra lịch khi soạn nháp

4. **Structured Output Parser**:
   - Đảm bảo cấu trúc đầu ra phù hợp với các node tiếp theo
   - Kiểm tra các trường dữ liệu cần thiết trong đầu ra

5. **IF Nodes**:
   - Cấu hình các điều kiện logic cho việc xóa email và tạo nháp
   - Điều chỉnh các giá trị ngưỡng cho các quyết định tự động

#### 3. Kích hoạt ⚡️
1. Test run với một email mẫu
2. Kiểm tra nhãn và nháp được tạo trong Gmail
3. Bật Active workflow khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack/Telegram để nhận thông báo khi có email mới
2. Thêm node lưu log các email đã xử lý
3. Tạo báo cáo hàng tuần về email đã xử lý
4. Kết nối với các dịch vụ CRM khác để theo dõi khách hàng

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm hàng giờ mỗi ngày trong việc quản lý email. Bằng cách tự động nhãn và tạo nháp trả lời thông minh, bạn có thể tập trung vào những công việc quan trọng hơn. Hãy thử ngay và trải nghiệm sự thay đổi đáng kể trong hiệu suất làm việc!