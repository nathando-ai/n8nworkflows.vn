---
title: "🚀 Tự động chuyển tiếp tin nhắn Slack sang WhatsApp bằng n8n và MoltFlow"
description: "Hướng dẫn cài đặt workflow n8n giúp chuyển tiếp tin nhắn quan trọng từ Slack sang WhatsApp tự động 100%, không lo bỏ lỡ thông báo quan trọng."
slug: "chuyen-tiep-tin-nhan-slack-sang-whatsapp-n8n"
tags: [n8n, automation, no-code, slack, whatsapp, moltflow, social-media]
keywords: [n8n workflow, tự động hóa slack, chuyển tiếp slack sang whatsapp, moltflow, tich hop slack whatsapp]
---

# 🚀 Tự động chuyển tiếp tin nhắn Slack sang WhatsApp bằng n8n và MoltFlow

Các sếp có bao giờ cảm thấy mệt mỏi vì phải mở ứng dụng Slack liên tục để kiểm tra thông báo, dẫn đến việc dễ bỏ sót những tin nhắn quan trọng từ team? Việc cứ phải "dính chặt" mắt vào màn hình máy tính theo dõi kênh Slack thực sự rất mất thời gian và làm giảm năng suất làm việc.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n cực kỳ thông minh này. Nó sẽ tự động bắt sự kiện từ Slack và chuyển tiếp ngay lập tức thông tin quan trọng đó thẳng đến số WhatsApp cá nhân của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Không bỏ lỡ thông tin:** Nhận cảnh báo/tin nhắn Slack quan trọng trực tiếp trên WhatsApp ngay trong tích tắc.
- **Tự động hóa hoàn toàn:** Hoạt động 24/7 ngầm dưới hệ thống, không cần thao tác thủ công.
- **Tiết kiệm thời gian:** Không cần kè kè mở app Slack trên điện thoại hay máy tính cả ngày.
- **Linh hoạt lọc tin nhắn:** Dễ dàng tùy chỉnh bộ lọc theo kênh hoặc từ khóa thông qua node xử lý code.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản [MoltFlow](https://molt.waiflow.app) đã kết nối sẵn với WhatsApp.
- Quyền quản trị hoặc cấu hình Webhook trên workspace Slack của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp hãy copy đoạn JSON của workflow (hoặc tải file từ n8n templates với ID `13485`), sau đó dán (paste) trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 5 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Slack Webhook (Webhook Node):** 
  - Kích hoạt và lấy đường dẫn URL Webhook mà n8n cung cấp. 
  - Đưa đường dẫn này vào cấu hình Webhook (hoặc Slack App / Incoming Webhooks) trong workspace Slack của các sếp để đẩy dữ liệu dạng `POST` về n8n.
- **Format Message (Code Node):** 
  - Node này chịu trách nhiệm trích xuất nội dung tin nhắn và tên người gửi từ Slack.
  - Các sếp cần cấu hình điền đúng thông tin `YOUR_SESSION_ID` và `YOUR_PHONE` của tài khoản MoltFlow bên trong đoạn code để hệ thống biết gửi tin đến đâu.
- **Valid? (If Node):** 
  - Kiểm tra xem tin nhắn có hợp lệ hoặc thỏa mãn điều kiện lọc hay không trước khi đẩy đi.
- **Send to WhatsApp (HTTP Request Node):** 
  - Gửi request đến API của MoltFlow.
  - Cần cài đặt Credentials dạng **Header Auth** với khóa `X-API-Key` được cung cấp từ tài khoản MoltFlow của các sếp.
- **Log (Code Node):** 
  - Ghi lại lịch sử hoặc trạng thái xử lý tin nhắn để tiện theo dõi, debug khi cần thiết.

#### 3. Kích hoạt ⚡️
- Thực hiện test thử (Test run) bằng cách bắn một tin nhắn mẫu từ Slack.
- Kiểm tra xem WhatsApp đã nhận được tin nhắn hay chưa.
- Sau khi mọi thứ chạy mượt mà, gạt công tắc sang **Active** để workflow chính thức vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Lọc thông minh:** Tùy chỉnh thêm điều kiện ở node `Valid?` hoặc `Format Message` để chỉ chuyển tiếp tin nhắn chứa các từ khóa quan trọng (như "urgent", "error", "hot fix",...).
- **Đa nền tảng:** Có thể mở rộng thêm một nhánh song song để vừa gửi WhatsApp, vừa bắn thông báo về Telegram hoặc Slack channel khác của công ty.
- **Lưu lịch sử:** Kết nối thêm một node Google Sheets hoặc Airtable vào sau node Log để lưu lại toàn bộ lịch sử tin nhắn đã chuyển tiếp phục vụ việc thống kê.

### 📌 Kết luận
Việc tích hợp Slack và WhatsApp chưa bao giờ dễ dàng đến thế với sức mạnh của n8n và MoltFlow. Hãy thiết lập ngay hôm nay để tối ưu hóa khả năng nhận thông tin và làm chủ thời gian của các sếp nhé!