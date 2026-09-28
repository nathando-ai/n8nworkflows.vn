---
title: "🚀 Tự Động Phân Loại & Chấm Điểm Lead bằng AI (OpenAI + Gmail + Sheets)"
description: "Workflow n8n giúp chấm điểm chất lượng lead bằng AI, tự động gửi email cảnh báo cho lead nóng và lưu trữ có hệ thống vào Google Sheets, tiết kiệm 100% thời gian sàng lọc thủ công."
slug: "tu-dong-phan-loai-lead-bang-ai"
tags: [n8n, automation, no-code, openai, lead-generation, google-sheets]
keywords: [n8n workflow, tự động hóa lead, chấm điểm lead bằng AI, openai integration, google sheets automation]
---

# 🚀 Tự Động Phân Loại & Chấm Điểm Lead bằng AI (OpenAI + Gmail + Sheets)

Trong môi trường kinh doanh hiện đại, việc nhận được hàng chục, thậm chí hàng trăm lead mỗi ngày từ các form đăng ký, landing page hay mạng xã hội là điều bình thường. Tuy nhiên, nỗi đau lớn nhất của các đội ngũ Sales và Marketing chính là **thời gian chết** khi phải đọc từng lead, đánh giá mức độ quan tâm và quyết định ai là khách hàng tiềm năng thực sự (Hot Lead) và ai chỉ là người tò mò (Cold Lead).

Làm thủ công không chỉ tốn thời gian mà còn thiếu nhất quán trong tiêu chí đánh giá. Workflow **"Score and route inbound web leads"** này chính là giải pháp hoàn hảo. Nó sử dụng sức mạnh của **OpenAI** để phân tích nội dung lead, chấm điểm chất lượng, và tự động định tuyến: gửi email cảnh báo tức thì cho lead nóng, đồng thời lưu trữ dữ liệu một cách có hệ thống vào Google Sheets. Tất cả diễn ra trong vài giây, không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian sàng lọc:** AI làm việc 24/7, không nghỉ phép, không mệt mỏi.
- **Phản hồi tức thì:** Lead nóng nhận được email thông báo ngay lập tức, tăng cơ hội chốt đơn.
- **Dữ liệu sạch & Có hệ thống:** Lead được phân loại rõ ràng vào các tab riêng biệt trong Google Sheets, dễ dàng báo cáo và phân tích.
- **Tiêu chí nhất quán:** AI áp dụng cùng một bộ tiêu chí chấm điểm cho mọi lead, loại bỏ yếu tố chủ quan của con người.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Bản miễn phí (Cloud) hoặc Self-hosted.
2. **API Key OpenAI:** Để gọi API chấm điểm lead (hoặc bất kỳ API LLM tương thích nào).
3. **Tài khoản Gmail:** Đã cấp quyền OAuth cho n8n để gửi email.
4. **Tài khoản Google Sheets:** Đã cấp quyền OAuth cho n8n để ghi dữ liệu.
5. **Form thu thập lead:** Một form bất kỳ (Typeform, Google Form, Form tự code...) có khả năng gửi dữ liệu qua HTTP Request (Webhook).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/15970) hoặc copy toàn bộ code JSON.
2. Mở n8n Editor, chọn **Import from URL** hoặc **Import from Clipboard**.
3. Workflow sẽ hiển thị với 9 nodes chính, đã được nhóm lại theo các giai đoạn logic rõ ràng.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần click vào từng node và cấu hình theo hướng dẫn sau:

*   **Node: `When Lead Received` (Webhook)**
    *   Đây là điểm bắt đầu. Copy **Webhook URL** (Production URL) và dán vào trường "Redirect URL" hoặc "Webhook URL" của form thu thập lead của bạn.
    *   Đảm bảo form gửi dữ liệu theo phương thức `POST` với format JSON.

*   **Node: `Set Lead Fields` (Set)**
    *   Node này chuẩn hóa dữ liệu đầu vào. Kiểm tra xem các trường `name`, `email`, `company`, `role` trong node này có khớp với tên trường dữ liệu mà form của bạn gửi lên không. Nếu form gửi `full_name` nhưng node này chờ `name`, các sếp cần chỉnh lại mapping ở đây.

*   **Node: `Post to AI Scoring API` (HTTP Request)**
    *   **Credentials:** Chọn hoặc tạo mới credential cho OpenAI (hoặc API LLM khác).
    *   **URL & Method:** Đảm bảo URL API và Method (POST) đúng với tài liệu của nhà cung cấp AI.
    *   **Body (JSON):** Đây là nơi chứa **Prompt** để AI chấm điểm. Các sếp có thể chỉnh sửa prompt để phù hợp với ngành nghề. Ví dụ: *"Hãy chấm điểm lead này từ 1-10 dựa trên mức độ quan tâm, ngân sách và thời gian mua hàng dự kiến. Trả về kết quả dạng JSON..."*

*   **Node: `Parse AI Scoring Response` (Code)**
    *   Node này dùng JavaScript để tách điểm số (score) và lý do (reason) từ phản hồi của AI.
    *   **Lưu ý:** Nếu AI trả về dữ liệu ở định dạng khác (ví dụ: text thuần thay vì JSON), các sếp cần chỉnh sửa code trong node này để parse đúng.

*   **Node: `Check for Hot Lead` (IF)**
    *   Đây là "bộ não" định tuyến.
    *   **Điều kiện:** Mặc định workflow kiểm tra nếu `score >= 7` (hoặc ngưỡng nào đó). Các sếp nên thay đổi con số này cho phù hợp với chiến lược sales của mình. Ví dụ: Chỉ coi là Hot Lead nếu điểm >= 8.

*   **Node: `Send Hot Lead Email` (Gmail)**
    *   **Credentials:** Chọn credential Gmail đã cấp quyền.
    *   **To:** Điền email của đội ngũ Sales hoặc Manager.
    *   **Subject & Body:** Chỉnh sửa tiêu đề và nội dung email. Nên chèn các biến động như `{{ $json.name }}`, `{{ $json.score }}` để email cá nhân hóa và chứa thông tin chi tiết về lead.

*   **Node: `Append to Hot Leads Sheet` & `Append to Cold Leads Sheet` (Google Sheets)**
    *   **Credentials:** Chọn credential Google Sheets.
    *   **Document ID:** Chọn file Sheet đã tạo sẵn.
    *   **Sheet Name:** Chọn tab (Sheet) tương ứng.
    *   **Mapping:** Đảm bảo các cột trong Sheet khớp với các trường dữ liệu được gửi lên (Name, Email, Company, Score, Reason, Timestamp...).

*   **Node: `Send Form Response` (Respond to Webhook)**
    *   Node này gửi phản hồi "Cảm ơn bạn đã đăng ký" hoặc thông báo tương tự trở lại cho người dùng ngay sau khi form được submit. Chỉnh sửa nội dung response cho phù hợp.

#### 3. Kích hoạt ⚡️
1. **Test Run:** Tạo một lead mẫu (dữ liệu giả) và gửi qua form.
2. Kiểm tra n8n:
   *   Dữ liệu có đi qua các node không?
   *   AI có trả về điểm số hợp lệ không?
   *   Email có được gửi không?
   *   Dữ liệu có xuất hiện đúng tab trong Google Sheets không?
3. Nếu mọi thứ ổn, bật nút **Active** ở góc trên bên phải n8n.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp CRM:** Thay vì chỉ lưu vào Sheets, các sếp có thể thêm node **HubSpot**, **Zoho** hoặc **Salesforce** sau bước "Check for Hot Lead" để tự động tạo deal trong CRM.
- **Thông báo Slack/Telegram:** Thêm node **Slack** hoặc **Telegram** để gửi thông báo lead nóng trực tiếp vào nhóm chat của đội sales, nhanh hơn cả email.
- **Chấm điểm đa chiều:** Thay vì một điểm duy nhất, hãy yêu cầu AI trả về các điểm riêng biệt: *Mức độ quan tâm*, *Khả năng chi trả*, *Thời gian mua hàng*. Sau đó, dùng node **IF** phức tạp hơn để định tuyến dựa trên tổng hợp các điểm này.
- **Lưu Log LLM:** Thêm node **Google Sheets** hoặc **Database** để lưu lại toàn bộ prompt và response của AI. Điều này giúp các sếp phân tích sau này xem AI có đang "chấm điểm" sai hay không và tinh chỉnh prompt tốt hơn.

### 📌 Kết luận
Việc để lead "nguội" đi vì chờ đợi phản hồi là sự lãng phí tài nguyên marketing khổng lồ. Với workflow **Score and route inbound web leads** này, các sếp đã biến quy trình sàng lọc lead từ một công việc thủ công, chậm chạp thành một quy trình tự động, chính xác và tức thì. Hãy import, cấu hình và để AI làm việc thay cho đội ngũ sales của bạn ngay hôm nay!