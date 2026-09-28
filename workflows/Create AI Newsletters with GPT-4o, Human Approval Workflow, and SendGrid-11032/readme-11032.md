---
title: "🚀 Tự Động Hóa Tạo & Phát Tín Điện Thông Tin AI (GPT-4o) Với Phê Duyệt Con Người & Gửi qua SendGrid – Không Cần Code!"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp tạo tin tức/email marketing bằng AI GPT-4o, phê duyệt thủ công qua email, và gửi đến danh sách người nhận tự động. Tiết kiệm 80% thời gian so với cách làm thủ công!"
slug: "tay-dong-hoa-tao-tin-dien-thong-tin-ai-gpt-4o-phan-duyet-con-nguoi"
tags: [n8n, automation, email marketing, ai-gpt-4o, sendgrid, google-sheets, no-code]
keywords: [tự động hóa tin tức email, gpt-4o tạo nội dung, phê duyệt tin tức tự động, sendgrid n8n, workflow ai marketing]
---

# 🚀 **Tự Động Hóa Tạo & Phát Tín Điện Thông Tin AI (GPT-4o) Với Phê Duyệt Con Người – Không Cần Code!**

Hết sức phiền phức phải không, các sếp? Mỗi tuần phải viết, chỉnh sửa, phê duyệt và gửi tin tức/email marketing cho khách hàng? Thời gian bị "ăn" mất trong việc:
- **Tìm ý tưởng** cho nội dung.
- **Chỉnh sửa** để phù hợp với từng nhóm đối tượng.
- **Phê duyệt** từ đồng nghiệp hoặc bản thân.
- **Gửi** đến hàng trăm người nhận.

**Workflow này giải quyết tất cả!** Sử dụng **AI GPT-4o** để tự động tạo **tin tức/email marketing** từ một form đơn giản, sau đó **phê duyệt thủ công** qua email và **gửi tự động** đến danh sách người nhận. **Không cần viết code, không cần kỹ thuật!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất tối ưu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian** so với cách làm thủ công (từ viết đến gửi).
✅ **Nội dung chuyên nghiệp** được AI GPT-4o tối ưu hóa cho từng đối tượng.
✅ **Phê duyệt linh hoạt** qua email, không phụ thuộc vào thời gian làm việc.
✅ **Gửi tự động** đến danh sách người nhận, không lo quên.
✅ **Lưu lịch sử** tất cả tin tức trên Google Sheets để theo dõi.
✅ **Cá nhân hóa** nội dung dựa trên input từ form.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** (API Key) để sử dụng **GPT-4o**.
2. **Tài khoản Google Cloud** (để sử dụng **Google Sheets** và **Gmail**).
3. **Tài khoản SendGrid** (để gửi email marketing).
4. **n8n Self-hosted** (để chạy workflow 24/7).
5. **Danh sách email** của người nhận (cần nhập vào **Workflow Configuration**).

---
:::note[CHUẨN BỊ CÁC THAM SỐ CẦN THIẾT]
- **Google Sheets**:
  - Tạo một bảng với các cột: `topic`, `target`, `sender`, `admin_email`.
  - Cung cấp **Document ID** và **Sheet Name** trong node **Store Form Responses**.
- **Gmail**:
  - Cần **OAuth 2.0** để gửi email phê duyệt.
- **SendGrid**:
  - **Email From** phải được xác thực trong tài khoản SendGrid.
- **OpenAI**:
  - API Key được lưu trong **credentials** với tên `openAiApi`.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Mở **n8n Editor** trên trang web hoặc VPS.
2. Nhấn **Import Workflow** và chọn file JSON (hoặc paste JSON).
3. **Không cần chỉnh sửa** nếu đã có tất cả credentials và tham số.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Dưới đây là **các node quan trọng** cần cấu hình kỹ lưỡng:

##### **🔹 Node 1: Newsletter Input Form (formTrigger)**
- **Cấu hình**:
  - Thêm các trường input như:
    - `topic` (chủ đề tin tức).
    - `target` (đối tượng mục tiêu).
    - `sender` (người gửi).
    - `admin_email` (email để phê duyệt).
  - **URL Form**: Sau khi cấu hình, URL này sẽ được sử dụng để gửi dữ liệu vào workflow.

##### **🔹 Node 2: Workflow Configuration (set)**
- **Cấu hình**:
  - Thay thế danh sách email người nhận bằng **danh sách email của bạn** (cách nhau bằng dấu phẩy).
  - Ví dụ: `nguyen@doanhnghiep.com,le@marketing.com,trung@tech.vn`.

##### **🔹 Node 3: Store Form Responses (googleSheets)**
- **Cấu hình**:
  - **Document ID**: Lấy từ liên kết Google Sheets (ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
  - **Sheet Name**: Tên sheet muốn lưu dữ liệu (ví dụ: `Newsletter_Logs`).
  - **Operation**: Đặt là `appendOrUpdate` để thêm hoặc cập nhật dữ liệu.

##### **🔹 Node 4: Generate Newsletter Content (agent)**
- **Cấu hình**:
  - **Prompt AI**: Workflow đã cấu hình sẵn, nhưng các sếp có thể chỉnh sửa **system message** trong node này để thay đổi **tone** (chuyên nghiệp, thân thiện, hài hước...).
  - **Input**: Dữ liệu từ form (topic, target, sender).

##### **🔹 Node 5: OpenAI GPT-4o Model (lmChatOpenAi)**
- **Cấu hình**:
  - **Credentials**: Chọn `openAiApi` (đã cấu hình trước).
  - **Model**: Đặt là `gpt-4o` (hoặc thay đổi nếu muốn dùng model khác).

##### **🔹 Node 6: JSON Output Parser (outputParserStructured)**
- **Cấu hình**:
  - Workflow tự động phân tích output từ AI thành **JSON** để chuyển đổi sang Markdown.

##### **🔹 Node 7: Convert Markdown to HTML (markdown)**
- **Cấu hình**:
  - Node này tự động chuyển đổi nội dung Markdown thành **HTML** để gửi qua SendGrid.

##### **🔹 Node 8: Send Approval Email (gmail)**
- **Cấu hình**:
  - **Credentials**: Chọn `gmailOAuth2`.
  - **Email To**: Đặt là `{{ $json["admin_email"] }}` (email từ form).
  - **Subject**: "Review Request: Your Newsletter Draft".
  - **Body**: Nội dung email bao gồm **preview tin tức** và **link phê duyệt**.

##### **🔹 Node 9: Wait for Approval (wait)**
- **Cấu hình**:
  - Thời gian chờ mặc định là **1 ngày**, nhưng các sếp có thể điều chỉnh.
  - Sau khi **click link phê duyệt**, workflow sẽ tiếp tục.

##### **🔹 Node 10: Send Newsletter to Subscribers (sendGrid)**
- **Cấu hình**:
  - **Credentials**: Cung cấp API Key SendGrid.
  - **From Email**: Đặt là email đã xác thực trong SendGrid.
  - **To**: Danh sách email từ **Workflow Configuration**.
  - **Subject & Body**: Lấy từ output của node **Convert Markdown to HTML**.

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** và điền dữ liệu vào form.
   - Kiểm tra email phê duyệt và **click link** để hoàn tất.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Slack/Telegram Notifications**:
   - Sử dụng node **Slack** hoặc **Telegram** để thông báo khi tin tức được phê duyệt.
2. **Lưu Log Chi tiết**:
   - Thêm node **Sticky Note** để ghi lại lịch sử phê duyệt và thời gian gửi.
3. **Gửi Báo cáo Định Kỳ**:
   - Sử dụng node **Google Sheets** hoặc **Airtable** để tự động cập nhật thống kê gửi email.
4. **Thay đổi AI Model**:
   - Thay **GPT-4o** bằng **Claude (Anthropic)** hoặc **local LLM** nếu muốn tiết kiệm chi phí.
5. **Tự động Xóa Email Sau Gửi**:
   - Thêm node **Gmail** để xóa email phê duyệt sau khi hoàn tất.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa toàn bộ quy trình tạo và gửi tin tức/email marketing** mà không cần viết code. **Tiết kiệm thời gian, tăng hiệu suất, và đảm bảo nội dung luôn chuyên nghiệp!**

**Hãy thử ngay và giảm bớt gánh nặng công việc hàng ngày!** 🚀

---
**🔗 [Tải workflow gốc từ n8n.io](https://n8n.io/workflows/11032)** (để tham khảo chi tiết)