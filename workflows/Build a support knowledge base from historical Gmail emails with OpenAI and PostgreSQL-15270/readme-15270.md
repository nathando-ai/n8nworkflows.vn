---
title: "🚀 Tự Động Xây Dựng Trang Triệu Tài Liệu Hỗ Trợ Từ Email Gmail Cũ Bằng AI (OpenAI) & PostgreSQL"
description: "Workflow này tự động chuyển đổi lịch sử email hỗ trợ Gmail thành cơ sở tri thức (KB) có cấu trúc, khả năng tìm kiếm bằng AI, giúp tăng cường chất lượng hỗ trợ khách hàng và tự động hóa quá trình tạo nội dung. Kết quả là một cơ sở tri thức AI-ready, sẵn sàng tích hợp với hệ thống tự động trả lời email."
slug: "tieu-dong-xay-dung-trang-tri-lieu-ho-tro-tu-email-gmail"
tags: [n8n, automation, ai-rag, knowledge-base, postgresql, openai, gmail, no-code]
keywords: [tự động hóa n8n, xây dựng cơ sở tri thức AI, email gmail tự động, openai gpt-4o-mini, postgresql pgvector, tự động hóa hỗ trợ khách hàng]
---

# 🚀 **Tự Động Xây Dựng Trang Triệu Tài Liệu Hỗ Trợ Từ Email Gmail Cũ Bằng AI (OpenAI) & PostgreSQL**

### **Giải quyết vấn đề gì?**
Các sếp đang mất hàng giờ mỗi tuần để:
- **Lọc và tổng hợp** lịch sử email hỗ trợ từ Gmail để tạo tài liệu tri thức (KB).
- **Tìm kiếm thủ công** câu trả lời cho khách hàng trong hàng ngàn email cũ.
- **Đảm bảo tính nhất quán** trong cách trả lời của đội hỗ trợ.

Workflow này **tự động hóa toàn bộ quá trình** bằng AI, chuyển đổi lịch sử email thành một **cơ sở tri thức có cấu trúc, khả năng tìm kiếm bằng AI**, giúp:
✅ **Tiết kiệm 80% thời gian** so với cách làm thủ công.
✅ **Tăng chất lượng hỗ trợ** với câu trả lời chính xác, dựa trên dữ liệu thực tế.
✅ **Tự động hóa trả lời email** bằng AI (sẵn sàng tích hợp với Workflow 2: AI Draft Generator).
✅ **Cập nhật liên tục** khi có email mới, không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo bảo mật và hiệu suất tối ưu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Cơ sở tri thức AI-ready**: Dữ liệu được cấu trúc thành Q&A, mẫu xử lý, và ví dụ thực tế, sẵn sàng cho tìm kiếm semantic.
- **Tự động loại bỏ trùng lặp**: Không cần lo lắng về email đã xử lý trùng lại.
- **Tích hợp với AI Draft Generator**: Workflow này là **cơ sở dữ liệu** cho Workflow 2, giúp AI tự động tạo bản nháp trả lời email giống với phong cách của đội hỗ trợ.
- **Tiết kiệm chi phí**: Không cần thuê thêm nhân viên tổng hợp tài liệu.
- **Cập nhật tự động**: Chỉ cần chạy workflow định kỳ (ví dụ: hàng tuần) để cập nhật KB mới.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (để fetch email hỗ trợ).
2. **API Key OpenAI** (để sử dụng GPT-4o-mini và text-embedding-3-small).
3. **PostgreSQL + pgvector** (để lưu trữ và tìm kiếm vector embeddings).
4. **Credentials OAuth2 cho Gmail** (cài đặt trong n8n).
5. **Thông tin cơ sở dữ liệu PostgreSQL**:
   - Host, Port, Database Name, Username, Password.
   - Bảng đã tồn tại: `kb_data`, `scenario_patterns`, `corrections`, `email_logs`.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/15270) hoặc copy toàn bộ JSON từ trang này.
- Trong **n8n Editor**, chọn **"Import"** → Chọn file JSON hoặc dán JSON vào ô **"Import Workflow"**.
- Click **"Import"** để workflow xuất hiện trên canvas.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **16 node** với các bước quan trọng sau. Các sếp cần chú ý cấu hình các node này:

##### **🔹 Node "Fetch Emails" (Gmail)**
- **Cấu hình**:
  - Chọn **credentials OAuth2** đã thiết lập cho Gmail.
  - Đặt `limit` ban đầu là **5 email** để test, sau đó tăng lên **50-100** cho bulk import.
  - **Lưu ý**: Workflow **bỏ qua email đã xử lý** (đã có trong `email_logs`).

##### **🔹 Node "Parse and Filter" (Code)**
- **Cần thay đổi**:
  - Thay thế `YOUR_DOMAIN` trong code bằng **domain của email hỗ trợ** (ví dụ: `@doanhnghiep.com`).
  - Code này **lọc bỏ**:
    - Email từ máy chủ tự động (SPAM).
    - Email không phải từ khách hàng (ví dụ: email nội bộ).
    - Email rỗng hoặc không có nội dung.

##### **🔹 Node "OpenAI Chat Model" (lmChatOpenAi)**
- **Cấu hình**:
  - Chọn mô hình: **gpt-4o-mini** (đã được cấu hình sẵn).
  - **Thêm API Key OpenAI** vào **credentials** của n8n.
  - **Lưu ý**: Node này **classify email thành JSON** với các trường:
    - `category` (danh mục hỗ trợ).
    - `qa_pair` (câu hỏi + trả lời).
    - `handling_pattern` (mẫu xử lý).
    - `sentiment` (tình trạng cảm xúc).
    - `confidence` (độ tin cậy, nếu < 0.7 → bỏ qua).

##### **🔹 Node "AI Extract KB Entries" (Agent)**
- **Cấu hình**:
  - **System Prompt** đã được tối ưu cho việc **tách email thành cấu trúc KB**.
  - **Lưu ý**: Node này **tạo embeddings** (vector 1536 chiều) để tìm kiếm semantic sau này.

##### **🔹 Node "Check Duplicate in DB" & "Check KB Duplicate" (PostgreSQL)**
- **Cấu hình**:
  - Đảm bảo **PostgreSQL + pgvector** đã cài đặt và hoạt động.
  - **Similarity Threshold**: Đặt ở mức **0.92** để tránh trùng lặp gần giống.
  - Query SQL đã được tối ưu để kiểm tra trùng lặp trong `kb_data` và `scenario_patterns`.

##### **🔹 Node "Process and Insert All" (Code)**
- **Cần kiểm tra**:
  - Code này **ghi dữ liệu vào 4 bảng**:
    1. `kb_data` (Q&A pair).
    2. `scenario_patterns` (mẫu xử lý).
    3. `corrections` (ví dụ thực tế).
    4. `email_logs` (đánh dấu email đã xử lý).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chọn **Manual Trigger** → Click **"Execute Workflow"**.
   - Kiểm tra **log** để đảm bảo không có lỗi.
   - **Kiểm tra PostgreSQL**: Đăng nhập vào DB để xác nhận dữ liệu đã được ghi vào `kb_data`, `scenario_patterns`, `corrections`.

2. **Bật Active**:
   - Sau khi test thành công, **bật Active** cho workflow.
   - **Lưu ý**: Workflow **an toàn để re-run** (đã có cơ chế tránh trùng lặp).

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram Webhook** sau **"Process and Insert All"** để thông báo khi workflow hoàn thành.

2. **Lưu log hoạt động**:
   - Sử dụng node **StickyNote** để ghi lại thời gian chạy, số email đã xử lý, và kết quả.

3. **Tự động chạy định kỳ**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow hàng tuần (ví dụ: `0 0 * * 1` để chạy mỗi thứ 2).

4. **Tối ưu AI Prompt**:
   - Nếu kết quả AI không tốt, **cập nhật System Prompt** trong node `AI Extract KB Entries` để phù hợp với phong cách hỗ trợ của doanh nghiệp.

5. **Xây dựng Workflow 2 (AI Draft Generator)**:
   - Dữ liệu từ `kb_data` và `corrections` sẽ được sử dụng để **tự động tạo bản nháp trả lời email** cho khách hàng mới.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** của các sếp khỏi công việc thủ công, đồng thời **tăng chất lượng hỗ trợ khách hàng** bằng cách tự động hóa quá trình xây dựng và cập nhật cơ sở tri thức. **Chỉ cần chạy 1 lần/tuần**, hệ thống sẽ tự động:
✔ Lọc email hỗ trợ.
✔ Tách và cấu trúc dữ liệu.
✔ Tránh trùng lặp.
✔ Lưu vào PostgreSQL sẵn sàng cho tìm kiếm AI.

**Hành động ngay hôm nay**:
1. **Import workflow** và cấu hình các node theo hướng dẫn.
2. **Test với 5 email** để đảm bảo hoạt động.
3. **Tăng limit lên 50-100** và chạy định kỳ.

**Kết quả?** Một **cơ sở tri thức AI-ready**, giúp đội hỗ trợ của các sếp **trả lời nhanh chóng và chính xác**, giống như có một "người trợ lý ảo" 24/7!

---
**🚀 Cần hỗ trợ thêm?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để chạy workflow ổn định và liên hệ với cộng đồng n8n để chia sẻ kinh nghiệm!