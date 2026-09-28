---
title: "🚀 Tự động Chấm điểm Lead và Phân bổ Khách hàng với GPT-4, GoHighLevel & Slack"
description: "Hướng dẫn xây dựng hệ thống tự động hóa nàn n8n giúp chấm điểm lead bằng GPT-4, phân loại Hot/Warm/Cold, tự động gán sale và gửi thông báo Slack từ GoHighLevel."
slug: "tu-dong-cham-diem-lead-gohighlevel-gpt4-n8n"
tags: [n8n, automation, no-code, gohighlevel, openai, slack]
keywords: [n8n workflow, cham diem lead, gohighlevel automation, gpt-4 lead scoring, tu dong hoa ban hang]
---

# 🚀 Tự động Chấm điểm Lead và Phân bổ Khách hàng với GPT-4, GoHighLevel & Slack

Các sếp có bao giờ gặp tình trạng lead từ hệ thống quảng cáo đổ về ào ào, nhưng đội ngũ sale lại phải mất quá nhiều thời gian để lọc xem ai là khách tiềm năng thật sự, dẫn đến việc phản hồi chậm và mất khách vào tay đối thủ? 

Việc phân loại và phân bổ lead thủ công vừa tốn nhân lực, vừa thiếu tính nhất quán. Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ, giải quyết triệt để bài toán này bằng cách kết hợp **GoHighLevel (GHL)**, **GPT-4 (OpenAI)** và **Slack**. Hệ thống sẽ tự động hóa từ A-Z: nhận lead mới -> lấy dữ liệu tương tác -> AI chấm điểm (1-100) -> phân loại (Hot/Warm/Cold) -> gán đúng sale phụ trách -> gắn tag -> bắn thông báo nóng hổi lên Slack. Tất cả diễn ra trong vài giây mà không cần một dòng code thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý dữ liệu webhook mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản hồi thần tốc:** Lead "Hot" (điểm >= 80) được gán ngay cho Top Sales và bắn thông báo tức thì lên Slack, giúp tỷ lệ chốt đơn tăng đột biến.
- **Phân loại thông minh:** GPT-4 phân tích nhân khẩu học, nguồn traffic và lịch sử tương tác để đưa ra điểm số và lý do cụ thể, chuẩn xác hơn các bộ lọc quy tắc (rules) thông thường.
- **Tự động hóa 100% quy trình CRM:** Tự động gắn tag (Hot, Warm, Cold) và phân bổ đúng chủ sở hữu (owner) trong GoHighLevel mà không cần con người nhúng tay.
- **Vận hành không gián đoạn:** Hoạt động liên tục 24/7 qua Webhook, không bỏ sót bất kỳ khách hàng tiềm năng nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **GoHighLevel (GHL) Account:** Có quyền cấu hình Webhook và lấy API Key/User IDs.
- **OpenAI Account:** Có API Key và hạn mức sử dụng (tích hợp GPT-4).
- **Slack Workspace:** Đã tạo Bot/App và có quyền gửi tin nhắn vào kênh thông báo bán hàng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ nguồn gốc (hoặc file đính kèm) và paste trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các node quan trọng sau đây:

- **GHL New Contact Trigger (Webhook):** Node này nhận dữ liệu HTTP POST từ GoHighLevel. Hãy copy URL của webhook này và dán vào phần cấu hình Webhook/Automation Trigger bên trong hệ thống GoHighLevel của các sếp.
- **Workflow Configuration (Set):** Nơi các sếp khai báo các thông số cốt lõi: GHL API Key, Base URL, Danh sách User ID của nhân viên sale (Top rep, Secondary rep, Nurture team) và kênh Slack nhận tin.
- **GHL Get Contact Details & GHL Fetch Engagement Data (HTTP Request):** Đảm bảo credentials kết nối GHL của các sếp được cấu hình đúng để lấy thông tin chi tiết và lịch sử tương tác của contact.
- **AI Lead Scoring (GPT-4) (OpenAI):** Chọn credential OpenAI API đã chuẩn bị. Tinh chỉnh system prompt nếu muốn AI chấm theo tiêu chí riêng của ngành hàng (mặc định AI trả về điểm số từ 1-100 kèm phân loại và lý do).
- **Parse Score to Numeric (Code):** Node code JavaScript nhỏ giúp chuyển đổi kết quả chữ từ AI thành dạng số nguyên (numeric) để các node điều kiện đọc được.
- **IF Score >= 80 (Hot) & IF Score >= 40 (Warm) (IF):** Thiết lập ngưỡng lọc điểm số (>=80 là Hot, từ 40 đến 79 là Warm, còn lại là Cold).
- **Các node GHL Tag & Assign (HTTP Request):** Các node như `GHL Tag Hot Lead`, `GHL Assign Hot to Top Rep`... sẽ thực hiện gọi API tới GHL để gắn thẻ (tag) và chuyển giao lead cho đúng người phụ trách.
- **Slack Notify Hot Lead (Slack):** Kết nối tài khoản Slack và chọn đúng kênh (ví dụ: `#sales-hot-leads`) để đội ngũ kinh doanh nhận cảnh báo ngay lập tức.
- **Webhook Response (Respond to Webhook):** Gửi phản hồi HTTP 200 OK về lại cho GoHighLevel để xác nhận webhook đã được xử lý thành công.

#### 3. Kích hoạt ⚡️
- Gửi một contact thử nghiệm từ GoHighLevel để chạy test (Test run) trên n8n.
- Kiểm tra kết quả trên GHL (xem đã gắn đúng tag, đổi đúng owner chưa) và xem thông báo có bắn lên Slack không.
- Sau khi mọi thứ chạy trơn tru, hãy bật công tắc **Active** cho workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Zalo/Telegram:** Ngoài Slack, các sếp có thể add thêm node Telegram Bot để bắn tin nhắn trực tiếp vào nhóm chat riêng của sales trên điện thoại.
- **Lưu log vào Google Sheets:** Thêm một node Google Sheets để ghi lại lịch sử chấm điểm của toàn bộ lead phục vụ cho việc phân tích marketing sau này.
- **Xử lý Lead trùng lặp:** Thêm bước kiểm tra số điện thoại/email trước khi chấm điểm để tránh gọi điện trùng lặp phiền khách hàng.

### 📌 Kết luận
Hệ thống Lead Scoring tự động với GPT-4 và GoHighLevel này chính là mảnh ghép còn thiếu giúp đội ngũ sales của các sếp làm việc thông minh hơn, nhanh hơn và chốt đơn hiệu quả hơn. Hãy thiết lập ngay hôm nay để không bỏ lỡ bất kỳ khách hàng tiềm năng nào!