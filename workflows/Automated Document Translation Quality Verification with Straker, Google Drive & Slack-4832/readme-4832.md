---
title: "🌍 Tự Động Hóa Kiểm Tra Chất Lượng Dịch Văn Bản với Straker, Google Drive & Slack - Không Cần Code!"
description: "Giải pháp tự động hóa hoàn toàn kiểm tra chất lượng dịch văn bản từ Google Drive sang Straker Verify, sau đó lưu kết quả vào Google Drive và thông báo trên Slack. Tiết kiệm thời gian 80% cho các sếp và đảm bảo độ chính xác cao."
slug: "tieu-dong-hoa-kiem-tra-chat-luong-dich-van-ban-straker-google-drive-slack"
tags: [n8n, automation, no-code, ai, google-drive, straker-verify, slack, translation]
keywords: [n8n workflow dịch văn bản, tự động hóa dịch thuật, Straker Verify API, Google Drive tự động hóa, Slack thông báo tự động, kiểm tra chất lượng dịch]
---

# 🚀 Tự Động Hóa Kiểm Tra Chất Lượng Dịch Văn Bản với Straker, Google Drive & Slack

### 🔍 **Nỗi Đau Của Các Sếp**
Hiện nay, việc dịch thuật và kiểm tra chất lượng dịch văn bản thường là công việc tốn thời gian, dễ sai sót và đòi hỏi sự theo dõi thủ công. Các sếp phải:
- **Tải xuống** file từ Google Drive.
- **Gửi dịch** qua Straker Verify.
- **Chờ đợi** kết quả và **kiểm tra** chất lượng.
- **Lưu lại** kết quả dịch và **thông báo** cho đội nhóm.

Quá trình này không chỉ tốn nhiều thời gian mà còn dễ xảy ra lỗi do con người. **Workflow này tự động hóa toàn bộ quy trình, giảm thiểu sai sót và tiết kiệm thời gian cho các sếp!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công từ đầu đến cuối.
- **Chất lượng cao**: Kiểm tra dịch qua Straker Verify, đảm bảo độ chính xác.
- **Tiết kiệm thời gian**: Giảm thiểu công việc lặp đi lặp lại, cho phép các sếp tập trung vào công việc chiến lược.
- **Thông báo tức thời**: Kết quả dịch được lưu vào Google Drive và thông báo ngay trên Slack.
- **Hoạt động liên tục**: Workflow chạy 24/7, không phụ thuộc vào giờ làm việc.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Straker Verify**:
   - API Key của Straker Verify (xem [hướng dẫn](https://api-verify.straker.ai/docs)).
   - Thiết lập **credentials** trong n8n với tên `strakerVerifyApi`.
2. **Tài khoản Google Drive**:
   - OAuth 2.0 API Key (xem [hướng dẫn](https://developers.google.com/drive/api/v3/quickstart/python)).
   - Thiết lập **credentials** trong n8n với tên `googleDriveOAuth2Api`.
3. **Tài khoản Slack**:
   - Token Slack (xem [hướng dẫn](https://api.slack.com/apps)).
   - Thiết lập **credentials** trong n8n với tên `slackToken`.
4. **Folder Google Drive**:
   - **Folder Input**: Để đặt file cần dịch (ví dụ: `Dịch Văn Bản`).
   - **Folder Output**: Để lưu kết quả dịch (ví dụ: `Dịch Xong`).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### 1. **Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON**: [Tải workflow từ n8n.io](https://n8n.io/workflows/4832).
- **Import**:
  1. Mở **n8n Editor**.
  2. Nhấn **Import** và chọn file JSON.
  3. Hoặc copy toàn bộ JSON và dán vào **Import Workflow** trong Editor.

#### 2. **Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này bao gồm **10 node** với các bước chính sau:

##### **Bước 1: Nhận File Từ Google Drive**
- **Node: `Watch Input Folder` (Google Drive Trigger)**
  - **Cấu hình**:
    - Chọn `googleDriveOAuth2Api` trong **Credentials**.
    - Điền **Folder ID** của `Folder Input` (tham khảo [hướng dẫn lấy Folder ID](https://support.google.com/drive/answer/188155)).
    - Chọn **File Type**: `Google Docs`, `Text Files`, `PDF`, hoặc `Excel` tùy thuộc vào loại file cần dịch.

##### **Bước 2: Tải File Xuống**
- **Node: `Download Files` (Google Drive)**
  - **Cấu hình**:
    - Chọn `googleDriveOAuth2Api` trong **Credentials**.
    - Đảm bảo **File ID** được truyền từ node `Watch Input Folder`.

##### **Bước 3: Gửi File Đến Straker Verify**
- **Node: `Start Translation` (Straker Verify - Create)**
  - **Cấu hình**:
    - Chọn `strakerVerifyApi` trong **Credentials**.
    - **Parameters**:
      - `projectTitle`: Tên dự án dịch (ví dụ: `Dịch Văn Bản Tháng 6`).
      - `targetLanguage`: Ngôn ngữ mục tiêu (ví dụ: `en` cho tiếng Anh).
      - `workflowId`: ID của workflow Straker Verify (tham khảo [hướng dẫn](https://api-verify.straker.ai/docs)).
      - `file`: File cần dịch (được truyền từ node `Download Files`).

##### **Bước 4: Chờ Kết Quả Dịch**
- **Node: `Wait for Completion` (Webhook)**
  - **Cấu hình**:
    - **Path**: `6540f764-161d-4627-b78a992daf1d` (không thay đổi).
    - **HTTP Method**: `POST`.
  - **Lưu ý**: Straker Verify sẽ gọi lại URL này khi dịch xong. Đảm bảo **Webhook URL** trong Straker Verify trùng với URL của node này (tham khảo [hướng dẫn Straker Verify](https://api-verify.straker.ai/docs)).

##### **Bước 5: Lấy Thông Tin Dự Án**
- **Node: `Fetch Job Info` (Straker Verify - Get)**
  - **Cấu hình**:
    - Chọn `strakerVerifyApi` trong **Credentials**.
    - **Parameters**:
      - `jobId`: ID của dự án dịch (được truyền từ node `Start Translation`).

##### **Bước 6: Lấy File Dịch Xong**
- **Node: `Grab Translation` (Straker Verify - File: Get)**
  - **Cấu hình**:
    - Chọn `strakerVerifyApi` trong **Credentials**.
    - **Parameters**:
      - `fileId`: ID của file dịch (được truyền từ node `Fetch Job Info`).

##### **Bước 7: Lưu File Dịch Vào Google Drive**
- **Node: `Save to Output Folder` (Google Drive)**
  - **Cấu hình**:
    - Chọn `googleDriveOAuth2Api` trong **Credentials**.
    - **Parameters**:
      - `folderId`: ID của `Folder Output`.
      - `fileName`: Tên file dịch (ví dụ: `Dịch_<tên_file_ban_dau>.pdf`).

##### **Bước 8: Thông Báo Trên Slack**
- **Node: `Notify` (Slack)**
  - **Cấu hình**:
    - Chọn `slackToken` trong **Credentials**.
    - **Message**: Thông báo mẫu (ví dụ: `📄 File dịch xong: <tên_file> đã được lưu vào Google Drive!`).
    - **Channel**: Chọn kênh Slack cần thông báo.

##### **Bước 9: Flatten Dữ Liệu (Nếu Cần)**
- **Node: `Flatten` (Code)**
  - **Lưu ý**: Node này được sử dụng để chuẩn hóa dữ liệu trước khi truyền sang các node khác. **Không cần chỉnh sửa** nếu workflow đã được cấu hình đúng.

##### **Bước 10: Aggregate (Nếu Có Nhiều File)**
- **Node: `Aggregate`**
  - **Lưu ý**: Node này được sử dụng để hợp nhất dữ liệu từ nhiều file. **Không cần chỉnh sửa** nếu workflow chỉ xử lý 1 file.

---

#### 3. **Kích Hoạt ⚡️**
1. **Test Run**:
   - Đặt 1 file mẫu vào `Folder Input`.
   - Chạy **Manual Trigger** trên node `Watch Input Folder`.
   - Kiểm tra kết quả:
     - File dịch được lưu vào `Folder Output`.
     - Thông báo Slack xuất hiện.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Hợp Với LLM (AI) Kiểm Tra Chất Lượng**:
   - Sau khi dịch xong, sử dụng **node `n8n-nodes-base.llm`** (ví dụ: OpenAI) để kiểm tra chất lượng dịch bằng cách so sánh với bản gốc.
   - **Cách làm**:
     - Thêm node `LLM` sau `Grab Translation`.
     - Gửi **bản gốc + bản dịch** vào prompt để AI đánh giá.
     - Lưu kết quả vào Google Drive hoặc Slack.

2. **Lưu Log Lịch Sử Dịch**:
   - Thêm node **Google Sheets** hoặc **Notion** để ghi lại lịch sử dịch:
     - **Node**: `Google Sheets` (n8n-nodes-base.googleSheets).
     - **Cấu hình**:
       - Thêm cột: `Tên File`, `Ngày Dịch`, `Ngôn Ngữ`, `Trạng Thái`, `Link File`.
     - **Lợi ích**: Theo dõi được tất cả các file đã dịch và trạng thái của chúng.

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **node `n8n-nodes-base.cron`** để chạy workflow định kỳ (ví dụ: hàng tuần) để kiểm tra file mới trong `Folder Input`.
   - **Cấu hình**:
     - Thiết lập lịch: `0 0 * * 1` (mỗi thứ 2 hàng tuần).
     - **Lợi ích**: Không cần phải kích hoạt thủ công.

4. **Thêm Nhận Dạng File Tự Động**:
   - Sử dụng **node `n8n-nodes-base.code`** để thêm logic nhận dạng loại file (PDF, DOCX, TXT) và chọn workflow dịch phù hợp.
   - **Ví dụ**:
     ```javascript
     // Node Code để phân loại file
     $input.all().forEach((file) => {
       if (file.name.endsWith('.pdf')) {
         file.type = 'pdf';
       } else if (file.name.endsWith('.docx')) {
         file.type = 'docx';
       } else {
         file.type = 'txt';
       }
     });
     ```

5. **Thông Báo Trên Telegram**:
   - Thay vì Slack, các sếp có thể sử dụng **node `n8n-nodes-base.telegram`** để gửi thông báo:
     - **Cấu hình**:
       - Thêm `telegramBotToken` trong credentials.
       - Gửi tin nhắn mẫu: `📄 File dịch xong: [Tên File]`.

---

### 📌 **Kết Luận**
Workflow này **tự động hóa hoàn toàn** quy trình dịch thuật và kiểm tra chất lượng, giúp các sếp:
✅ **Tiết kiệm thời gian** lên đến 80%.
✅ **Đảm bảo độ chính xác** với Straker Verify.
✅ **Lưu trữ và theo dõi** dễ dàng trên Google Drive và Slack.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**Hãy áp dụng ngay workflow này để nâng cao hiệu suất dịch thuật của doanh nghiệp!**
👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/4832) và bắt đầu tự động hóa ngay hôm nay!

---
**Chia sẻ & phản hồi**:
Nếu các sếp có bất kỳ câu hỏi hoặc cần hỗ trợ, hãy để lại comment bên dưới hoặc liên hệ qua [n8n Community](https://community.n8n.io/). Chúc các sếp thành công! 🚀