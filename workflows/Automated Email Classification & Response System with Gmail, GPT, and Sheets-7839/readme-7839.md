---
title: "🤖 Hệ Thống Tự Động Phân Loại & Trả Lời Email Gmail Với AI (GPT-4 + Google Sheets) - Tiết Kiệm 100% Thời Gian Quản Lý Email"
description: "Workflow tự động hóa phân loại email Gmail thành 5 loại: Hỗ trợ, Kinh doanh, Khiếu nại, Thông tin và Khác, tự động gắn nhãn và tạo bản nháp trả lời thông minh bằng GPT-4.1-mini. Giúp các sếp quản lý email hiệu quả hơn 50% thời gian, giảm thiểu sai sót và cá nhân hóa tương tác với khách hàng."
slug: "automated-email-classification-gmail-gpt-sheets"
tags: [n8n, automation, gmail, ai, openai, google-sheets, no-code, email-management, workflow]
keywords: [tự động hóa email gmail, phân loại email với ai, gpt-4 tự động trả lời email, google sheets log email, n8n workflow gmail, tự động hóa hỗ trợ khách hàng]
---

# 🚀 **Hệ Thống Tự Động Phân Loại & Trả Lời Email Gmail Với AI (GPT-4 + Google Sheets)**

## **📩 Nỗi Đau Của Các Sếp Với Email Hàng Ngày**
Hàng ngày, các sếp phải:
- **Lọc và phân loại** hàng trăm email vào các danh mục khác nhau (hỗ trợ, kinh doanh, khiếu nại, thông tin...).
- **Trả lời từng email** một cách thủ công, mất thời gian và dễ bị bỏ quên.
- **Giám sát và lưu trữ** lịch sử tương tác để theo dõi khách hàng.
- **Đối mặt với rủi ro** khi nhầm lẫn giữa các loại email, dẫn đến phản hồi không phù hợp.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Phân loại tự động** email thành **5 loại chính** (Hỗ trợ, Kinh doanh, Khiếu nại, Thông tin, Khác) với độ chính xác cao.
✅ **Tạo bản nháp trả lời thông minh** bằng **GPT-4.1-mini** cho các loại email **Hỗ trợ** và **Kinh doanh**.
✅ **Gắn nhãn tự động** cho email theo loại, giúp dễ dàng quản lý và tìm kiếm sau này.
✅ **Lưu log toàn bộ quá trình** vào **Google Sheets**, bao gồm nội dung email gốc, quyết định phân loại và bản nháp trả lời.
✅ **Báo lỗi tự động** nếu workflow gặp sự cố, giúp các sếp kiểm soát và khắc phục kịp thời.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng thay vì dùng phiên bản miễn phí (Community).
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 50%+ thời gian** quản lý email hàng ngày.
- **Chính xác 95%+** trong phân loại email nhờ AI.
- **Trả lời email cá nhân hóa** với nội dung phù hợp, tăng trải nghiệm khách hàng.
- **Lưu trữ và theo dõi** toàn bộ lịch sử tương tác trong Google Sheets.
- **Không cần viết code** – chỉ cần cấu hình và chạy.
- **Hoạt động liên tục** 24/7, không phụ thuộc vào nhân viên.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (để kết nối với Gmail và tạo nhãn tự động).
2. **API Key OpenAI** (để sử dụng GPT-4.1-mini tạo bản nháp trả lời).
3. **Google Sheets** với **2 bảng tính**:
   - **Logs**: Để lưu trữ email gốc, quyết định phân loại và bản nháp trả lời.
   - **Errors**: Để ghi lại lỗi nếu workflow gặp sự cố.
4. **Danh sách nhãn Gmail** (các sếp cần tạo trước trong Gmail):
   - `compliants` (Khiếu nại)
   - `info` (Thông tin)
   - `other` (Khác)
   - `support` (Hỗ trợ)
   - `sales` (Kinh doanh)

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7839](https://n8n.io/workflows/7839) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import** → Dán JSON và nhấn **Import**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **23 node**, nhưng các node quan trọng nhất cần cấu hình kỹ như sau:

##### **A. Cấu Hình Gmail (Triggers & Actions)**
- **Gmail Trigger**:
  - Chọn **credentials**: `gmailOAuth2` (cần tạo trước trong n8n).
  - Thiết lập **interval**: 1 phút (để kiểm tra email mới).
- **Add Labels (compliants, info, other, support, sales)**:
  - Chọn **credentials**: `gmailOAuth2`.
  - Đảm bảo các nhãn đã được tạo trong Gmail trước khi chạy.

##### **B. Cấu Hình AI (OpenAI)**
- **OpenAI Chat Model (gpt-4.1-mini)**:
  - Chọn **credentials**: `openAiApi` (cần tạo trước trong n8n).
  - **Prompt mẫu** (các sếp có thể tùy chỉnh):
    ```json
    "You are an email assistant. For a {category} email, generate a professional and polite response. Keep it concise and relevant."
    ```
- **Message a model (Support/Sales)**:
  - Chọn **credentials**: `openAiApi`.
  - Đảm bảo **input** từ node **Text Classifier** truyền đúng loại email.

##### **C. Cấu Hình Google Sheets**
- **Google Sheets (Logs & Errors)**:
  - Chọn **credentials**: `googleSheetsOAuth2Api`.
  - **Điền chính xác**:
    - `documentId`: ID của file Google Sheets (tìm trong liên kết chia sẻ).
    - `sheetName`: Tên của bảng tính (`Logs` hoặc `Errors`).
  - **Cấu trúc bảng Logs** (các sếp cần tạo trước):
    | Original Email | Decision | Output Email |
    |----------------|----------|--------------|
    | (JSON email)   | (loại)   | (nội dung trả lời) |
  - **Cấu trúc bảng Errors** (các sếp cần tạo trước):
    | Node with Error | Error Message | Time | Execution ID | Workflow ID |
    |-----------------|--------------|------|-------------|-------------|

##### **D. Cấu Hình Set & Decision Nodes**
- Các node **Set 1, Set 2, Set 3, Set 4** được sử dụng để **lưu trữ dữ liệu tạm** giữa các bước.
- Các node **Add label to thread** và **Create draft** sẽ hoạt động dựa trên **kết quả phân loại** từ **Text Classifier**.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi một email mẫu vào Gmail (ví dụ: email hỗ trợ hoặc kinh doanh).
  - Kiểm tra:
    - Email có được **phân loại chính xác** không?
    - Bản nháp trả lời có được **tạo thành công** không?
    - Log có được **ghi vào Google Sheets** không?
- **Bật Active**:
  - Sau khi test thành công, chuyển workflow từ **Draft** sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tùy chỉnh Prompt cho AI**:
   - Các sếp có thể **điều chỉnh prompt** trong node `OpenAI Chat Model` để phù hợp với **ngôn ngữ doanh nghiệp** của mình.
   - Ví dụ: Thêm **tên công ty**, **tôn chỉ phục vụ khách hàng**, hoặc **các từ khóa cụ thể**.

2. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack/Telegram** để **báo cáo tự động** khi có email mới hoặc lỗi xảy ra.
   - Cấu hình trong node **Webhook** hoặc **Slack API**.

3. **Lưu Log Chi Tiết Hơn**:
   - Thêm cột **`Customer ID`** hoặc **`Ticket ID`** vào bảng `Logs` để theo dõi khách hàng dễ dàng hơn.

4. **Tự Động Gửi Email Trả Lời**:
   - Sau khi tạo bản nháp, các sếp có thể thêm node **Gmail Send Email** để **gửi tự động** thay vì chỉ tạo draft.

5. **Phân Loại Nâng Cao**:
   - Nếu workflow phân loại sai, các sếp có thể **tùy chỉnh mô hình Text Classifier** bằng cách:
     - Thêm **ví dụ phân loại** vào node `TextClassifier`.
     - Sử dụng **các label khác** nếu cần phân loại chi tiết hơn.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa quản lý email**, **tiết kiệm thời gian** và **cải thiện trải nghiệm khách hàng**. Với **AI GPT-4.1-mini** và **Google Sheets**, hệ thống không chỉ phân loại email mà còn **tạo bản nháp trả lời thông minh** và **lưu trữ lịch sử** một cách tự động.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với email mẫu** để đảm bảo hoạt động chính xác.
3. **Bật Active** và bắt đầu tự động hóa email của mình!

**🚀 Cảm ơn các sếp đã lựa chọn n8n!** Nếu có bất kỳ câu hỏi hoặc gặp khó khăn, hãy để lại bình luận dưới đây. Chúc các sếp thành công! 🎉