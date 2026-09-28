---
title: "🚀 Tự Động Hóa Theo Dõi Lead: Gửi Email Tự Động Từ Google Sheet Sang Gmail & Cập Nhật Trạng Thái - N8N"
description: "Giải pháp tự động hóa 100% không code giúp các sếp tự động gửi email chào hàng cho lead mới từ Google Sheet, đồng thời cập nhật trạng thái liên lạc trong bảng tính - tiết kiệm thời gian lên đến 80% mỗi ngày."
slug: "tieu-dong-hoa-theo-doi-lead-google-sheet-gmail"
tags: [n8n, automation, lead nurturing, google sheets, gmail, no-code, sales automation]
keywords: [n8n workflow lead nurturing, tự động hóa bán hàng, gửi email tự động từ google sheet, cập nhật trạng thái lead, tự động hóa sales]
---

# 🚀 **Tự Động Hóa Theo Dõi Lead: Gửi Email Tự Động Từ Google Sheet Sang Gmail & Cập Nhật Trạng Thái**

### **Nỗi Đau Của Các Sếp Trong Quá Trình Theo Dõi Lead**
Các sếp bán hàng hay marketing thường phải mất **giờ đồng hồ** mỗi ngày để:
- **Lọc lead mới** từ Google Sheet (Excel/Sheets).
- **Gửi email chào hàng** một cách thủ công, dễ bị bỏ quên.
- **Cập nhật trạng thái** (chưa liên lạc, đã gọi, đã gửi email...) sau mỗi lần tương tác.
- **Đối mặt với rủi ro** như gửi email trùng lặp hoặc bỏ qua lead quan trọng.

**Kết quả?** Thời gian quý giá bị "chôn vùi" trong công việc lặp đi lặp lại, trong khi lead tiềm năng có thể rơi vào tay đối thủ.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** theo dõi lead mỗi ngày (tự động lọc và gửi email).
- **Chính xác 100%** với việc cập nhật trạng thái tự động sau mỗi tương tác.
- **Tăng tỷ lệ chuyển đổi** nhờ gửi email kịp thời và cá nhân hóa.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Giảm thiểu lỗi** như email trùng lặp hoặc bỏ qua lead.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để sử dụng Google Sheets và Gmail).
2. **Bảng Google Sheet** chứa lead với các cột:
   - `Email` (địa chỉ email của lead).
   - `Name` (tên lead).
   - `Status` (trạng thái hiện tại, ví dụ: "Chưa liên lạc").
   - `Last Contact` (ngày tháng cuối cùng liên lạc, để lọc lead mới).
3. **API Key của Google Sheets** (tạo từ [Google Cloud Console](https://console.cloud.google.com/)).
4. **Tài khoản Gmail** được kết nối với n8n (để gửi email).
5. **VPS Self-hosted n8n** (để workflow chạy liên tục 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [liên kết gốc](https://n8n.io/workflows/6083).
- **Nhấn "Import"** trong n8n Editor và chọn file JSON.
- **Hoặc copy toàn bộ JSON** và dán vào ô "Import Workflow" trong Editor.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này bao gồm **6 node** chính. Dưới đây là hướng dẫn chi tiết để cấu hình:

##### **Node 1: Trigger: Run Every Day 🕒 (scheduleTrigger)**
- **Cấu hình**:
  - Chọn **Run every day** và thiết lập thời gian phù hợp (ví dụ: 9h sáng).
  - **Không cần thay đổi** các tham số khác.

##### **Node 2: Fetch Leads from Google Sheet 📄 (googleSheets)**
- **Cấu hình**:
  - **Credentials**: Chọn tài khoản Google đã kết nối.
  - **Operation**: Chọn `Get rows`.
  - **Sheet Name**: Điền tên sheet chứa lead (ví dụ: "Leads").
  - **Range**: Điền `Sheet1!A:Z` (hoặc điều chỉnh theo cột thực tế).
  - **Lưu ý**: Đảm bảo cột `Last Contact` được định dạng là **ngày tháng** để node sau có thể lọc lead mới.

##### **Node 3: Filter Only New Leads 🔍 (if)**
- **Cấu hình**:
  - **Condition**: Chọn `Last Contact` > `Today` (để lọc lead chưa liên lạc trong ngày).
  - **Lưu ý**:
    - Nếu cột `Last Contact` trống, các sếp có thể thay đổi điều kiện thành `Last Contact is empty`.
    - Nếu muốn lọc lead trong vòng 7 ngày, thay đổi thành `Last Contact < 7 days ago`.

##### **Node 4: Batch Process Leads 🔁 (splitInBatches)**
- **Cấu hình**:
  - **Batch Size**: Đặt số lượng email gửi đồng thời (ví dụ: **5** để tránh bị chặn spam).
  - **Lưu ý**: Nếu gửi quá nhiều email cùng lúc, Gmail có thể đánh dấu là spam.

##### **Node 5: Send Email to Lead ✉️ (gmail)**
- **Cấu hình**:
  - **Credentials**: Chọn tài khoản Gmail đã kết nối.
  - **Operation**: Chọn `Send Email`.
  - **Email Address**: Sử dụng `{{ $json["Email"] }}` (địa chỉ email từ Google Sheet).
  - **Subject**: Điền tiêu đề email (ví dụ: `Xin chào {{ $json["Name"] }}! Chúng tôi quan tâm đến bạn`).
  - **Body**: Sử dụng **HTML template** hoặc văn bản cá nhân hóa:
    ```html
    <p>Xin chào {{ $json["Name"] }},</p>
    <p>Tôi là [Tên Bạn], từ [Tên Công Ty]. Tôi thấy thông tin của bạn qua [Nguồn] và muốn chia sẻ một giải pháp phù hợp cho [Yêu cầu của Lead].</p>
    <p>Vui lòng liên hệ với tôi qua email hoặc số điện thoại để thảo luận chi tiết.</p>
    <p>Trân trọng,</p>
    <p>[Tên Bạn]</p>
    ```
  - **Lưu ý**:
    - **Không gửi email trùng lặp** với cùng nội dung. Nếu lead đã được gửi email trước, hãy thêm điều kiện trong node `if` để kiểm tra.
    - **Kiểm tra spam**: Nếu email bị đánh dấu là spam, giảm số lượng batch hoặc sử dụng **SMTP khác** như SendGrid.

##### **Node 6: Mark Lead as Contacted ✅ (googleSheets)**
- **Cấu hình**:
  - **Credentials**: Chọn tài khoản Google cùng với node `Fetch Leads`.
  - **Operation**: Chọn `Update row`.
  - **Sheet Name**: Điền tên sheet (ví dụ: "Leads").
  - **Range**: Điền `Sheet1!A:Z` (hoặc điều chỉnh).
  - **Update Values**:
    - Cột `Status`: Đặt giá trị `Đã liên lạc` (hoặc `Contacted`).
    - Cột `Last Contact`: Cập nhật thành ngày hiện tại (`{{ $json["$dateTimeNow"] }}`).
  - **Lưu ý**: Đảm bảo cột `Status` và `Last Contact` được định dạng đúng trong Google Sheet.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhấn **Run Workflow** và kiểm tra:
    - Email có được gửi không?
    - Trạng thái trong Google Sheet có được cập nhật không?
- **Bật Active**:
  - Sau khi kiểm tra thành công, chuyển trạng thái workflow sang **Active**.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Slack/Telegram**:
   - Thêm node `webhook` hoặc `slack` để thông báo khi email được gửi thành công/bất thành công.
   - Ví dụ: Khi email gửi thành công, gửi tin nhắn Slack: `📧 Email đã gửi cho {{ $json["Name"] }}`.

2. **Lưu Log Hoạt Động**:
   - Thêm node `set` hoặc `file` để lưu lịch sử hoạt động (ví dụ: ngày gửi, trạng thái, nội dung email).

3. **Gửi Email Cá Nhân Hóa**:
   - Sử dụng **LLM như Mistral AI** để tự động tạo nội dung email dựa trên thông tin lead.
   - Ví dụ: Nếu lead có nhu cầu "tìm kiếm giải pháp CRM", workflow có thể tự động tạo email phù hợp.

4. **Báo Cáo Định Kỳ**:
   - Thêm node `scheduleTrigger` để gửi báo cáo hàng tuần về số lượng lead được liên lạc, tỷ lệ mở email,...

5. **Kết Hợp với CRM**:
   - Nếu sử dụng **HubSpot, Salesforce**, các sếp có thể thay thế Google Sheet bằng API của CRM để đồng bộ lead.
---

### **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp bán hàng hoặc marketing muốn **tự động hóa hoàn toàn quá trình theo dõi lead** mà không cần viết một dòng code. Với chỉ **vài phút cấu hình**, các sếp có thể:
✅ **Tiết kiệm thời gian** để tập trung vào việc bán hàng.
✅ **Tăng tỷ lệ chuyển đổi** nhờ gửi email kịp thời.
✅ **Cập nhật trạng thái lead** một cách chính xác.

**Hành động ngay hôm nay!**
1. **Chuẩn bị tài khoản Google và VPS n8n**.
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và để workflow làm việc 24/7 cho bạn!

👉 [Tải workflow nguyên bản](https://n8n.io/workflows/6083) và bắt đầu tự động hóa ngay!