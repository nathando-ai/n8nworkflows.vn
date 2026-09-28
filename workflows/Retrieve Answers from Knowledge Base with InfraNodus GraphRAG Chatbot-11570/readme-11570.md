---
title: "🤖 Tự Động Hóa Chatbot Trí Tuệ Nhân Tạo với GraphRAG - Không Cần Vector Store"
description: "Tạo chatbot chuyên nghiệp trả lời câu hỏi từ cơ sở tri thức bằng công nghệ GraphRAG của InfraNodus, hoàn toàn tự động hóa và không cần code. Giúp doanh nghiệp tiết kiệm thời gian hỗ trợ khách hàng và cung cấp thông tin chính xác 24/7."
slug: "tự-dộng-hoa-chatbot-graphrag-infranodus"
tags: [n8n, automation, ai-chatbot, graph-rag, infranodus, no-code]
keywords: [n8n workflow chatbot, tự động hóa hỗ trợ khách hàng, graphrag chatbot, chatbot không cần vector store, tự động trả lời câu hỏi]
---

# 🚀 Chatbot Trí Tuệ Nhân Tạo với GraphRAG - Giải Pháp Hỗ Trợ Khách Hàng Tự Động Hóa

## 💡 Giới Thiệu
Hãy tưởng tượng một chatbot không chỉ trả lời câu hỏi của khách hàng mà còn **hiểu ngữ cảnh**, **liên kết thông tin** và **cung cấp câu trả lời chính xác** từ cơ sở tri thức của doanh nghiệp - **không cần bạn phải viết code hoặc cấu hình vector store phức tạp**. Đây chính là sức mạnh của **GraphRAG** kết hợp với n8n, và bạn đã có thể triển khai nó ngay hôm nay!

Workflow này sử dụng **InfraNodus GraphRAG**, một công nghệ tiên tiến phân tích mạng lưới kiến thức để tạo ra câu trả lời logic và liên kết, thay vì chỉ dựa vào các vector store truyền thống. Đặc biệt, nó phù hợp cho các doanh nghiệp cần hỗ trợ khách hàng **24/7** mà không tốn thời gian của nhân viên.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian hỗ trợ khách hàng**: Chatbot tự động trả lời câu hỏi thường gặp, giảm tải cho đội ngũ CSKH.
- **Câu trả lời chính xác và logic**: GraphRAG phân tích kiến thức dưới dạng mạng lưới, không chỉ trả lời đơn giản mà còn liên kết thông tin liên quan.
- **Không cần cấu hình phức tạp**: Không cần vector store hoặc model AI phức tạp, chỉ cần API key của InfraNodus.
- **Hoạt động liên tục 24/7**: Cung cấp hỗ trợ khách hàng mọi lúc, mọi nơi.
- **Dễ dàng mở rộng**: Kết hợp với Slack, Telegram, hoặc widget chat để tích hợp vào website.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản InfraNodus**:
   - [Đăng ký API key](https://infranodus.com/api-access) (miễn phí cho các dự án nhỏ).
   - [Tạo graph kiến thức](https://infranodus.com/docs/graph-rag-knowledge-graph) (cơ sở tri thức cho chatbot).
2. **Tài khoản n8n**:
   - N8n self-hosted (nên cài trên VPS để ổn định).
   - [Tài liệu cài đặt n8n](https://docs.n8n.io/hosting/installation/).
3. **Credentials cho n8n**:
   - Thêm **InfraNodus API key** vào n8n dưới **Credentials** (Settings > Credentials > Add New Credential).
   - Tên credential: `infranodusApi` (phải trùng với tên trong workflow).
4. **Widget Chat (tùy chọn)**:
   - [n8n Chat Widget](https://n8n-chat-widget.com/) để embed vào website.
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- **Tải workflow JSON**: Tải file JSON từ [n8n.io/workflows/11570](https://n8n.io/workflows/11570).
- **Import vào n8n Editor**:
  - Mở n8n Editor > Nhấn **Import** > Chọn file JSON vừa tải.
  - Hoặc **copy/paste** JSON vào **Import Workflow** (nút ở góc phải).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm **5 node chính**, các sếp cần chú ý cấu hình như sau:

##### **A. Cấu hình Webhook (Node "Webhook")**
- **Tên node**: `Webhook`
- **Lưu ý**:
  - Path mặc định là `eaff3dbc-70dd-4f57-9432-24f503b2852f` (không cần thay đổi).
  - Sau khi import, **không cần chỉnh sửa** node này trừ khi muốn thay đổi URL.

##### **B. Cấu hình InfraNodus (Node "Get a response from knowledge base")**
- **Tên node**: `Get a response from knowledge base`
- **Credentials**:
  - Chọn `infranodusApi` (đã thêm trước đó).
- **Key Parameters**:
  - `prompt`: `={{ $json.chatInput }}` (sử dụng input từ chat).
- **Lưu ý**:
  - **Thêm tên graph**: Trong node này, các sếp cần **thêm tham số `graphName`** (không có trong workflow gốc) với giá trị là **tên graph của bạn** (ví dụ: `company_knowledge`).
    - Cách thêm: Nhấn vào node > **Add Parameter** > Thêm `graphName` với type `String` và giá trị là tên graph.
  - **Test API**: Đảm bảo API key và graph đã được tạo đúng trên [InfraNodus](https://infranodus.com/).

##### **C. Cấu hình Chat Trigger (Node "When chat message received")**
- **Tên node**: `When chat message received`
- **Lưu ý**:
  - Đây là node test ban đầu. Sau khi hoàn thành, các sếp sẽ **thay thế bằng Webhook** (đã cấu hình ở trên).

##### **D. Cấu hình Trả Lời Chat (Node "Respond to Chat")**
- **Tên node**: `Respond to Chat`
- **Lưu ý**:
  - Node này sẽ trả lời người dùng dựa trên kết quả từ InfraNodus.
  - **Không cần chỉnh sửa** trừ khi muốn thay đổi format trả lời.

##### **E. Cấu hình Trả Lời Webhook (Node "Respond to Webhook")**
- **Tên node**: `Respond to Webhook`
- **Lưu ý**:
  - Node này sẽ **trả về kết quả** cho webhook (dùng khi embed vào website).

#### 3. Kích hoạt ⚡️
- **Test run dữ liệu mẫu**:
  - Gửi một câu hỏi test (ví dụ: *"Làm thế nào để sử dụng sản phẩm của chúng tôi?"*) qua **Chat Trigger** (node test).
  - Kiểm tra kết quả trả lời từ node `Get a response from knowledge base`.
- **Bật Active workflow**:
  - Sau khi test thành công, **disable** node `When chat message received` và `Respond to Chat` (node test).
  - **Active** node `Webhook` và `Respond to Webhook` để chatbot hoạt động với webhook.

---

### ✍️ Mẹo & gợi ý nâng cao
:::tip[CÁCH TIẾP CẬN THÊM SLACK/TELEGRAM]
- **Kết hợp với Slack/Telegram**:
  - Sử dụng node `n8n-nodes-slack` hoặc `n8n-nodes-telegram` để nhận tin nhắn từ Slack/Telegram và chuyển vào webhook.
  - Ví dụ: Tạo một **Slack App** và sử dụng node `Slack Webhook` để gửi tin nhắn vào workflow.
- **Lưu log hoạt động**:
  - Thêm node `n8n-nodes-base.terminate` sau node `Respond to Webhook` để lưu log vào Google Sheets hoặc Notion.
- **Gửi báo cáo định kỳ**:
  - Sử dụng node `n8n-nodes-base.schedule` để chạy workflow hàng ngày và gửi báo cáo tổng hợp về câu hỏi thường gặp.

:::note[CẤU HÌNH GRAPH TRÊN INFRANODUS]
- **Tạo graph hiệu quả**:
  - Đảm bảo graph chứa **kiến thức liên kết** (ví dụ: sản phẩm, FAQ, hướng dẫn) để GraphRAG phân tích logic.
  - Sử dụng [tutorial của InfraNodus](https://support.noduslabs.com/hc/en-us/articles/24079266183196-Building-Expert-Ontology-for-InfraNodus-GraphRAG-n8n-Expert-Node) để tối ưu graph.
- **Cập nhật liên tục**:
  - Khi cơ sở tri thức thay đổi, cập nhật graph trên InfraNodus để chatbot luôn có thông tin mới nhất.

---

### 📌 Kết luận
Chatbot GraphRAG với n8n là **giải pháp hoàn hảo** cho các doanh nghiệp muốn tự động hóa hỗ trợ khách hàng mà không cần đầu tư vào AI phức tạp. Với **không cần vector store**, **cấu hình đơn giản** và **câu trả lời logic**, workflow này giúp tiết kiệm thời gian, tăng trải nghiệm khách hàng và giảm tải cho đội ngũ CSKH.

**Bắt tay vào triển khai ngay!**
1. Tạo graph trên InfraNodus.
2. Import workflow và cấu hình credentials.
3. Test và deploy vào website hoặc ứng dụng của bạn.

Nếu có vấn đề, hãy tham khảo:
- [Tutorial video của InfraNodus](https://www.youtube.com/watch?v=qP4KTLBzoWQ)
- [Hỗ trợ n8n](https://docs.n8n.io/)
- [Hỗ trợ InfraNodus](https://support.noduslabs.com/)

**Chúc các sếp thành công!** 🚀