---
title: "🤖 **Tự Động Hóa Trợ Lý AI Tìm Kiếm Hàng Hóa Cứng Với Supabase Vector RAG & Google Gemini (N8n)**
"
description: "Workflow này nâng cấp trợ lý AI từ việc đọc đơn giản trên Google Sheets thành hệ thống tìm kiếm vector RAG siêu tốc, giúp tìm kiếm hàng ngàn sản phẩm trong kho với độ chính xác cao, ngay cả khi người dùng nhập sai hoặc dùng từ khác. Phù hợp cho doanh nghiệp có danh mục sản phẩm lớn (100+ sản phẩm) hoặc hỗ trợ khách hàng kỹ thuật."
slug: "tieu-dong-hoa-tro-ly-ai-tim-kiem-hang-hoa-cung-suabase-vector-rag-google-gemini"
tags: [n8n, automation, ai-rag, google-gemini, supabase, no-code, chatbot]
keywords: [n8n workflow tự động hóa, AI RAG với Supabase, tìm kiếm hàng hóa cứng, Google Gemini API, tự động hóa kho hàng, trợ lý AI cho doanh nghiệp]
---

# 🚀 **Trợ Lý AI Tìm Kiếm Hàng Hóa Cứng Siêu Tốc Với Supabase Vector RAG & Google Gemini**

## **Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải chịu những thách thức sau khi quản lý kho hàng thủ công:
- **Tốn thời gian**: Tìm kiếm sản phẩm trong danh sách hàng ngàn hàng hóa bằng cách scan từng dòng trên Google Sheets.
- **Độ chính xác thấp**: Người dùng thường nhập sai tên sản phẩm hoặc dùng từ khác (ví dụ: "CPU i7" thay vì "Intel Core i7-13700K").
- **Không thể mở rộng**: Hệ thống truyền thống không hỗ trợ tìm kiếm thông minh (semantic search) cho danh mục lớn.
- **Không tự động hóa**: Cần phải tương tác trực tiếp với nhân viên để tra cứu, làm chậm quá trình phục vụ khách hàng.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tìm kiếm siêu tốc** với Vector RAG (Retrieval-Augmented Generation) trên Supabase, giúp AI hiểu ngữ nghĩa và trả lời chính xác ngay cả khi người dùng nhập sai.
✅ **Tích hợp AI Google Gemini** để phân tích và trả lời các câu hỏi phức tạp về kho hàng.
✅ **Tự động hóa hoàn toàn** – không cần code, chỉ cần cấu hình và chạy 24/7.
✅ **Phù hợp cho doanh nghiệp** có danh mục sản phẩm lớn (100+ sản phẩm) hoặc hỗ trợ khách hàng kỹ thuật.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tìm kiếm siêu tốc**: AI trả lời trong giây chốc, ngay cả với danh mục hàng ngàn sản phẩm.
- **Độ chính xác cao**: Vector RAG giúp AI hiểu ngữ nghĩa, giảm thiểu lỗi do người dùng nhập sai.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công, tiết kiệm thời gian cho nhân viên.
- **Cá nhân hóa**: AI có thể trả lời theo phong cách riêng của doanh nghiệp (tone of voice).
- **Mở rộng dễ dàng**: Thêm sản phẩm mới chỉ cần cập nhật Google Sheets, không cần thay đổi hệ thống.
- **Hỗ trợ khách hàng 24/7**: Trợ lý AI có thể trả lời các câu hỏi kỹ thuật ngay cả khi cửa hàng đóng cửa.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** với danh sách sản phẩm (cấu trúc chi tiết sau).
2. **Tài khoản Supabase** (đã tạo bảng `documents` và hàm `match_documents` theo SQL trong hướng dẫn).
3. **API Key Google Gemini** (đăng ký tại [Google AI Studio](https://makersuite.google.com/)).
4. **Credentials trong n8n**:
   - `googleApi` (để truy cập Google Sheets).
   - `googlePalmApi` (để kết nối với Google Gemini).
   - `supabaseApi` (để kết nối với Supabase).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/13410](https://n8n.io/workflows/13410) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **2 phần chính**:
- **Path A (Sync Workflow)**: Chỉ chạy 1 lần để đồng bộ dữ liệu từ Google Sheets sang Supabase Vector Store.
- **Path B (Chat Workflow)**: Chạy liên tục để trả lời các câu hỏi từ người dùng.

##### **A. Cấu Hình Credentials**
| Node | Yêu cầu cấu hình |
|------|------------------|
| **Get row(s) in sheet** | Chọn `googleApi` (credentials đã tạo trước). Chỉnh `Sheet Name` và `Range` để trỏ đến bảng sản phẩm. |
| **Supabase Vector Store** | Chọn `supabaseApi`. Điền `Table Name` là `documents` và `Function Name` là `match_documents`. |
| **Embeddings Google Gemini** | Chọn `googlePalmApi`. Chọn model `embeddings-001`. |
| **Google Gemini** | Chọn `googlePalmApi`. Chọn model `gemini-1.0-pro`. |
| **Default Data Loader** | Không cần cấu hình thêm, chỉ cần chọn file Google Sheets chứa dữ liệu sản phẩm. |

##### **B. Cấu Hình Prompt (System Prompt)**
- Mở node **AI Agent** và chỉnh sửa **System Prompt** để phù hợp với doanh nghiệp:
  ```plaintext
  Bạn là trợ lý AI chuyên về sản phẩm hàng hóa cứng. Hãy trả lời các câu hỏi về danh mục sản phẩm của [Tên Doanh Nghiệp] một cách chính xác và chuyên nghiệp.

  Nếu người dùng hỏi về sản phẩm, hãy:
  1. Tìm kiếm thông tin từ kho dữ liệu trong Supabase Vector Store.
  2. Trả lời bằng cách liệt kê các sản phẩm phù hợp, bao gồm:
     - Tên sản phẩm
     - Mã sản phẩm (SKU)
     - Giá (nếu có)
     - Đặc điểm kỹ thuật (nếu có)
  3. Nếu không tìm thấy sản phẩm, hãy thông báo "Không tìm thấy sản phẩm phù hợp. Vui lòng kiểm tra lại tên sản phẩm."

  Nếu người dùng hỏi về giá hoặc trạng thái hàng, hãy tra cứu từ kho và trả lời ngay lập tức.
  ```
- **Lưu ý**: Customize **System Prompt** để phù hợp với tone of voice của doanh nghiệp (ví dụ: thân thiện, chuyên nghiệp, hoặc bán hàng).

##### **C. Chạy Path A (Sync Workflow) Để Đồng Bộ Dữ Liệu**
1. Chọn node **When clicking ‘Execute workflow’** và nhấn **Execute Workflow**.
2. Workflow sẽ tự động:
   - Lấy dữ liệu từ Google Sheets.
   - Chuyển đổi thành vector và lưu vào Supabase.
   - **Chỉ cần chạy 1 lần** (dữ liệu sẽ tự cập nhật khi bạn chỉnh sửa Google Sheets).

##### **D. Chạy Path B (Chat Workflow) Để Trả Lời Người Dùng**
1. Chọn node **When chat message received** và bật **Active**.
2. Test bằng cách gửi tin nhắn vào chat (ví dụ: "Hãy tìm cho tôi CPU i7 mới nhất").
3. AI sẽ trả lời dựa trên dữ liệu trong Supabase.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Gửi một câu hỏi mẫu như: *"Hãy liệt kê tất cả các máy tính xách tay có giá dưới 20 triệu"*.
   - Kiểm tra kết quả trả về có chính xác không.
2. **Bật Active**:
   - Chọn node **When chat message received** và bật **Active**.
   - Workflow sẽ hoạt động liên tục và trả lời tất cả các tin nhắn vào chat.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Với Slack/Telegram**:
   - Thêm node **Slack/Telegram Webhook** để nhận tin nhắn từ các kênh và trả lời tự động.
   - Cấu hình như sau:
     - Node **When chat message received** → **Set** → **Slack/Telegram Webhook** → **Send Message**.

2. **Lưu Log Tất Cả Các Câu Hỏi**:
   - Thêm node **Google Sheets** sau **AI Agent** để ghi lại tất cả các câu hỏi và trả lời vào một sheet riêng.
   - Cấu trúc sheet:
     ```
     | Thời gian | Người dùng | Câu hỏi | Trả lời |
     ```

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng node **Set Interval** để chạy định kỳ (ví dụ: hàng ngày) và gửi báo cáo về sản phẩm mới hoặc sản phẩm cạn kiệt.
   - Ví dụ: *"Có 5 sản phẩm trong kho dưới 50% số lượng. Vui lòng kiểm tra."*

4. **Cập Nhật Dữ Liệu Tự Động**:
   - Sử dụng node **HTTP Request** để kiểm tra Google Sheets mỗi ngày và chạy **Path A** tự động nếu có thay đổi.

5. **Optimize Prompt**:
   - Nếu AI trả lời không chính xác, hãy chỉnh sửa **System Prompt** để rõ ràng hơn về cách xử lý dữ liệu.

---

### 📌 **Kết Luận**
Workflow này không chỉ **tự động hóa tìm kiếm hàng hóa cứng** mà còn nâng cao **trải nghiệm khách hàng** bằng cách cung cấp trợ lý AI thông minh, trả lời nhanh chóng và chính xác. Đặc biệt phù hợp cho:
- **Doanh nghiệp bán hàng hóa cứng** (máy tính, điện thoại, linh kiện).
- **Cửa hàng kỹ thuật** cần hỗ trợ khách hàng nhanh chóng.
- **Công ty có danh mục sản phẩm lớn** (100+ sản phẩm).

**Hành động ngay**:
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và cấu hình credentials.
3. **Chạy Path A** để đồng bộ dữ liệu.
4. **Bật Path B** và test với các câu hỏi mẫu.

**Kết quả?** Một trợ lý AI **siêu tốc, chính xác và tự động hóa hoàn toàn** – giúp các sếp tiết kiệm thời gian và nâng cao hiệu suất kinh doanh!

---
**🔗 [Xem hướng dẫn chi tiết trên n8n.io](https://n8n.io/workflows/13410)**
**📖 [Đọc bài chi tiết về Vector RAG với Supabase](https://n8nplaybook.com/post/2026/02/scaling-n8n-inventory-ai-agent-supabase-vector-rag/)**