---
title: "🤖 Tự Động Trích Xuất Dữ Liệu Từ Đính Kèm Email Sang Airtable Với AI DocuPipe - Không Cần Code!"
description: "Giải pháp tự động hóa hoàn toàn trích xuất dữ liệu từ các tệp đính kèm email (hoá đơn, hợp đồng, giấy tờ pháp lý) bằng AI DocuPipe và lưu vào Airtable, tiết kiệm thời gian lên tới 80% cho bộ phận tài chính, hành chính và quản lý."
slug: "tieu-dung-danh-muc-tu-email-sang-airtable"
tags: [n8n, automation, no-code, ai-document-extraction, airtable, docupipe, imap-email]
keywords: [tự động hóa trích xuất dữ liệu email, docupipe n8n, lưu dữ liệu từ email sang airtable, tự động hóa tài chính hành chính, trích xuất hoá đơn từ email]
---

# 🚀 **Tự Động Trích Xuất Dữ Liệu Từ Đính Kèm Email Sang Airtable Với AI DocuPipe**

### **Giải pháp cho những ai đang mệt mỏi vì việc nhập liệu thủ công từ email?**
Hàng ngày, bộ phận tài chính, hành chính hoặc quản lý phải mất **giờ đồng hồ** để mở email, tải xuống tệp đính kèm (hoá đơn, hợp đồng, giấy tờ pháp lý), rồi nhập liệu vào Airtable hoặc Excel. **Sai sót, mất thời gian, và hiệu suất thấp** là những vấn đề thường gặp. **Workflow này sẽ thay đổi mọi thứ!**

Với **n8n + DocuPipe AI**, bạn có thể:
✅ **Tự động phát hiện** email mới có đính kèm (hoá đơn, hợp đồng, giấy tờ).
✅ **Trích xuất dữ liệu** từ các tệp PDF, Word, Excel **bằng AI** (không cần quy trình OCR phức tạp).
✅ **Lưu dữ liệu** vào Airtable với **cấu trúc sẵn sàng** cho báo cáo, phân tích hoặc tự động hóa tiếp theo.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này **chạy ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên **VPS riêng** thay vì dùng phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ xử lý nhanh cho DocuPipe AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm **80% thời gian nhập liệu thủ công** cho bộ phận tài chính, hành chính.
- **Chính xác 100%**: AI DocuPipe tự động trích xuất dữ liệu từ các tệp đính kèm, **không sai sót** như khi nhập thủ công.
- **Cá nhân hóa và tự động hóa**: Dữ liệu được **ghi nhãn tự động** (ví dụ: "Hoá đơn", "Hợp đồng", "Giấy tờ pháp lý") và lưu vào Airtable với **cấu trúc sẵn sàng**.
- **Hoạt động liên tục**: Workflow **chạy 24/7** mà không cần can thiệp, **không bỏ lỡ bất kỳ email nào**.
- **Kết nối với nhiều hệ thống**: Dữ liệu sau khi lưu vào Airtable có thể **kết nối với Slack, Notion, Google Sheets, hoặc các workflow tự động hóa khác**.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản email có IMAP** (Outlook, Gmail, Yahoo, hoặc email doanh nghiệp với IMAP).
✔ **Tài khoản DocuPipe AI** (đăng ký tại [docupipe.ai](https://docupipe.ai)).
✔ **API Key của DocuPipe** (tìm tại [app.docupipe.ai/settings/general](https://app.docupipe.ai/settings/general)).
✔ **Tài khoản Airtable** và **bảng dữ liệu (table)** đã cấu hình sẵn.
✔ **Schema trích xuất** trong DocuPipe (ví dụ: "Invoice", "Contract", "Legal Document").
✔ **Node DocuPipe cho n8n** (cần cài đặt từ [npmjs.com/package/n8n-nodes-docupipe](https://www.npmjs.com/package/n8n-nodes-docupipe)).

---
:::note[LƯU Ý QUAN TRỌNG]
- **Gmail không hỗ trợ IMAP** (nên dùng **Outlook, Yahoo, hoặc email doanh nghiệp**).
- **Airtable cần có cột với tên trùng khớp với schema DocuPipe** (ví dụ: nếu schema có `invoiceAmount`, Airtable phải có cột `invoiceAmount`).
- **DocuPipe có giới hạn miễn phí** (nên kiểm tra tài khoản trước khi sử dụng).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Bước 1: **Tải workflow** từ [n8n.io/workflows/14328](https://n8n.io/workflows/14328) hoặc copy JSON từ trang này.
Bước 2: **Mở n8n Editor** và chọn **"Import Workflow"** (hoặc **"Paste JSON"**).
Bước 3: **Chọn "Import"** và workflow sẽ xuất hiện trên canvas.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **2 phần chính**:
- **Phần 1: Upload email + trích xuất bằng DocuPipe** (IMAP → DocuPipe).
- **Phần 2: Nhận kết quả + lưu vào Airtable** (DocuPipe → Airtable).

##### **A. Cấu hình phần 1: Upload email và trích xuất**
1. **Node "New Email with Attachment" (IMAP)**
   - **Credentials**: Chọn **"imap"** (nếu chưa có, tạo mới tại **Settings > Credentials**).
   - **Điền thông tin IMAP**:
     - **Server**: `imap.outlook.com` (Outlook), `imap.mail.me.com` (Yahoo), hoặc server của nhà cung cấp email.
     - **Port**: `993` (IMAP SSL).
     - **Username & Password**: Tài khoản email và mật khẩu (nếu cần **App Password**, tạo tại [Microsoft Account Security](https://account.microsoft.com/devices/security)).
   - **Folder**: Chọn **Inbox** hoặc folder chứa email cần theo dõi.

2. **Node "Filter by Subject" (If)**
   - **Điền từ khóa lọc email** (ví dụ: `invoice`, `receipt`, `contract`, `legal`).
   - **Lưu ý**: Nếu không lọc, workflow sẽ xử lý **tất cả email có đính kèm**, có thể gây **tải quá tải DocuPipe**.

3. **Node "Upload Attachment & Extract Data" (DocuPipe)**
   - **Credentials**: Chọn **"docuPipeApi"** (nếu chưa có, tạo mới tại **Settings > Credentials** và điền **API Key** từ DocuPipe).
   - **Schema**: Chọn **schema trích xuất** đã cấu hình trong DocuPipe (ví dụ: "Invoice Extraction").
   - **Lưu ý**:
     - Nếu schema chưa có, tạo mới tại [DocuPipe Dashboard](https://app.docupipe.ai/schemas).
     - **Kích thước tệp đính kèm**: DocuPipe hỗ trợ **PDF, Word, Excel** (tối đa **50MB**).

4. **Node "Extraction Complete" (DocuPipeTrigger)**
   - **Credentials**: Chọn **"docuPipeApi"** (giống như trên).
   - **Lưu ý**: Node này **chờ kết quả từ DocuPipe** trước khi chuyển sang phần 2.

##### **B. Cấu hình phần 2: Nhận kết quả và lưu vào Airtable**
1. **Node "Get Extracted Data" (DocuPipe)**
   - **Credentials**: Chọn **"docuPipeApi"**.
   - **Lưu ý**: Node này **lấy dữ liệu đã trích xuất** từ DocuPipe.

2. **Node "Process for Airtable" (Code)**
   - **Mã JavaScript mặc định** đã xử lý **nested objects và arrays** thành dạng phù hợp với Airtable.
   - **Lưu ý**:
     - Nếu Airtable có **cấu trúc phức tạp**, có thể cần **sửa mã** để trùng khớp với schema.
     - Ví dụ: Nếu DocuPipe trích xuất `invoice.items`, Airtable cần có **cột "items"** với kiểu **Array**.

3. **Node "Add Metadata" (Set)**
   - **Thêm metadata** như:
     - `emailSubject` (tiêu đề email).
     - `emailFrom` (người gửi).
     - `extractionDate` (ngày trích xuất).
   - **Lưu ý**: Metadata này sẽ **hiển thị trong Airtable** để dễ theo dõi nguồn gốc dữ liệu.

4. **Node "Create Record in Airtable" (Airtable)**
   - **Credentials**: Chọn **"airtableTokenApi"** (nếu chưa có, tạo mới tại **Settings > Credentials** và điền **API Key** từ Airtable).
   - **Base & Table**: Chọn **bảng dữ liệu (table)** đã cấu hình.
   - **Lưu ý**:
     - **Tên cột trong Airtable phải trùng khớp** với **schema DocuPipe**.
     - Nếu Airtable có **cột kiểu "Relation"**, cần **định nghĩa mối quan hệ** trước khi lưu.

#### **3. Kích hoạt ⚡️**
1. **Test Run** với **email mẫu**:
   - Gửi **email có đính kèm** (ví dụ: hoá đơn PDF) và kiểm tra **log** trong n8n.
   - Nếu có **lỗi**, kiểm tra:
     - **IMAP credentials** có đúng không?
     - **DocuPipe API Key** có hiệu lực không?
     - **Schema DocuPipe** có phù hợp không?
2. **Bật Active workflow**:
   - Chọn **"Active"** trên canvas và **lưu lại**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết nối với Slack/Telegram để báo cáo**
   - Thêm **node Slack/Telegram** sau khi lưu vào Airtable để **báo cáo tự động** khi có dữ liệu mới.
   - Ví dụ: `"New invoice extracted! Subject: [Subject] - Amount: [Amount]"`.
   - **Cách làm**:
     ```json
     {
       "node": "slack",
       "type": "n8n-nodes-base.slack",
       "credentials": {
         "slackApiToken": "your_slack_token"
       },
       "parameters": {
         "text": "📄 New extraction complete!\n**Subject:** {{$node["Extract Email Info"].json["emailSubject"]}}\n**Amount:** {{$node["Get Extracted Data"].json["invoiceAmount"]}}"
       }
     }
     ```

2. **Lưu log vào Google Sheets**
   - Thêm **node Google Sheets** để **ghi lại lịch sử trích xuất**.
   - **Cách làm**:
     - Tạo **bảng mới** trong Google Sheets với cột: `Date`, `Email Subject`, `Extraction Status`, `Error (if any)`.
     - Sử dụng **node Google Sheets (Write Row)** sau khi lưu vào Airtable.

3. **Tự động gửi báo cáo định kỳ**
   - Sử dụng **node n8n-nodes-base.schedule** để **chạy workflow hàng ngày/tuần** để **tổng hợp báo cáo**.
   - **Cách làm**:
     - Tạo **workflow mới** với **node Schedule** (chọn thời gian chạy).
     - Sử dụng **node Airtable API** để **tính tổng hợp** (ví dụ: tổng doanh thu, số lượng hợp đồng).
     - Gửi **báo cáo qua email** bằng **node Email**.

4. **Sử dụng DocuPipe với nhiều schema khác nhau**
   - Nếu cần **trích xuất nhiều loại tệp** (ví dụ: hoá đơn, hợp đồng, giấy tờ pháp lý), tạo **schema riêng** trong DocuPipe và **chuyển đổi logic** trong **node Code**.
   - **Cách làm**:
     ```javascript
     // Trong node "Process for Airtable" (Code)
     if (jsonNode.extractionType === "invoice") {
       return { fields: { invoiceAmount: jsonNode.invoiceAmount } };
     } else if (jsonNode.extractionType === "contract") {
       return { fields: { contractSignDate: jsonNode.contractSignDate } };
     }
     ```

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc **nhập liệu thủ công**, đồng thời **giảm sai sót** và **tăng hiệu suất** cho bộ phận tài chính, hành chính. **Chỉ cần 30 phút cấu hình**, bạn đã có một **hệ thống tự động hóa hoàn chỉnh** từ email đến Airtable.

**Bắt đầu ngay!**
1. **Import workflow** và **cấu hình IMAP, DocuPipe, Airtable**.
2. **Test với email mẫu** và **bật Active**.
3. **Tận hưởng thời gian tự do** mà không cần nhập liệu nữa!

---
**🚀 Cần hỗ trợ thêm?**
- **Trang hỗ trợ n8n**: [docs.n8n.io](https://docs.n8n.io/)
- **Community DocuPipe**: [docupipe.ai/community](https://docupipe.ai/community)
- **Hỏi đáp nhanh**: [n8n.io/community](https://n8n.io/community)