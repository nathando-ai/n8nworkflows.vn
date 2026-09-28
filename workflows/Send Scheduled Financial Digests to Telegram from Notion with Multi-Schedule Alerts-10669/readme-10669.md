---
title: "💰 Tự động hóa tài chính cá nhân: Gửi báo cáo tài chính định kỳ qua Telegram từ Notion"
description: "Hướng dẫn tự động hóa báo cáo tài chính cá nhân với n8n, kết nối Notion và Telegram để nhận thông báo định kỳ về giao dịch, ngân sách và tài sản."
slug: "tu-dong-hoa-tai-chinh-ca-nhan-notion-telegram"
tags: [n8n, automation, no-code, personal finance, notion, telegram]
keywords: [n8n workflow, tự động hóa tài chính, báo cáo tài chính, notion, telegram]
---

# 💰 Tự động hóa tài chính cá nhân: Gửi báo cáo tài chính định kỳ qua Telegram từ Notion

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có biết rằng quản lý tài chính cá nhân thủ công là một công việc tốn thời gian và dễ gây lỗi? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình báo cáo tài chính hàng ngày, hàng tuần và hàng tháng chỉ trong vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động tổng hợp dữ liệu tài chính từ Notion mà không cần can thiệp thủ công.
- **Chính xác**: Giảm thiểu lỗi do nhập liệu thủ công với dữ liệu được xử lý tự động.
- **Cá nhân hóa**: Nhận báo cáo tài chính định kỳ theo nhu cầu cá nhân.
- **Hoạt động liên tục**: Workflow chạy tự động 24/7, không cần giám sát.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Notion đã tạo và cấu hình hệ thống tài chính cá nhân theo [template này](https://www.notion.so/templates/personal-finance-system).
- Token Notion Integration và kết nối với các database tài chính.
- Tài khoản Telegram và bot token từ BotFather.
- Tài khoản n8n đã cài đặt và cấu hình các credentials: Notion API và Telegram Bot.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào [n8n.io/workflows/10669](https://n8n.io/workflows/10669) để tải file JSON của workflow.
2. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON đã tải về.
3. Hoặc copy toàn bộ nội dung JSON và paste vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Daily Trigger**: Cấu hình thời gian gửi báo cáo hàng ngày.
2. **Weekly Trigger**: Cấu hình thời gian gửi báo cáo hàng tuần.
3. **Monthly Start Trigger & Monthly End Trigger**: Cấu hình thời gian gửi báo cáo đầu và cuối tháng.
4. **Notion Nodes**:
   - **Get Financial Obligations**: Cập nhật ID của database "Financial Obligations" trong Notion.
   - **Get Debit Transactions**: Cập nhật ID của database "Debit Transactions" trong Notion.
   - **Get Monthly Budget Left**: Cập nhật ID của database "Budget" trong Notion.
   - **Get Monthly Budget Spent**: Cập nhật ID của database "Budget" trong Notion.
   - **Get Invoices**: Cập nhật ID của database "Invoices" trong Notion.
   - **Fund Amount Left**: Cập nhật ID của database "Funds" trong Notion.
   - **Get Income This Month**: Cập nhật ID của database "Income" trong Notion.
   - **Get Liquidity**: Cập nhật ID của database "Assets and Liabilities" trong Notion.
   - **Get Semi Liquid**: Cập nhật ID của database "Assets and Liabilities" trong Notion.
5. **Telegram Node**:
   - **Send Message4**: Cập nhật chat ID của Telegram nơi bạn muốn nhận báo cáo.

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, nhấn vào nút "Activate" để kích hoạt workflow.
2. Thực hiện test run với dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
3. Kiểm tra Telegram để xác nhận báo cáo đã được gửi thành công.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm các báo cáo khác**: Các sếp có thể thêm các báo cáo khác như báo cáo đầu tư, báo cáo tiết kiệm, v.v.
- **Kết hợp với Slack**: Thay thế node Telegram bằng node Slack để nhận báo cáo trên Slack.
- **Lưu log**: Thêm node lưu log để theo dõi lịch sử gửi báo cáo.
- **Gửi báo cáo định kỳ**: Cấu hình gửi báo cáo theo tuần, tháng hoặc quý.

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình báo cáo tài chính cá nhân chỉ trong vài bước đơn giản. Workflow này giúp tiết kiệm thời gian, giảm thiểu lỗi và cung cấp dữ liệu tài chính chính xác và cập nhật. Hãy áp dụng ngay để quản lý tài chính cá nhân một cách hiệu quả hơn!