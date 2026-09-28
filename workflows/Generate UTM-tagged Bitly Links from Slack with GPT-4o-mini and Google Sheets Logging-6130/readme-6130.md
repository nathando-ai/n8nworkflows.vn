---
title: "🚀 Tự động tạo link UTM và rút gọn Bitly từ Slack bằng AI Agent và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tích hợp AI (GPT-4o-mini), Slack, Bitly và Google Sheets giúp team Marketing tự động tạo link UTM chuẩn chỉnh chỉ qua một tin nhắn."
slug: "tao-link-utm-bitly-tu-slack-ai-google-sheets"
tags: [n8n, automation, ai-agent, slack, bitly, google-sheets, marketing]
keywords: [n8n workflow, tao link utm tu dong, bitly ai agent, slack bot n8n, google sheets logger, gpt-4o-mini]
---

# 🚀 Tự động tạo link UTM và rút gọn Bitly từ Slack bằng AI Agent và Google Sheets

Các sếp làm Marketing chắc chắn đã quá quen thuộc với nỗi đau: Mất hàng giờ để thủ công điền các thông số UTM (`utm_source`, `utm_medium`, `utm_campaign`), vào Bitly rút gọn, rồi lại copy qua Google Sheets để lưu trữ. Sai sót một chút là hỏng cả một chiến dịch tracking!

Giải pháp đây rồi các sếp ơi! Workflow n8n này sẽ biến Slack thành một trợ lý AI thông minh. Team chỉ cần gắn thẻ bot và nhập yêu cầu bằng ngôn ngữ tự nhiên, AI sẽ tự động phân tích, chuẩn hóa tham số UTM, tạo link rút gọn Bitly, lưu log vào Google Sheets và trả kết quả ngược lại ngay trong thread Slack. 100% tự động, không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần thủ công gõ tham số UTM hay truy cập nhiều nền tảng khác nhau.
- **Chuẩn hóa dữ liệu 100%:** AI (GPT-4o-mini) tự động chuyển đổi các từ viết tắt (vd: "IG" thành "instagram") và tuân thủ quy tắc đặt tên UTM (chữ thường, gạch dưới).
- **Lưu trữ tập trung:** Mọi link tạo ra đều được log tự động vào Google Sheets để team dễ dàng quản lý và báo cáo.
- **Tương tác mượt mà:** Trả kết quả trực tiếp trong Slack thread, giúp mọi người cùng nắm thông tin chiến dịch.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để triển khai trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Slack Workspace:** Đã tạo Bot App với các quyền cần thiết để đọc/gửi tin nhắn (`Slack Trigger`, `Slack Response`, `Slack - Get User Name`).
- **OpenAI API Key:** Sử dụng cho các node `OpenAI Chat Model` (chạy model `gpt-4o-mini`).
- **Bitly Account & Access Token:** Để node `Bitly` tạo link rút gọn gắn UTM.
- **Google Sheets:** Một trang tính (Sheet) đã thiết lập sẵn các cột tiêu đề nhận dữ liệu UTM (Link gốc, Link Bitly, Source, Medium, Campaign, Người tạo...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor, hoặc import file JSON thông qua menu tuỳ chọn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các node quan trọng sau:

- **Slack Trigger & Slack Response:** Kết nối tài khoản Slack của tổ chức. Đảm bảo bot có quyền lắng nghe sự kiện (mention) và gửi tin nhắn phản hồi.
- **OpenAI Chat Model (và Model1):** Điền OpenAI API Key và chọn model `gpt-4o-mini`. Node này chịu trách nhiệm cho AI Agent phân tích ngữ cảnh tin nhắn Slack.
- **Bitly:** Cấu hình thông thực thực thực (Credentials) bằng Bitly Access Token để cấp quyền cho `Bitly Tool Node` sinh link rút gọn.
- **Google Sheets:** Kết nối tài khoản Google OAuth2. Chọn đúng file Spreadsheet và Sheet Name, sau đó ánh xạ (map) các trường dữ liệu mà AI và Bitly trả về vào đúng cột trong bảng.
- **If Node & Stop and Error:** Kiểm tra luồng logic rẽ nhánh, đảm bảo nếu quá trình tạo link Bitly gặp sự cố, workflow sẽ dừng lại an toàn và báo lỗi thay vì sập ngầm.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử gửi một tin nhắn gọi bot trên Slack (vd: `@BitlyBot tạo link https://example.com cho chiến dịch black friday trên ig`) để test run.
- Kiểm tra kết quả trả về trên Slack và dữ liệu đã được đẩy lên Google Sheets chưa.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để đưa vào sử dụng chính thức 24/7!

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Discord:** Có thể nối thêm node Telegram hoặc Discord sau node Google Sheets để bắn thông báo về channel chung của team Marketing mỗi khi có link chiến dịch mới được tạo.
- **Kiểm duyệt tự động:** Thêm một bước AI kiểm tra nội dung URL trước khi rút gọn để tránh việc nhân viên tạo link tới các trang web độc hại.
- **Báo cáo định kỳ:** Kết hợp thêm Google Sheets Trigger hoặc Schedule Trigger để tổng hợp số lượng link tạo theo tuần/tháng và gửi báo cáo tự động cho quản lý.

### 📌 Kết luận
Workflow tích hợp AI, Slack, Bitly và Google Sheets này là mảnh ghép hoàn hảo giúp tối ưu hóa quy trình làm việc cho các team Marketing hiện đại. Hãy áp dụng ngay hôm nay để giải phóng đội ngũ khỏi những thao tác thủ công nhàm chán!