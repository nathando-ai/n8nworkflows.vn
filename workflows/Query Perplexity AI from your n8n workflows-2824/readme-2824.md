---
title: "🤖 Query Perplexity AI Tự Động Trong n8n: Tiết Kiệm Thời Gian & Tăng Cường Tính Năng AI Cho Workflow"
description: "Hướng dẫn chi tiết cách tích hợp API Perplexity AI vào n8n để tự động hóa việc truy vấn thông tin, phân tích dữ liệu và xây dựng ứng dụng AI không cần code. Giúp các sếp tiết kiệm thời gian lên tới 80% trong công việc liên quan đến AI."
slug: "query-perplexity-ai-trong-n8n"
tags: [n8n, automation, ai-automation, perplexity-ai, no-code-ai]
keywords: [n8n query perplexity, tự động hóa ai với n8n, api perplexity trong n8n, xây dựng ứng dụng ai không code, tiết kiệm thời gian với ai]
---

# 🚀 Query Perplexity AI Tự Động Trong n8n: Giải Pháp AI Cho Người Không Code

Bạn đã bao giờ cảm thấy mệt mỏi khi phải tra cứu thông tin, phân tích dữ liệu hoặc xây dựng ứng dụng AI mà không có kiến thức lập trình? Hay thậm chí phải mất nhiều giờ để tìm kiếm thông tin từ nhiều nguồn khác nhau? **Workflow này sẽ giúp bạn tự động hóa toàn bộ quá trình đó chỉ với một cú nhấp chuột!**

Với **Perplexity AI** - một trong những mô hình AI tiên tiến nhất hiện nay, kết hợp với **n8n**, bạn có thể xây dựng các ứng dụng AI mạnh mẽ mà không cần viết một dòng code nào. Workflow này sẽ cho phép bạn **truy vấn Perplexity AI từ bên trong n8n**, lấy kết quả và xử lý tiếp theo một cách tự động hóa hoàn toàn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Thay vì phải tra cứu thủ công, workflow sẽ tự động lấy kết quả từ Perplexity AI chỉ trong giây lát.
- **Tính chính xác cao**: Sử dụng mô hình AI tiên tiến của Perplexity để phân tích và trả về thông tin chính xác nhất.
- **Tự động hóa hoàn toàn**: Kết hợp với các node khác trong n8n để xử lý tiếp kết quả (ví dụ: gửi email, lưu vào Google Sheets, hoặc gửi thông báo Slack).
- **Không cần code**: Thiết lập và chạy workflow chỉ với một số bước đơn giản, phù hợp cho người không có kiến thức lập trình.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Perplexity AI**:
   - Đăng ký và mua **credits** trên [Perplexity Dashboard](https://www.perplexity.ai/settings/api).
   - Tạo **API Key** để sử dụng trong workflow.
2. **n8n Workflow Editor**:
   - Tài khoản n8n (cả phiên bản Cloud lẫn Self-hosted đều được).
3. **Thông tin API Key**:
   - API Key của Perplexity (được tạo từ bước 1).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Bước 1: **Tải workflow từ nguồn gốc**
- Truy cập [link workflow gốc](https://n8n.io/workflows/2824) và nhấp vào nút **"Export"** để tải file JSON về máy.
- Hoặc copy toàn bộ JSON từ trang này và lưu vào file `perplexity-query.json`.

Bước 2: **Import vào n8n Editor**
- Mở **n8n Workflow Editor** và nhấp vào **"Import"** ở góc trên bên phải.
- Chọn file JSON vừa tải hoặc dán toàn bộ nội dung JSON vào ô **"Paste JSON"** và nhấp **"Import"**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần **cấu hình các node quan trọng** như sau:

##### **Node 1: Manual Trigger (Kích hoạt thủ công)**
- Đây là node để **bắt đầu workflow** khi bạn nhấp vào nút **"Test workflow"**.
- **Không cần chỉnh sửa gì** ở node này.

##### **Node 2: Set Params (Đặt tham số)**
- Node này **không cần chỉnh sửa** vì nó sẽ tự động truyền dữ liệu cho node tiếp theo.

##### **Node 3: Clean Output (Làm sạch kết quả)**
- Node này **không cần chỉnh sửa** vì nó sẽ chuẩn hóa kết quả từ Perplexity AI trước khi truyền tiếp.

##### **Node 4: Perplexity Request (Gửi yêu cầu API)**
⚠️ **Đây là node quan trọng nhất!** Các sếp cần cấu hình như sau:
1. **Chọn loại Authentification**:
   - Trong node **Perplexity Request**, nhấp vào **"Credentials"** và chọn **"Generic Credentials"**.
   - Sau đó chọn **"Header Auth"**.

2. **Thêm Header Authorization**:
   - Nhấp vào **"Add"** trong phần **Headers**.
   - Điền:
     - **Name**: `Authorization`
     - **Value**: `Bearer pplx-YOUR_API_KEY_HERE` (thay `YOUR_API_KEY_HERE` bằng API Key của bạn từ Perplexity).

3. **Cấu hình URL và Method**:
   - Trong phần **URL**, điền:
     ```
     https://api.perplexity.ai/chat/completions
     ```
   - Chọn **Method**: `POST`.

4. **Thêm Body Request (Nội dung yêu cầu API)**:
   - Trong phần **Body**, chọn **"Raw"** và điền JSON sau (có thể tùy chỉnh prompt):
     ```json
     {
       "model": "sonar-pro",
       "messages": [
         {
           "role": "user",
           "content": "$json.query"
         }
       ]
     }
     ```
   - `$json.query` là biến động để truyền **prompt** từ node trước (Set Params). Nếu muốn truyền prompt cố định, thay thế bằng nội dung cụ thể (ví dụ: `"Tôi muốn biết về công nghệ AI hiện nay"`).

5. **Thêm biến động cho Prompt (Tùy chọn)**:
   - Nếu muốn truyền **prompt động** từ một node khác (ví dụ: từ một form hoặc webhook), hãy đảm bảo node **Set Params** truyền biến `$json.query` với nội dung prompt.

#### 3. Kích hoạt ⚡️
- **Test Run**:
  - Nhấp vào nút **"Test workflow"** để kích hoạt node **Manual Trigger**.
  - Nhập **prompt** vào node **Set Params** (nếu cần) và nhấp **"Execute"**.
  - Kiểm tra kết quả từ node **Perplexity Request** để đảm bảo API trả về dữ liệu chính xác.

- **Bật Active**:
  - Sau khi test thành công, nhấp vào nút **"Active"** ở góc trên bên phải để workflow chạy tự động.

---

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram để thông báo kết quả**:
   - Sau khi lấy kết quả từ Perplexity, bạn có thể gửi thông báo tự động đến Slack hoặc Telegram bằng node **Slack Webhook** hoặc **Telegram Bot**.

2. **Lưu kết quả vào Google Sheets/Notion**:
   - Sử dụng node **Google Sheets** hoặc **Notion API** để lưu lịch sử truy vấn và kết quả.

3. **Tự động hóa theo lịch trình**:
   - Sử dụng node **Schedule Trigger** để chạy workflow định kỳ (ví dụ: mỗi ngày để cập nhật tin tức từ AI).

4. **Tích hợp với các API khác**:
   - Sau khi lấy kết quả từ Perplexity, bạn có thể xử lý tiếp bằng các API khác như **Google Search, Wikipedia, hoặc API nội bộ** để enrich dữ liệu.

5. **Sử dụng mô hình AI khác**:
   - Nếu muốn thay đổi mô hình AI (khác với `sonar-pro`), tham khảo [đây](https://docs.perplexity.ai/guides/model-cards) và thay đổi giá trị `model` trong body request.

---

### 📌 Kết luận
Với workflow này, các sếp đã có thể **tự động hóa việc truy vấn Perplexity AI trong n8n một cách dễ dàng**, tiết kiệm thời gian và nâng cao hiệu suất công việc. Đây là bước đầu tiên để xây dựng các ứng dụng AI mạnh mẽ mà không cần viết code!

🚀 **Hãy áp dụng ngay và khám phá thế giới tự động hóa AI với n8n!**
Nếu có bất kỳ câu hỏi nào, hãy để lại comment bên dưới hoặc tham gia **Skool Community** của Emmanuel Bernard để học thêm về AI Automation: [Skool Community](https://skool.com/emmanuelbernard).

---