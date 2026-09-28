---
title: "🚀 Tự Động Gửi Thông Báo Đặc Tính Mới Cho Người Dùng Với Tính Năng Tìm Kiếm Bằng AI (Tally → Gmail)"
description: "Workflow tự động hóa hoàn toàn không cần code để tìm kiếm và thông báo cho người dùng về các tính năng mới phù hợp với yêu cầu cũ của họ, giảm thiểu tỷ lệ rời bỏ và tăng doanh thu từ upsell. Sử dụng AI RAG, vector search và Gmail để cá nhân hóa email."
slug: "tu-dong-hoa-thong-bao-dac-tinh-moi-cho-nguoi-dung"
tags: [n8n, automation, ai-rag, crm, gmail, tallyforms, vector-search, no-code]
keywords: [n8n workflow tự động hóa, tìm kiếm đặc tính mới bằng AI, tự động hóa email cá nhân hóa, vector search với Supabase, n8n + OpenAI, giảm tỷ lệ rời bỏ khách hàng]
---

# 🚀 **Tự Động Gửi Thông Báo Đặc Tính Mới Cho Người Dùng Với Tính Năng Tìm Kiếm Bằng AI**

Bạn đã từng phải mất hàng giờ để tra cứu và gửi email cá nhân hóa cho khách hàng để thông báo về tính năng mới mà họ đã yêu cầu trước đây? Hay thậm chí, những yêu cầu đó bị "quên lãng" trong hệ thống, khiến khách hàng cảm thấy bị bỏ rơi? **Workflow này giải quyết vấn đề đó 100% tự động hóa**, kết hợp **AI RAG (Retrieval-Augmented Generation)**, **tìm kiếm vector** và **Gmail** để:
- **Tự động tìm kiếm** yêu cầu cũ của khách hàng trong Tally Forms.
- **So sánh ngữ nghĩa** với các tính năng mới vừa ra mắt (thông qua RSS Feed hoặc thủ công).
- **Tự động viết email cá nhân hóa** và lưu vào Draft Gmail (không gửi tự động).
- **Giảm tỷ lệ rời bỏ** và **tăng doanh thu từ upsell** khi khách hàng nhận thấy bạn đã "nghe họ nói".

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 với hiệu suất tối ưu, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thủ công tra cứu yêu cầu cũ và viết email.
- **Cá nhân hóa cao**: Email phản hồi dựa trên **ngữ cảnh cụ thể** của yêu cầu cũ (không phải email chung).
- **Hoạt động liên tục**: Kích hoạt bằng **RSS Feed** (changelog) hoặc **thủ công** (test nhanh).
- **Giảm tỷ lệ rời bỏ**: Khách hàng cảm thấy được "lắng nghe" và được thông báo kịp thời.
- **Tăng doanh thu**: Dễ dàng chuyển đổi yêu cầu cũ thành **upsell** khi tính năng mới ra mắt.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản và API Keys**:
   - **Tally Forms**: Tạo form để thu thập yêu cầu từ khách hàng (cần cài đặt plugin `n8n-nodes-tallyforms`).
   - **Supabase**: Tạo project và database (cần cài đặt plugin `@n8n/n8n-nodes-langchain`).
     - **Bảng dữ liệu**: Cần chạy script SQL từ **Template Description** trong workflow (chi tiết ở phần **Cách setup**).
   - **Gmail**:
     - Tạo **OAuth 2.0 Credential** trong n8n (cài đặt plugin `n8n-nodes-base.gmail`).
     - **Email từ**: Sử dụng email chính thức của doanh nghiệp.
   - **OpenAI**:
     - **API Key** cho model `command-r7b` (để viết email) và `nomic-embed-text` (để tạo embedding).
     - **Ollama** (lựa chọn thay thế cho OpenAI Embeddings, nếu muốn giảm chi phí).
   - **RSS Feed** (nếu sử dụng trigger tự động):
     - URL RSS của blog/changelog (ví dụ: `https://tên-blog.com/feed.xml`).

2. **Plugin cần cài đặt**:
   - `n8n-nodes-tallyforms` (để kết nối với Tally Forms).
   - `@n8n/n8n-nodes-langchain` (để sử dụng AI RAG, embeddings, vector store).
   - `n8n-nodes-base.gmail` (để gửi email draft).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### 1. **Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/11369) hoặc copy toàn bộ JSON từ trang này.
- Trong **n8n Editor**, chọn **Import Workflow** và dán JSON vào.
- **Không cần chỉnh sửa** các node có màu xám (đã được cấu hình sẵn).

#### 2. **Các lưu ý BẮT BUỘC phải chỉnh 📌**
##### **A. Cấu hình Tally Trigger**
- Mở node **"Tally Trigger"** → Chọn **credentials** của form Tally Forms.
- **Kiểm tra lại mapping field** trong node **"Data Cleaner"** (chi tiết ở phần sau).

##### **B. Cấu hình Supabase Vector Store**
1. **Chạy script SQL**:
   - Trong **Template Description** của workflow, copy script SQL và chạy trong **Supabase SQL Editor**.
   - Script này tạo bảng `user_requests` để lưu trữ **embeddings** và thông tin người dùng.
   ```sql
   -- Dữ liệu mẫu trong Template Description (copy và chạy)
   CREATE TABLE IF NOT EXISTS user_requests (
     id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
     user_name TEXT,
     user_email TEXT,
     original_text TEXT,
     embedding vector(768),
     created_at TIMESTAMPTZ DEFAULT NOW()
   );
   ```
2. **Cập nhật URL Supabase**:
   - Mở node **"HTTP Request - Supabase Search"** → Thay đổi **URL** thành:
     ```
     https://<your-project-ref>.supabase.co/rest/v1/user_requests
     ```
     (Thay `<your-project-ref>` bằng ref của project Supabase).

##### **C. Cấu hình Data Cleaner (Mapping Field)**
- Mở node **"Data Cleaner"** → Chỉnh sửa **JavaScript code** để mapping đúng field từ Tally Forms:
  ```javascript
  // Ví dụ: Mapping field từ Tally Forms
  $input.all().forEach((item) => {
    item.user_name = item.Name;       // Field "Name" trong Tally → user_name
    item.user_email = item.Email;     // Field "Email" trong Tally → user_email
    item.original_text = item.Request; // Field "Request" trong Tally → original_text
  });
  ```
  - **Lưu ý**: Đảm bảo tên field trong Tally Forms **khớp với code trên**.

##### **D. Cấu hình Embeddings & AI Agent**
1. **Embeddings OpenAI/Ollama**:
   - Node **"Embeddings OpenAI"** → Điền **API Key** của OpenAI (nếu dùng) hoặc cấu hình Ollama.
   - Model mặc định: `nomic-embed-text:latest` (hoặc `text-embedding-ada-002` của OpenAI).
2. **AI Agent - Draft text maker**:
   - Node **"OpenAI Chat Model3"** → Chọn model `command-r7b` (hoặc model tương đương).
   - **Prompt** đã được cấu hình sẵn để viết email cá nhân hóa.

##### **E. Cấu hình Trigger**
- **RSS Feed Trigger**:
  - Mở node **"RSS Feed Trigger"** → Điền URL RSS của blog/changelog.
  - **Lưu ý**: Nếu không muốn dùng RSS, có thể **tắt node này** và chỉ dùng **Manual Trigger**.
- **Manual Trigger**:
  - Mở node **"When clicking ‘Execute workflow’"** → Điền **mô tả tính năng mới** vào field `Lunch description` (ví dụ: "Tính năng chatbot tự động hóa hỗ trợ khách hàng").

##### **F. Cấu hình Gmail**
- Mở node **"Create Draft"** → Chọn **credentials Gmail OAuth 2.0** đã tạo trước.
- **Email From**: Đảm bảo là email chính thức của doanh nghiệp.

#### 3. **Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Execute"** trên node **"When clicking ‘Execute workflow’"** (Manual Trigger).
   - Nhập mô tả tính năng mới vào `Lunch description` (ví dụ: "Tính năng backup tự động").
   - Kiểm tra **Gmail Drafts** để xem email đã được tạo chưa.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram Webhook** sau node **"Done!"** để thông báo khi email draft được tạo thành công.
   ```javascript
   // Ví dụ: Thêm node Slack Webhook
   $node.set("message", `📩 Email draft đã được tạo cho ${item.user_name} (${item.user_email})!`);
   $node.set("channel", "#automation-alerts");
   ```

2. **Lưu log vào Google Sheets**:
   - Thêm node **Google Sheets** sau node **"Done!"** để ghi lại lịch sử thông báo:
   ```javascript
   // Ví dụ: Ghi log vào Google Sheets
   $node.set("sheetName", "Feature_Notifications");
   $node.set("row", {
     "Date": new Date().toISOString(),
     "User": item.user_name,
     "Email": item.user_email,
     "Feature": item.feature_description,
     "Status": "Draft Created"
   });
   ```

3. **Tự động gửi email sau 24h**:
   - Thêm node **Set** sau **"Create Draft"** để lưu ID draft, rồi sử dụng node **Gmail Send** sau 24h bằng **Scheduled Trigger**:
   ```javascript
   // Ví dụ: Lưu ID draft vào biến
   $node.set("draftId", $node.input.all()[0].id);
   ```

4. **Tối ưu vector search**:
   - Nếu lượng dữ liệu lớn, có thể **tăng độ chính xác** bằng cách:
     - Sử dụng model embedding mạnh hơn (ví dụ: `text-embedding-ada-002` của OpenAI).
     - Thêm **filter** trong query Supabase để loại bỏ yêu cầu cũ hơn 1 năm.

5. **Duy trì dữ liệu**:
   - Thêm **Scheduled Trigger** hàng tuần để **xóa yêu cầu cũ** (trên 1 năm) khỏi Supabase:
   ```sql
   DELETE FROM user_requests WHERE created_at < NOW() - INTERVAL '1 year';
   ```

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để các sếp:
✅ **Tự động hóa** quá trình tìm kiếm và thông báo tính năng mới.
✅ **Cá nhân hóa email** với khách hàng, tăng trải nghiệm và giảm tỷ lệ rời bỏ.
✅ **Tăng doanh thu** từ upsell khi khách hàng nhận thấy yêu cầu cũ của họ đã được thực hiện.

**Hành động ngay**:
1. **Import workflow** và cấu hình theo hướng dẫn trên.
2. **Test với mô tả tính năng mới** trong `Lunch description`.
3. **Kiểm tra Gmail Drafts** sau khi chạy để xem kết quả!

**Nếu gặp vấn đề**, hãy để lại comment dưới đây hoặc liên hệ với tác giả **Ehsan** qua [n8n Community](https://community.n8n.io/). Chúc các sếp thành công! 🚀

---
:::note[Lưu ý quan trọng]
- **Không gửi email tự động**: Workflow chỉ tạo **draft**, các sếp cần **review và gửi** trước khi khách hàng nhận được.
- **Chi phí**: Sử dụng OpenAI có thể tốn kém. Để giảm chi phí, có thể thử **Ollama** (cài đặt local) cho embeddings.
- **Mở rộng**: Có thể kết hợp với **HubSpot/CRM khác** để tự động cập nhật thông tin khách hàng.
:::

---
**Bạn đã sẵn sàng tự động hóa CRM của mình chưa?** 😉