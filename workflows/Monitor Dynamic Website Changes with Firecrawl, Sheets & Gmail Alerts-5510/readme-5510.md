---
title: "🚀 Giám sát thay đổi website động tự động với Firecrawl, Google Sheets & Gmail"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu web bằng Firecrawl, so sánh sự thay đổi với Google Sheets và gửi cảnh báo qua Gmail khi có biến động."
slug: "giam-sat-thay-doi-website-firecrawl-google-sheets-gmail"
tags: [n8n, automation, firecrawl, google-sheets, gmail, web-scraping]
keywords: [n8n workflow, giám sát website, firecrawl api, google sheets automation, cảnh báo thay đổi website, tự động hóa n8n]
---

# 🚀 Giám sát thay đổi website động tự động với Firecrawl, Google Sheets & Gmail

Các sếp có đang mất hàng giờ mỗi ngày chỉ để vào check xem đối thủ có thay đổi giá, cập nhật sản phẩm hay trang web tin tức có gì mới không? Việc kiểm tra thủ công này vừa nhàm chán, tốn thời gian lại cực kỳ dễ bỏ sót thông tin quan trọng. 

Đừng lo, bài toán này sẽ được giải quyết triệt để với **Workflow n8n giám sát website động tự động**. Workflow này sẽ thay các sếp "cắm chốt" 24/7 trên trang web mục tiêu, tự động cào dữ liệu, so sánh nội dung cũ - mới và bắn thông báo thẳng vào Gmail ngay lập tức khi phát hiện bất kỳ thay đổi nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập nguồn hay mất kết nối, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần động tay kiểm tra thủ công, tiết kiệm hàng chục giờ mỗi tuần.
- **Phát hiện chớp nhoáng:** Nhận email cảnh báo ngay lập tức (`Gmail`) kèm theo nội dung thay đổi chi tiết khi website có biến động.
- **Lưu trữ lịch sử minh bạch:** Mọi thay đổi và lịch sử quét đều được ghi lại khoa học trên `Google Sheets`.
- **Hoạt động không nghỉ:** Tích hợp linh hoạt với Webhook, Cron Job hoặc các dịch vụ monitoring bên ngoài để chạy định kỳ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã hoạt động (Cloud hoặc Self-hosted).
- **Tài khoản Firecrawl:** Lấy API Key tại [firecrawl.dev](https://firecrawl.dev).
- **Google Cloud Console:** Cấu hình API và OAuth2 cho Google Sheets.
- **Tài khoản Gmail:** Cấp quyền OAuth2 để gửi email tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow hoặc import file trực tiếp vào giao diện n8n Editor để hiển thị toàn bộ 13 nodes bao gồm: `Webhook`, `Firecrawl HTTP Request`, `Get Timestamp`, `Google Sheets` (các node đọc/ghi/cập nhật), `Is Equal?`, `Extract Differences`, `Gmail`, và `Respond to Webhook`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình kỹ các điểm sau:
- **Firecrawl HTTP Request:** Thêm Credentials dạng `Bearer Auth` sử dụng API Key từ Firecrawl. Cập nhật `url` của trang web cần theo dõi tại tham số của node.
- **Google Sheets Nodes (5 nodes liên quan):**
  - Tạo một Google Sheet có 2 tab: tab **'Log'** (ghi lịch sử) và tab **'comparison'** (lưu trạng thái so sánh).
  - Copy **Spreadsheet ID** từ URL và dán vào tất cả các node Google Sheets trong workflow.
  - Cấu trúc chuẩn cho tab **comparison**: Cột A (`last_timestamp`), Cột B (`last_content`), Cột C (`current_timestamp`), Cột D (`current_content`), Cột E (`row_number` - điền giá trị `2` ở dòng 2).
- **Gmail Node:** Kết nối tài khoản Gmail qua OAuth2, cấu hình địa chỉ nhận (`sendTo`), tiêu đề và mẫu email cảnh báo theo ý muốn.
- **Webhook Node:** Nhận URL kích hoạt từ bên ngoài (hoặc có thể thay thế bằng Cron Trigger nếu muốn chạy định kỳ tự động).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để chạy thử nghiệm thủ công xem dữ liệu có đổ về Google Sheets và email có bắn đi hay không.
- Bật công tắc **Active** để đưa workflow vào trạng thái hoạt động tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Chatops:** Thay vì chỉ gửi Gmail, hãy kết hợp thêm node `Slack` hoặc `Telegram` để nhận thông báo tức thời ngay trên điện thoại hoặc máy tính nhóm làm việc.
- **Lên lịch thông minh:** Kết hợp workflow này với dịch vụ như UptimeRobot hoặc Cron Job (`*/30 * * * *`) để gọi Webhook tự động quét website mỗi 30 phút.
- **Quản lý dữ liệu log:** Thêm một bước tự động xóa bớt các log cũ trên Google Sheets sau mỗi 30 ngày để bảng tính luôn gọn gàng, nhẹ nhàng.

### 📌 Kết luận
Workflow giám sát website với Firecrawl và Google Sheets thực sự là một "vũ khí bí mật" cho anh em làm Research, Marketing hoặc theo dõi đối thủ cạnh tranh. Hãy cài đặt ngay hôm nay để không bỏ lỡ bất kỳ biến động nào từ các trang web quan trọng!