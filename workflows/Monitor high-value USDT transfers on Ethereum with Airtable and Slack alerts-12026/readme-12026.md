---
title: "🚀 Tự động giám sát giao dịch USDT giá trị cao trên Ethereum với n8n, Airtable và Slack"
description: "Hướng dẫn xây dựng workflow n8n tự động quét blockchain Ethereum mỗi ngày, lọc các giao dịch USDT 'khủng', lưu vào Airtable và gửi cảnh báo thông minh qua Slack."
slug: "giam-sat-giao-dich-usdt-ethereum-airtable-slack"
tags: [n8n, automation, crypto, blockchain, airtable, slack]
keywords: [n8n workflow, giám sát USDT, crypto automation, airtable slack bot, ethereum tracker]
---

# 🚀 Tự động giám sát giao dịch USDT giá trị cao trên Ethereum với Airtable và Slack

Các nhà đầu tư crypto, quỹ đầu tư hoặc dự án Web3 thường tốn rất nhiều thời gian để theo dõi các dòng tiền lớn (whale tracking) trên blockchain một cách thủ công. Việc cứ phải dán mắt vào các trình duyệt block explorer như Etherscan vừa mệt mỏi, vừa dễ bỏ lỡ cơ hội.

Đừng lo, workflow n8n cực xịn sò được thiết kế bởi **WeblineIndia** này sẽ thay các sếp làm việc đó 24/7. Hệ thống sẽ tự động quét các giao dịch USDT trên mạng Ethereum, lọc ra các khoản chuyển tiền "cá voi" (high-value), tự động lưu trữ cơ sở dữ liệu vào **Airtable** và bắn thông báo tổng hợp cực kỳ chi tiết lên **Slack**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Theo dõi dòng tiền tự động:** Không cần check blockchain thủ công hay sợ bỏ lỡ biến động lớn.
- **Lọc thông minh:** Chỉ tập trung vào các giao dịch vượt ngưỡng giá trị (threshold) cài đặt sẵn.
- **Lưu trữ gọn gàng:** Tự động đồng bộ toàn bộ dữ liệu giao dịch khủng vào Airtable để phục vụ phân tích.
- **Cảnh báo tức thì:** Gửi báo cáo tổng hợp kèm giao dịch lớn nhất thẳng vào kênh Slack của team.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn (Cloud hoặc Self-hosted).
- **Alchemy API / Node RPC:** Cần một URL API Ethereum Mainnet (từ Alchemy, Infura, v.v.) cho node HTTP Request.
- **Tài khoản Airtable:** Để lưu trữ log giao dịch.
- **Workspace Slack:** Để nhận thông báo (kèm Slack App / Bot token).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ n8n.io hoặc copy toàn bộ JSON và dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình kỹ các node sau để hệ thống chạy trơn tru:

- **Get latest blocknumber** & **Fetch USDT transaction logs** (HTTP Request): 
  - Điền URL API Ethereum Mainnet (Ví dụ: Alchemy API URL) vào các node HTTP.
  - Hợp đồng USDT (USDT Contract Address) và Topic sự kiện `Transfer` đã được cấu hình sẵn trong logic request.
- **Filter high value transaction** (Node `IF`): 
  - Điều chỉnh hạn mức giá trị USDT (value threshold) tại đây theo nhu cầu của các sếp (ví dụ: giao dịch từ $10,000 trở lên mới được coi là "high-value").
- **Save transaction** (Node `Airtable`):
  - Kết nối tài khoản Airtable bằng **Airtable Token API**.
  - Chọn đúng Base và Table. Đảm bảo các trường (fields) trong bảng Airtable khớp với dữ liệu workflow đẩy lên: `Contract`, `From Address`, `To Address`, `Value`, `Block Number`, và `txHash`.
- **Send transaction alert** (Node `Slack`):
  - Kết nối tài khoản **Slack API**.
  - Chọn kênh (channel) muốn bot bắn tin nhắn cảnh báo giao dịch khủng.

#### 3. Kích hoạt ⚡️
- Chạy thử (Test run) thủ công một lần với node **Daily Check** (`scheduleTrigger`) để kiểm tra dữ liệu từ bước gọi API đến Slack.
- Kiểm tra lại các bảng Airtable xem data đã đổ về đúng chuẩn chưa.
- Bật công tắc **Active** để workflow tự động chạy định kỳ mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Ngoài Slack, các sếp có thể nhân bản node thông báo để bắn thêm tin nhắn vào nhóm Telegram qua Telegram Bot.
- **Tần suất linh hoạt:** Đổi node `Daily Check` sang dạng chạy mỗi giờ (Hourly) nếu theo dõi các token có biến động thanh khoản cực cao.
- **Lưu trữ mở rộng:** Có thể kết hợp thêm Google Sheets hoặc Notion nếu không muốn dùng Airtable.

### 📌 Kết luận
Một workflow hoàn hảo giúp các sếp nắm thóp dòng tiền lớn trên hệ sinh thái Ethereum mà không tốn một phút check thủ công nào. Lên đồ ngay và tự động hóa việc theo dõi crypto của team thôi nào!