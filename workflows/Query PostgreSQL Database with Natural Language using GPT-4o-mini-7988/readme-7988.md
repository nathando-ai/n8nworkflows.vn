---
title: "🔍 Tự Động Hỏi Đáp Câu Hỏi Tự Nhiên với PostgreSQL bằng GPT-4o-mini (Không Cần Code)"
description: "Hướng dẫn xây dựng một agent AI tự động chuyển đổi câu hỏi tiếng Việt thành truy vấn SQL và trả kết quả từ PostgreSQL, tiết kiệm 90% thời gian phân tích dữ liệu thủ công cho các sếp."
slug: "tự-dộng-hỏi-dáp-postgresql-gpt-4o-mini"
tags: [n8n, automation, ai-chatbot, postgresql, gpt-4o-mini, langchain]
keywords: [n8n workflow postgresql, tự động hóa hỏi đáp cơ sở dữ liệu, gpt-4o-mini tự động hóa, agent ai cho doanh nghiệp, truy vấn sql tự động]
---

# 🔍 **Tự Động Hỏi Đáp PostgreSQL bằng Câu Hỏi Tiếng Việt với GPT-4o-mini**

### **Giải pháp cho các sếp bị "chìm" trong dữ liệu PostgreSQL**
Hãy tưởng tượng: Bạn không cần phải viết một dòng SQL nào cả, chỉ cần nói *"Hãy cho tôi danh sách khách hàng mua sản phẩm X trong tháng 12"* là hệ thống tự động:
✅ **Chuyển câu hỏi thành truy vấn SQL chính xác**
✅ **Trả kết quả từ PostgreSQL dưới dạng bảng hoặc văn bản**
✅ **Lưu lịch sử câu hỏi để AI "hiểu" ngữ cảnh**

Workflow này **giải phóng 90% thời gian** của các sếp khỏi công việc phân tích dữ liệu thủ công, đồng thời **giảm thiểu lỗi** do truy vấn SQL sai.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 với hiệu suất tối ưu, các sếp nên **self-host** n8n trên VPS:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
*Lưu ý: Dùng VPS có RAM ≥4GB để chạy GPT-4o-mini ổn định.*
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần viết SQL thủ công, giảm 90% công việc phân tích dữ liệu.
- **Chính xác 100%**: AI tự động chuyển đổi câu hỏi thành truy vấn SQL chính xác.
- **Hoạt động liên tục**: Workflow chạy 24/7 trên VPS, không phụ thuộc vào người dùng.
- **Tích hợp AI hiện đại**: Sử dụng **GPT-4o-mini** (OpenAI) để hiểu ngữ cảnh câu hỏi.
- **Lưu lịch sử**: AI nhớ các câu hỏi trước để trả lời logic hơn.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản n8n**:
   - Self-hosted (khuyến nghị) hoặc n8n.cloud (miễn phí cho thử nghiệm).
2. **PostgreSQL Database**:
   - Một cơ sở dữ liệu PostgreSQL có **thuộc tính read access** (không cần write).
   - Đảm bảo người dùng có quyền **SELECT** trên các bảng mục tiêu.
3. **OpenAI API Key**:
   - [Tạo API Key tại OpenAI](https://platform.openai.com/account/api-keys) (miễn phí cho 500k token/month).
4. **Bảng mục tiêu**:
   - Workflow mặc định sử dụng `"table_name"` (các sếp phải thay đổi theo bảng thực tế).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1: Import từ JSON**
  1. Tải file JSON từ [n8n.io/workflows/7988](https://n8n.io/workflows/7988).
  2. Trong n8n Editor, nhấn **Import** → Chọn file JSON → Nhấn **Import**.
- **Cách 2: Copy/Paste JSON**
  1. Mở n8n Editor → Nhấn **Create new workflow** → Chọn **Import from JSON**.
  2. Dán JSON từ [n8n.io/workflows/7988](https://n8n.io/workflows/7988) → Nhấn **Import**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **7 node** quan trọng, các sếp phải cấu hình như sau:

##### **A. Thiết lập Credentials (BẮT BUỘC)**
1. **OpenAI API Key**:
   - Trong n8n Editor, nhấn **Credentials** (góc trên bên phải) → **Add Credential** → Chọn **OpenAI**.
   - Nhập **API Key** từ OpenAI (đã tạo ở trên).
   - **Lưu ý**: Node `lmChatOpenAi` sẽ tự động lấy key này.

2. **PostgreSQL Connection**:
   - Tạo **một credential mới** cho PostgreSQL:
     - **Host**: `localhost` (nếu self-host) hoặc IP VPS.
     - **Port**: `5432` (mặc định).
     - **Database**: Tên cơ sở dữ liệu của bạn.
     - **User**: Tên người dùng có quyền **SELECT**.
     - **Password**: Mật khẩu của người dùng.
   - **Lưu ý**: Node `postgresTool` sẽ tự động lấy credential này.

##### **B. Cấu hình Table Name**
- Mở node **"Set Table Name"** (node thứ 2).
- Thay đổi giá trị `"table_name"` thành **tên bảng thực tế** của bạn (ví dụ: `"customers"`).
- **Lưu ý**: Workflow sẽ tự động lấy định nghĩa của bảng này để AI hiểu cấu trúc.

##### **C. Kích hoạt Agent AI**
- Node **"Database Agent"** (node thứ 7) là **cốt lõi** của workflow.
- Các sếp không cần chỉnh sửa node này, chỉ cần **bật Active** sau khi cấu hình xong.

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** (icon play) để kiểm tra.
   - Gửi câu hỏi mẫu như:
     - *"Hãy cho tôi danh sách khách hàng có status 'active'".*
     - *"Tìm số lượng đơn hàng trong tháng 12/2023".*
   - Kiểm tra kết quả trả về từ node `postgresTool`.

2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÂNG CAO]
1. **Tích hợp với Slack/Telegram**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để người dùng gửi câu hỏi qua chat.
   - Cấu hình **webhook** để nhận tin nhắn và truyền vào node `chatTrigger`.

2. **Lưu lịch sử câu hỏi**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu tất cả câu hỏi và kết quả.
   - Cấu hình node `memoryBufferWindow` để AI nhớ các câu hỏi trước.

3. **Cập nhật định nghĩa bảng tự động**:
   - Thêm một **cron job** (node `schedule`) để định kỳ lấy lại định nghĩa bảng (ví dụ: hàng tuần).

4. **Sử dụng LLM khác**:
   - Thay đổi node `lmChatOpenAi` thành **Mistral AI** hoặc **Anthropic Claude** nếu muốn tiết kiệm chi phí.

5. **Báo cáo định kỳ**:
   - Tạo một workflow riêng để gửi **báo cáo tổng hợp** (ví dụ: "5 câu hỏi phổ biến nhất trong tuần") qua email.
:::

---

### 📌 **Kết luận**
Workflow này **giải phóng các sếp khỏi công việc phân tích dữ liệu thủ công**, đồng thời **tăng cường hiệu suất** với AI hiện đại. Bằng cách tự động chuyển đổi câu hỏi tiếng Việt thành SQL và trả kết quả chính xác, nó **giúp doanh nghiệp làm việc thông minh hơn, không chỉ nhanh hơn**.

**Hành động ngay**:
1. **Import workflow** từ [n8n.io/workflows/7988](https://n8n.io/workflows/7988).
2. **Cấu hình PostgreSQL + OpenAI API Key**.
3. **Thay đổi tên bảng** và **bật Active**.
4. **Test với câu hỏi thực tế** và **tích hợp vào hệ thống**.

*Chúc các sếp thành công với tự động hóa AI!* 🚀