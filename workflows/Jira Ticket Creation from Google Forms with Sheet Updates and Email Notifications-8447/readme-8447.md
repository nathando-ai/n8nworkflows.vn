---
title: "🚀 Tự động tạo Jira Ticket từ Google Forms, cập nhật Sheets và gửi Email thông báo"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tiếp nhận yêu cầu từ Google Forms, tạo Jira ticket, đồng bộ Google Sheets và gửi email thông báo qua Gmail."
slug: "tu-dong-hoa-tao-jira-ticket-tu-google-forms"
tags: [n8n, automation, no-code, jira, google-sheets, gmail]
keywords: [n8n workflow, tự động hóa jira, google forms n8n, đồng bộ google sheets, tự động gửi email gmail]
---

# 🚀 Tự động hóa tạo Jira Ticket từ Google Forms với n8n

Các sếp có đang gặp tình trạng nhân sự hoặc khách hàng gửi yêu cầu qua Google Form, rồi đội ngũ IT/Project Manager phải copy-paste thủ công từng dòng sang Jira, sau đó lại lọ mọ cập nhật lại file Excel/Google Sheets và gửi email phản hồi? Quy trình thủ công này không chỉ tốn thời gian, dễ bỏ sót thông tin mà còn làm chậm tiến độ dự án.

Với workflow n8n này, các sếp sẽ tự động hóa 100% quy trình từ lúc khách hàng bấm "Gửi" form cho đến khi Jira Ticket được tạo, Google Sheets được cập nhật và email thông báo bay thẳng đến hộp thư người liên quan!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Chuyển đổi dữ liệu từ Google Form thành Jira Ticket ngay lập tức mà không cần chạm tay vào.
- **Đồng bộ dữ liệu hai chiều:** Tự động ghi nhận mã Ticket (Jira Key) và đường dẫn (URL) ngược lại vào Google Sheets để dễ dàng tra cứu.
- **Thông minh & Chuẩn hóa:** Tự động làm sạch dữ liệu văn bản (cắt bỏ khoảng trắng thừa, chuẩn hóa định dạng đoạn văn).
- **Chăm sóc khách hàng chuyên nghiệp:** Tự động gửi email xác nhận kèm thông tin chi tiết về ticket vừa tạo cho người gửi.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU]
- Google Form kết nối với Google Sheet (chứa response sheet).
- Jira Cloud Project (chuẩn bị API Email và API Token).
- Tài khoản Gmail để cấu hình gửi thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, dán trực tiếp vào n8n Editor hoặc sử dụng file JSON được cung cấp từ nguồn gốc để import vào hệ thống n8n của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Trigger when row added (Node `googleSheetsTrigger`):** 
  - Kết nối tài khoản Google qua OAuth2.
  - Chọn đúng file Google Sheet và Sheet Name nhận dữ liệu từ Google Form.
- **Normalize fields (Node `code`):** 
  - Node này dùng ngôn ngữ JavaScript để làm sạch dữ liệu (`summary` được trim text, `description` giữ nguyên định dạng đoạn văn, tách `reporter_email` từ form). Các sếp có thể tùy chỉnh code nếu form của các sếp có tên cột khác biệt.
- **Cretate Jira Ticket (Node `jira`):** 
  - Kết nối tài khoản Jira Cloud API.
  - Chọn Project đích, cấu hình Type (ví dụ: *Story* hoặc *Task*), map mức độ ưu tiên (*Priority*) theo ID của Jira, và cấu hình Description theo chuẩn template.
- **Update the Google sheet with tickets information (Node `googleSheets`):** 
  - Sử dụng thao tác `update`.
  - Dựa vào cột định danh (ví dụ cột thời gian `Horodateur` hoặc ID) để match dòng dữ liệu, sau đó ghi đè các thông tin như `jira_key`, `jira_url`, trạng thái `Created`, và thời gian `created_at`.
- **Notification email (Node `gmail`):** 
  - Kết nối tài khoản Gmail.
  - Thiết lập nội dung email gửi đến người yêu cầu với các thông tin: Mã ticket, Link ticket, Tiêu đề, Mức độ ưu tiên và trạng thái tạo thành công.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử gửi một bản ghi mẫu trên Google Form để test dữ liệu chạy qua từng node.
- Kiểm tra xem Jira đã tạo ticket chưa, Google Sheets đã cập nhật dòng đó chưa và Gmail đã nhận được thư chưa.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm kênh thông báo nội bộ:** Kết hợp thêm node Slack hoặc Telegram để bắn thông báo vào nhóm chat của team kỹ thuật ngay khi có ticket mới từ khách hàng.
- **Bổ sung xử lý lỗi (Error Handling):** Thêm Error Trigger để nếu Jira gặp sự cố hoặc API lỗi, hệ thống sẽ tự động gửi một email cảnh báo cho Admin.
- **Phân loại tự động bằng AI:** Tích hợp thêm một node AI (OpenAI/Anthropic) trước bước tạo Jira để tự động phân loại mức độ ưu tiên hoặc gắn nhãn (label) cho ticket dựa trên nội dung mô tả của người dùng.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ lợi hại cho các Product Owner, IT Helpdesk hoặc Project Manager muốn tối ưu hóa quy trình tiếp nhận yêu cầu. Triển khai ngay hôm nay để tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần cho đội ngũ của các sếp nhé!