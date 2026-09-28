---
title: "🚀 Tự động hóa tìm kiếm khách hàng Upwork: Trích xuất email từ LinkedIn với AI và n8n"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình tìm kiếm khách hàng tiềm năng từ Upwork, trích xuất thông tin bằng AI, tìm kiếm trên LinkedIn và lưu kết quả vào Google Sheets."
slug: "tu-dong-hoa-tim-kiem-khach-hang-upwork-voi-ai-va-n8n"
tags: [n8n, automation, no-code, upwork, linkedin, ai, google-sheets]
keywords: [n8n workflow, tự động hóa, upwork, linkedin, ai, google sheets]
---

# 🚀 **Tự động hóa tìm kiếm khách hàng Upwork: Trích xuất email từ LinkedIn với AI và n8n**

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm hàng giờ làm việc thủ công
- Tự động trích xuất thông tin khách hàng từ Upwork
- Sử dụng AI để phân loại và tìm kiếm thông tin chính xác
- Tích hợp với LinkedIn và Hunter.io để tìm kiếm email
- Lưu trữ dữ liệu khách hàng trong Google Sheets để quản lý dễ dàng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Upwork (để lấy dữ liệu công việc)
- Tài khoản Apify (để lấy dữ liệu từ Upwork)
- Tài khoản OpenAI (để sử dụng mô hình AI)
- Tài khoản Phantombuster (để tìm kiếm trên LinkedIn)
- Tài khoản Hunter.io (để tìm kiếm email)
- Tài khoản Google (để lưu dữ liệu vào Google Sheets)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào [n8n.io/workflows/4794](https://n8n.io/workflows/4794)
2. Nhấn vào nút "Download" để tải file JSON của workflow
3. Trong n8n Editor, nhấn vào nút "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **OpenAI Chat Model**:
   - Chọn credentials OpenAI API
   - Đảm bảo mô hình được chọn là "gpt-4o-mini" hoặc mô hình tương tự

2. **Run Every X Hours**:
   - Cấu hình thời gian chạy định kỳ (ví dụ: mỗi 6 giờ)

3. **Fetch Latest Upwork Jobs (Apify)**:
   - Cấu hình URL API Apify với token của bạn
   - Đảm bảo URL API được cập nhật với token hợp lệ

4. **Extract Company or Person Name from Job**:
   - Cấu hình prompt cho mô hình AI để trích xuất tên công ty hoặc người
   - Ví dụ prompt: "Extract a full person or company name from this job description. If not found, say 'none'."

5. **Search LinkedIn for Company (Phantombuster)**:
   - Cấu hình URL API Phantombuster với token của bạn
   - Đảm bảo URL API được cập nhật với token hợp lệ

6. **Find Company Email (Hunter.io)**:
   - Cấu hình URL API Hunter.io với API key của bạn
   - Đảm bảo URL API được cập nhật với API key hợp lệ

7. **Search LinkedIn for Person (Phantombuster)**:
   - Cấu hình URL API Phantombuster với token của bạn
   - Đảm bảo URL API được cập nhật với token hợp lệ

8. **Find Personal Email (Hunter.io)**:
   - Cấu hình URL API Hunter.io với API key của bạn
   - Đảm bảo URL API được cập nhật với API key hợp lệ

9. **Store Results in Google Sheet**:
   - Chọn credentials Google Sheets OAuth2 API
   - Cấu hình ID của Google Sheet và tên của sheet cần lưu dữ liệu

#### 3. Kích hoạt ⚡️
1. Kiểm tra kết nối với tất cả các dịch vụ bên ngoài (OpenAI, Apify, Phantombuster, Hunter.io, Google Sheets)
2. Chạy thử với dữ liệu mẫu để đảm bảo workflow hoạt động đúng
3. Bật Active workflow để chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để gửi email thông báo khi tìm thấy khách hàng mới
- Tích hợp với Slack hoặc Telegram để nhận thông báo tức thời
- Lưu log hoạt động của workflow để theo dõi hiệu suất
- Tự động gửi báo cáo hàng tuần về khách hàng mới tìm thấy

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm hàng giờ làm việc thủ công, tự động hóa quá trình tìm kiếm khách hàng tiềm năng từ Upwork, trích xuất thông tin bằng AI, tìm kiếm trên LinkedIn và lưu kết quả vào Google Sheets. Hãy áp dụng ngay để nâng cao hiệu quả kinh doanh của bạn!