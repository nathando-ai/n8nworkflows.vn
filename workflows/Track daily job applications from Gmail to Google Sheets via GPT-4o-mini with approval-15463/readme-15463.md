---
title: "🚀 Tự động hóa theo dõi ứng tuyển việc làm từ Gmail đến Google Sheets với GPT-4o-mini và phê duyệt"
description: "Workflow n8n tự động hóa việc theo dõi ứng tuyển việc làm từ Gmail đến Google Sheets với GPT-4o-mini và phê duyệt. Tiết kiệm thời gian và tránh bỏ sót các cập nhật quan trọng."
slug: "tu-dong-hoa-theo-doi-ung-tuyen-viec-lam-gmail-google-sheets-gpt-4o-mini"
tags: [n8n, automation, no-code, google-sheets, gmail, ai]
keywords: [n8n workflow, tự động hóa, theo dõi ứng tuyển, google sheets, gmail, gpt-4o-mini]
---

# 🚀 Tự động hóa theo dõi ứng tuyển việc làm từ Gmail đến Google Sheets với GPT-4o-mini và phê duyệt

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa việc theo dõi ứng tuyển việc làm hàng ngày.
- Chính xác: Sử dụng GPT-4o-mini để trích xuất thông tin chính xác từ email.
- Cá nhân hóa: Theo dõi từng ứng tuyển với thông tin chi tiết về công ty, vị trí, ngày ứng tuyển và trạng thái hiện tại.
- Hoạt động liên tục: Chạy tự động hàng ngày vào lúc 9 AM để cập nhật thông tin mới nhất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail với quyền truy cập vào các email ứng tuyển việc làm.
- Tài khoản Google Sheets để lưu trữ thông tin ứng tuyển.
- API Key của OpenAI để sử dụng GPT-4o-mini.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và nhập URL: [https://n8n.io/workflows/15463](https://n8n.io/workflows/15463).
3. Hoặc tải file JSON về và chọn "Import from File".

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Fetch Job Application Emails**: Cấu hình credentials cho Gmail và điền tham số `newer_than:25h` để chỉ lấy email mới trong 25 giờ.
- **Open AI**: Cấu hình credentials cho OpenAI và chọn model `gpt-4o-mini`.
- **Track New Application** và **Update Application**: Cấu hình credentials cho Google Sheets và điền tên sheet cần lưu trữ thông tin.
- **Email Updates & Wait for Approval**: Cấu hình credentials cho Gmail và điền địa chỉ email người nhận phê duyệt.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có cập nhật mới.
- Lưu log các email bị bỏ qua để kiểm tra và cải thiện bộ lọc.
- Gửi báo cáo định kỳ về tiến trình ứng tuyển.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và tránh bỏ sót các cập nhật quan trọng trong quá trình ứng tuyển việc làm. Bằng cách tự động hóa việc theo dõi và sử dụng AI để trích xuất thông tin, các sếp có thể tập trung vào các cơ hội việc làm quan trọng hơn. Hãy áp dụng ngay để nâng cao hiệu suất công việc!