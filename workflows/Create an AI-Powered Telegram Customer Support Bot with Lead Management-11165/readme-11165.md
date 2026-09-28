---
title: "🤖 Tạo Bot Hỗ Trợ Khách Hàng AI Trên Telegram Với Quản Lý Lead Tự Động (N8n + LangChain)"
description: "Workflow tự động hóa hoàn chỉnh giúp doanh nghiệp xây dựng bot hỗ trợ khách hàng AI trên Telegram, quản lý lead tự động, và trả lời thông minh dựa trên dữ liệu khách hàng. Giảm thời gian phản hồi 90% và cải thiện trải nghiệm khách hàng."
slug: "tai-tao-bot-ai-telegram-quan-ly-lead-n8n"
tags: [n8n, automation, ai-chatbot, telegram-bot, lead-management, no-code]
keywords: [n8n workflow telegram bot, tự động hóa hỗ trợ khách hàng, bot ai quản lý lead, langchain n8n, tự động trả lời tin nhắn telegram]
---

# 🚀 Bot Hỗ Trợ Khách Hàng AI Trên Telegram: Quản Lý Lead Tự Động Với N8n

## 📌 Nỗi Đau Của Doanh Nghiệp
Hiện nay, các doanh nghiệp thường phải đối mặt với những thách thức sau khi hỗ trợ khách hàng qua Telegram:
- **Thời gian phản hồi chậm**: Đội ngũ hỗ trợ phải xử lý hàng trăm tin nhắn mỗi ngày, dẫn đến trải nghiệm khách hàng kém.
- **Dữ liệu khách hàng phân tán**: Thông tin khách hàng (lịch sử tương tác, thông tin liên hệ) thường được lưu trữ rải rác, khó quản lý.
- **Trả lời không cá nhân hóa**: Các bot cơ bản chỉ trả lời theo script, không hiểu được ngữ cảnh cụ thể của từng khách hàng.
- **Không tự động hóa quản lý lead**: Khách hàng tiềm năng (lead) thường bị bỏ qua sau khi gửi tin nhắn đầu tiên.

Workflow này **giải quyết tất cả những vấn đề trên** bằng cách xây dựng một **bot hỗ trợ AI thông minh** trên Telegram, kết hợp với hệ thống quản lý lead tự động. Bot sẽ:
✅ **Trả lời tin nhắn khách hàng ngay lập tức** với trí tuệ nhân tạo (AI).
✅ **Tự động lưu trữ và cập nhật thông tin khách hàng** trong cơ sở dữ liệu.
✅ **Hiểu ngữ cảnh** và trả lời cá nhân hóa dựa trên lịch sử tương tác.
✅ **Quản lý lead tự động**, chuyển đổi khách hàng tiềm năng thành khách hàng thực tế.

---

### 🎯 Kết Quả Các Sếp Nhận Được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm 90% công việc hỗ trợ thủ công, cho phép đội ngũ tập trung vào vấn đề phức tạp.
- **Trải nghiệm khách hàng cao cấp**: Bot trả lời nhanh chóng và cá nhân hóa, tăng tỷ lệ hài lòng.
- **Quản lý lead hiệu quả**: Tự động tạo và cập nhật hồ sơ khách hàng, theo dõi tiến trình chuyển đổi.
- **Hoạt động 24/7**: Bot hoạt động liên tục, không cần nhân viên trực ca.
- **Dễ dàng mở rộng**: Thêm tính năng mới chỉ bằng cách chỉnh sửa prompt hoặc kết nối với cơ sở dữ liệu.
:::

---

### 🔧 Yêu Cầu Cần Thiết
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo bot mới trên [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Cài đặt bot vào nhóm hoặc chat cá nhân để test.

2. **API Key OpenRouter** (hoặc mô hình AI khác):
   - Đăng ký tại [OpenRouter](https://openrouter.ai/) để lấy API Key.
   - Mô hình AI được sử dụng trong workflow là **OpenRouter Chat Model** (có thể thay thế bằng mô hình khác như Mistral, Llama2...).

3. **Cơ sở dữ liệu (Data Table) trong n8n**:
   - **chat_logs**: Lưu lịch sử tin nhắn giữa bot và khách hàng.
   - **leads**: Quản lý thông tin khách hàng (tên, email, số điện thoại, trạng thái lead...).
   - **faq**: Danh sách câu hỏi thường gặp và câu trả lời.
   - **services**: Danh sách dịch vụ của doanh nghiệp.
   - **settings**: Cấu hình chung (ví dụ: thông tin liên hệ, giờ làm việc...).

4. **N8n Self-hosted** (không dùng phiên bản miễn phí):
   - Để workflow hoạt động 24/7, các sếp nên cài n8n trên **VPS riêng**.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---

### 🚀 Cách Import & Lưu Ý Khi "Lên Đồ"

#### 1. Import Workflow 📥
- **Bước 1**: Tải workflow từ [n8n.io/workflows/11165](https://n8n.io/workflows/11165) hoặc sử dụng file JSON đã cung cấp.
- **Bước 2**: Mở **n8n Editor** và chọn **Import Workflow** (từ menu bên trái).
- **Bước 3**: Chọn file JSON và nhấn **Import**.

:::note[LƯU Ý]
- Nếu import từ link, có thể gặp lỗi do các node phụ thuộc (như LangChain). Đảm bảo đã cài đặt **n8n-nodes-langchain** trong n8n.
- Nếu sử dụng phiên bản n8n cloud, một số node có thể không hoạt động do hạn chế API.
:::

---

#### 2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌
Workflow này gồm **15 node** quan trọng, các sếp cần cấu hình kỹ lưỡng như sau:

##### **A. Cấu Hình Telegram**
1. **Telegram - Incoming Message** (Node `telegramTrigger`):
   - Đi đến **Credentials** > **Add** > **Telegram API**.
   - Nhập **API Token** từ bot trên Telegram.
   - Chọn **Chat Type**: `Private` (chat cá nhân) hoặc `Group` (nhóm).
   - **Lưu ý**: Bot chỉ phản hồi tin nhắn từ người dùng đã thêm vào danh sách (`chat_id`).

2. **Telegram - Send Response** (Node `telegram`):
   - Sử dụng cùng **credentials** Telegram như trên.
   - Đảm bảo **chat_id** được truyền từ node trước để bot trả lời chính xác.

##### **B. Cấu Hình AI Agent**
1. **OpenRouter Chat Model** (Node `lmChatOpenRouter`):
   - Đi đến **Credentials** > **Add** > **openRouterApi**.
   - Nhập **API Key** từ OpenRouter.
   - Chọn mô hình AI (ví dụ: `openai/gpt-3.5-turbo`).
   - **Lưu ý**: Nếu muốn thay đổi mô hình, chỉnh sửa trong **Configuration** của node.

2. **AI - Smart Support Assistant** (Node `agent`):
   - Node này sử dụng **LangChain Agent** để xử lý logic AI.
   - **Prompt mặc định** đã được tối ưu hóa để:
     - Trả lời câu hỏi khách hàng.
     - Cập nhật thông tin lead nếu thiếu.
     - Truy cập dữ liệu từ **FAQ**, **Services**, **Settings**.
   - **Lưu ý**: Nếu muốn thay đổi hành vi của bot, chỉnh sửa **prompt** trong **Configuration** của node `agent`.

##### **C. Cấu Hình Quản Lý Lead**
1. **DB - Get Lead by User ID** (Node `dataTable`):
   - Chọn **Data Table** là `leads`.
   - Cấu hình **Key Parameters**:
     - `operation`: `get`
     - `filter`: `{ "chat_id": "$node['Telegram - Incoming Message'].json()['chat']['id']" }`
   - **Lưu ý**: Đảm bảo cột `chat_id` trong bảng `leads` tồn tại.

2. **DB - Create Lead** (Node `dataTable`):
   - Chọn **Data Table** là `leads`.
   - Cấu hình **New Row Data**:
     ```json
     {
       "chat_id": "$node['Telegram - Incoming Message'].json()['chat']['id']",
       "first_name": "$node['Telegram - Incoming Message'].json()['from']['first_name']",
       "last_name": "$node['Telegram - Incoming Message'].json()['from']['last_name']",
       "status": "new"
     }
     ```

3. **DB - Update Lead** (Node `dataTableTool`):
   - Chọn **Data Table** là `leads`.
   - Cấu hình **Key Parameters**:
     - `operation`: `update`
     - `filter`: `{ "chat_id": "$node['Telegram - Incoming Message'].json()['chat']['id']" }`
   - **Lưu ý**: Node này sẽ tự động cập nhật thông tin lead khi AI phát hiện thông tin mới trong tin nhắn.

##### **D. Cấu Hình Logging**
1. **Log - User Message** và **Log - Bot Message** (Node `dataTable`):
   - Chọn **Data Table** là `chat_logs`.
   - Cấu hình **New Row Data**:
     - **User Message**:
       ```json
       {
         "chat_id": "$node['Telegram - Incoming Message'].json()['chat']['id']",
         "message": "$node['Telegram - Incoming Message'].json()['text']",
         "is_bot": false,
         "timestamp": "$node['Telegram - Incoming Message'].json()['date']"
       }
       ```
     - **Bot Message**:
       ```json
       {
         "chat_id": "$node['Telegram - Incoming Message'].json()['chat']['id']",
         "message": "$node['Telegram - Send Response'].json()['text']",
         "is_bot": true,
         "timestamp": "$node['Telegram - Send Response'].json()['date']"
       }
       ```

##### **E. Cấu Hình Context Builder**
1. **Build Assistant Context** (Node `code`):
   - Node này kết hợp dữ liệu từ:
     - Tin nhắn của khách hàng.
     - Thông tin lead (nếu có).
     - Thông tin Telegram user.
   - **Mã mặc định** đã tối ưu hóa, nhưng các sếp có thể chỉnh sửa để thêm thông tin khác (ví dụ: lịch sử tương tác trước đó).

##### **F. Cấu Hình If Condition**
1. **Check – Lead Record** (Node `if`):
   - Node này kiểm tra xem lead có tồn tại hay không.
   - **Condition**:
     ```json
     {
       "condition": "$node['DB - Get Lead by User ID'].json()['items'].length > 0"
     }
     ```
   - Nếu **true**: Bot sẽ cập nhật lead hiện có.
   - Nếu **false**: Bot sẽ tạo lead mới.

---

#### 3. Kích Hoạt ⚡️
1. **Test Run**:
   - Gửi tin nhắn từ Telegram đến bot và kiểm tra:
     - Bot có trả lời không?
     - Thông tin lead có được lưu đúng không?
     - AI có trả lời phù hợp không?

2. **Bật Active Workflow**:
   - Sau khi test thành công, chuyển trạng thái workflow từ **Inactive** sang **Active**.

---

### ✍️ Mẹo & Gợi Ý Nâng Cao
:::tip[CÁCH TIẾP CẬN THÊM]
1. **Kết Nối Với CRM**:
   - Thay vì sử dụng Data Table trong n8n, kết nối với **HubSpot**, **Zoho CRM**, hoặc **Salesforce** để quản lý lead chuyên nghiệp hơn.

2. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng node **Email** hoặc **Slack** để gửi báo cáo hàng ngày về số lượng lead mới, câu hỏi thường gặp, và tiến độ hỗ trợ.

3. **Thêm Tính Năng Chat History**:
   - Lưu toàn bộ lịch sử chat trong một bảng riêng và hiển thị lại cho khách hàng khi họ quay lại (ví dụ: "Lần trước bạn hỏi về...").

4. **Tích Hợp với Google Sheets/Excel**:
   - Nếu không muốn sử dụng Data Table trong n8n, thay thế bằng **Google Sheets** để dễ dàng theo dõi và phân tích dữ liệu.

5. **Cập Nhật FAQ & Services Tự Động**:
   - Sử dụng API của doanh nghiệp để cập nhật danh sách dịch vụ hoặc FAQ từ một nguồn dữ liệu trung tâm.

6. **Thêm Hỗ Trợ Ngôn Ngữ**:
   - Sử dụng mô hình AI đa ngôn ngữ (ví dụ: `openai/gpt-4-1106-vision-preview`) để bot hỗ trợ khách hàng trên nhiều ngôn ngữ.

7. **Xây Dựng Hệ Thống Tích Lũy Điểm**:
   - Bot có thể khuyến khích khách hàng trả lời câu hỏi bằng cách tích lũy điểm (ví dụ: "Câu trả lời của bạn giúp bot học hỏi hơn!").

---

### 📌 Kết Luận
Workflow này là **giải pháp hoàn chỉnh** để các doanh nghiệp xây dựng một **bot hỗ trợ khách hàng AI thông minh** trên Telegram, kết hợp với hệ thống quản lý lead tự động. Với bot này, các sếp sẽ:
- **Giảm thời gian phản hồi** từ giờ đến phút.
- **Tăng tỷ lệ chuyển đổi lead** nhờ tự động hóa.
- **Cải thiện trải nghiệm khách hàng** với trả lời cá nhân hóa.
- **Tiết kiệm chi phí** bằng cách giảm công việc hỗ trợ thủ công.

**Hành động ngay hôm nay**:
1. Cài đặt n8n trên VPS và import workflow.
2. Cấu hình Telegram Bot và API Key.
3. Test và bật workflow.
4. Theo dõi kết quả và mở rộng tính năng!

👉 **Bắt đầu tự động hóa ngay**: [Tải workflow từ n8n.io](https://n8n.io/workflows/11165)

---
:::note[CHÚ Ý CUỐI CÙNG]
- Workflow này yêu cầu **n8n self-hosted** để hoạt động 24/7. Nếu sử dụng phiên bản cloud, một số tính năng có thể bị giới hạn.
- Để tối ưu hóa AI, các sếp nên **cập nhật prompt** và **dữ liệu training** thường xuyên.
- Nếu gặp vấn đề, tham khảo [Community n8n](https://community.n8n.io/) hoặc liên hệ với tác giả Osama Goda.
:::