---
title: "🚀 Theo dõi khóa học Udemy giảm giá 50%+ với Airtop, Google Sheets và cảnh báo Telegram"
description: "Tự động theo dõi khóa học Udemy giảm giá sâu (50%+) hàng ngày, lưu dữ liệu vào Google Sheets và nhận cảnh báo qua Telegram - giải pháp tự động hóa hoàn toàn không cần code."
slug: "theo-doi-khoa-hoc-udemy-giam-gia-50-voi-airtop-google-sheets-telegram"
tags: [n8n, automation, no-code, udemy, google-sheets, telegram]
keywords: [n8n workflow, tự động hóa, udemy, giảm giá, google sheets, telegram]
---

# 🚀 Theo dõi khóa học Udemy giảm giá 50%+ với Airtop, Google Sheets và cảnh báo Telegram

[Đoạn mở đầu: Phân tích nỗi đau thực tế của học viên/doanh nghiệp khi phải theo dõi thủ công các khóa học Udemy giảm giá. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian theo dõi thủ công hàng ngày
- Nhận thông báo tức thì về các khóa học giảm giá sâu (50%+)
- Dữ liệu được lưu trữ và quản lý chuyên nghiệp trên Google Sheets
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Airtop (để tự động hóa trình duyệt)
- Tài khoản Google với Google Sheets đã tạo
- Bot Telegram và Chat ID để nhận thông báo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/12248)
2. Nhấn nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, nhấn "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Create a session"**:
   - Kết nối tài khoản Airtop của bạn
   - Đảm bảo tài khoản có đủ credit để chạy workflow

2. **Node "Create a window"**:
   - Cập nhật URL tìm kiếm Udemy theo sở thích của bạn
   - Ví dụ: `https://www.udemy.com/courses/search/?q=python&price=price-free&sort=highest-rated`

3. **Node "Append 50% up disc data"**:
   - Kết nối tài khoản Google của bạn
   - Chọn spreadsheet và worksheet để lưu dữ liệu
   - Đảm bảo tài khoản có quyền chỉnh sửa spreadsheet

4. **Node "Send notify course deal"**:
   - Kết nối bot Telegram của bạn
   - Điền Bot Token và Chat ID để nhận thông báo

5. **Node "Schedule Trigger"**:
   - Điều chỉnh thời gian chạy workflow theo nhu cầu (mặc định: 00:00 hàng ngày)

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Execute Workflow" để test với dữ liệu mẫu
2. Kiểm tra kết quả trên Google Sheets và Telegram
3. Sau khi xác nhận hoạt động, nhấn "Activate" để chạy workflow tự động

### ✍️ Mẹo & gợi ý nâng cao
1. Thêm node "Email" để nhận bản sao các thông báo khóa học giảm giá
2. Kết hợp với workflow khác để tự động đăng ký khóa học giảm giá
3. Thiết lập cảnh báo cho các mức giảm giá khác (ví dụ: 30%+)
4. Tạo bản sao workflow cho các trang khóa học khác (Coursera, LinkedIn Learning...)

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và tiền bạc khi tìm kiếm khóa học Udemy giảm giá. Bằng cách tự động hóa quá trình theo dõi và cảnh báo, bạn sẽ không bỏ lỡ cơ hội học tập với giá ưu đãi. Hãy thử ngay và nâng cấp trải nghiệm học tập của mình!