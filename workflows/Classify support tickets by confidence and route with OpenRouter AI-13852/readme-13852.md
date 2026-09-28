---
title: "🤖 Tự Động Phân Loại & Chuyển Hướng Ticket Hỗ Trợ Với AI (OpenRouter)"
description: "Workflow n8n sử dụng AI để phân loại ticket hỗ trợ khách hàng, đánh giá độ tin cậy và tự động chuyển hướng đến đúng bộ phận (Kỹ thuật, Hóa đơn, Sales) hoặc hàng đợi con người."
slug: "tu-dong-phan-loai-ticket-ho-tro-voi-ai"
tags: [n8n, automation, ai, customer-support, openrouter, no-code]
keywords: [n8n workflow, phân loại ticket, tự động hóa hỗ trợ khách hàng, AI agent, openrouter]
---

# 🤖 Tự Động Phân Loại & Chuyển Hướng Ticket Hỗ Trợ Với AI (OpenRouter)

Trong môi trường kinh doanh hiện đại, đội ngũ hỗ trợ khách hàng (Support Team) thường bị quá tải với hàng trăm ticket mỗi ngày. Việc đọc, hiểu và phân loại từng ticket thủ công không chỉ tốn thời gian mà còn dễ dẫn đến sai sót: gửi ticket kỹ thuật cho bộ phận sales, hoặc bỏ sót các vấn đề khẩn cấp về hóa đơn.

Workflow **"Classify support tickets by confidence and route with OpenRouter AI"** chính là giải pháp "chốt hạ" cho bài toán này. Thay vì con người phải làm việc lặp đi lặp lại, workflow này sử dụng sức mạnh của AI (cụ thể là mô hình Gemini 3 Flash qua OpenRouter) để đọc nội dung ticket, xác định chủ đề, đánh giá độ tin cậy (confidence score) và tự động chuyển hướng ticket đến đúng đội ngũ xử lý. Nếu AI không chắc chắn, nó sẽ tự động chuyển ticket vào hàng đợi để con người xem xét, đảm bảo không có ticket nào bị "lọt lưới".

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý lượng lớn ticket mà không bị gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80-90% thời gian phân loại:** AI xử lý tức thì, con người chỉ tập trung vào việc giải quyết vấn đề phức tạp.
- **Chính xác & Minh bạch:** Mỗi ticket đều có điểm số độ tin cậy (confidence score), giúp quản lý đánh giá hiệu quả của AI theo thời gian.
- **Giảm rủi ro sai sót:** Cơ chế "Confidence Threshold" đảm bảo các ticket khó xử lý hoặc AI không chắc chắn sẽ được chuyển ngay cho con người, tránh trường hợp AI "bịa" hoặc xử lý sai quy trình.
- **Tích hợp linh hoạt:** Có thể dễ dàng thay thế các node xử lý giả lập (Code nodes) bằng các tích hợp thực tế như Slack, Jira, Zendesk hay Email.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Bản Self-hosted hoặc Cloud.
- **Tài khoản OpenRouter:** Các sếp cần có API Key từ [OpenRouter.ai](https://openrouter.ai/) để kết nối với các mô hình LLM (workflow mặc định dùng `google/gemini-3-flash-preview`).
- **Endpoint nhận ticket:** Một webhook hoặc API từ hệ thống ticket hiện tại (Zendesk, Freshdesk, hoặc một form đơn giản) để gửi dữ liệu vào n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Nhấn vào nút **"Import from File"** hoặc **"Import from URL"**.
3. Chọn file JSON của workflow hoặc dán link gốc: `https://n8n.io/workflows/13852`.
4. Workflow sẽ hiện ra trên canvas với các nhóm node được sắp xếp rõ ràng theo luồng: *Receive & Normalize* -> *AI Classification* -> *Confidence Routing* -> *Category Routing*.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Dưới đây là các node quan trọng mà các sếp cần cấu hình để workflow hoạt động đúng ý đồ:

*   **Node: `OpenRouter Chat Model`**
    *   Đây là "bộ não" của workflow.
    *   **Credentials:** Chọn hoặc tạo credential mới cho OpenRouter.
    *   **Model:** Mặc định là `google/gemini-3-flash-preview`. Các sếp có thể đổi sang các model khác hỗ trợ trên OpenRouter (như Llama 3, Mistral, GPT-4o mini...) tùy theo ngân sách và nhu cầu tốc độ/độ chính xác.

*   **Node: `Webhook - Incoming Ticket`**
    *   Đây là điểm đầu vào.
    *   **Path:** Mặc định là `route-ticket`. Các sếp cần đảm bảo hệ thống ticket của mình gửi POST request đến đúng URL này.
    *   **Body:** Dữ liệu gửi vào cần có cấu trúc chuẩn (thường là JSON chứa `subject` và `description`). Node `Normalize Ticket` sẽ xử lý dữ liệu thô này.

*   **Node: `AI - Classify` (Agent)**
    *   Node này chứa prompt hướng dẫn AI phân loại ticket.
    *   Các sếp nên kiểm tra prompt bên trong node này để đảm bảo danh sách các **Category** (Danh mục) khớp với cấu trúc tổ chức của mình (Ví dụ: Billing, Technical, Sales, General). Nếu công ty có thêm bộ phận "HR" hay "Legal", hãy thêm vào prompt để AI nhận diện.

*   **Node: `Confidence Threshold` (Switch)**
    *   Đây là node quyết định "AI tự xử lý" hay "Giao cho người".
    *   Mặc định:
        *   **High (> 0.85):** Tự động chuyển tiếp.
        *   **Medium (0.6 - 0.85):** Đánh dấu để xem xét (Flag for Review).
        *   **Low (< 0.6):** Chuyển vào hàng đợi con người (Human Queue).
    *   **Mẹo:** Ban đầu, các sếp nên giữ ngưỡng cao (0.85) để đảm bảo chất lượng. Sau khi chạy ổn định và thấy AI chính xác, có thể hạ ngưỡng xuống (ví dụ 0.7) để tăng tỷ lệ tự động hóa.

*   **Các Node Xử Lý Đội Ngũ (`Billing Team`, `Technical Team`, `Sales Team`, `General Inbox`)**
    *   Trong workflow mẫu, đây là các **Code nodes** chỉ để mô phỏng việc gửi đi.
    *   **Hành động bắt buộc:** Các sếp cần thay thế các node này bằng các node tích hợp thực tế.
        *   *Ví dụ:* Thay `Technical Team` bằng node **Slack** (gửi tin nhắn vào kênh #tech-support), hoặc **Jira** (tạo ticket mới), hoặc **Email** (gửi cho email bộ phận kỹ thuật).

*   **Node: `Respond`**
    *   Node này trả về phản hồi cho hệ thống gọi webhook (ví dụ: trả về status `success` kèm theo category đã phân loại). Các sếp có thể chỉnh sửa nội dung trả về nếu hệ thống ticket của mình cần thông tin phản hồi cụ thể.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
    *   Nhấn nút **"Test Workflow"**.
    *   Mở tab **Webhook** và copy URL test.
    *   Dùng Postman hoặc cURL để gửi một ticket mẫu:
      ```json
      {
        "subject": "Lỗi không thể đăng nhập",
        "description": "Tôi nhập đúng mật khẩu nhưng vẫn bị báo sai. Đã thử reset nhưng không được."
      }
      ```
    *   Quan sát luồng chạy: AI sẽ phân loại là "Technical" với confidence score cao, và ticket sẽ đi vào nhánh `Technical Team`.
    *   Thử một ticket mơ hồ:
      ```json
      {
        "subject": "Cần hỗ trợ",
        "description": "Có vấn đề gì đó với tài khoản của tôi."
      }
      ```
    *   Quan sát: AI sẽ có confidence score thấp, ticket sẽ đi vào nhánh `Send to Human Queue`.

2. **Bật Active:**
    *   Sau khi test thành công, tắt chế độ test và bật nút **Active** ở góc trên bên phải.
    *   Copy **Production URL** từ node Webhook và cấu hình hệ thống ticket của các sếp gửi dữ liệu đến đây.

### ✍️ Mẹo & gợi ý nâng cao

1. **Tích hợp Slack/Telegram cho cảnh báo:**
   Thay vì chỉ lưu log, hãy thêm node **Slack** hoặc **Telegram** vào nhánh `Flag for Review` và `Send to Human Queue`. Khi AI không chắc chắn, nó sẽ gửi thông báo ngay lập tức cho quản lý hoặc nhân viên trực để can thiệp, tránh tình trạng ticket bị "chôn" trong hàng đợi.

2. **Lưu lịch sử phân loại vào Google Sheets:**
   Thêm node **Google Sheets** sau node `Parse + Validate` để lưu lại: `Ticket ID`, `Subject`, `Category`, `Confidence Score`, `Timestamp`. Điều này giúp các sếp có dữ liệu để phân tích: "AI đang phân loại sai loại nào nhiều nhất?" và từ đó tinh chỉnh prompt.

3. **Tinh chỉnh Prompt theo ngành nghề:**
   Nếu các sếp hoạt động trong lĩnh vực y tế, tài chính hoặc pháp lý, hãy thêm các quy tắc nghiêm ngặt vào prompt của node `AI - Classify`. Ví dụ: *"Nếu ticket liên quan đến dữ liệu bệnh nhân, luôn gán confidence score thấp nhất để chuyển cho con người"*.

4. **Kết nối với CRM (HubSpot/Salesforce):**
   Thay vì chỉ gửi email, hãy dùng node **HubSpot** để cập nhật trường `Ticket Category` và `AI Confidence` trực tiếp trên profile khách hàng. Điều này giúp bộ phận Sales hiểu rõ hơn về trải nghiệm của khách hàng trước khi liên lạc tiếp.

### 📌 Kết luận

Workflow **"Classify support tickets by confidence and route with OpenRouter AI"** là một ví dụ điển hình cho việc ứng dụng AI một cách thực dụng và an toàn trong doanh nghiệp. Thay vì để AI "làm hết", workflow này tạo ra một cơ chế kiểm soát chặt chẽ dựa trên độ tin cậy, giúp các sếp vừa tận dụng được tốc độ của AI, vừa đảm bảo chất lượng dịch vụ khách hàng.

Hãy import workflow, thay thế các node giả lập bằng tích hợp thực tế của công ty mình, và bắt đầu tự động hóa quy trình hỗ trợ ngay hôm nay. Chúc các sếp triển khai thành công! 🚀