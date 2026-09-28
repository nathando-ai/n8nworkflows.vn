---
title: "🚀 Tự Động Hóa Xử Lý Hóa Đơn Ảnh từ Google Drive sang Google Sheets với AI (Không Cần Code)"
description: "Giải pháp tự động hóa hoàn toàn cho các sếp quản lý tài chính, kế toán hoặc doanh nghiệp nhỏ: Nhận hóa đơn ảnh từ Google Drive → AI tự động trích xuất dữ liệu → Ghi vào Google Sheets → Nhận email thông báo. Tiết kiệm 10+ giờ/lần so với cách làm thủ công!"
slug: "tu-dong-hoa-xu-ly-hoa-don-ai-google-drive-sheets"
tags: [n8n, automation, no-code, ai-summarization, google-drive, google-sheets, openai, invoice-processing]
keywords: [n8n tự động hóa hóa đơn, trích xuất dữ liệu hóa đơn AI, google drive google sheets tự động, lưu hóa đơn vào google sheets, tự động hóa kế toán không code]
---

# 🚀 **Tự Động Hóa Xử Lý Hóa Đơn Ảnh với AI: Từ Google Drive → Google Sheets → Email Thông Báo**

### **Nỗi Đau Của Các Sếp Khi Xử Lý Hóa Đơn Thủ Công**
Mỗi tháng, các sếp phải:
- **Quét/đính kèm** hàng chục hóa đơn ảnh từ email, camera, hoặc Google Drive.
- **Nhập liệu thủ công** vào Excel/Google Sheets: Tên nhà cung cấp, ngày mua, chi tiết sản phẩm, tổng tiền...
- **Tìm kiếm sai sót**: Dữ liệu nhập nhầm, mất hóa đơn, hoặc mất thời gian kiểm tra lại.
- **Không có báo cáo tự động**: Phải tổng hợp thủ công để báo cáo cho ban lãnh đạo.

**Kết quả?** Thời gian mất từ **3-5 giờ/lần** (hoặc nhiều hơn nếu có nhiều hóa đơn), dễ xảy ra lỗi, và không thể mở rộng cho nhiều nhân viên.

---
### **🎯 Kết Quả Các Sếp Nhận Được Với Workflow Này**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 100% thời gian nhập liệu**: AI tự động trích xuất dữ liệu từ hóa đơn ảnh.
✅ **Chính xác 100%**: Không còn sai sót do nhập nhầm hoặc mất hóa đơn.
✅ **Hoạt động 24/7**: Workflow chạy tự động khi có hóa đơn mới trong Google Drive.
✅ **Báo cáo tự động**: Dữ liệu được ghi vào Google Sheets và gửi email thông báo ngay khi xử lý xong.
✅ **Dễ dàng mở rộng**: Thêm nhiều nhân viên hoặc bộ phận khác vào quy trình.
✅ **Kết nối với nhiều dịch vụ**: Có thể mở rộng để gửi Slack/Telegram, lưu log, hoặc tích hợp với phần mềm kế toán.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
- **Tài khoản Google** (để kết nối Google Drive, Google Sheets, và Gmail).
- **Tài khoản OpenAI** (để sử dụng AI trích xuất dữ liệu).
- **File mẫu Google Sheets** (sẽ được cung cấp trong hướng dẫn).
- **Mô hình AI**: Workflow sử dụng **GPT-4-mini** (có thể thay đổi theo nhu cầu).

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/12954) (click "Export").
- **Mở n8n Editor** (n8n.io) → **Import Workflow** → Chọn file JSON vừa tải.
- **Hoặc copy toàn bộ JSON** từ file và dán vào **Import Workflow** trong n8n.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này có **8 node chính**, các sếp cần chú ý cấu hình các node sau:

##### **🔹 Node 1: "Monitor Receipts Folder" (Google Drive Trigger)**
- **Chức năng**: Theo dõi folder chứa hóa đơn trong Google Drive.
- **Cấu hình**:
  - **Credentials**: Chọn `googleDriveOAuth2Api` (cần kết nối tài khoản Google Drive).
  - **Folder ID**: Điền **ID của folder** chứa hóa đơn (có thể lấy từ liên kết folder: `https://drive.google.com/drive/folders/[FOLDER_ID]`).
  - **File Type**: Chọn `image/*` (để chỉ theo dõi file ảnh).

##### **🔹 Node 2: "Download file" (Google Drive)**
- **Chức năng**: Tải file hóa đơn từ Google Drive xuống.
- **Cấu hình**:
  - **Credentials**: Chọn `googleDriveOAuth2Api` (giống node 1).
  - **File ID**: Auto lấy từ node trước (không cần chỉnh).

##### **🔹 Node 3: "Extract Receipt Data with AI" (Agent)**
- **Chức năng**: AI phân tích hóa đơn và trích xuất dữ liệu (tên nhà cung cấp, ngày, chi tiết, tổng tiền).
- **Cấu hình**:
  - **Prompt**: Workflow đã cấu hình sẵn, các sếp **không cần chỉnh** (nếu muốn thay đổi, cần hiểu kỹ về **LangChain Agent**).
  - **Output**: Dữ liệu sẽ ra dưới dạng **JSON structured**.

##### **🔹 Node 4: "OpenAI Chat Model" (lmChatOpenAi)**
- **Chức năng**: Gọi API OpenAI để xử lý AI.
- **Cấu hình**:
  - **Credentials**: Chọn `openAiApi` (cần kết nối tài khoản OpenAI và điền **API Key**).
  - **Model**: Workflow mặc định là `gpt-4-mini` (có thể thay đổi thành `gpt-4` nếu muốn chất lượng cao hơn).

##### **🔹 Node 5: "Structured Output Parser" (outputParserStructured)**
- **Chức năng**: Chuyển dữ liệu JSON từ AI thành định dạng dễ đọc.
- **Cấu hình**: **Không cần chỉnh**, node này tự động xử lý.

##### **🔹 Node 6: "Append Receipt to Google Sheet" (Google Sheets)**
- **Chức năng**: Ghi dữ liệu vào Google Sheets.
- **Cấu hình**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (kết nối tài khoản Google Sheets).
  - **Sheet ID**: Điền **ID của Google Sheet** (lấy từ liên kết: `https://docs.google.com/spreadsheets/d/[SHEET_ID]`).
  - **Range**: Điền tên **tab** (sheet) muốn ghi dữ liệu (ví dụ: `Sheet1!A1`).
  - **Headers**: Chọn `Use first row as header` (nếu sheet có tiêu đề).

##### **🔹 Node 7: "Convert Receipt to HTML Table" (html)**
- **Chức năng**: Chuyển dữ liệu thành bảng HTML (dùng cho email).
- **Cấu hình**: **Không cần chỉnh**, node này tự động chuyển đổi.

##### **🔹 Node 8: "Send Receipt Email Notification" (Gmail)**
- **Chức năng**: Gửi email thông báo hóa đơn đã xử lý.
- **Cấu hình**:
  - **Credentials**: Chọn `gmailOAuth2` (kết nối tài khoản Gmail).
  - **To**: Điền **email nhận thông báo** (ví dụ: `sếp@doanhnghiep.com`).
  - **Subject**: Workflow mặc định là `New Receipt Processed`, có thể chỉnh.
  - **Body**: Nội dung email sẽ tự động bao gồm **bảng HTML** của hóa đơn.

---

#### **3. Kích Hoạt ⚡️ Workflow**
- **Test Run**: Chọn **Run Workflow** và chọn **1 file mẫu** (nếu có) để kiểm tra.
- **Bật Active**: Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động khi có hóa đơn mới.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Slack/Telegram Notification**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để gửi thông báo khi có hóa đơn mới.
   - Cấu hình:
     - **Credentials**: Kết nối tài khoản Slack/Telegram.
     - **Message**: Chỉnh nội dung thông báo (ví dụ: `📄 New Receipt: [Vendor Name] - [Total Amount]`).

2. **Lưu Log Dữ Liệu**:
   - Thêm node **Google Drive** hoặc **Google Sheets** để lưu **log** của quá trình xử lý (ngày giờ, file ID, trạng thái).

3. **Tích Hợp với Phần Mềm Kế Toán**:
   - Nếu sử dụng **QuickBooks, Xero, hoặc SAP**, có thể kết nối với node **QuickBooks API** để tự động ghi sổ.

4. **Chuyển Dữ Liệu Sang JSON API**:
   - Sử dụng node **HTTP Request** để gửi dữ liệu đã trích xuất về **API nội bộ** của doanh nghiệp.

5. **Tự Động Xóa File Sau Xử Lý**:
   - Thêm node **Google Drive** với **operation: delete** để xóa file hóa đơn sau khi đã xử lý (nếu không cần lưu trữ).

---

### **📌 Kết Luận**
Workflow này **giải phóng hoàn toàn thời gian** của các sếp khỏi công việc nhập liệu thủ công, đồng thời **giảm thiểu sai sót** và **tăng tính minh bạch** trong quản lý tài chính. Với **AI trích xuất dữ liệu**, các sếp có thể tập trung vào việc **quản lý chiến lược** thay vì mất thời gian với công việc lặp lại.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n của mình.
2. **Kết nối các tài khoản** (Google, OpenAI).
3. **Chỉnh folder và email** theo nhu cầu.
4. **Bật Active** và **nhận hóa đơn tự động** từ bây giờ!

---
**💡 Cần hỗ trợ thêm?**
- **Đăng ký tư vấn miễn phí** với SmoothWork: [https://smoothwork.ai/book-a-call](https://smoothwork.ai/book-a-call)
- **Xem video hướng dẫn chi tiết**: [https://youtu.be/Vl0wCc9pEGM](https://youtu.be/Vl0wCc9pEGM)