---
title: "💰 **Tự Động Hóa Theo Dõi Chi Phí Qua Telegram + easybits + Google Sheets (Không Cần Code!)**"
description: "Workflow tự động hóa hoàn toàn giúp các sếp tiết kiệm hàng giờ mỗi tháng theo dõi chi phí, trích xuất dữ liệu từ hóa đơn qua Telegram, và tự động cập nhật vào Google Sheets với định dạng chuyên nghiệp. Giảm thiểu sai sót, tăng độ chính xác và cá nhân hóa theo từng tháng."
slug: "tieu-dong-hoa-theo-doi-chi-phi-telegram-easybits-google-sheets"
tags: [n8n, automation, no-code, google-sheets, telegram-bot, expense-tracking, easybits]
keywords: [tự động hóa theo dõi chi phí, workflow n8n telegram, trích xuất hóa đơn tự động, google sheets api, bot quản lý chi tiêu]
---

# 🚀 **Tự Động Hóa Theo Dõi Chi Phí Hóa Đơn Qua Telegram – Không Cần Code!**

### **🔥 Nỗi Đau Của Các Sếp Và Giải Pháp Tự Động Hóa 100%**
Hàng tháng, các sếp phải:
- **Làm thủ công** trích xuất dữ liệu từ hàng chục hóa đơn, tờ giấy, hoặc ảnh chụp.
- **Nhập sai số** do phải gõ tay nhiều lần, dẫn đến báo cáo không chính xác.
- **Tốn thời gian** để phân loại chi phí theo tháng, loại chi phí, và người chi.
- **Quên hoặc bỏ sót** một số hóa đơn quan trọng, ảnh hưởng đến quyết định tài chính.

**Workflow này giải quyết tất cả!** Với chỉ một **câu lệnh Telegram**, bot sẽ:
✅ **Trích xuất tự động** thông tin từ hóa đơn (PDF/ảnh) qua API **easybits**.
✅ **Phân loại chi phí** theo ngày, nhà cung cấp, và loại chi (thuộc tính tùy chỉnh).
✅ **Cập nhật vào Google Sheets** với định dạng chuyên nghiệp (đậm, màu sắc, tự động tạo sheet mới mỗi tháng).
✅ **Xác nhận ngay** với người dùng thông qua Telegram, tránh sai sót.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-15 giờ/tháng** so với cách làm thủ công.
- **Giảm sai sót** đến **90%** nhờ trích xuất tự động và xác nhận tự động.
- **Báo cáo chi phí chính xác** mỗi tháng, giúp quản lý ngân sách hiệu quả.
- **Hoạt động liên tục** 24/7, không phụ thuộc vào giờ làm việc của ai.
- **Cá nhân hóa** theo từng tháng (tự động tạo sheet mới mỗi tháng).
- **Dễ dàng mở rộng** (thêm Slack, email báo cáo, hoặc tích hợp với phần mềm kế toán khác).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Telegram**:
   - Tạo **bot Telegram** qua [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Thêm bot vào nhóm hoặc chat cá nhân để test.

2. **Tài khoản easybits**:
   - Tạo **pipeline** trên [easybits.tech](https://extractor.easybits.tech/) để trích xuất dữ liệu từ hóa đơn.
   - Lấy **API Key** của pipeline để kết nối với n8n.

3. **Tài khoản Google Sheets**:
   - Tạo **OAuth 2.0 Credentials** cho Google Sheets (đăng ký tại [Google Cloud Console](https://console.cloud.google.com/)).
   - Cấp quyền cho workflow truy cập vào Google Sheets.

4. **File mẫu hóa đơn**:
   - Chuẩn bị **1-2 hóa đơn mẫu** (PDF hoặc ảnh) để test trích xuất.

---
:::note[LƯU Ý QUAN TRỌNG]
- **Không cần kỹ năng code** – workflow đã được cấu hình sẵn, chỉ cần điền thông tin API.
- **Dữ liệu an toàn**: easybits và Google Sheets chỉ lưu thông tin cần thiết, không xâm phạm quyền riêng tư.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/11659) và import vào **n8n Editor**.
- **Copy/paste JSON** từ file vào **Create Workflow** trong n8n.

**Bước chi tiết**:
1. Mở **n8n Editor** (trang chủ của workflow).
2. Nhấn **Import Workflow** và chọn file JSON đã tải.
3. Chọn **Active** để bắt đầu.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **24 node**, nhưng chỉ **5 node quan trọng** cần cấu hình kỹ:
##### **A. Cấu Hình Telegram Webhook**
- **Node**: `Telegram Webhook`
- **Cần thiết**:
  - Điền **API Token** từ bot Telegram vào **Webhook URL** (dạng: `https://<tên-domain>/webhook/expense-bot`).
  - Kiểm tra **HTTP Method** là `POST`.

##### **B. Cấu Hình easybits API**
- **Node**: `Extract with easybits`
- **Cần thiết**:
  - Điền **API Key** của pipeline easybits vào **Headers** (`Authorization: Bearer <API_KEY>`).
  - Thêm **file Base64** (từ node `Convert to Base64`) vào **Body** của request.

##### **C. Cấu Hình Google Sheets OAuth**
- **Nodes liên quan**: `Check Sheet Exists`, `Create Sheet`, `Add Expense Row`, `Format Data Row`
- **Cần thiết**:
  1. Tạo **OAuth 2.0 Credentials** cho Google Sheets (đăng ký tại [Google Cloud Console](https://console.cloud.google.com/)).
  2. Trong **n8n Credentials**, thêm **googleSheetsOAuth2Api** với:
     - **Client ID** và **Client Secret** từ Google Cloud.
     - **Refresh Token** (lấy từ quá trình authorize).
  3. Điền **Sheet Name** (ví dụ: `ChiPhi_Thang_<Tháng>`) vào node `Build Headers Request`.

##### **D. Cấu Hình Reimbursement Rates (Tùy Chọn)**
- **Node**: `Process Extraction` (Code Node)
- **Cần thiết**:
  - Sửa đổi **mảng `validCategories`** để phù hợp với doanh nghiệp (ví dụ: `Food`, `Transport`, `Office Supplies`).
  - Cập nhật **tỷ lệ hoàn trả** (nếu có) trong phần `reimbursementRates`.

##### **E. Cấu Hình Telegram API**
- **Node**: `Ask for Category` (nếu hóa đơn không phân loại được)
- **Cần thiết**:
  - Điền **API Token** của bot Telegram vào **Credentials** (`telegramApi`).
  - Cấu hình **chat ID** của người dùng (có thể lấy từ URL chat Telegram).

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với **1 hóa đơn mẫu**:
   - Gửi ảnh hóa đơn qua Telegram bot.
   - Kiểm tra **Google Sheets** có cập nhật dữ liệu không.
   - Xác nhận bot trả lời chính xác hay không.
2. **Bật Active** workflow sau khi test thành công.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Email Báo Cáo**:
   - Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.email` để gửi báo cáo chi phí hàng tháng.

2. **Lưu Log Dữ Liệu**:
   - Sử dụng node `n8n-nodes-base.telegram` hoặc `n8n-nodes-base.httpRequest` để lưu lịch sử giao dịch vào cơ sở dữ liệu (ví dụ: Firebase, Airtable).

3. **Tự Động Tạo Sheet Mới Hàng Tháng**:
   - Sử dụng **Google Apps Script** kết hợp với n8n để tự động tạo sheet mới mỗi đầu tháng.

4. **Phân Loại Chi Phí Tự Động**:
   - Cập nhật **mảng `validCategories`** trong node `Process Extraction` để phù hợp với doanh nghiệp.

5. **Xác Minh AI (LLM) cho Hóa Đơn**:
   - Thêm node **LLM** (ví dụ: `n8n-nodes-base.llm`) để xác minh nội dung hóa đơn nếu easybits không trích xuất chính xác.

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công, **tăng độ chính xác** trong quản lý chi phí, và **cung cấp báo cáo tự động** mỗi tháng. **Không cần code**, chỉ cần **cấu hình API** và **test một lần** là xong!

**Hành động ngay**:
1. **Self-host n8n** trên VPS để workflow hoạt động 24/7.
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Gửi hóa đơn đầu tiên** qua Telegram và xem bot làm việc như thế nào!

**🚀 Cùng tự động hóa quản lý chi phí ngay hôm nay!** 🚀