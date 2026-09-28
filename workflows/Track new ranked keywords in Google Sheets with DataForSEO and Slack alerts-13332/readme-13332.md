---
title: "🚀 Theo dõi từ khóa mới xếp hạng trên Google Sheets với DataForSEO và cảnh báo Slack"
description: "Tự động hóa theo dõi từ khóa mới xếp hạng cho các domain của bạn, lưu vào Google Sheets và nhận cảnh báo Slack hàng tuần. Tiết kiệm thời gian SEO và tăng hiệu quả công việc."
slug: "theo-doi-tu-khoa-moi-xep-hang-google-sheets-dataforseo-slack"
tags: [n8n, automation, no-code, seo, dataforseo, google-sheets, slack]
keywords: [n8n workflow, tự động hóa seo, từ khóa xếp hạng, dataforseo, google sheets, slack alerts]
---

# 🚀 Theo dõi từ khóa mới xếp hạng với Google Sheets và Slack Alerts

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp SEO khi phải theo dõi thủ công hàng trăm từ khóa xếp hạng hàng tuần. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa quá trình theo dõi hàng tuần
- **Chính xác cao**: So sánh dữ liệu từ nhiều nguồn đáng tin cậy
- **Cá nhân hóa**: Nhận báo cáo chỉ chứa những từ khóa mới quan trọng
- **Hoạt động liên tục**: Theo dõi 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (để sử dụng Google Sheets API)
- API Key từ DataForSEO (để truy cập dữ liệu xếp hạng)
- Tài khoản Slack (để nhận cảnh báo)
- File Google Sheets mẫu đã được chuẩn bị theo [hướng dẫn này](https://docs.google.com/spreadsheets/d/1FO9Btg5y5TmE56La4O-QzJbEjGAZLe3zG0phB7eXnqs/edit?pli=1&gid=0#gid=0)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [trang workflow trên n8n.io](https://n8n.io/workflows/13332)
2. Click vào nút "Copy Workflow Code"
3. Trong n8n Editor, click vào "Import from Clipboard" và dán mã JSON đã copy

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get targets"**:
   - Chọn credentials Google Sheets OAuth2
   - Điền ID của spreadsheet chứa danh sách domain mục tiêu
   - Đảm bảo spreadsheet có cấu trúc giống như [mẫu này](https://docs.google.com/spreadsheets/d/1FO9Btg5y5TmE56La4O-QzJbEjGAZLe3zG0phB7eXnqs/edit?pli=1&gid=0#gid=0)

2. **Node "Get ranked keywords"**:
   - Chọn credentials DataForSEO API
   - Cấu hình các tham số bổ sung nếu cần (country, language, device...)

3. **Node "Get previous keywords"**:
   - Chọn credentials Google Sheets OAuth2
   - Điền ID của spreadsheet lưu trữ từ khóa xếp hạng
   - Đảm bảo spreadsheet có cấu trúc giống như [mẫu này](https://docs.google.com/spreadsheets/d/1FO9Btg5y5TmE56La4O-QzJbEjGAZLe3zG0phB7eXnqs/edit?pli=1&gid=1681593026#gid=1681593026)

4. **Node "Send a message"**:
   - Chọn credentials Slack OAuth2
   - Cấu hình kênh Slack nhận thông báo
   - Tùy chỉnh nội dung thông báo nếu cần

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Node" trên node "Run every Monday" để test dữ liệu mẫu
2. Sau khi test thành công, click vào nút "Activate" để kích hoạt workflow
3. Workflow sẽ tự động chạy hàng tuần vào thứ Hai theo múi giờ đã cấu hình

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Telegram**: Thay thế node Slack bằng node Telegram để nhận thông báo trên ứng dụng nhắn tin phổ biến hơn
- **Lưu log hoạt động**: Thêm node lưu log hoạt động vào Google Sheets để theo dõi lịch sử thay đổi
- **Báo cáo định kỳ**: Tạo bản báo cáo tổng hợp hàng tháng từ dữ liệu đã thu thập
- **Kết hợp với các công cụ khác**: Kết nối với các công cụ SEO khác như Ahrefs, Moz để có dữ liệu toàn diện hơn

### 📌 Kết luận
Workflow này giúp các sếp SEO tiết kiệm thời gian quý giá trong việc theo dõi từ khóa xếp hạng hàng tuần. Bằng cách tự động hóa quá trình này, các sếp có thể tập trung vào những nhiệm vụ quan trọng hơn và tăng hiệu quả công việc lên gấp nhiều lần. Hãy thử ngay và trải nghiệm sự khác biệt!