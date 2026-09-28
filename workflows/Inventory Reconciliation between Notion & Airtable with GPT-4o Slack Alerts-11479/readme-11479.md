---
title: "🚀 Tự động đối soát kho hàng Notion và Airtable bằng GPT-4o và Slack Alerts"
description: "Hướng dẫn xây dựng workflow n8n tự động so sánh tồn kho giữa Notion và Airtable, tự động cập nhật lệch kho, dùng GPT-4o tổng hợp báo cáo gửi Slack."
slug: "tu-dong-doi-soat-kho-notion-airtable-gpt-4o-slack"
tags: [n8n, automation, airtable, notion, openai, slack]
keywords: [n8n workflow, đối soát kho tự động, notion airtable sync, gpt-4o slack alert, tự động hóa kho hàng]
---

# 🚀 Tự động đối soát kho hàng Notion và Airtable bằng GPT-4o và Slack Alerts

Các sếp có đang đau đầu vì số liệu tồn kho giữa hệ thống quản lý (Airtable) và kiểm kê thực tế (Notion) thường xuyên lệch nhau? Việc kiểm tra thủ công từng mặt hàng vừa tốn thời gian, dễ nhầm lẫn, lại chậm trễ trong việc phát hiện thất thoát.

Giải pháp ở đây là sử dụng workflow n8n tự động hóa 100% được thiết kế bởi chuyên gia Rahul Joshi. Workflow này sẽ tự động kéo dữ liệu từ Notion và Airtable, so sánh số liệu, tự động đồng bộ lại số lượng chính xác, đồng thời sử dụng sức mạnh của **GPT-4o** để tóm tắt và gửi cảnh báo trực quan qua **Slack** cho đội ngũ vận hành.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Đồng bộ dữ liệu thông minh:** Tự động đối soát giữa kho thực tế (Notion) và hệ thống (Airtable) mà không cần can thiệp thủ công.
- **Tự động sửa lỗi:** Nếu phát hiện lệch kho, workflow sẽ tự động cập nhật lại số lượng chính xác vào Airtable.
- **Cảnh báo sắc bén với AI:** Sử dụng GPT-4o (Azure OpenAI) để tạo thông báo ngắn gọn, dễ hiểu gửi thẳng vào kênh Slack của bộ phận vận hành.
- **Quản trị lỗi chuyên nghiệp:** Mọi payload không hợp lệ đều được ghi log chi tiết vào Google Sheets để dễ dàng kiểm tra.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn (Self-hosted hoặc Cloud).
- **Tài khoản & Credentials:**
  - **Notion API:** Nơi lưu trữ số liệu kiểm kê vật lý.
  - **Airtable API:** Nơi lưu trữ dữ liệu hệ thống (System inventory record).
  - **Azure OpenAI (GPT-4o):** Dùng cho các node Agent tạo nội dung tóm tắt trên Slack.
  - **Slack API:** Để gửi thông báo kết quả đối soát.
  - **Google Sheets OAuth2:** Để lưu log các yêu cầu có cấu trúc không hợp lệ.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp copy đoạn mã JSON của workflow từ nguồn gốc hoặc tải file về.
- Tại giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng ba chấm ở góc trên bên phải -> Chọn **Import from File** hoặc **Paste JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công, các sếp cần cấu hình lại các node cốt lõi sau:
- **Fetch Records from Notion Database & Fetch Records from Airtable:** Chọn đúng Credentials của Notion và Airtable, sau đó trỏ đến đúng Database ID và Table Name của các sếp.
- **Log Invalid Versioning Requests to Google Sheets:** Cấu hình tài khoản Google Sheets và chọn file/sheet dùng để lưu log dữ liệu lỗi.
- **Configure GPT-4o – Slack Summary Model & Model2:** Kết nối thông tin Azure OpenAI API của các sếp và đảm bảo model được chọn là `gpt-4o`.
- **Slack – Send Summary Notification & Send Update Notification:** Cấu hình Slack Credentials và chọn Channel nhận thông báo cảnh báo/tóm tắt tồn kho.

#### 3. Kích hoạt ⚡️
- Nhấn nút **‘Execute workflow’** (thông qua trigger `When clicking ‘Execute workflow’`) để chạy thử nghiệm với dữ liệu mẫu.
- Kiểm tra kết quả trên Slack và Google Sheets xem hệ thống đã hoạt động trơn tru chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
- **Đổi Trigger:** Thay vì dùng `Manual Trigger`, các sếp có thể đổi thành `Schedule Trigger` (Cron node) để chạy tự động đối soát kho vào mỗi cuối ngày hoặc đầu tuần.
- **Mở rộng kênh thông báo:** Kết hợp thêm node Telegram hoặc Microsoft Teams bên cạnh Slack để đa dạng hóa kênh nhận tin cho quản lý kho.
- **Báo cáo định kỳ:** Tạo thêm một nhánh tổng hợp dữ liệu hàng tuần gửi qua Email cho ban giám đốc.

### 📌 Kết luận
Việc kiểm kê và đối soát kho thủ công không chỉ mất thời gian mà còn tiềm ẩn nhiều rủi ro sai sót tài chính. Với workflow n8n kết hợp Notion, Airtable và GPT-4o này, các sếp hoàn toàn có thể tự động hóa toàn bộ quy trình kiểm soát tồn kho một cách chuyên nghiệp và chính xác tuyệt đối. Triển khai ngay thôi nào các sếp!