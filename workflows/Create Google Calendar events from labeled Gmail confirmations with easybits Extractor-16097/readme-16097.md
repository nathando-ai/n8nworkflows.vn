---
title: "🚀 Tự Động Hóa Sáng Lập Lịch Google Từ Email Xác Nhận: Khắc Phục Nỗi Đau Quên Lịch Hẹn & Làm Thủ Công"
description: "Workflow này tự động chuyển đổi tất cả email xác nhận (đặt vé máy bay, đặt khách sạn, đặt bàn ăn, khám bệnh, giao hàng...) thành sự kiện trên Google Calendar với đầy đủ thông tin chi tiết. Giúp các sếp tiết kiệm 10+ giờ/tháng và không bao giờ bỏ lỡ lịch hẹn quan trọng."
slug: "tu-dong-hoa-sang-lap-lich-google-tu-email-xac-nhan"
tags: [n8n, automation, no-code, google-calendar, gmail, easybits-extractor, ai-summarization]
keywords: [n8n workflow tự động hóa, tự động hóa email thành lịch Google, tự động hóa đặt vé máy bay, tự động hóa đặt khách sạn, tự động hóa lịch hẹn, easybits extractor n8n]
---

# 🚀 **Tự Động Hóa Sáng Lập Lịch Google Từ Email Xác Nhận: Giải Pháp 100% Không Code**

## **Nỗi Đau Thực Tế Của Các Sếp**
Bạn có bao giờ:
- **Quên lịch hẹn quan trọng** vì phải tra cứu email xác nhận giữa hàng trăm tin nhắn?
- **Phải nhập thủ công** thông tin đặt vé máy bay, đặt khách sạn, đặt bàn ăn vào Google Calendar?
- **Mất thời gian** để đọc email, copy-paste thông tin vào lịch, và lo sợ có lỗi nháp?
- **Bị trùng lịch** vì không kiểm tra kỹ ngày giờ khi nhập thủ công?

Workflow này **giải quyết tất cả** những vấn đề trên bằng cách **tự động chuyển đổi email xác nhận thành sự kiện trên Google Calendar** với đầy đủ thông tin chi tiết (ngày giờ, địa điểm, mã xác nhận, người tham dự...). **Không cần viết code, không cần kỹ thuật!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng**: Không phải nhập thủ công lịch hẹn nữa.
- **Không bao giờ quên lịch**: Tự động chuyển đổi email thành sự kiện ngay lập tức.
- **Chính xác 100%**: Trích xuất thông tin từ email và tài liệu đính kèm (PDF, hình ảnh).
- **Lịch riêng biệt**: Tất cả sự kiện tự động được thêm vào **Google Calendar "Auto-imported"** để dễ quản lý.
- **Xử lý tự động email không phải sự kiện**: Email không xác nhận (quảng cáo, tin nhắn rác) sẽ được **bỏ qua** và được nhắc nhở kiểm tra.
- **Hoạt động liên tục 24/7**: Workflow chạy tự động mỗi khi có email mới được nhãn `Events`.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** (Gmail + Google Calendar).
2. **Tài khoản easybits Extractor** ([đăng ký tại đây](https://extractor.easybits.tech/)).
3. **Email mẫu** (đặt vé máy bay, đặt khách sạn, đặt bàn ăn...) để tạo **Pipeline Extractor**.
4. **Nhãn Gmail**:
   - `Events` (email cần tự động hóa).
   - `Events/Needs-Review` (email cần kiểm tra thủ công).
5. **Google Calendar** riêng biệt (ví dụ: `Auto-imported`).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/16097) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Editor** (trang chủ của workflow).
  2. Nhấn **Import** → Chọn file JSON hoặc dán JSON từ link trên.
  3. Chọn **Create Workflow**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **13 node** quan trọng. Dưới đây là hướng dẫn chi tiết để cấu hình:

##### **A. Cấu Hình Gmail Trigger**
- **Node**: `Gmail Trigger`
- **Cấu hình**:
  - Chọn **Label**: `Events` (nhãn email cần tự động hóa).
  - **Polling Interval**: 60 giây (kiểm tra email mỗi phút).
  - **Credentials**: Chọn tài khoản Gmail đã kết nối.

##### **B. Cấu Hình easybits Extractor**
- **Node**: `Extractor: Email Body` và `Extractor: Attachment`
- **Cấu hình**:
  1. **Tạo Pipeline Extractor**:
     - Đăng ký tại [extractor.easybits.tech](https://extractor.easybits.tech).
     - Tải lên **email mẫu** (PDF hoặc hình ảnh).
     - Chọn **Auto-Mapping** để hệ thống tự động trích xuất các trường sau:
       - `event_type` (loại sự kiện: bay, khách sạn, ăn uống...).
       - `title` (tiêu đề ngắn).
       - `start_datetime` (thời gian bắt đầu, định dạng ISO 8601).
       - `end_datetime` (thời gian kết thúc).
       - `location` (địa điểm).
       - `confirmation_number` (mã xác nhận).
       - `vendor` (công ty cung cấp dịch vụ).
       - `notes` (chi tiết bổ sung).
       - `participants` (người tham dự).
     - Lưu Pipeline và **copy Pipeline ID + API Key**.
  2. **Điền vào n8n**:
     - Trong node `Extractor: Email Body` và `Extractor: Attachment`, điền:
       - **Pipeline ID**: ID Pipeline từ easybits.
       - **API Key**: API Key từ easybits.
       - **Input Format**: `pdf` (nếu email có đính kèm PDF) hoặc `image` (nếu là hình ảnh).

##### **C. Cấu Hình Google Calendar**
- **Node**: `Calendar: Create Event`
- **Cấu hình**:
  - Chọn **Calendar**: `Auto-imported` (hoặc tên calendar đã tạo).
  - **Mapped Fields**:
    - **Summary** ← `title`.
    - **Start** ← `start_datetime` (định dạng ISO 8601, ví dụ: `2024-05-20T14:30:00+07:00`).
    - **End** ← `end_datetime` (nếu không có, sẽ tự động lấy từ `start_datetime`).
    - **Location** ← `location`.
    - **Description** ← **Set: Build Event Description** (sẽ tự động xây dựng từ các trường trích xuất).

##### **D. Cấu Hình Gmail Actions**
- **Node**: `Gmail: Remove Events Label` (xóa nhãn sau khi xử lý thành công).
- **Node**: `Gmail: Flag for Review` (đánh nhãn `Events/Needs-Review` nếu email không phải sự kiện).
- **Node**: `Gmail: Send Review Notification` (gửi email cảnh báo nếu cần kiểm tra thủ công).
  - **Cấu hình**:
    - **Send To**: Điền email của mình.
    - **Subject**: `Needs Review: Missing Fields in Email`.
    - **HTML Content**: Sử dụng template mặc định (n8n sẽ tự động xây dựng).

##### **E. Cấu Hình Code Nodes**
- **Node**: `Code: Email Body Preparation` (chuyển email thành PDF).
  - **Lưu ý**: Node này tự động xử lý, không cần chỉnh sửa.
- **Node**: `Code: Explode Attachments` (tách các file đính kèm thành các mục riêng).
  - **Filter**: Chỉ cho phép `application/pdf` và `image/*` (PDF và hình ảnh).
- **Node**: `Code: Merge Extractions` (ghép kết quả trích xuất từ email và đính kèm).
  - **Lưu ý**: Đính kèm có ưu tiên hơn nội dung email (nếu có).

##### **F. Cấu Hình If: Valid Event?**
- **Node**: `If: Valid Event?`
- **Cấu hình**:
  - **Condition**: `start_datetime` **and** `event_type` **không null**.
  - **True branch**: Tạo sự kiện trên Calendar.
  - **False branch**: Đánh nhãn `Events/Needs-Review` và gửi email cảnh báo.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Đánh nhãn một email mẫu với nhãn `Events`.
   - Chạy **Manual Execution** trong n8n để kiểm tra workflow.
   - Kiểm tra Google Calendar và Gmail xem có sự kiện được tạo hay không.
2. **Bật Active**:
   - Nhấn **Active** ở góc trên phải của n8n.
   - Workflow sẽ chạy tự động mỗi khi có email mới được nhãn `Events`.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tạo Nhãn Gmail Tự Động**:
   - Sử dụng **n8n + Gmail API** để tự động đánh nhãn `Events` cho email từ các địa chỉ cụ thể (ví dụ: `booking@airline.com`, `confirmation@hotel.com`).
2. **Lưu Log Xử Lý**:
   - Thêm node **Google Sheets** hoặc **Notion** để ghi lại lịch sử sự kiện đã tự động hóa.
3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n + Slack/Telegram** để báo cáo số lượng sự kiện đã tự động hóa hàng tuần.
4. **Tối Ưu Pipeline Extractor**:
   - Thêm **email mẫu mới** vào Pipeline để cải thiện độ chính xác trích xuất.
   - Sử dụng **field descriptions cụ thể** (ví dụ: `start_datetime: "Ngày và giờ bắt đầu của chuyến bay"`) để Extractor hiểu rõ hơn.
5. **Xử Lý Email Nhiều Đính Kèm**:
   - Nếu email có nhiều file đính kèm, node `Code: Explode Attachments` sẽ tự động xử lý từng file riêng biệt.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp khỏi việc nhập thủ công lịch hẹn và **giảm thiểu rủi ro quên lịch** nhờ tự động hóa hoàn toàn. **Không cần kỹ thuật, không cần code!**

**Bắt đầu ngay hôm nay**:
1. **Import workflow** từ link trên.
2. **Cấu hình Gmail, Google Calendar và easybits Extractor**.
3. **Đánh nhãn email xác nhận** với nhãn `Events`.
4. **Xem sự kiện tự động xuất hiện trên Google Calendar!**

👉 **Nếu có vấn đề**, hãy để lại comment dưới đây hoặc liên hệ Felix (tác giả) qua [n8n Community](https://community.n8n.io/). Chúc các sếp thành công! 🚀