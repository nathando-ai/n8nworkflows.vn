---
title: "🚀 Tự động hóa tạo Zendesk Ticket từ Gmail và ghi log Google Sheets bằng n8n"
description: "Hướng dẫn xây dựng quy trình tự động biến email khách hàng thành Zendesk Ticket và tự động lưu vết lịch sử vào Google Sheets với n8n."
slug: "tu-dong-hoa-gmail-zendesk-google-sheets-n8n"
tags: [n8n, automation, zendesk, gmail, google-sheets, customer-support]
keywords: [n8n workflow, tu dong hoa gmail zendesk, zendesk ticket automation, google sheets logging n8n]
---

# 🚀 Tự động hóa tạo Zendesk Ticket từ Gmail và ghi log Google Sheets

Các sếp có bao giờ cảm thấy quá tải khi đội ngũ chăm sóc khách hàng phải liên tục kiểm tra hộp thư Gmail, copy nội dung thủ công để tạo ticket trên hệ thống Zendesk, rồi lại lọ mọ ghi chép lại vào bảng Excel/Google Sheets để theo dõi chưa? Quy trình thủ công này vừa mất thời gian, dễ bỏ sót email quan trọng, lại vừa thiếu tính đồng bộ.

Giải pháp là đây! Với workflow n8n được thiết kế bởi chuyên gia Rahul Joshi, hệ thống sẽ tự động hóa 100% từ khâu nhận email mới từ Gmail, chuẩn hóa dữ liệu, khởi tạo ticket trên Zendesk, cho đến việc ghi log lưu vết toàn bộ thông tin vào Google Sheets mà không cần một dòng code phức tạp nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tốc độ phản hồi tức thì:** Khách hàng vừa gửi email là ngay lập tức có ticket trên Zendesk được khởi tạo, không còn độ trễ do con người.
- **Loại bỏ sai sót:** Dữ liệu từ tiêu đề, nội dung email, thông tin người gửi được chuẩn hóa và truyền tải chính xác 100% vào hệ thống hỗ trợ.
- **Quản lý minh bạch:** Mọi yêu cầu hỗ trợ đều được tự động lưu vết và cập nhật trạng thái vào Google Sheets, giúp việc thống kê, tra cứu trở nên cực kỳ dễ dàng.
- **Vận hành 24/7 không mệt mỏi:** Hệ thống tự động chạy ngầm liên tục, giải phóng thời gian cho đội ngũ support tập trung vào việc giải quyết vấn đề của khách hàng thay vì làm việc chân tay.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Gmail** (để cấu hình Trigger nhận email).
- **Tài khoản Zendesk** (với quyền tạo API/Credentials để hệ thống kết nối).
- **Google Sheets** (tạo sẵn một trang tính với các cột tương ứng để lưu log: Thời gian, Email người gửi, Tiêu đề, Mã Ticket, Link Ticket, Trạng thái...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc copy đoạn JSON từ nguồn, sau đó dán trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các credentials và thông số tại các node sau:

- **Gmail Trigger**: 
  - Kết nối tài khoản `gmailOAuth2`.
  - Cấu hình thư mục hoặc nhãn (label) email cần lắng nghe (ví dụ: Inbox hoặc một nhãn hỗ trợ riêng). Node này sẽ phát ra thông tin chi tiết về tiêu đề, nội dung (plain/HTML), người gửi, thời gian...
- **Normalize Gmail Data (Node Code)**: 
  - Node này dùng để làm sạch và chuyển đổi dữ liệu thô từ Gmail thành một schema chuẩn (như `requesterEmail`, `subject`, `bodyText/bodyHtml`, `threadId`, `messageId`,...). Các sếp có thể giữ nguyên cấu trúc code có sẵn.
- **Create Zendesk Ticket (Node Zendesk)**: 
  - Kết nối tài khoản `zendeskApi`.
  - Thiết lập hành động `create: ticket`. Map các trường dữ liệu từ bước trước vào như: Người yêu cầu (`requesterEmail`), Tiêu đề (`subject`), Nội dung mô tả (`bodyText/bodyHtml`), cùng với độ ưu tiên (priority) hoặc thẻ (tags) nếu cần.
- **Format Sheet Data (Node Code)**: 
  - Node này kết hợp dữ liệu từ Gmail và kết quả trả về của Zendesk (như `ticketId`, `ticketUrl`, `status`) thành một dòng dữ liệu hoàn chỉnh, sẵn sàng đẩy lên Google Sheets.
- **Log to Google Sheets (Node Google Sheets)**: 
  - Kết nối tài khoản `googleSheetsOAuth2Api`.
  - Chọn thao tác `appendOrUpdate` (Thêm mới hoặc cập nhật dựa trên khóa duy nhất như `messageId` hoặc `ticketId`). Chọn đúng file Spreadsheet và Sheet Name đã chuẩn bị sẵn.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi một email test vào Gmail đã cấu hình để kiểm tra luồng chạy xem dữ liệu đã qua các node suôn sẻ chưa.
- Sau khi test thành công, gạt công tắc sang **Active** để workflow chính thức hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Slack/Telegram:** Thêm một node Slack hoặc Telegram ngay sau khi tạo ticket thành công để bắn thông báo "Đã có ticket mới từ [Email]" vào group chat nội bộ của team support.
- **Phân loại thông minh bằng AI:** Kết hợp thêm một node AI Agent (OpenAI/Anthropic) trước bước tạo Zendesk để tự động phân tích độ khẩn cấp (Urgency) hoặc gắn nhãn (Category) cho email khách hàng.
- **Báo cáo định kỳ:** Sử dụng lịch (Schedule Trigger) kết hợp Google Sheets để tổng hợp số lượng ticket mỗi ngày và gửi báo cáo qua email cho quản lý.

### 📌 Kết luận
Tự động hóa quy trình chăm sóc khách hàng từ Gmail sang Zendesk chưa bao giờ dễ dàng đến thế với n8n. Hãy áp dụng ngay workflow này để tối ưu hóa hiệu suất làm việc và mang lại trải nghiệm chuyên nghiệp nhất cho khách hàng của các sếp nhé!