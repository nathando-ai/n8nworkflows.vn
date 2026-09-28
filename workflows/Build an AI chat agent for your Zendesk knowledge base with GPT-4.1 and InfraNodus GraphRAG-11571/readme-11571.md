---
title: "🤖 **Tự Động Hóa Trợ Lý Chat AI Cho Zendesk Sử Dụng GPT-4.1 + GraphRAG (InfraNodus) - Giúp Khách Hàng Trả Lời Tự Động 24/7**"
description: "Workflow này tự động hóa việc trả lời câu hỏi hỗ trợ khách hàng từ cơ sở tri thức Zendesk bằng trí tuệ nhân tạo GPT-4.1 và công nghệ GraphRAG của InfraNodus, giảm thiểu thời gian phản hồi và nâng cao chất lượng dịch vụ. Đặc biệt phù hợp cho các doanh nghiệp có lượng ticket hỗ trợ lớn."
slug: "tự-dộng-hoa-trợ-ly-chat-ai-zendesk-gpt-4-1-graphrag"
tags: [n8n, automation, ai-chatbot, zendesk, graphrag, infra-nodus, no-code]
keywords: [tự động hóa hỗ trợ khách hàng, chatbot zendesk, graphrag ai, gpt-4.1 tự động hóa, n8n workflow hỗ trợ, tự động trả lời ticket zendesk]
---

# 🚀 **Tạo Trợ Lý Chat AI Tự Động Hóa Cho Zendesk Với GPT-4.1 + GraphRAG (InfraNodus)**

## **Giải Pháp Cho Nỗi Đau Của Các Sếp**
Hỗ trợ khách hàng là một trong những công việc tốn thời gian và đòi hỏi sự chính xác nhất của doanh nghiệp. Khi khách hàng gửi câu hỏi liên quan đến cơ sở tri thức Zendesk, việc tìm kiếm và trả lời thủ công không chỉ tốn thời gian mà còn dễ gây sai sót, đặc biệt khi lượng ticket tăng cao. **Workflow này tự động hóa toàn bộ quy trình trả lời bằng trí tuệ nhân tạo (AI) kết hợp với công nghệ GraphRAG của InfraNodus**, giúp:
- **Trả lời tự động** trong thời gian thực (thậm chí khi nhân viên nghỉ ngơi).
- **Nâng cao chất lượng** bằng cách phân tích ngữ cảnh và kết nối thông tin từ cơ sở tri thức một cách logic.
- **Giảm tải cho đội ngũ hỗ trợ**, tập trung vào các vấn đề phức tạp hơn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Trả lời tự động hàng nghìn ticket/ngày mà không cần nhân viên.
- **Chính xác cao**: Sử dụng GraphRAG để hiểu ngữ cảnh và kết nối thông tin từ Zendesk một cách logic.
- **Cá nhân hóa**: Trợ lý AI hiểu được lịch sử trò chuyện qua **bộ nhớ hội thoại (Chat Memory)**.
- **Hoạt động liên tục**: Khách hàng được hỗ trợ ngay cả khi hệ thống Zendesk offline.
- **Nâng cao trải nghiệm khách hàng**: Trả lời nhanh chóng và chuyên nghiệp, tăng độ tin tưởng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản và API Key**:
   - **OpenAI API Key**: Để sử dụng mô hình GPT-4.1 (mô hình miễn phí và hiệu suất cao).
   - **Zendesk API Token**: Truy cập tại **Admin > Apps & Integrations > API Tokens** (ví dụ: `https://[tên-portal].zendesk.com/admin/apps-integrations/apis/api-tokens`).
   - **InfraNodus API Key**: Để kết nối với công cụ GraphRAG (mô tả chi tiết tại [InfraNodus Docs](https://infranodus.com/docs/)).
2. **Cơ sở tri thức Zendesk**: Workflow sẽ tìm kiếm và trả lời dựa trên nội dung trong **Help Center** của Zendesk.
3. **n8n Self-hosted**: Để chạy workflow 24/7 mà không phụ thuộc vào phiên bản cloud.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/11571](https://n8n.io/workflows/11571) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/11571) và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này gồm **7 node chính**, mỗi node đều cần cấu hình kỹ lưỡng:

##### **A. Webhook (Bắt đầu workflow)**
- **Node**: `Webhook`
- **Cấu hình**:
  - **Path**: Giá trị mặc định là `486b2675-a4d1-4050-ad3a-7d92a57c084b` (có thể thay đổi nếu muốn).
  - **Kết nối với n8n Chat Widget**: Sau khi import, **không thay đổi path** nếu đã cài đặt widget trên website.

##### **B. Trợ Lý AI (Agent) với LangChain**
- **Node**: `Support Agent` (type: `agent`)
- **Cấu hình**:
  - **Prompt**: Đã được tối ưu hóa để:
    1. **Tìm kiếm thông tin từ GraphRAG** (InfraNodus) trước khi gửi query đến Zendesk.
    2. **Tái cấu trúc câu hỏi** để tăng độ chính xác khi tìm kiếm trong Zendesk.
    3. **Tổng hợp và trả lời** dựa trên kết quả từ cả hai nguồn.
  - **Lưu ý**: **Không chỉnh sửa cấu trúc prompt** nếu không hiểu rõ GraphRAG, chỉ thay đổi nội dung phù hợp với cơ sở tri thức của bạn.

##### **C. GraphRAG (InfraNodus) - Trí Tuệ Báo Trước**
- **Node**: `Get a response from knowledge base in InfraNodus Graph RAG`
- **Cấu hình**:
  - **Credentials**: Chọn `infranodusApi` (đã cấu hình trước khi import).
  - **Prompt**: Workflow tự động lấy **câu hỏi từ user** và gửi đến InfraNodus để phân tích.
  - **Lưu ý**:
    - Nếu chưa có **ontology** (bản đồ tri thức) trong InfraNodus, hãy tạo trước tại [InfraNodus Dashboard](https://infranodus.com/docs/).
    - **Không cần chỉnh sửa prompt** nếu muốn sử dụng cấu trúc mặc định.

##### **D. Tìm Kiếm Zendesk API**
- **Node**: `Zendek Search` (type: `httpRequestTool`)
- **Cấu hình**:
  - **Credentials**: Chọn `zendeskApi` (API Token từ Zendesk).
  - **Endpoint**: `https://[tên-portal].zendesk.com/api/v2/help_center/articles/search.json`
  - **Query**: Workflow tự động lấy từ **trợ lý AI** (node `Support Agent`) sau khi được cải tiến bởi GraphRAG.
  - **Lưu ý**:
    - Đảm bảo **API Token** có quyền truy cập vào **Help Center**.
    - Thêm tham số `q={{$json["query"]}}` vào **Body** của request.

##### **E. Bộ Nhớ Hội Thoại (Chat Memory)**
- **Node**: `Simple Memory` (type: `memoryBufferWindow`)
- **Cấu hình**:
  - **Window Size**: Giá trị mặc định là `5` (lưu 5 lần trò chuyện gần nhất).
  - **Lưu ý**: Nếu muốn lưu nhiều hơn, tăng giá trị này (nhưng không quá 10 để tránh quá tải).

##### **F. Trả Lời Webhook**
- **Node**: `Respond to Webhook`
- **Cấu hình**:
  - **Body**: `{{$node["Support Agent"].json}}` (trả lời dựa trên kết quả từ trợ lý AI).
  - **Lưu ý**: Đảm bảo **Webhook URL** trong `n8n Chat Widget` trùng khớp với path trong node `Webhook`.

##### **G. OpenAI Chat Model (GPT-4.1)**
- **Node**: `OpenAI Chat Model`
- **Cấu hình**:
  - **Credentials**: Chọn `openAiApi`.
  - **Model**: Chọn `gpt-4.1-mini` (mô hình hiệu suất cao và rẻ).
  - **Lưu ý**:
    - Đảm bảo **API Key OpenAI** được cập nhật trong credentials.
    - Nếu muốn sử dụng mô hình khác (ví dụ: `gpt-4`), thay đổi tại `keyParameters.model`.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Gửi một **câu hỏi mẫu** (ví dụ: *"Làm thế nào để reset mật khẩu?"*) qua **n8n Chat Widget**.
   - Kiểm tra kết quả trả lời từ **node `Respond to Webhook`**.
2. **Bật Active**:
   - Chuyển trạng thái workflow từ **Inactive** sang **Active**.
   - Đảm bảo **n8n chạy 24/7** trên VPS.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Sử dụng **node `webhook`** để gửi kết quả trả lời AI về **Slack/Telegram** để giám sát.
   - Cách làm: Thêm node `httpRequest` để gửi thông báo khi có ticket mới được trả lời tự động.

2. **Lưu Log Trò Chuyện**:
   - Thêm **node `n8n-nodes-base.if`** để lưu lịch sử trò chuyện vào **Google Sheets** hoặc **Notion**.
   - Cách làm:
     ```json
     {
       "resources": {
         "sheets": {
           "type": "googleSheets",
           "credentials": "googleSheetsApi"
         }
       }
     }
     ```

3. **Báo Cáo Định Kỳ**:
   - Sử dụng **node `n8n-nodes-base.schedule`** để gửi báo cáo hàng ngày về:
     - Số lượng ticket tự động trả lời.
     - Thời gian phản hồi trung bình.
     - Tỷ lệ thành công của GraphRAG.

4. **Cải Tiến Prompt**:
   - Nếu muốn **tăng độ chính xác**, hãy:
     - Thêm **ví dụ cụ thể** vào prompt của `Support Agent`.
     - Sử dụng **ontology** trong InfraNodus để định nghĩa rõ ràng các khái niệm trong cơ sở tri thức.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa hỗ trợ khách hàng trên Zendesk với **trí tuệ nhân tạo GPT-4.1 + GraphRAG**, giúp doanh nghiệp:
✅ **Giảm thời gian phản hồi** từ giờ đến giây.
✅ **Nâng cao chất lượng dịch vụ** với trả lời logic và chính xác.
✅ **Tiết kiệm chi phí** bằng cách giảm tải cho đội ngũ hỗ trợ.

**Hành động ngay hôm nay**:
1. **Cài đặt n8n trên VPS** (sử dụng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình API keys.
3. **Test với n8n Chat Widget** trên website.
4. **Bật Active** và theo dõi kết quả!

---
**💡 Lưu ý cuối cùng**: Nếu gặp vấn đề, hãy tham khảo [hướng dẫn video của InfraNodus](https://www.youtube.com/watch?v=aYoPSEmGJbc) hoặc liên hệ hỗ trợ tại [n8n Community](https://community.n8n.io/). Chúc các sếp thành công! 🚀