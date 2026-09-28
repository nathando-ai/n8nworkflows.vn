---
title: "🚀 Tự Động Phân Loại & Chấm Điểm Lead Sales Bằng AI (Gmail + Gemini + Salesforce)"
description: "Workflow n8n giúp tự động đọc email khách hàng, dùng Google Gemini phân tích cảm xúc và trích xuất thông tin, sau đó định tuyến lead vào Salesforce hoặc Google Sheets dựa trên mức độ quan tâm."
slug: "tu-dong-phan-loai-lead-sales-ai-gmail-salesforce"
tags: [n8n, automation, no-code, ai, salesforce, lead-generation]
keywords: [n8n workflow, tự động hóa sales, ai lead scoring, gmail to salesforce, gemini ai]
---

# 🚀 Tự Động Phân Loại & Chấm Điểm Lead Sales Bằng AI (Gmail + Gemini + Salesforce)

Trong môi trường kinh doanh B2B, đội ngũ Sales thường bị quá tải với hàng trăm email đến mỗi ngày. Việc đọc từng email, xác định mức độ quan tâm của khách hàng (intent), và nhập liệu thủ công vào CRM (Salesforce) không chỉ tốn thời gian mà còn dễ gây sai sót. Nhiều lead tiềm năng bị bỏ sót hoặc không được phản hồi kịp thời chỉ vì quy trình xử lý chậm.

Workflow này là giải pháp "chìa khóa trao tay" giúp các sếp tự động hóa toàn bộ quy trình: Từ lúc nhận email qua Gmail, sử dụng sức mạnh của **Google Gemini** để phân tích cảm xúc (sentiment) và trích xuất thông tin quan trọng, cho đến việc định tuyến (routing) lead vào đúng hệ thống (Salesforce hoặc Google Sheets) dựa trên logic kinh doanh. Tất cả diễn ra hoàn toàn tự động, không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian xử lý lead:** AI tự động đọc và phân loại email, Sales chỉ cần tập trung vào việc chốt đơn.
- **Chấm điểm Lead chính xác:** Sử dụng AI Sentiment Analysis để đánh giá mức độ quan tâm thực sự của khách hàng.
- **Tích hợp liền mạch:** Dữ liệu được đẩy thẳng vào Salesforce (cho lead nóng) hoặc Google Sheets (để theo dõi lead lạnh), giảm thiểu thao tác nhập liệu thủ công.
- **Truy xuất thông tin tự động:** Tự động trích xuất tên, công ty, nhu cầu cụ thể từ nội dung email lộn xộn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Bản Self-hosted hoặc Cloud.
2. **Gmail Account:** Đã cấp quyền OAuth2 cho n8n (để đọc email).
3. **Google Gemini API Key:** Từ Google AI Studio (dùng cho các node LangChain).
4. **Salesforce Account:** Đã tạo Connected App hoặc OAuth2 Credentials trong n8n.
5. **Google Sheets:** Một bảng tính trống để lưu trữ dữ liệu lead (nếu cần).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/13738).
2. Mở n8n Editor, chọn **Import from File** hoặc **Import from URL**.
3. Chọn file JSON vừa tải và nhấn **Import**.
4. Workflow sẽ xuất hiện với đầy đủ các node đã được kết nối.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là các node quan trọng cần cấu hình lại cho phù hợp với hệ thống của các sếp:

*   **Node: Gmail Trigger**
    *   Chọn **Credentials** Gmail của bạn.
    *   Cấu hình **Filter** (nếu muốn) để chỉ nhận email từ các địa chỉ cụ thể hoặc có subject chứa từ khóa "Sales", "Inquiry".
    *   Đảm bảo bật **Polling** hoặc cấu hình Webhook nếu dùng bản Cloud.

*   **Node: Code (Pre-processing)**
    *   Node này thường dùng để làm sạch dữ liệu email (loại bỏ HTML, trích xuất body text).
    *   Kiểm tra lại logic trong tab **JavaScript** nếu email của bạn có cấu trúc đặc biệt.

*   **Node: Sentiment Analysis (LangChain)**
    *   Chọn **Credentials** cho **Google Gemini**.
    *   Đảm bảo model được chọn là `gemini-1.5-flash` hoặc `gemini-1.5-pro` (tùy tốc độ và độ chính xác cần thiết).
    *   Node này sẽ trả về điểm cảm xúc (Positive, Negative, Neutral).

*   **Node: Information Extractor (LangChain)**
    *   Chọn **Credentials** cho **Google Gemini**.
    *   Trong phần **Schema**, các sếp cần định nghĩa rõ các trường dữ liệu cần trích xuất (ví dụ: `company_name`, `contact_name`, `budget`, `timeline`).
    *   *Mẹo:* Càng mô tả rõ schema, AI càng trích xuất chính xác.

*   **Node: Switch / If (Routing Logic)**
    *   Đây là "bộ não" định tuyến. Các sếp cần chỉnh lại điều kiện:
        *   *Ví dụ:* Nếu `Sentiment` là "Positive" VÀ `Budget` > 1000 -> Đi vào nhánh **Salesforce**.
        *   *Ví dụ:* Nếu `Sentiment` là "Neutral" -> Đi vào nhánh **Google Sheets**.
    *   Hãy tùy chỉnh các ngưỡng (threshold) này theo chiến lược sales của công ty.

*   **Node: Salesforce**
    *   Chọn **Credentials** Salesforce.
    *   Chọn **Operation**: `Create`.
    *   Chọn **Resource**: `Lead` (hoặc `Contact` tùy cấu trúc CRM).
    *   Map các trường dữ liệu từ node Information Extractor vào các trường tương ứng trong Salesforce.

*   **Node: Google Sheets**
    *   Chọn **Credentials** Google Sheets.
    *   Chọn **Document** (Sheet ID) và **Sheet Name**.
    *   Map dữ liệu để append vào bảng tính.

*   **Node: Slack (Optional)**
    *   Nếu muốn thông báo ngay khi có Lead nóng, chọn **Credentials** Slack.
    *   Cấu hình **Channel** (ví dụ: `#sales-alerts`).
    *   Viết message template động, ví dụ: `🔥 Lead mới: {{ $json.contact_name }} từ {{ $json.company_name }}. Mức độ quan tâm: {{ $json.sentiment }}`.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** để test với dữ liệu mẫu (có thể dùng node "Set" để giả lập một email test).
2. Kiểm tra xem dữ liệu có được đẩy đúng vào Salesforce/Sheets không.
3. Kiểm tra xem thông báo Slack có nhận được không.
4. Nếu mọi thứ ổn, bật công tắc **Active** ở góc trên bên phải.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/WhatsApp:** Thay vì chỉ dùng Slack, các sếp có thể thêm node Telegram để gửi thông báo lead nóng trực tiếp vào điện thoại của Sales Manager.
- **Lưu Log chi tiết:** Thêm một node Google Sheets riêng để lưu lại toàn bộ email gốc và kết quả phân tích AI, giúp team Sales xem lại bối cảnh khi cần.
- **Báo cáo định kỳ:** Thêm một workflow con chạy hàng tuần, tổng hợp số lượng lead từ Gmail, tỷ lệ chuyển đổi từ Sheets/Salesforce và gửi báo cáo email cho Ban Giám đốc.
- **Nâng cấp Prompt:** Trong node Information Extractor, hãy thử nghiệm các prompt khác nhau để AI hiểu rõ hơn về sản phẩm/dịch vụ của bạn, từ đó trích xuất thông tin chính xác hơn.

### 📌 Kết luận
Việc để lead "nguội" đi vì chờ đợi phản hồi thủ công là một trong những nguyên nhân lớn nhất khiến doanh nghiệp mất doanh thu. Với workflow này, các sếp có thể biến hộp thư Gmail thành một cỗ máy lọc lead thông minh, tự động chấm điểm và phân phối công việc cho đội ngũ Sales một cách chính xác nhất. Hãy import và tùy chỉnh ngay hôm nay để trải nghiệm sự khác biệt!