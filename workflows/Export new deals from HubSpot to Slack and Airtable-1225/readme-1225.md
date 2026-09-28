---
title: "🚀 Tự động hóa đồng bộ Deal mới từ HubSpot sang Slack, Airtable và Google Slides với n8n"
description: "Hướng dẫn chi tiết xây dựng workflow n8n giúp tự động bắt sự kiện deal mới từ HubSpot, phân loại mức độ ưu tiên, thông báo qua Slack và lưu trữ dữ liệu vào Airtable cùng Google Slides."
slug: "export-new-deals-hubspot-slack-airtable"
tags: [n8n, automation, no-code, hubspot, slack, airtable, sales]
keywords: [n8n workflow, hubspot automation, đồng bộ hubspot slack airtable, tự động hóa sales, n8n hubspot trigger]
---

# 🚀 Tự động hóa đồng bộ Deal mới từ HubSpot sang Slack, Airtable và Google Slides

Các sếp trong đội ngũ Sales và Operations có đang gặp cơn ác mộng mỗi khi có deal mới hoặc ticket được tạo trên HubSpot? Đội ngũ cứ phải liên tục kiểm tra CRM thủ công, copy-paste thông tin qua Airtable để lưu trữ, rồi lại thủ công bắn tin nhắn lên group Slack để thông báo cho team, chưa kể việc phải tạo tài liệu trên Google Slides cho từng khách hàng lớn. Quá nhiều thao tác chân tay dễ dẫn đến sai sót và chậm trễ trong việc chăm sóc khách hàng!

Giải pháp ở đây là gì? Hãy để workflow n8n này "gánh" toàn bộ quy trình đó thay các sếp hoàn toàn tự động 24/7 mà không tốn một đồng chi phí code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Ngay khi có deal hoặc ticket mới trên HubSpot, hệ thống sẽ tự kích hoạt mà không cần con người nhúng tay.
- **Phân loại thông minh:** Tự động lọc và xử lý theo mức độ ưu tiên (high-priority / low-priority) để có luồng chăm sóc phù hợp.
- **Đa kênh đồng bộ:** Vừa đẩy thông báo tức thì lên kênh Slack (như `#closedwon`), vừa ghi nhận dữ liệu vào bảng Airtable và tạo slide trên Google Slides.
- **Loại bỏ sai sót:** Đảm bảo không bỏ sót bất kỳ khách hàng tiềm năng nào, tối ưu hóa tốc độ phản hồi của đội ngũ Sales.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **HubSpot** có quyền cấu hình Webhook/Trigger.
- Workspace **Slack** và quyền tạo/kết nối Bot để gửi tin nhắn.
- Tài khoản **Airtable** với Base và Table đã được tạo sẵn để hứng dữ liệu Deal.
- Tài khoản **Google** để kết nối với Google Slides.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ [n8n Workflow #1225](https://n8n.io/workflows/1225), sau đó chọn **Import from File** hoặc copy trực tiếp mã JSON và dán vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 10 nodes chính phối hợp nhịp nhàng với nhau. Các sếp cần cấu hình kỹ các điểm sau:

- **Hubspot Trigger**: Node này đóng vai trò "còi báo động". Các sếp cần kết nối tài khoản HubSpot (`hubspotApi`) và chọn sự kiện kích hoạt (Event) khi có deal hoặc ticket mới được tạo.
- **Hubspot (Get)**: Node dùng để lấy thông tin chi tiết đầy đủ của deal/ticket vừa kích hoạt từ HubSpot dựa vào ID.
- **IF / Switch / Set**: Các node xử lýlogic logic để chuẩn hóa dữ liệu, phân loại luồng chạy tùy thuộc vào thuộc tính của deal.
- **high-priority & low-priority (Hubspot)**: Xử lý các tác vụ liên quan đến ticket/deal theo mức độ ưu tiên cao hay thấp.
- **#closedwon (Slack)**: Chọn đúng channel Slack (ví dụ: `#closedwon` hoặc kênh thông báo sales của công ty) để bot bắn tin nhắn chúc mừng/thông báo deal mới. Cần cấu hình `slackApi` credentials.
- **Airtable**: Kết nối tài khoản (`airtableApi`), chọn đúng Base và Table, sau đó mapping các trường dữ liệu từ HubSpot (như tên deal, giá trị, khách hàng) vào các cột tương ứng trong Airtable với thao tác `append`.
- **Google Slides**: Kết nối tài khoản Google (`googleSlidesOAuth2Api`) nếu muốn tự động hóa việc khởi tạo template slide thuyết trình/hợp đồng cho deal.

#### 3. Kích hoạt ⚡️
- Nhấp vào **Execute Workflow** để chạy thử nghiệm (Test Run) bằng cách tạo một deal mẫu trên HubSpot và kiểm tra xem dữ liệu có chảy mượt mà sang Slack và Airtable hay không.
- Nếu mọi thứ xanh mướt (success), các sếp hãy bật công tắc **Active** ở góc trên cùng bên phải để workflow chính thức chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống quản lý sales trở nên "bá đạo" hơn nữa, các sếp có thể mở rộng workflow bằng cách:
- **Tích hợp AI (OpenAI/Claude):** Thêm node AI để tự động tóm tắt nội dung deal/ticket và viết văn phong chào mừng sinh động hơn trước khi đẩy lên Slack.
- **Báo cáo định kỳ:** Kết hợp thêm node Cron (Schedule Trigger) để tổng hợp số lượng deal trong tuần và gửi báo cáo tóm tắt vào mỗi thứ Hai hàng tuần.
- **Đa kênh thông báo:** Ngoài Slack, có thể bắn thêm một nhánh sang Telegram hoặc Email cho Giám đốc kinh doanh nắm bắt các deal giá trị lớn.

### 📌 Kết luận
Việc tự động hóa quy trình đồng bộ dữ liệu từ HubSpot sang Slack và Airtable không chỉ giúp tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần mà còn giúp đội ngũ Sales phản ứng cực nhanh với các cơ hội kinh doanh mới. Hãy cài đặt ngay hôm nay và tối ưu hóa vận hành doanh nghiệp cùng n8n các sếp nhé!