---
title: "🚀 Tự động Giám sát Chi tiêu Quảng cáo hàng ngày qua Google Sheets và Cảnh báo Slack với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động kiểm tra chi tiêu quảng cáo từ Google Sheets mỗi ngày, tính toán tổng tiền và gửi cảnh báo tức thì qua Slack nếu vượt ngân sách $100."
slug: "giam-sat-chi-tieu-quang-cao-google-sheets-slack-n8n"
tags: [n8n, automation, google-sheets, slack, marketing-automation]
keywords: [n8n workflow, tự động hóa chi tiêu quảng cáo, Google Sheets n8n, Slack alert n8n, quản lý ngân sách marketing]
---

# 🚀 Tự động Giám sát Chi tiêu Quảng cáo hàng ngày qua Google Sheets và Cảnh báo Slack

Các sếp chạy quảng cáo Facebook, Google hay TikTok chắc chắn đã từng đau đầu vì quên kiểm tra ngân sách, dẫn đến việc "vượt khung" tiền quảng cáo mà cuối tháng mới phát hiện ra. Việc kiểm tra thủ công mỗi ngày vừa mất thời gian lại dễ bỏ sót.

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ xịn sò được thiết kế bởi chuyên gia **Robert Breen**. Workflow này sẽ tự động hóa 100% quy trình: lấy dữ liệu từ Google Sheets, tổng hợp chi tiêu theo ngày, sắp xếp theo thứ tự mới nhất và bắn tin nhắn cảnh báo thẳng vào Slack nếu chi tiêu vượt mức $100!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải mở file Excel/Google Sheets kiểm tra thủ công mỗi sáng.
- **Cảnh báo tức thì**: Nhận thông báo ngay lập tức trên Slack khi chi tiêu ngày vượt ngưỡng $100 để kịp thời tối ưu chiến dịch.
- **Vận hành tự động 24/7**: Lên lịch chạy tự động hàng ngày bằng Cron hoặc test thủ công bất cứ lúc nào.
- **Chính xác & Minh bạch**: Dữ liệu được tổng hợp tự động chuẩn xác từ Google Sheets, loại bỏ sai sót do con người.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản **Google Cloud Console** để cấu hình Google Sheets API & OAuth2.
- Tài khoản **Slack** và quyền tạo Bot/App để gửi thông báo.
- Bản sao file Google Sheets mẫu: [Marketing Data Sheet - Copy Me](https://docs.google.com/spreadsheets/d/19aUQYZq02qHsCelO4eeV4sx_MTJJupC5qe0gDLQBtRA/edit?usp=sharing)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng danh sách 9 nodes sau để tạo workflow trong n8n Editor:
- `Test Workflow` (manualTrigger)
- `Schedule Workflow` (scheduleTrigger)
- `Get Data` (googleSheets)
- `Sum spend by Day` (summarize)
- `Sort Dates Descending` (code)
- `Keep only Last Day` (set)
- `Check if Spend over $100` (if)
- `Send Slack Message` (slack)
- `Do Nothign. Under 100` (noOp)

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

* **Node `Get Data` (Google Sheets):**
  - Kết nối tài khoản Google Sheets thông qua OAuth2.
  - Trỏ đến file Google Sheet dữ liệu quảng cáo của các sếp (đảm bảo file có các cột `Date` và `Spend ($)` ở dòng tiêu đề).

* **Node `Sort Dates Descending` (Code):**
  - Node này dùng đoạn mã JavaScript để sắp xếp ngày mới nhất lên đầu. Các sếp giữ nguyên đoạn code sau:
  ```js
  const items = $input.all();
  items.sort((a, b) => new Date(b.json.Date) - new Date(a.json.Date));
  return items;
  ```

* **Node `Check if Spend over $100` (If):**
  - Cấu hình điều kiện kiểm tra biến `sum_Spend_($)` xem có lớn hơn `100` hay không. Các sếp có thể thay đổi hạn mức này tùy theo nhu cầu ngân sách thực tế.

* **Node `Send Slack Message` (Slack):**
  - Tạo một Slack App tại [Slack API](https://api.slack.com/apps), cấp quyền `chat:write` và `channels:read`.
  - Kết nối Credentials trong n8n và chọn channel nhận cảnh báo.

#### 3. Kích hoạt ⚡️
- Nhấn **Test Workflow** để chạy thử nghiệm xem dữ liệu có đổ về đúng không và Slack có nhận được tin nhắn hay không.
- Bật công tắc **Active** để workflow tự động chạy theo lịch đã cài đặt ở node `Schedule Workflow`.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Zalo**: Ngoài Slack, các sếp có thể nối thêm node Telegram để gửi tin nhắn cảnh báo về điện thoại cá nhân tiện hơn.
- **Ghi log vào Google Sheets**: Tạo thêm một dòng ghi chú trạng thái cảnh báo vào Google Sheets để tiện theo dõi lịch sử kiểm tra.
- **Tùy biến ngưỡng cảnh báo động**: Thay vì cố định số tiền $100, các sếp có thể đọc hạn mức ngân sách từ một bảng cấu hình riêng biệt để dễ quản lý nhiều chiến dịch khác nhau.

### 📌 Kết luận
Với workflow n8n siêu việt này, các sếp đã có thể tự động hóa hoàn toàn việc giám sát chi tiêu quảng cáo mà không tốn một phút kiểm tra thủ công nào. Hãy áp dụng ngay để kiểm soát dòng tiền marketing hiệu quả và tối ưu hóa lợi nhuận cho doanh nghiệp!