---
title: "🚀 Tự động viết đề xuất Upwork từ cảnh báo Vollna bằng Claude, Gmail và Sheets"
description: "Giải phóng thời gian của bạn với workflow tự động hóa viết đề xuất Upwork từ cảnh báo Vollna. Tiết kiệm 20 phút mỗi đề xuất bằng cách sử dụng AI Claude để tạo nội dung cá nhân hóa và lưu nháp Gmail."
slug: "tu-dong-viet-de-xuat-upwork-tu-canh-bao-vollna"
tags: [n8n, automation, no-code, upwork, ai]
keywords: [n8n workflow, tự động hóa, ai đề xuất, upwork, vollna]
---

# 🚀 Tự động viết đề xuất Upwork từ cảnh báo Vollna bằng Claude, Gmail và Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp Upwork thường phải mất 20 phút để viết mỗi đề xuất từ đầu. Workflow này sẽ giúp bạn tự động hóa quy trình này bằng cách:

1. Đọc email cảnh báo công việc từ Vollna
2. Đánh giá từng công việc phù hợp với hồ sơ của bạn
3. Sử dụng AI Claude để viết đề xuất cá nhân hóa
4. Lưu nháp Gmail sẵn sàng gửi

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 20 phút mỗi đề xuất
- Đề xuất cá nhân hóa theo từng công việc
- Tự động lưu nháp Gmail sẵn sàng gửi
- Theo dõi toàn bộ quá trình xử lý công việc
- Hoạt động liên tục 24/7 không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Upwork và Vollna
- Tài khoản Gmail để nhận cảnh báo công việc
- API key của Anthropic cho Claude AI
- Google Sheets để lưu log công việc
- (Tùy chọn) Tài khoản Slack để nhận thông báo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15789](https://n8n.io/workflows/15789)
2. Click "Import" và chọn "Import from URL"
3. Dán URL workflow vào ô nhập liệu
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Check for Vollna Alerts (gmailTrigger)**
   - Kết nối tài khoản Gmail của bạn
   - Đảm bảo bạn đã cấu hình Vollna gửi cảnh báo đến email này

2. **Configure Profile and Settings (code)**
   - Cấu hình hồ sơ cá nhân:
     - Tên của bạn
     - Kỹ năng chuyên môn
     - Mức giá giờ
     - Ngân sách tối thiểu
     - Ngưỡng điểm (score threshold)
     - Tiểu sử ngắn

3. **Claude Haiku (lmChatAnthropic)**
   - Tạo mới credential Anthropic
   - Nhập API key từ [console.anthropic.com](https://console.anthropic.com)
   - Đảm bảo bạn đã chọn model "claude-haiku-4-5-20251001"

4. **Save Proposal as Draft (gmail)**
   - Kết nối tài khoản Gmail của bạn
   - Đảm bảo bạn đã chọn operation "createDraft"

5. **Log Job to Sheets (googleSheets)**
   - Tạo mới Google Sheet với các cột:
     - Timestamp
     - Job Title
     - Budget
     - Score
     - Status
     - Draft Saved
     - Job URL
   - Kết nối tài khoản Google của bạn
   - Đảm bảo bạn đã chọn operation "append"

6. **Notify New Draft - Slack (slack) (Tùy chọn)**
   - Tạo mới credential Slack
   - Nhập thông tin xác thực Slack
   - Chọn channel để nhận thông báo

#### 3. Kích hoạt ⚡️
1. Click vào nút "Activate" để kích hoạt workflow
2. Test workflow bằng cách gửi email cảnh báo Vollna mẫu
3. Kiểm tra nháp Gmail và Google Sheets để xác nhận workflow hoạt động

### ✍️ Mẹo & gợi ý nâng cao
- Thay đổi SCORE_THRESHOLD trong node Settings để điều chỉnh độ chọn lọc
- Chỉnh sửa prompt trong node Write Proposal with Claude để phù hợp với phong cách viết của bạn
- Thêm node Slack sau khi lưu nháp để nhận thông báo mỗi khi có đề xuất mới
- Tự động gửi email nháp sau khi đã được duyệt
- Kết hợp với các công cụ khác như Trello để quản lý công việc

### 📌 Kết luận
Workflow này sẽ giúp các sếp Upwork tiết kiệm thời gian quý giá, tạo ra đề xuất chất lượng cao và duy trì quy trình làm việc hiệu quả. Bằng cách tự động hóa quy trình viết đề xuất, bạn có thể tập trung vào những công việc quan trọng hơn và tăng năng suất làm việc.