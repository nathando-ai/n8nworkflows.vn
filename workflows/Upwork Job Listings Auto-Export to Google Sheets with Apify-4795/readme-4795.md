---
title: "🚀 Tự động hóa thu thập công việc Upwork và lưu vào Google Sheets với Apify"
description: "Hướng dẫn chi tiết cách tự động thu thập danh sách công việc từ Upwork và lưu vào Google Sheets hàng ngày bằng n8n và Apify. Giải pháp hoàn toàn không cần code cho freelancer và nhà tuyển dụng."
slug: "tu-dong-hoa-thu-thap-cong-viec-upwork-google-sheets"
tags: [n8n, automation, no-code, freelancer, apify, google-sheets]
keywords: [n8n workflow, tự động hóa, thu thập công việc, upwork, google sheets]
---

# 🚀 Tự động hóa thu thập công việc Upwork và lưu vào Google Sheets với Apify

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 2-3 giờ mỗi ngày từ việc thu thập công việc thủ công
- Có dữ liệu thị trường công việc cập nhật liên tục
- Dễ dàng phân tích xu hướng thị trường
- Tự động hóa hoàn toàn không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets API đã được kích hoạt
- Tài khoản Apify với actor đã được cấu hình để thu thập công việc từ Upwork
- API Key từ Apify để thực hiện các yêu cầu HTTP
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link: https://n8n.io/workflows/4795
3. Hoặc tải file JSON về và chọn "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Check Upwork Jobs - Trigger"**:
   - Cấu hình lịch chạy (ví dụ: mỗi ngày lúc 8h sáng)
   - Đảm bảo thời gian chạy phù hợp với múi giờ của bạn

2. **Node "Fetch Upwork Jobs using Apify"**:
   - Thiết lập credentials cho Apify
   - Cấu hình URL endpoint của Apify actor
   - Điền các tham số tìm kiếm (nếu có) vào body của request

3. **Node "Format scrape Data"**:
   - Kiểm tra và điều chỉnh các trường dữ liệu cần lưu
   - Đảm bảo tên cột trong Google Sheets phù hợp với dữ liệu thu thập

4. **Node "Log Jobs to Google Sheets"**:
   - Thiết lập Google Sheets OAuth2 credentials
   - Chỉ định ID của Google Sheet đích
   - Điền tên của Sheet trong file Google Sheets (thường là "Sheet1" nếu chưa đổi tên)

#### 3. Kích hoạt ⚡️
- Thực hiện test run với dữ liệu mẫu trước khi kích hoạt
- Kiểm tra kết quả trong Google Sheets sau khi workflow chạy
- Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để gửi email báo cáo hàng tuần về các công việc mới
- Kết hợp với Slack để thông báo khi có công việc phù hợp với tiêu chí của bạn
- Thêm bộ lọc để loại bỏ các công việc trùng lặp
- Tự động hóa việc gửi ứng tuyển cho các công việc phù hợp

### 📌 Kết luận
Workflow này giúp các freelancer và nhà tuyển dụng tiết kiệm thời gian quý giá trong việc theo dõi thị trường công việc. Bằng cách tự động hóa quá trình thu thập và lưu trữ dữ liệu, bạn có thể tập trung vào việc phát triển kỹ năng và tìm kiếm cơ hội tốt hơn. Hãy thử ngay và nâng cao hiệu quả làm việc của mình!