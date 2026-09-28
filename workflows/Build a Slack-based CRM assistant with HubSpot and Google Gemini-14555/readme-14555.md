---
title: "🚀 Xây Dựng Trợ Lý CRM Trên Slack Với HubSpot & Google Gemini"
description: "Biến Slack thành trung tâm điều hành CRM thông minh. Truy vấn dữ liệu HubSpot bằng ngôn ngữ tự nhiên, nhận phản hồi tức thì từ AI Gemini, không cần code."
slug: "tro-ly-crm-slack-hubspot-gemini"
tags: [n8n, automation, no-code, hubspot, slack, ai-agent, gemini]
keywords: [n8n workflow, tự động hóa CRM, hubspot slack, ai chatbot, gemini agent]
---

# 🚀 Xây Dựng Trợ Lý CRM Trên Slack Với HubSpot & Google Gemini

Các sếp đang vận hành đội ngũ Sales hay Marketing có bao giờ cảm thấy mệt mỏi khi phải liên tục hỏi lại đồng nghiệp: *"Deal của khách hàng X đang ở giai đoạn nào?"* hay *"Có bao nhiêu contact mới từ tuần trước?"*? Việc rời khỏi Slack để mở HubSpot, tìm kiếm, lọc dữ liệu rồi quay lại trả lời không chỉ tốn thời gian mà còn làm gián đoạn luồng làm việc.

Workflow này giải quyết triệt để nỗi đau đó bằng cách biến Slack thành một **trợ lý CRM AI**. Chỉ cần mention bot trong kênh làm việc, các sếp có thể hỏi bất kỳ câu hỏi nào về Deals, Companies hay Contacts bằng ngôn ngữ tự nhiên. Hệ thống sẽ tự động truy xuất dữ liệu từ HubSpot, sử dụng AI Agent (Google Gemini) để phân tích và tổng hợp lại thành câu trả lời rõ ràng, dễ đọc ngay trên Slack.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và phản hồi tức thì, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tốc độ truy vấn tức thì:** Không cần mở HubSpot, mọi thông tin CRM đều có mặt ngay trong kênh chat.
- **Ngôn ngữ tự nhiên:** Hỏi như nói chuyện với đồng nghiệp, không cần nhớ cú pháp tìm kiếm phức tạp.
- **Dữ liệu chính xác & Tổng hợp:** AI Agent không chỉ trả về raw data mà còn tóm tắt, định dạng lại cho dễ hiểu.
- **Tăng hiệu suất đội ngũ:** Sales tập trung vào chốt đơn thay vì dành thời gian cho việc tìm kiếm thông tin hành chính.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị các tài khoản và credentials sau:
1. **Tài khoản n8n:** Bản Self-hosted hoặc Cloud.
2. **Tài khoản Slack:**
   - Tạo một Slack App.
   - Cấp quyền (Scopes): `app_mention` (để nhận mention) và `chat:write` (để gửi tin nhắn).
   - Invite bot vào kênh làm việc.
3. **Tài khoản HubSpot:**
   - Tạo một **Private App** hoặc **Integration** trong HubSpot.
   - Cấp quyền đọc (Read) cho các đối tượng: `contacts`, `companies`, `deals`.
   - Lấy **Private App Token** hoặc **API Key**.
4. **Tài khoản Google AI Studio:**
   - Lấy **API Key** cho Google Gemini.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải xuống file JSON của workflow từ link gốc hoặc copy toàn bộ code JSON.
2. Mở n8n Editor, chọn **Import from URL** hoặc **Import from File**.
3. Sau khi import, các sếp sẽ thấy 12 nodes được kết nối sẵn theo luồng: *Slack Trigger -> Code -> HubSpot (x3) -> Filter (x3) -> Merge -> AI Agent -> Slack Send*.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần cấu hình từng node cụ thể như sau:

*   **Node: Slack Trigger**
    *   Chọn **Credentials** của Slack App đã tạo.
    *   Đảm bảo Event được chọn là `app_mention` (khi bot bị mention).
    *   *Lưu ý:* Phải invite bot vào kênh trước khi test.

*   **Node: Code in JavaScript**
    *   Node này dùng để "làm sạch" tin nhắn từ Slack (xóa các tag mention, user ID, channel ID) để chỉ giữ lại nội dung câu hỏi thuần túy.
    *   Các sếp có thể kiểm tra lại logic nếu tin nhắn vào không đúng định dạng, nhưng thường thì code mặc định đã xử lý tốt các trường hợp phổ biến.

*   **Nodes: Get many companies, Get Contacts, Get Deals (HubSpot)**
    *   Chọn **Credentials** HubSpot (Private App Token).
    *   **Get many companies:** Operation là `getAll`.
    *   **Get Contacts:** Operation là `getAll`.
    *   **Get Deals:** Operation là `search`.
    *   *Mẹo:* Nếu dữ liệu HubSpot của các sếp quá lớn (hàng nghìn records), việc fetch `getAll` có thể chậm. Các sếp có thể cân nhắc thêm filter theo thời gian (ví dụ: chỉ lấy contact tạo trong 30 ngày gần nhất) ngay tại node HubSpot để tối ưu tốc độ.

*   **Nodes: Filter Contacts, Filter Companies, Filter Deals**
    *   Các node này dùng để lọc dữ liệu thô từ HubSpot dựa trên từ khóa trong câu hỏi của user.
    *   Logic mặc định thường là kiểm tra xem tên contact/company/deal có chứa từ khóa trong query không.
    *   Các sếp có thể chỉnh sửa điều kiện lọc (Filter Condition) nếu muốn độ chính xác cao hơn (ví dụ: khớp chính xác thay vì chứa).

*   **Node: Merge**
    *   Kết hợp dữ liệu từ 3 luồng lọc (Contacts, Companies, Deals) thành một bundle duy nhất để đưa vào AI.

*   **Node: Google Gemini Chat Model**
    *   Chọn **Credentials** Google Gemini.
    *   Chọn Model phù hợp (ví dụ: `gemini-1.5-flash` cho tốc độ nhanh, hoặc `gemini-1.5-pro` nếu cần độ phức tạp cao hơn).

*   **Node: AI Agent**
    *   Đây là "bộ não" của workflow.
    *   **System Prompt:** Các sếp nên chỉnh sửa prompt để định hình cách AI trả lời. Ví dụ: *"Bạn là trợ lý CRM. Hãy tóm tắt dữ liệu HubSpot được cung cấp dưới đây một cách ngắn gọn, chuyên nghiệp. Nếu không tìm thấy dữ liệu, hãy thông báo rõ ràng."*
    *   **Input:** Đảm bảo node này nhận dữ liệu từ node `Merge`.

*   **Node: Send a message**
    *   Chọn **Credentials** Slack.
    *   **Channel:** Có thể để trống nếu muốn gửi về đúng channel mà user đã mention, hoặc hardcode ID channel nếu muốn gửi báo cáo cố định.
    *   **Message:** Tham chiếu đến output của node `AI Agent`.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   *   Bật chế độ **Listen for Test Event** ở node Slack Trigger.
   *   Vào Slack, mention bot: `@BotName deal của khách hàng ABC đang ở giai đoạn nào?`
   *   Quan sát n8n xem dữ liệu có chạy qua các node HubSpot và AI không.
2. **Active Workflow:**
   *   Nếu kết quả trả về Slack chính xác và dễ đọc, các sếp hãy bật nút **Active** ở góc trên bên phải.
   *   Từ giờ, mọi mention bot trong kênh đã invite đều sẽ được xử lý tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm thông tin chi tiết:** Trong node HubSpot, các sếp có thể thêm các trường (properties) cụ thể vào query (ví dụ: `deal_value`, `close_date`) để AI có thể trả lời chi tiết hơn về giá trị hợp đồng hay ngày dự kiến chốt.
- **Tích hợp thêm Slack Actions:** Thay vì chỉ trả lời, các sếp có thể thêm nút "Xem trên HubSpot" hoặc "Gán cho tôi" vào tin nhắn phản hồi bằng cách sử dụng Slack Block Kit trong node Send a message.
- **Log hoạt động:** Thêm một node Google Sheets hoặc Airtable để lưu lại lịch sử các câu hỏi và câu trả lời. Điều này giúp các sếp phân tích xem đội ngũ đang quan tâm đến loại dữ liệu nào nhất.
- **Hỗ trợ đa ngôn ngữ:** Chỉnh sửa System Prompt của AI Agent để yêu cầu trả lời bằng tiếng Việt nếu câu hỏi đầu vào là tiếng Việt, giúp trải nghiệm người dùng nội địa hóa tốt hơn.

### 📌 Kết luận
Việc tích hợp HubSpot, Slack và AI Gemini vào một workflow n8n không chỉ là một tính năng "xịn xò" mà là một công cụ thực chiến giúp tăng tốc độ ra quyết định trong đội ngũ Sales. Với chi phí vận hành thấp và khả năng tùy biến cao, đây là bước đi hoàn hảo để các sếp hiện đại hóa quy trình CRM của mình. Hãy import workflow, cấu hình credentials và trải nghiệm ngay sự khác biệt!