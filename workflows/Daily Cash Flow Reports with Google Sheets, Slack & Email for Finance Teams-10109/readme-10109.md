---
title: "💰 Tự Động Hóa Báo Cáo Lưu Chuyển Tiền Mỗi Ngày với Google Sheets, Slack & Email – Giúp Đội Ngũ Tài Chính Tiết Kiệm 50% Thời Gian"
description: "Workflow này tự động thu thập, tính toán và phân phối báo cáo lưu chuyển tiền hàng ngày (dòng tiền vào/ra) đến Google Sheets, gửi email PDF cho đội ngũ tài chính và thông báo trên Slack. Giúp các sếp theo dõi tài chính 24/7 mà không cần làm thủ công."
slug: "tu-dong-hoa-bao-cao-luu-chuyen-tien-moi-ngay"
tags: [n8n, tài chính, tự động hóa, báo cáo, google-sheets, slack, email, pdf, pdfmonkey]
keywords: [tự động hóa báo cáo tài chính, n8n workflow tài chính, báo cáo lưu chuyển tiền hàng ngày, tự động hóa google sheets, gửi báo cáo tài chính qua email, tích hợp slack với n8n]
---

# 🚀 **Tự Động Hóa Báo Cáo Lưu Chuyển Tiền Mỗi Ngày – Giải Pháp Cho Đội Ngũ Tài Chính**

### **Nỗi Đau Của Các Sếp Tài Chính Hàng Ngày**
Làm thủ công báo cáo lưu chuyển tiền (cash flow) là một việc **mệt mỏi, dễ sai sót và tốn thời gian** của đội ngũ tài chính. Các sếp phải:
- **Thu thập dữ liệu** từ nhiều nguồn khác nhau (ngân hàng, ứng dụng quản lý tài chính, Excel...).
- **Tính toán thủ công** dòng tiền vào (inflows) và dòng tiền ra (outflows) theo từng danh mục.
- **Lập báo cáo** và gửi cho ban lãnh đạo, đồng thời **lưu trữ** để theo dõi dài hạn.
- **Gặp rủi ro** như quên gửi báo cáo, sai sót trong tính toán, hoặc mất thời gian để tổng hợp.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động thu thập** dữ liệu từ API (hoặc nguồn dữ liệu của các sếp).
✅ **Tính toán chính xác** dòng tiền vào/ra và lưu chuyển tiền net.
✅ **Gửi báo cáo PDF** qua email và **đăng báo cáo trên Slack** để toàn bộ team theo dõi.
✅ **Lưu trữ bản sao** trên Google Drive để an toàn và truy cập dễ dàng.
✅ **Chạy tự động hàng ngày** vào 6h chiều, không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và ổn định.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 50% thời gian** của đội ngũ tài chính (không cần tổng hợp dữ liệu thủ công).
- **Chính xác 100%** nhờ tính toán tự động, không sai sót như khi làm bằng tay.
- **Cá nhân hóa báo cáo** với định dạng HTML/PDF chuyên nghiệp.
- **Hoạt động liên tục** 24/7, không phụ thuộc vào giờ làm việc.
- **Truy cập dễ dàng** thông qua Google Sheets, email và Slack.
- **An toàn dữ liệu** với bản sao lưu tự động trên Google Drive.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **API Keys hoặc Credentials** cho:
- **Google Sheets** (để lưu trữ báo cáo).
- **Google Drive** (để backup).
- **SMTP** (để gửi email báo cáo).
- **Slack API** (để thông báo trên Slack).
- **PDFMonkey API** (để chuyển HTML thành PDF).
✔ **Dữ liệu mẫu** (nếu sử dụng `httpRequest` để lấy dòng tiền vào/ra từ API bên thứ ba).
✔ **Google Sheets** đã tạo sẵn với **cấu trúc cột phù hợp** (các sếp có thể tham khảo mẫu dưới đây).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/10109](https://n8n.io/workflows/10109).
2. Trong **n8n Editor**, nhấn **"Import"** và chọn file JSON.
3. Hoặc copy toàn bộ JSON và dán vào **"Import Workflow"** trong giao diện.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này có **13 node**, nhưng các sếp cần chú ý đặc biệt đến các node sau:

##### **🔹 Node "Get Cash Inflows" & "Get Cash Outflows" (HTTP Request)**
- **Mục đích**: Thu thập dữ liệu dòng tiền vào/ra từ API bên thứ ba (ví dụ: API ngân hàng, ứng dụng quản lý tài chính).
- **Cách cấu hình**:
  - Thay đổi **URL** trong `httpRequest` để trỏ đến API của các sếp.
  - Nếu không có API, các sếp có thể **sử dụng Google Sheets** để nhập dữ liệu thủ công (xem hướng dẫn dưới đây).
  - **Headers** cần có `Authorization` (nếu API yêu cầu).

##### **🔹 Node "Calculate Inflows" & "Calculate Outflows" (Code)**
- **Mục đích**: Tính tổng dòng tiền vào/ra theo từng danh mục (ví dụ: doanh thu, chi phí, lương...).
- **Lưu ý**:
  - Các sếp **không cần chỉnh sửa mã** nếu dữ liệu đầu vào đúng định dạng.
  - Nếu cần thay đổi logic, mở node và chỉnh sửa trong **n8n Code Editor**.

##### **🔹 Node "Merge Data" (Merge)**
- **Mục đích**: Gộp dữ liệu dòng tiền vào và ra thành một bảng duy nhất.
- **Không cần chỉnh sửa**, chỉ cần đảm bảo dữ liệu đầu vào từ `Get Cash Inflows` và `Get Cash Outflows` đúng định dạng.

##### **🔹 Node "Calculate Net Cash Flow" (Code)**
- **Mục đích**: Tính **lưu chuyển tiền net** = Dòng tiền vào - Dòng tiền ra.
- **Lưu ý**: Node này tự động tính toán, nhưng các sếp có thể mở ra để kiểm tra logic.

##### **🔹 Node "Save to Google Sheets" (Google Sheets)**
- **Mục đích**: Lưu báo cáo vào Google Sheets để theo dõi dài hạn.
- **Cách cấu hình**:
  - Chọn **Google Sheets** đã tạo sẵn.
  - **Sheet Name**: Đặt tên phù hợp (ví dụ: "Cash Flow Daily").
  - **Operation**: Đặt là **"Append"** (thêm dữ liệu mới vào cuối).
  - **Cấu trúc cột**: Các sếp nên chuẩn bị trước một bảng với các cột như:
    ```
    Ngày, Danh mục, Dòng tiền vào, Dòng tiền ra, Tổng dòng tiền, Lưu chuyển tiền net
    ```

##### **🔹 Node "Generate HTML Report" (Code)**
- **Mục đích**: Tạo báo cáo HTML đẹp mắt từ dữ liệu đã tính toán.
- **Lưu ý**: Node này tự động sinh HTML, nhưng các sếp có thể mở ra để chỉnh sửa **template HTML** nếu muốn thay đổi định dạng.

##### **🔹 Node "Email Report" (Email Send)**
- **Mục đích**: Gửi báo cáo PDF qua email cho đội ngũ tài chính.
- **Cách cấu hình**:
  - Chọn **SMTP credentials** đã thiết lập trước.
  - **To**: Địa chỉ email của người nhận (ví dụ: `team-finance@company.com`).
  - **Subject**: Thay đổi thành `"Báo cáo Lưu Chuyển Tiền Ngày [Ngày]`".
  - **HTML Body**: Sử dụng nội dung từ node `Generate HTML Report`.

##### **🔹 Node "Convert to PDF" (PDFMonkey)**
- **Mục đích**: Chuyển báo cáo HTML thành PDF chuyên nghiệp.
- **Cách cấu hình**:
  - Đảm bảo đã thêm **PDFMonkey API Key** trong credentials.
  - Node này tự động lấy HTML từ node trước và chuyển thành PDF.

##### **🔹 Node "Post to Slack" (Slack)**
- **Mục đích**: Thông báo tóm tắt báo cáo trên Slack.
- **Cách cấu hình**:
  - Chọn **Slack workspace** và **channel** phù hợp.
  - **Message**: Có thể chỉnh sửa để hiển thị thông tin ngắn gọn như:
    ```
    📊 **Báo cáo Lưu Chuyển Tiền Ngày [Ngày]**
    - Tổng dòng tiền vào: $X
    - Tổng dòng tiền ra: $Y
    - Lưu chuyển tiền net: $Z
    - [Xem báo cáo chi tiết](link-to-google-sheets)
    ```

##### **🔹 Node "Backup to Google Drive" (Google Drive)**
- **Mục đích**: Lưu bản sao lưu báo cáo PDF trên Google Drive.
- **Cách cấu hình**:
  - Chọn **Google Drive folder** để lưu trữ.
  - Tên file: Thay đổi thành `"Báo cáo_Lưu_Chuyển_Tiền_[Ngày].pdf"`.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **"Execute"** trong n8n Editor để kiểm tra workflow.
   - Kiểm tra email, Slack và Google Sheets để đảm bảo dữ liệu đúng.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Google Finance API**:
   - Nếu các sếp muốn tự động lấy dữ liệu từ ngân hàng, có thể sử dụng **Google Finance API** hoặc **API ngân hàng** (nếu có).

2. **Tự động gửi báo cáo định kỳ**:
   - Nếu muốn gửi báo cáo hàng tuần/tháng, các sếp có thể **sao chép workflow** và thay đổi `scheduleTrigger` thành:
     - **"Every Monday at 8 AM"** (báo cáo tuần).
     - **"First day of the month at 9 AM"** (báo cáo tháng).

3. **Thêm cảnh báo khi lưu chuyển tiền âm**:
   - Sử dụng **n8n-nodes-base.if** để kiểm tra nếu `Net Cash Flow < 0`, sau đó gửi **email cảnh báo** hoặc **thông báo Slack khẩn cấp**.

4. **Lưu log hoạt động**:
   - Thêm node **Sticky Note** (`n8n-nodes-base.stickyNote`) để ghi lại lịch sử chạy workflow.

5. **Tích hợp với Trello/Notion**:
   - Sau khi hoàn thành, các sếp có thể thêm node **Trello** hoặc **Notion** để cập nhật báo cáo vào bảng quản lý dự án.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để các sếp **tự động hóa báo cáo tài chính hàng ngày**, tiết kiệm thời gian và giảm thiểu sai sót. Với chỉ **một lần cấu hình**, workflow sẽ **chạy tự động hàng ngày**, gửi báo cáo đến email, Slack và lưu trữ trên Google Sheets và Drive.

**Hành động ngay hôm nay:**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình credentials** và dữ liệu đầu vào.
3. **Test và kích hoạt** để bắt đầu tự động hóa!

---
**🚀 Cảm ơn các sếp đã đọc đến cuối!** Nếu có bất kỳ câu hỏi hoặc gặp khó khăn, hãy để lại comment bên dưới. Chúc các sếp thành công với việc tự động hóa tài chính! 💸💻