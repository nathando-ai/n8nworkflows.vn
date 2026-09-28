---
title: "🚀 Tự Động Phân Loại Email & Soạn Thảo Trả Lời Bằng GPT-5.1 + Cảnh Báo Telegram"
description: "Workflow n8n giúp tự động phân loại email vào hộp thư Gmail, soạn thảo câu trả lời thông minh dựa trên cơ sở dữ liệu doanh nghiệp và gửi cảnh báo qua Telegram để duyệt nhanh."
slug: "tu-dong-phan-loai-email-gmail-gpt-telegram"
tags: [n8n, automation, ai-agent, gmail, telegram, gpt-5.1]
keywords: [n8n workflow, tự động hóa email, ai agent gmail, soạn thảo email bằng ai, cảnh báo telegram]
---

# 🚀 Tự Động Phân Loại Email & Soạn Thảo Trả Lời Bằng GPT-5.1 + Cảnh Báo Telegram

Các sếp có bao giờ cảm thấy quá tải khi phải xử lý hàng chục, thậm chí hàng trăm email mỗi ngày? Việc đọc từng email, xác định loại (hỏi giá, khiếu nại, hỗ trợ kỹ thuật), tìm kiếm thông tin trong các tài liệu nội bộ để trả lời chính xác, rồi soạn lại câu từ chuyên nghiệp... là một quy trình lặp đi lặp lại, tốn kém thời gian và dễ gây sai sót do mệt mỏi.

Workflow này chính là "trợ lý ảo" 24/7 cho hộp thư Gmail của các sếp. Nó sử dụng sức mạnh của **GPT-5.1** (mô hình AI mới nhất) kết hợp với **RAG (Retrieval-Augmented Generation)** để:
1. Tự động đọc và phân loại email vào các nhãn (Labels) phù hợp.
2. Soạn thảo sẵn câu trả lời dựa trên **Cơ sở dữ liệu kiến thức (Knowledge Base)** của công ty (giá cả, chính sách, FAQ...).
3. Gửi thông báo ngay lập tức qua **Telegram** kèm link để các sếp chỉ cần bấm "Gửi" sau khi duyệt nhanh.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian phản hồi:** AI làm phần việc nặng nhọc (đọc, phân loại, soạn thảo), các sếp chỉ cần duyệt và gửi.
- **Độ chính xác cao nhờ RAG:** Câu trả lời luôn dựa trên dữ liệu thực tế của công ty (giá, chính sách) chứ không phải "bịa" của AI, giảm thiểu rủi ro thông tin sai lệch.
- **Tổ chức hộp thư gọn gàng:** Email được tự động gắn nhãn (Labels) theo đúng quy trình, dễ dàng lọc và tìm kiếm sau này.
- **Phản hồi tức thì:** Nhận cảnh báo qua Telegram ngay khi có email quan trọng, không bỏ lỡ cơ hội kinh doanh hay hỗ trợ khách hàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Gmail:** Đã bật OAuth2 cho n8n.
2. **Tài khoản OpenAI:** Có API Key để sử dụng mô hình `gpt-5.1`.
3. **Tài khoản Telegram:** Đã tạo Bot và lấy được `Chat ID` của mình.
4. **Cơ sở dữ liệu kiến thức (Knowledge Base):** Một bảng dữ liệu (Data Table) chứa thông tin về công ty, sản phẩm, bảng giá, chính sách đổi trả, FAQ...
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/12955) hoặc copy toàn bộ JSON code và dán vào n8n Editor.
- Mở n8n -> Click vào biểu tượng "Import from URL" hoặc "Import from File".
- Dán link hoặc file JSON vào.
- Workflow sẽ hiện ra với 9 nodes chính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Các sếp cần cấu hình từng node theo thứ tự sau:

**1. Node: `New Email Trigger` (Gmail Trigger)**
- **Credentials:** Chọn tài khoản Gmail OAuth2 của các sếp.
- **Settings:** Mặc định nó sẽ kiểm tra email mới mỗi 1 phút. Các sếp có thể chỉnh tần suất này nếu cần (ví dụ: 5 phút/lần để tiết kiệm API call).
- **Filter:** Có thể thêm điều kiện lọc để chỉ xử lý email từ một domain cụ thể hoặc có từ khóa nhất định, tránh xử lý spam.

**2. Node: `Get Knowledge Base Data` (Data Table)**
- **Operation:** `get`
- **Data Table:** Các sếp cần tạo một Data Table trong n8n (hoặc kết nối với nguồn dữ liệu khác nếu có) có tên là **"Customer Support Knowledge Base"**.
- **Nội dung bảng:** Đây là "xương sống" của workflow. Các sếp cần điền vào bảng này các cột như: `Topic` (Chủ đề), `Answer` (Câu trả lời mẫu), `Price` (Giá), `Policy` (Chính sách). Càng nhiều dữ liệu chính xác, AI trả lời càng tốt.

**3. Node: `Get Gmail Labels List` & `Aggregate Labels Data`**
- **Credentials:** Chọn cùng tài khoản Gmail OAuth2.
- **Mục đích:** Workflow sẽ tự động lấy danh sách các Label (Nhãn) hiện có trong hộp thư Gmail của các sếp.
- **Lưu ý:** Các sếp nên tạo sẵn các Label trong Gmail trước khi chạy workflow (ví dụ: `Hỏi Giá`, `Khiếu Nại`, `Hỗ Trợ Kỹ Thuật`, `Đã Xử Lý`). AI sẽ dựa vào danh sách này để gán nhãn chính xác.

**4. Node: `Email Categorization AI Agent` (Agent)**
- **Model:** Chọn `OpenAI Chat Model` (đã cấu hình ở bước dưới).
- **Prompt:** Đây là "bộ não" của workflow. Các sếp cần đọc kỹ prompt mặc định và chỉnh sửa cho phù hợp với ngành nghề của mình.
    - *Ví dụ:* Thay vì "existing_order", các sếp có thể đổi thành "Đơn hàng cũ".
    - *Ví dụ:* Thay vì "quote_request", đổi thành "Yêu cầu báo giá".
    - Đảm bảo prompt hướng dẫn AI rõ ràng: "Nếu email là hỏi giá, hãy soạn thảo câu trả lời dựa trên Knowledge Base và gán nhãn 'Hỏi Giá'".

**5. Node: `OpenAI Chat Model`**
- **Credentials:** Chọn API Key OpenAI của các sếp.
- **Model:** Mặc định là `gpt-5.1`. Các sếp có thể giữ nguyên hoặc đổi sang `gpt-4o` nếu muốn tiết kiệm chi phí, nhưng `gpt-5.1` sẽ cho chất lượng phân loại và soạn thảo tốt hơn.

**6. Node: `Create a draft in Gmail` (Gmail Tool)**
- **Credentials:** Chọn tài khoản Gmail OAuth2.
- **Mục đích:** AI sẽ tạo một bản nháp (Draft) trong hộp thư Gmail với nội dung đã soạn sẵn. Các sếp sẽ thấy email này ở mục "Drafts".

**7. Node: `Add label to message in Gmail` (Gmail Tool)**
- **Credentials:** Chọn tài khoản Gmail OAuth2.
- **Mục đích:** Tự động gắn nhãn (Label) đã phân loại vào email gốc.

**8. Node: `Send a text message in Telegram` (Telegram Tool)**
- **Credentials:** Chọn Bot Token của Telegram.
- **Chat ID:** **BẮT BUỘC** các sếp phải thay `Chat ID` bằng ID của chính mình. Các sếp có thể tìm Chat ID bằng cách nhắn tin cho bot `@userinfobot` trên Telegram.
- **Nội dung:** Thông báo sẽ bao gồm: Tiêu đề email, Người gửi, Loại email, và Link trực tiếp đến bản nháp trong Gmail.

#### 3. Kích hoạt ⚡️
- **Test Run:** Gửi một email mẫu từ một tài khoản khác vào hộp thư Gmail của các sếp.
- Chạy workflow (Click "Execute Workflow").
- Kiểm tra:
    1. Email có được gắn nhãn đúng không?
    2. Bản nháp (Draft) có xuất hiện trong Gmail không? Nội dung có hợp lý không?
    3. Có nhận được thông báo trên Telegram không?
- Nếu mọi thứ ổn, bật công tắc **Active** để workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy biến Prompt theo ngành:** Nếu các sếp làm trong lĩnh vực y tế, luật, hay tài chính, hãy thêm các quy tắc đặc thù vào Prompt của AI Agent (ví dụ: "Luôn nhắc khách hàng tham khảo ý kiến bác sĩ" hoặc "Không cam kết lãi suất cụ thể").
- **Kết nối với CRM:** Thay vì chỉ tạo Draft, các sếp có thể thêm node để cập nhật trạng thái khách hàng trong CRM (như HubSpot, Salesforce) ngay khi email được phân loại.
- **Gửi báo cáo định kỳ:** Thêm một workflow con chạy hàng tuần để tổng hợp số lượng email theo từng loại, tỷ lệ phản hồi, và gửi báo cáo qua Email hoặc Slack.
- **Xử lý đa ngôn ngữ:** Nếu khách hàng gửi email bằng tiếng Anh, các sếp có thể thêm bước dịch thuật hoặc yêu cầu AI trả lời bằng ngôn ngữ tương ứng trong Prompt.

### 📌 Kết luận
Với workflow này, các sếp không còn phải lo lắng về việc bỏ sót email hay trả lời chậm. AI sẽ làm phần việc nặng nhọc, còn các sếp chỉ cần tập trung vào việc duyệt và chốt đơn. Đây là bước đi đầu tiên để xây dựng một hệ thống hỗ trợ khách hàng tự động hóa, chuyên nghiệp và hiệu quả. Hãy thử ngay và cảm nhận sự khác biệt!