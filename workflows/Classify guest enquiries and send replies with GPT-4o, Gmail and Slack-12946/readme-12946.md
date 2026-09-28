---
title: "🏨 Tự Động Phân Loại & Trả Lời Khách Hàng Với GPT-4o, Gmail & Slack"
description: "Workflow n8n thông minh giúp tự động phân loại yêu cầu của khách (đặt phòng, giá, chính sách), tạo phản hồi cá nhân hóa bằng AI và phân công cho đội ngũ phù hợp qua Slack."
slug: "tu-dong-phan-loi-khach-hang-gpt-4o-gmail-slack"
tags: [n8n, ai-automation, hospitality, customer-support, gpt-4o]
keywords: [n8n workflow, tự động hóa khách sạn, AI agent n8n, phân loại ticket, gmail automation]
---

# 🏨 Tự Động Phân Loại & Trả Lời Khách Hàng Với GPT-4o, Gmail & Slack

Trong ngành khách sạn, resort hay homestay, việc xử lý hàng chục đến hàng trăm tin nhắn hỏi về giá, lịch đặt phòng hay chính sách hủy mỗi ngày là một gánh nặng lớn. Nhân viên thường xuyên bị quá tải, dẫn đến việc phản hồi chậm trễ, sai sót thông tin hoặc bỏ sót các yêu cầu quan trọng. Điều này không chỉ ảnh hưởng đến trải nghiệm khách hàng mà còn trực tiếp làm giảm doanh thu.

Workflow n8n này là giải pháp "chốt hạ" cho bài toán đó. Thay vì con người phải đọc từng tin nhắn và quyết định chuyển cho ai, hệ thống sẽ sử dụng **AI Agent (GPT-4o)** để tự động "đọc vị" ý định của khách hàng, phân loại chính xác vào các nhóm (Đặt phòng, Giá, Sẵn sàng, Chính sách), tạo ra một email phản hồi lịch sự, cá nhân hóa và tự động phân công cho đúng người phụ trách trong Slack. Tất cả diễn ra trong vài giây, 24/7, không cần code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian xử lý ticket:** AI tự động hóa toàn bộ quy trình từ nhận tin đến phân công, nhân viên chỉ cần tập trung vào việc giải quyết vấn đề phức tạp.
- **Phản hồi tức thì & Chuyên nghiệp:** Khách hàng nhận được email xác nhận ngay lập tức với giọng văn tự nhiên, tạo ấn tượng tốt về sự chuyên nghiệp.
- **Phân công chính xác 100%:** Không còn tình trạng "đá bóng" giữa các bộ phận. AI nhận diện đúng ý định (Booking, Pricing, Policy...) và gửi thẳng cho đội ngũ tương ứng.
- **Truy vết & Báo cáo minh bạch:** Mọi tương tác đều được log chi tiết vào Slack, giúp quản lý dễ dàng theo dõi hiệu suất và SLA (thời gian phản hồi).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Chạy local hoặc trên VPS.
2. **OpenAI API Key:** Để sử dụng model GPT-4o-mini (hoặc GPT-4o) cho AI Agent.
3. **Gmail OAuth2:** Kết nối tài khoản Gmail mà khách hàng sẽ nhận được email phản hồi.
4. **Slack API:** Kết nối workspace Slack để nhận thông báo nội bộ và log hoạt động.
5. **Form thu thập dữ liệu:** Một form web (có thể dùng Base44, Typeform, hoặc form HTML đơn giản) có khả năng gửi dữ liệu qua Webhook POST.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from File** hoặc **Import from URL**.
3. Tải file JSON workflow hoặc dán link gốc: `https://n8n.io/workflows/12946`.
4. Sau khi import, các sếp sẽ thấy một canvas chứa 16 nodes được sắp xếp logic rõ ràng.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần click vào từng node và cấu hình như sau:

*   **Node: `Webhook Trigger1`**
    *   Đây là điểm bắt đầu. Đảm bảo HTTP Method là **POST**.
    *   Copy **Production URL** (hoặc Test URL khi chạy thử) và dán vào trường "Webhook URL" của form thu thập dữ liệu khách hàng.
    *   Dữ liệu gửi vào nên bao gồm: `name`, `email`, `message` (nội dung hỏi), và `contact_preference` (email hoặc phone).

*   **Node: `AI Agent: Classify Intent & Generate Reply`**
    *   Đây là "bộ não" của workflow.
    *   Kiểm tra **System Prompt** (nếu có) hoặc cấu hình của Agent. Nó sẽ phân tích `message` và trả về cấu trúc dữ liệu gồm: `category` (booking/pricing/availability/policy) và `reply_text`.
    *   Đảm bảo **OpenAI Chat Model** (`gpt-4o-mini`) đã được gắn credentials OpenAI hợp lệ.

*   **Node: `Structured Output Parser1`**
    *   Node này đảm bảo AI trả về đúng định dạng JSON (ví dụ: `{ "category": "booking", "reply": "..." }`).
    *   Kiểm tra schema output để khớp với các node xử lý tiếp theo.

*   **Node: `Route by Intent Category` (Switch Node)**
    *   Node này sẽ chia luồng dựa trên trường `category` mà AI trả về.
    *   Các sếp cần đảm bảo các giá trị (Output) của Switch khớp với tên các node gán nhiệm vụ bên dưới (Booking, Pricing, Availability, Policy).

*   **Nodes: `Assign to Booking Team`, `Assign to Pricing Team`, ...**
    *   Trong mỗi node Set này, các sếp cần **thay đổi email hoặc ID nhân viên** phụ trách.
    *   Ví dụ: Trong `Assign to Booking Team`, điền email của trưởng nhóm đặt phòng.
    *   Có thể thêm trường `SLA_hours` để quy định thời gian phản hồi cho từng loại.

*   **Node: `Check Guest Contact Preference` (If Node)**
    *   Logic: Nếu khách chọn nhận phản hồi qua Email -> Gửi Email. Nếu không -> Chỉ log nội bộ.
    *   Kiểm tra điều kiện so sánh trường `contact_preference` từ webhook.

*   **Node: `Send Email Reply to Guest`**
    *   Gắn **Gmail OAuth2** credentials.
    *   Cấu hình Subject và Body. Body nên tham chiếu đến `reply_text` do AI tạo ra để đảm bảo sự cá nhân hóa.

*   **Nodes: `Post Enquiry Summary to Slack` & `Log AI Reply to Slack`**
    *   Gắn **Slack API** credentials.
    *   Chọn **Channel ID** (ví dụ: `#guest-enquiries` hoặc `#support-team`).
    *   Cấu hình message format để hiển thị rõ: Tên khách, Nội dung hỏi, Phân loại AI, và Email phản hồi đã gửi.

*   **Node: `Slack: Send Error Alert`**
    *   Gắn Slack credentials.
    *   Chọn channel quản trị (ví dụ: `#dev-alerts`).
    *   Node này sẽ tự động báo lỗi nếu workflow gặp sự cố (ví dụ: hết quota OpenAI, lỗi kết nối Gmail).

#### 3. Kích hoạt ⚡️
1. **Test Run:**
    *   Mở **Test** mode của Webhook.
    *   Gửi một tin nhắn mẫu từ form (ví dụ: "Chào, phòng đôi giá bao nhiêu cho 2 đêm?").
    *   Quan sát luồng chạy: AI phân loại là "Pricing" -> Chuyển sang `Assign to Pricing Team` -> Gửi Slack -> Gửi Email (nếu khách chọn email).
2. **Active Workflow:**
    *   Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải.
    *   Workflow sẽ bắt đầu nhận dữ liệu thực tế từ form.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp CRM:** Thay vì chỉ gửi Slack, các sếp có thể thêm node để cập nhật trạng thái khách hàng vào CRM (HubSpot, Salesforce) ngay khi nhận được yêu cầu.
- **Đa ngôn ngữ:** Chỉnh sửa Prompt của AI Agent để yêu cầu nó phản hồi bằng ngôn ngữ mà khách hàng sử dụng (tiếng Anh, tiếng Việt, tiếng Nhật...).
- **Cảnh báo SLA:** Thêm một node Schedule Trigger để kiểm tra các ticket trong Slack/Sheet đã quá thời gian SLA nhưng chưa được xử lý, và gửi cảnh báo nhắc nhở nhân viên.
- **Phân tích dữ liệu:** Lưu toàn bộ dữ liệu vào Google Sheets hoặc Database để tạo báo cáo tuần về loại câu hỏi phổ biến nhất, từ đó cải thiện website hoặc FAQ.

### 📌 Kết luận
Với workflow này, các sếp không chỉ giải quyết được bài toán quá tải nhân sự mà còn nâng tầm trải nghiệm khách hàng lên một đẳng cấp mới. Sự kết hợp giữa tốc độ của AI và sự linh hoạt của n8n giúp doanh nghiệp hospitality của bạn luôn sẵn sàng phục vụ, chuyên nghiệp và hiệu quả. Hãy import, cấu hình và trải nghiệm ngay hôm nay!