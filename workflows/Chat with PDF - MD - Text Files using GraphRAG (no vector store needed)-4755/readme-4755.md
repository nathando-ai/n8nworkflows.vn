---
title: "🤖 Tự Động Hóa Chat Trực Tuyến Với Tài Liệu PDF, MD & Text Bằng GraphRAG (Không Cần Vector Store)"
description: "Tự động hóa việc xây dựng và truy vấn cơ sở tri thức từ tài liệu PDF, Markdown và text bằng công nghệ GraphRAG của InfraNodus, giúp các sếp tiết kiệm thời gian và nâng cao hiệu quả tìm kiếm thông tin. Workflow này không yêu cầu kiến thức code và hoạt động liên tục 24/7."
slug: "tieu-dong-hoa-chat-voi-ta-lieu-pdf-md-text-bang-graphrag"
tags: [n8n, automation, ai, graphrag, no-code, knowledge-base]
keywords: [n8n workflow chat pdf, tự động hóa chat với tài liệu, graphrag không cần vector store, n8n ai agent, tự động hóa tri thức doanh nghiệp]
---

# 🚀 Tự Động Hóa Chat Trực Tuyến Với Tài Liệu PDF, MD & Text Bằng GraphRAG (Không Cần Vector Store)

### 🔍 Nỗi Đau Của Các Sếp
Các sếp thường phải mất nhiều thời gian để tìm kiếm thông tin trong các tài liệu PDF, Markdown hoặc text phân tán trên Google Drive. Thông thường, việc này yêu cầu:
- Tìm kiếm thủ công trên từng tài liệu.
- Sử dụng công cụ vector store phức tạp và đắt tiền.
- Không thể kết nối các tài liệu một cách logic để hiểu toàn cảnh.

**Giải pháp này** tự động hóa việc xây dựng một **cơ sở tri thức thông minh** từ tài liệu của các sếp, cho phép chat trực tiếp với nội dung như một người trợ lý AI thông minh, **không cần kiến thức code** và hoạt động liên tục 24/7.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định và không bị gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết Quả Các Sếp Nhận Được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tìm kiếm thủ công trên từng tài liệu.
- **Truy vấn thông minh**: Chat trực tiếp với tài liệu như một người trợ lý AI.
- **Hiểu toàn cảnh**: GraphRAG giúp hiểu mối quan hệ giữa các khái niệm trong tài liệu.
- **Hoạt động liên tục**: Workflow tự động hóa và không cần can thiệp thủ công.
- **Không cần kiến thức code**: Sử dụng công nghệ no-code của n8n.
:::

---

### 🔧 Yêu Cầu Cần Thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (để lưu trữ tài liệu PDF, MD, text).
2. **Tài khoản InfraNodus** (để xây dựng và truy vấn GraphRAG):
   - [Đăng ký tài khoản](https://infranodus.com) và lấy **API Key** tại [đây](https://infranodus.com/api-access).
   - Chọn **tên Graph** (ví dụ: `tri-thuc-doanh-nghiep`) để lưu trữ tài liệu.
3. **API Key OpenAI** (để sử dụng mô hình AI chat):
   - Lấy tại [OpenAI API](https://platform.openai.com/api-keys).
4. **Tài liệu PDF, Markdown hoặc text** trên Google Drive (để tự động hóa việc upload).
:::

---

### 🚀 Cách Import & Lưu Ý Khi "Lên Đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập vào tài khoản.
2. Nhấp vào **"Create Workflow"** và chọn **"Import Workflow"**.
3. Chọn file JSON hoặc copy/paste JSON từ [link gốc](https://n8n.io/workflows/4755) vào ô nhập liệu.
4. Nhấp **"Import"** để hoàn tất.

#### 2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌
Sau khi import, các sếp cần cấu hình các node quan trọng như sau:

##### **Step 1: Upload Tài Liệu Vào GraphRAG**
- **Node "Search Google Drive"**:
  - Chọn **credentials**: `googleDriveOAuth2Api` (đã cấu hình trước khi import).
  - Điền **folder ID** của Google Drive chứa tài liệu (PDF, MD, text).
  - **Lưu ý**: Folder này phải được chia sẻ với tài khoản n8n (nếu sử dụng OAuth2).

- **Node "Loop Over Items"**:
  - Node này tự động lặp qua từng file trong folder đã chọn.

- **Node "Retrieve File"**:
  - Sử dụng cùng **credentials** `googleDriveOAuth2Api`.
  - Node này sẽ tải xuống từng file từ Google Drive.

- **Node "Switch"**:
  - Chọn **condition** để phân loại file (PDF, MD, text) và chuyển đến node tương ứng:
    - **PDF** → "Extract from PDF".
    - **Markdown** → "Extract from Markdown".
    - **Text** → "Extract from Text File".

- **Node "Extract from PDF" / "Extract from Markdown" / "Extract from Text File"**:
  - Node này tự động trích xuất nội dung từ file.
  - **Lưu ý**: Nếu muốn chất lượng trích xuất cao hơn cho PDF, các sếp có thể sử dụng **ConvertAPI** (xem phần **Mẹo & Gợi Ý Nâng Cao**).

- **Node "InfraNodus Save to Graph"**:
  - Chọn **credentials**: `httpBearerAuth` (điền **API Key InfraNodus**).
  - Điền **tên Graph** (ví dụ: `tri-thuc-doanh-nghiep`) vào trường `graphName`.
  - **Lưu ý**: Đảm bảo tên Graph này khớp với tên đã đăng ký trên [InfraNodus](https://infranodus.com).

- **Node "Convert File to PDF" (nếu sử dụng ConvertAPI)**:
  - Chỉnh sửa **URL API** và **API Key** của ConvertAPI (nếu muốn nâng cao chất lượng trích xuất từ PDF).

##### **Step 2: Chat Với Tài Liệu**
- **Node "When chat message received"**:
  - Node này sẽ kích hoạt khi có yêu cầu chat từ người dùng (có thể kết nối với Slack, Telegram hoặc webhook).
  - **Lưu ý**: Các sếp có thể bật/tắt node này tùy thuộc vào việc muốn sử dụng chức năng chat hay không.

- **Node "AI Agent"**:
  - Node này sẽ quản lý logic chat và gọi đến **OpenAI Chat Model**.

- **Node "OpenAI Chat Model"**:
  - Chọn **credentials**: `openAiApi` (điền **API Key OpenAI**).
  - Chọn mô hình: `gpt-4o-mini` (hoặc mô hình khác nếu muốn).

- **Node "Simple Memory"**:
  - Node này lưu trữ lịch sử chat để AI có thể tham khảo trong các lần tương tác sau.

- **Node "Knowledge Base GraphRAG"**:
  - Chọn **credentials**: `httpBearerAuth` (điền **API Key InfraNodus**).
  - Điền **tên Graph** (khớp với Step 1) vào trường `graphName`.
  - **Lưu ý**: Nếu có nhiều Graph, các sếp cần mô tả rõ ràng trong **Project Notes** của InfraNodus để AI biết truy vấn Graph nào.

#### 3. Kích Hoạt ⚡️
1. **Test Run**:
   - Nhấp **"Run Workflow"** và chọn **node "Click ‘Test workflow’ to ingest the documents"** để tải tài liệu lên GraphRAG.
   - Kiểm tra kết quả trên [InfraNodus](https://infranodus.com/your_user_name/your_graph_name/edit).

2. **Bật Active Workflow**:
   - Sau khi test thành công, các sếp có thể bật **node "When chat message received"** để kích hoạt chức năng chat.
   - **Lưu ý**: Đảm bảo các node quan trọng như `googleDriveOAuth2Api`, `openAiApi` và `httpBearerAuth` đã được cấu hình đúng.

---

### ✍️ Mẹo & Gợi Ý Nâng Cao
1. **Sử Dụng ConvertAPI Để Chất Lượng Trích Xuất Cao Hơn**:
   - Thay thế node **"Map PDF to Text"** bằng node **"Convert File to PDF"** (nếu đã cấu hình ConvertAPI).
   - ConvertAPI sẽ trích xuất nội dung PDF một cách chính xác hơn, giữ nguyên cấu trúc và đoạn văn bản.

2. **Kết Nối Với Slack/Telegram**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để người dùng có thể chat với tài liệu qua kênh này.
   - Cấu hình **webhook** từ Slack/Telegram vào node **"When chat message received"**.

3. **Lưu Log Hoạt Động**:
   - Sử dụng node **Google Sheets** hoặc **Airtable** để lưu lịch sử chat và truy vấn.
   - Có thể kết nối với node **"Simple Memory"** để lưu trữ dữ liệu chat.

4. **Tạo Báo Cáo Định Kỳ**:
   - Sử dụng node **Google Drive** hoặc **Email** để gửi báo cáo tổng hợp về hoạt động chat hàng tuần/tháng.
   - Ví dụ: Báo cáo số lượng truy vấn, chủ đề phổ biến, tài liệu được tham khảo nhiều nhất.

5. **Tối Ưu Hóa Mô Hình AI**:
   - Thử nghiệm với các mô hình OpenAI khác như `gpt-4` hoặc `gpt-4-turbo` nếu muốn chất lượng chat cao hơn.
   - Cấu hình **temperature** và **max_tokens** trong node **"OpenAI Chat Model"** để điều chỉnh độ chính xác và sáng tạo của AI.

---

### 📌 Kết Luận
Workflow này giúp các sếp **tự động hóa việc xây dựng và truy vấn cơ sở tri thức** từ tài liệu PDF, Markdown và text một cách **mạnh mẽ và thông minh**, không cần kiến thức code. Bằng cách kết hợp **GraphRAG của InfraNodus** và **AI Agent của n8n**, các sếp có thể:
✅ **Tiết kiệm thời gian** tìm kiếm thông tin.
✅ **Hiểu toàn cảnh** từ tài liệu thông qua mạng lưới mối quan hệ.
✅ **Chat trực tiếp** với tài liệu như một người trợ lý AI thông minh.

**Hãy áp dụng ngay workflow này và nâng cao hiệu quả làm việc của doanh nghiệp!** 🚀

---