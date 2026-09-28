---
title: "💰 Tự Động Hóa Xử Lý Hóa Đơn Du Lịch với GPT-4.1-mini, Google Sheets & Email Thông Báo – Giảm 90% Thời Gian Chăm Sóc Hóa Đơn"
description: "Workflow này tự động trích xuất dữ liệu từ hóa đơn du lịch (PDF), tổng hợp thông tin vào Google Sheets và gửi email thông báo chi tiết cho bộ phận tài chính. Giúp doanh nghiệp tiết kiệm 90% thời gian chăm sóc hóa đơn, giảm sai sót và tăng độ minh bạch trong quá trình xin hoàn trả chi phí."
slug: "tieu-dong-hoa-xu-ly-hoa-don-du-lich-gpt-4-1-mini"
tags: [n8n, automation, no-code, ai, google-sheets, email-notification, expense-reporting]
keywords: [n8n workflow tự động hóa hóa đơn du lịch, trích xuất dữ liệu từ PDF với GPT-4.1-mini, gửi email thông báo chi phí cho tài chính, tiết kiệm thời gian xử lý hóa đơn, tự động hóa xin hoàn trả chi phí]
---

# 🚀 **Tự Động Hóa Xử Lý Hóa Đơn Du Lịch với AI GPT-4.1-mini, Google Sheets & Email Thông Báo**

### **Giải pháp hoàn hảo cho các sếp và nhân viên hành chính**
Hãy tưởng tượng một ngày không còn phải **quét hàng chục hóa đơn du lịch**, **ghi chép thủ công vào Excel**, hoặc **gửi email nhắc nhở tài chính** một cách mệt mỏi. Workflow này **tự động hóa toàn bộ quy trình** từ khi nhân viên nộp hóa đơn cho đến khi bộ phận tài chính nhận được báo cáo chi tiết, **giúp tiết kiệm tới 90% thời gian** và giảm thiểu sai sót.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted) để đảm bảo **mật mã hóa dữ liệu** và **không phụ thuộc vào nền tảng bên thứ ba**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 90% thời gian** xử lý hóa đơn du lịch (không còn phải quét, ghi chép thủ công).
✅ **Giảm sai sót** nhờ AI GPT-4.1-mini tự động trích xuất dữ liệu chính xác từ PDF.
✅ **Minh bạch toàn diện** với báo cáo chi tiết được lưu vào Google Sheets và gửi email cho tài chính.
✅ **Hoạt động liên tục** (24/7) mà không cần can thiệp của con người.
✅ **Cá nhân hóa thông báo** với email HTML đẹp mắt, bao gồm chi tiết chi phí và thông tin du lịch.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
- **Tài khoản Google** (để kết nối Google Drive & Google Sheets).
- **API Key OpenAI** (để sử dụng GPT-4.1-mini).
- **Tài khoản SMTP** (hoặc Gmail) để gửi email thông báo.
- **Google Sheet** đã tạo sẵn để lưu trữ dữ liệu hóa đơn (cấu trúc bao gồm cột: **Employee Name, Department, Trip Purpose, Date, Vendor, Total, Tax, Items**).
- **Form Google** (hoặc công cụ khác) để nhân viên nộp hóa đơn (cần có trường **tên nhân viên, bộ phận, mục đích du lịch, ngày đi, ngày về, và upload file PDF**).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [n8n.io/workflows/6896](https://n8n.io/workflows/6896).
- **Nhấn "Import"** trong n8n Editor và chọn file JSON.
- **Hoặc copy toàn bộ JSON** và dán vào **Create from JSON** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Dưới đây là **các node quan trọng** cần cấu hình kỹ lưỡng:

##### **🔹 Node 1: "On form submission" (formTrigger)**
- **Cấu hình**:
  - Chọn **Google Form** (hoặc công cụ khác như Typeform, JotForm) làm trigger.
  - **Kiểm tra các trường bắt buộc**:
    - **Employee Name** (tên nhân viên)
    - **Department** (bộ phận)
    - **Trip Purpose** (mục đích du lịch)
    - **From Date / To Date** (ngày đi và về)
    - **Receipt/Invoice File Upload** (upload file PDF).

##### **🔹 Node 2: "Upload file" (googleDrive)**
- **Credentials**: Chọn **googleDriveOAuth2Api** (đã cấu hình trước).
- **Cấu hình**:
  - **Folder ID**: Chọn thư mục Google Drive để lưu trữ hóa đơn (cần tạo sẵn).
  - **File Name**: Dùng **`{{ $node["On form submission"].json["employee_name"] }}_{{ $node["On form submission"].json["trip_purpose"] }}.pdf`** để đặt tên file tự động.

##### **🔹 Node 3: "Extract from File" (extractFromFile)**
- **Operation**: Chọn **PDF** (do file hóa đơn là PDF).
- **Lưu ý**:
  - Nếu hóa đơn có định dạng không chuẩn, cần **cải thiện chất lượng PDF** trước khi upload.

##### **🔹 Node 4: "GPT" (lmChatOpenAi)**
- **Credentials**: Chọn **openAiApi** (đã cấu hình API Key).
- **Model**: Chọn **gpt-4.1-mini** (đã được cấu hình sẵn).
- **Prompt**: Workflow đã sử dụng **cấu trúc prompt mặc định** để trích xuất dữ liệu từ PDF. Nếu cần **tùy chỉnh**, các sếp có thể chỉnh sửa tại **Node "DocClaim Assistant Agent"**.

##### **🔹 Node 5: "Append row in sheet" (googleSheets)**
- **Credentials**: Chọn **googleSheetsOAuth2Api**.
- **Operation**: Chọn **append** (thêm hàng mới).
- **Sheet Name**: Đặt tên sheet (ví dụ: **"Expense_Reports"**).
- **Range**: Chọn **Sheet1!A1** (hoặc tùy chỉnh theo cấu trúc sheet).
- **Data**: Dùng **`{{ $json["data"] }}`** (dữ liệu đã được AI trích xuất).

##### **🔹 Node 6: "Send trip expense request to finance team" (emailSend)**
- **Credentials**: Chọn **smtp** (hoặc Gmail).
- **To**: Điền email bộ phận tài chính (ví dụ: **finance@doanhnghiep.com**).
- **Subject**: **"Yêu cầu hoàn trả chi phí du lịch: {{ $node["On form submission"].json["employee_name"] }}"** (tự động thêm tên nhân viên).
- **HTML Template**: Sử dụng **Node "Create HTML Email Template"** (cần chỉnh sửa nội dung email theo yêu cầu).

##### **🔹 Node 7: "DocClaim Assistant Agent" (agent)**
- **Lưu ý quan trọng**:
  - Workflow sử dụng **LangChain Agent** để tự động trích xuất dữ liệu từ PDF.
  - Nếu dữ liệu trích xuất **không chính xác**, các sếp cần **tùy chỉnh prompt** tại đây:
    ```json
    {
      "prompt": "Trích xuất dữ liệu từ hóa đơn PDF bao gồm: tên nhà cung cấp, ngày hóa đơn, tổng tiền, thuế, và chi tiết các mặt hàng. Đảm bảo dữ liệu được định dạng JSON chuẩn."
    }
    ```

##### **🔹 Node 8: "Transform invoice record" & "Transform Output" (code)**
- **Lưu ý**:
  - Các Node này **chuyển đổi dữ liệu** từ format crud sang JSON chuẩn.
  - Nếu cần **thêm trường dữ liệu**, các sếp phải chỉnh sửa mã JavaScript trong Node này.

---

#### **3. Kích hoạt ⚡️**
- **Test run dữ liệu mẫu**:
  - Nhập **một hóa đơn du lịch PDF** vào form và kiểm tra:
    - Dữ liệu có được trích xuất chính xác không?
    - Email có được gửi đúng không?
    - Dữ liệu có được lưu vào Google Sheets không?
- **Bật Active workflow**:
  - Sau khi kiểm tra xong, **bật workflow** để hoạt động tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Gửi email với file đính kèm**:
   - Thêm **Node "Attach file"** (n8n-nodes-base.attachment) để gửi **hóa đơn PDF gốc** cùng email.
2. **Thêm bước xác thực**:
   - Sử dụng **Node "Slack Notification"** để thông báo khi có hóa đơn mới.
3. **Tự động phân loại chi phí**:
   - Sử dụng **Node "Code"** để thêm **thẻ/nhãn** cho chi phí (ví dụ: "Đi công tác", "Hàng hóa", "Phí dịch vụ").
4. **Báo cáo định kỳ**:
   - Sử dụng **Node "Google Sheets"** để **tính tổng chi phí theo tháng** và gửi email báo cáo cho CEO.
5. **Kết nối với QuickBooks/Xero**:
   - Thay thế **Google Sheets** bằng **Node QuickBooks** để tự động nhập hóa đơn vào hệ thống kế toán.

---

### 📌 **Kết luận**
Workflow này **giải phóng nhân viên hành chính** khỏi công việc mệt mỏi là **quét và nhập liệu hóa đơn**, đồng thời **tăng độ chính xác** nhờ AI GPT-4.1-mini. **Bộ phận tài chính** cũng được **tiết kiệm thời gian** khi nhận được báo cáo chi tiết và tự động.

**Hành động ngay hôm nay!**
- **Import workflow** và **cấu hình theo hướng dẫn**.
- **Test với một hóa đơn mẫu** trước khi áp dụng toàn bộ.
- **Tích hợp vào hệ thống** và **giải phóng đội ngũ** của mình!

👉 **Bắt đầu tự động hóa hóa đơn du lịch ngay bây giờ!** 🚀