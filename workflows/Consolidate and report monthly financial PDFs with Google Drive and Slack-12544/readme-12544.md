---
title: "📊 Tự Động Hoà Trộn & Báo Cáo Tài Chính Tháng Hàng (PDF) Với Google Drive + Slack - Không Cần Code"
description: "Workflow tự động hóa hoàn toàn để thu thập, hợp nhất tất cả các báo cáo tài chính PDF từ Google Drive thành một 'Báo Cáo Thống Nhất' định kỳ hàng tháng, sau đó tự động upload lên Drive và thông báo cho đội ngũ tài chính qua Slack. Giúp các sếp tiết kiệm 10-15 giờ công mỗi tháng, tránh sai sót do thủ công, và duy trì tính nhất quán trong báo cáo."
slug: "tieu-dong-hoa-tai-chinh-thang-hang-google-drive-slack"
tags: [n8n, automation, tài chính doanh nghiệp, google-drive, slack-integration, pdf-manipulation, no-code]
keywords: [tự động hóa tài chính, hợp nhất PDF, báo cáo tháng hàng, n8n workflow, tự động hóa Google Drive, Slack báo cáo tài chính]
---

# 🚀 **Tự Động Hợp Nhất & Báo Cáo Tài Chính Tháng Hàng (PDF) Với Google Drive + Slack**

### **Nỗi Đau Của Các Sếp:**
Hàng tháng, đội ngũ tài chính phải:
- **Tìm kiếm và tải xuống** hàng chục tệp PDF từ Google Drive (hoặc các nguồn khác) để tổng hợp báo cáo.
- **Kiểm tra thủ công** từng tệp để đảm bảo đúng định dạng (PDF) và không bị lỗi.
- **Hợp nhất** các tệp này thành một báo cáo thống nhất bằng cách sử dụng các công cụ như Adobe Acrobat (tốn thời gian và dễ sai sót).
- **Upload lại** báo cáo cuối cùng lên Drive và **gửi thông báo** cho toàn bộ đội ngũ qua Slack/Email.
- **Rủi ro cao** khi làm thủ công: Báo cáo trùng lặp, thiếu tệp, hoặc sai sót trong dữ liệu.

**Workflow này giải quyết tất cả vấn đề trên bằng cách tự động hóa 100% quy trình, chỉ cần chạy một lần/month!**

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-15 giờ công/month**: Không cần làm thủ công nữa.
- **Chính xác 100%**: Không bỏ sót tệp nào và tránh sai sót do con người.
- **Báo cáo thống nhất**: Tất cả dữ liệu tài chính được hợp nhất thành một tệp PDF duy nhất.
- **Thông báo tự động**: Slack sẽ gửi tin nhắn định dạng cho đội ngũ tài chính ngay khi báo cáo hoàn thành.
- **Hoạt động 24/7**: Workflow chạy tự động vào ngày 1 hàng tháng, không cần can thiệp.
- **Dễ dàng mở rộng**: Có thể kết nối với các nguồn dữ liệu khác (Excel, Airtable) hoặc gửi báo cáo qua Email.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive**:
   - Một **folder chứa các tệp PDF tài chính** (ví dụ: `Báo cáo tháng 12/2023`).
   - **Quản lý quyền**: Đảm bảo tài khoản n8n có quyền đọc/tải xuống và upload tệp vào folder này.
   - **Credentials**: Tạo **Google Drive OAuth 2.0 API** trong n8n (cài đặt tại: **Settings > Credentials > Add Credential > Google Drive OAuth 2.0**).

2. **API HTML/CSS to PDF**:
   - Đăng ký miễn phí tại [html-css-to-pdf.com](https://html-css-to-pdf.com/) để lấy **API Key**.
   - Thêm **credentials** trong n8n với tên `htmlcsstopdfApi` (cài đặt tại: **Settings > Credentials > Add Credential > HTML/CSS to PDF**).

3. **Tài khoản Slack**:
   - Một **channel Slack** dành cho đội ngũ tài chính (ví dụ: `#finance-dept`).
   - **Credentials Slack OAuth 2.0**: Cài đặt trong n8n (tương tự Google Drive).

4. **Hệ thống n8n**:
   - **Self-hosted** (khuyến nghị) để workflow chạy 24/7 ổn định.
   - **N8n Community Edition** (miễn phí) hoặc **n8n Enterprise** (nếu cần tính năng nâng cao).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON**: [Tải workflow từ n8n.io](https://n8n.io/workflows/12544) (ấn vào "Export Workflow").
- **Import trong n8n**:
  1. Mở **n8n Editor** (https://n8n.io/editor).
  2. Nhấn **Import** (góc trên bên phải) và chọn file JSON tải xuống.
  3. Hoặc **Copy toàn bộ JSON** và dán vào **Import Workflow** trong Editor.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này gồm **8 node** chính, các sếp cần cấu hình kỹ các node sau:

##### **A. Node "Trigger: Monthly on the 1st" (ScheduleTrigger)**
- **Cấu hình**:
  - **Schedule**: Chọn `Day of Month` và nhập `1` (ngày 1 hàng tháng).
  - **Time**: Đặt giờ chạy (ví dụ: 8h sáng để tránh ảnh hưởng đến hoạt động).
  - **Time Zone**: Chọn timezone phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).
- **Lưu ý**: Workflow sẽ chạy tự động vào ngày 1 hàng tháng, không cần kích hoạt thủ công.

##### **B. Node "List Financial PDFs from Drive" (Google Drive - List)**
- **Cấu hình**:
  - **Credentials**: Chọn `googleDriveOAuth2Api` (đã tạo trước).
  - **Folder ID**: Nhập **ID của folder chứa tệp PDF tài chính** (lấy từ liên kết folder Google Drive: `https://drive.google.com/drive/folders/[FOLDER_ID]`).
  - **Query Parameters**:
    - `q`: `mimeType = "application/pdf"` (chỉ lọc tệp PDF).
    - `fields`: `files(id, name, modifiedTime)` (trích xuất thông tin cần thiết).
  - **Test Run**: Nhấn **Execute Node** để kiểm tra danh sách tệp PDF.

##### **C. Node "Validate File Format (PDF only)" (If)**
- **Cấu hình**:
  - **Condition**: Kiểm tra `$.mimeType === "application/pdf"` (đảm bảo chỉ tệp PDF được xử lý).
  - **Lưu ý**: Nếu tệp không phải PDF, nó sẽ bị bỏ qua tự động.

##### **D. Node "Download Documents for Processing" (Google Drive - Download)**
- **Cấu hình**:
  - **Credentials**: Chọn `googleDriveOAuth2Api`.
  - **File ID**: Sử dụng `$.id` từ node trước (trích xuất từ danh sách tệp PDF).
  - **Test Run**: Chạy node này với một tệp mẫu để kiểm tra tải xuống thành công.

##### **E. Node "Batch Files for Merging" (Aggregate)**
- **Cấu hình**:
  - **Aggregate By**: Chọn `$.fileId` (để nhóm tất cả tệp PDF cùng một lúc).
  - **Lưu ý**: Node này sẽ hợp nhất tất cả tệp PDF đã tải xuống thành một danh sách duy nhất.

##### **F. Node "Merge multiple PDFS into one" (HTML/CSS to PDF)**
- **Cấu hình**:
  - **Credentials**: Chọn `htmlcsstopdfApi`.
  - **Input Data**: Sử dụng kết quả từ node Aggregate (danh sách tệp PDF).
  - **Merge Logic**:
    - Sử dụng **HTML/CSS template** để hợp nhất các tệp PDF thành một tệp duy nhất.
    - **Lưu ý**: Nếu không có template HTML/CSS, các sếp có thể sử dụng **PDF.js** hoặc **LibreOffice** để tạo template đơn giản.
  - **Test Run**: Chạy với 2-3 tệp mẫu để kiểm tra kết quả hợp nhất.

##### **G. Node "Upload Consolidated Master Report" (Google Drive - Upload)**
- **Cấu hình**:
  - **Credentials**: Chọn `googleDriveOAuth2Api`.
  - **Folder ID**: Chọn folder **mới** (ví dụ: `Báo cáo Thống Nhất`) để lưu tệp PDF hợp nhất.
  - **File Name**: Đặt tên tự động theo tháng (ví dụ: `Báo cáo_Thống_Nhất_12-2023.pdf`).
  - **File Content**: Sử dụng kết quả từ node Merge PDF.
  - **Test Run**: Upload tệp mẫu để kiểm tra.

##### **H. Node "Notify Finance Team (Slack)" (Slack)**
- **Cấu hình**:
  - **Credentials**: Chọn `slackOAuth2Api`.
  - **Channel**: Chọn `#finance-dept` (hoặc channel tương ứng).
  - **Message Template**:
    ```json
    {
      "text": "📊 **Báo cáo tài chính tháng {{ $now.format('MMMM') }} đã hoàn thành!**",
      "attachments": [
        {
          "title": "Báo cáo thống nhất",
          "title_link": "https://drive.google.com/drive/folders/[FOLDER_ID]",
          "text": "Tệp PDF đã được hợp nhất và upload lên Google Drive.",
          "mrkdwn_in": ["text", "pretext", "fields"]
        }
      ]
    }
    ```
  - **Lưu ý**: Thay thế `[FOLDER_ID]` bằng ID folder chứa báo cáo thống nhất.

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Chạy workflow với **dữ liệu mẫu** (1-2 tệp PDF) để kiểm tra toàn bộ quy trình.
- **Bật Active**: Sau khi kiểm tra thành công, chuyển **Workflow Status** từ `Inactive` sang `Active`.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Google Sheets/Excel**:
   - Thêm node **Google Sheets** để tự động ghi dữ liệu từ báo cáo PDF vào bảng tính (ví dụ: số liệu doanh thu, chi phí).
   - **Cách làm**: Sử dụng node **Google Sheets - Create Spreadsheet** sau node Merge PDF.

2. **Gửi báo cáo qua Email**:
   - Thêm node **Email** (ví dụ: **SendGrid** hoặc **Gmail SMTP**) để gửi báo cáo PDF cho các sếp cấp cao.
   - **Cách làm**: Sử dụng node **Email - Send Email** với tệp PDF làm đính kèm.

3. **Lưu log hoạt động**:
   - Thêm node **Sticky Note** hoặc **Database** (ví dụ: **Airtable**) để ghi lại lịch sử các lần chạy workflow.
   - **Cách làm**: Sử dụng node **Sticky Note - Create** để lưu thông tin như ngày chạy, số tệp PDF được hợp nhất.

4. **Tự động xóa tệp cũ**:
   - Thêm node **Google Drive - Delete** để xóa các tệp PDF đã được hợp nhất sau khi báo cáo thống nhất được tạo.
   - **Lưu ý**: Cần cẩn thận để không xóa nhầm tệp quan trọng.

5. **Báo cáo định kỳ qua Slack/Telegram**:
   - Tạo một **dashboards** trong Slack/Telegram để hiển thị trạng thái của báo cáo tài chính.
   - **Cách làm**: Sử dụng node **Slack - Post Message** với các thông tin như số tệp hợp nhất, thời gian chạy.

6. **Kết hợp với AI (LLM)**:
   - Sử dụng node **LLM** (ví dụ: **OpenAI**) để tự động tổng hợp dữ liệu từ báo cáo PDF thành báo cáo văn bản.
   - **Cách làm**: Sau khi hợp nhất PDF, sử dụng node **LLM - Chat** với prompt:
     ```json
     "Analyze the attached financial report and summarize the key metrics: revenue, expenses, and profit."
     ```
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để các sếp tự động hóa quy trình báo cáo tài chính tháng hàng, tiết kiệm thời gian và tránh sai sót. Với chỉ **cấu hình đơn giản** và **chạy tự động hàng tháng**, các sếp có thể tập trung vào việc phân tích dữ liệu thay vì làm thủ công.

**Hành động ngay hôm nay:**
1. **Chuẩn bị credentials** (Google Drive, HTML/CSS to PDF, Slack).
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Test run** với dữ liệu mẫu.
4. **Bật Active** và để workflow chạy tự động vào ngày 1 hàng tháng!

**🎁 Đăng ký VPS cho n8n tại TinoHost với mã giảm giá VPSN8N (giảm 39%) để workflow chạy ổn định 24/7:**
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)

---
**Chúc các sếp thành công với tự động hóa tài chính!** 🚀