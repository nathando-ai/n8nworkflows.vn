---
title: "🎬 Tự Động Hoá Sáng Tạo Video AI Bulk với Freepik Minimax Hailuo + Google Suite - Không Cần Code"
description: "Workflow tự động hóa tạo video AI bulk từ text prompt, tự động upload lên Google Drive và quản lý quy trình từ đầu đến cuối. Giúp các sếp tiết kiệm 80% thời gian so với thủ công, đồng thời đảm bảo chất lượng và tính nhất quán cao."
slug: "tieu-dong-hoa-tao-video-ai-bulk-freepik-google-drive"
tags: [n8n, automation, ai-video-generation, google-suite, freepik, no-code, content-creation]
keywords: [n8n workflow video AI, tự động hóa tạo video bulk, Freepik Minimax Hailuo, Google Drive API, tự động hóa nội dung đa phương tiện]
---

# 🚀 **Tự Động Hoá Sáng Tạo Video AI Bulk: Từ Prompt → Video → Google Drive - Không Cần Code**

### **Nỗi Đau Của Các Sếp Trong Sáng Tạo Video AI**
Các sếp đang phải đối mặt với những thách thức lớn khi tạo nội dung video AI:
- **Thời gian dài**: Tạo một video AI thủ công từ đầu đến cuối có thể mất từ 10-30 phút/video.
- **Khó quản lý quy trình**: Không biết video đã hoàn thành hay bị lỗi, phải check thủ công liên tục.
- **Chất lượng không nhất quán**: Mỗi lần tạo video khác nhau, khó đảm bảo tính nhất quán.
- **Không tích hợp hệ thống**: Dữ liệu prompt và video phải được quản lý riêng biệt, gây rối loạn.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa toàn bộ quy trình** từ lấy prompt từ Google Sheets → tạo video AI bulk → kiểm tra trạng thái → download và upload lên Google Drive.
✅ **Tối ưu hóa thời gian**: Tạo **một loạt video** trong cùng một lần chạy, thay vì một video một lần.
✅ **Quản lý tự động**: Kiểm tra trạng thái video và tự động tiếp tục khi cần thiết.
✅ **Tích hợp Google Suite**: Lưu kết quả vào Google Drive với tên file tự động hóa, dễ quản lý.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tạo **5-10 video trong 1 lần chạy** thay vì 1 video/lần.
- **Chất lượng nhất quán**: Mỗi video được tạo từ cùng một template và quy trình.
- **Tự động hóa hoàn toàn**: Không cần check thủ công, workflow chạy 24/7.
- **Tích hợp Google Drive**: Video được tự động lưu vào folder đã chỉ định, dễ dàng chia sẻ hoặc sử dụng lại.
- **Không giới hạn số lượng**: Dễ dàng mở rộng để tạo hàng trăm video trong một lần chạy.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow này, các sếp cần chuẩn bị:
1. **Tài khoản Freepik Minimax Hailuo API**:
   - Đăng ký tại [Freepik AI](https://www.freepik.com/ai/) và lấy **API Key** (Generic HTTP Header Auth).
   - Cài đặt **n8n-nodes-base.httpRequest** và tạo **credentials** với tên `"Header Auth account"`:
     - **Type**: Generic → HTTP Header Auth
     - **Header Name**: `Authorization`
     - **Header Value**: `Bearer YOUR_API_KEY_HERE`

2. **Tài khoản Google OAuth2**:
   - Cài đặt **n8n-nodes-base.googleDrive** và **n8n-nodes-base.googleSheets**.
   - Tạo **credentials** với tên `"googleDriveOAuth2Api"` và `"googleSheetsOAuth2Api"`:
     - Chọn **Google Drive API** và **Google Sheets API**.
     - Cấp quyền cho n8n truy cập vào Google Drive và Google Sheets.

3. **Google Sheet chứa Prompt**:
   - Sử dụng **Google Sheet mẫu** từ [đây](https://docs.google.com/spreadsheets/d/1_u9IxEZINcwKQB15Rfx7C1hM71zeDST58Fz3nRHTCUY/edit).
   - Cấu trúc Sheet phải có **cột `Prompt`** (nội dung text cho video) và **cột `Name`** (tên video).
   - Ví dụ:
     | Name       | Prompt                                                                 |
     |------------|-------------------------------------------------------------------------|
     | Video 1    | A modern office with a sleek design and a person working on a laptop. |
     | Video 2    | A cozy bedroom with soft lighting and a comfortable bed.               |

4. **Folder Google Drive để lưu video**:
   - Tạo một **folder mới** trên Google Drive để lưu video tự động.
   - Lấy **Folder ID** của folder này (có thể tìm thấy trong URL khi mở folder trên trình duyệt).

5. **n8n Workflow**:
   - Cài đặt **n8n Self-hosted** (khuyến nghị) hoặc sử dụng n8n Cloud.
   - Cài đặt các **nodes** cần thiết: `code`, `wait`, `switch`, `googleDrive`, `googleSheets`, `httpRequest`, `splitInBatches`.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/7335) (hoặc copy toàn bộ JSON từ link trên).
- Trong **n8n Editor**, nhấn **Import** → Chọn file JSON hoặc dán JSON vào ô **Import Workflow**.
- Workflow sẽ tự động được tạo với **9 nodes** như mô tả.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp cần **cấu hình chi tiết** cho từng node quan trọng:

##### **A. Get prompt from google sheet (Google Sheets)**
- **Document ID**: Lấy từ URL của Google Sheet (phần sau `/d/` và trước `/edit`).
  - Ví dụ: Nếu URL là `https://docs.google.com/spreadsheets/d/1_u9IxEZINcwKQB15Rfx7C1hM71zeDST58Fz3nRHTCUY/edit`, thì **Document ID** là `1_u9IxEZINcwKQB15Rfx7C1hM71zeDST58Fz3nRHTCUY`.
- **Sheet Name**: Đặt là `Sheet1` (hoặc tên sheet của các sếp).
- **Credentials**: Chọn `"googleSheetsOAuth2Api"` (đã tạo trước đó).

##### **B. Duplicate Rows2 (Code Node)**
- **Mục đích**: Tạo **2 bản sao** của mỗi prompt để tạo video khác nhau (ví dụ: video 1 và video 2 từ cùng một prompt).
- **JavaScript Code** (không cần chỉnh sửa):
  ```javascript
  const original = items[0].json;

  return [
    { json: { ...original, run: 1 } },
    { json: { ...original, run: 2 } },
  ];
  ```
- **Lưu ý**: Nếu muốn tạo **3 bản sao**, chỉ cần thêm `{ json: { ...original, run: 3 } }` vào mảng `return`.

##### **C. Loop Over Items (Split in Batches)**
- **Mục đích**: Xử lý các prompt theo **lượt** để tránh bị giới hạn API.
- **Cấu hình**:
  - **Batch Size**: Giá trị mặc định (ví dụ: 5) là đủ.
  - **Reset**: Đặt là `false`.

##### **D. Create Video (HTTP Request)**
- **Method**: `POST`
- **URL**: `https://api.freepik.com/v1/ai/image-to-video/minimax-hailuo-02-768p`
- **Authentication**: Chọn `"Header Auth account"` (đã tạo trước đó).
- **Body Parameters**:
  - **Name**: `prompt`
  - **Value**: `={{ $json.Prompt }}` (lấy từ Google Sheet).

##### **E. Get Video URL (HTTP Request)**
- **Method**: `GET`
- **URL**: `https://api.freepik.com/v1/ai/image-to-video/minimax-hailuo-02-768p/{{ $json.data.task_id }}`
- **Authentication**: Chọn `"Header Auth account"`.
- **Timeout**: `120000` (2 phút) để API có thời gian hoàn thành.
- **Lưu ý**: Node này **polling** (kiểm tra trạng thái) video liên tục cho đến khi hoàn thành.

##### **F. Switch (Switch Node)**
- **Mục đích**: **Lọc video** theo trạng thái:
  - **Completed**: `{{ $json.data.status }}` == `COMPLETED` → Tiến đến node **Download Video**.
  - **Failed**: `{{ $json.data.status }}` == `FAILED` → Bỏ qua (không xử lý).
  - **In Progress**: `{{ $json.data.status }}` == `IN_PROGRESS` → Tiến đến node **Wait**.
  - **Created**: `{{ $json.data.status }}` == `CREATED` → Tiến đến node **Wait**.

##### **G. Wait (Wait Node)**
- **Amount**: `30` giây (thời gian chờ giữa các lần polling).
- **Mục đích**: Tránh quá tải API khi kiểm tra trạng thái video.

##### **H. Download Video as Base64 (HTTP Request)**
- **Method**: `GET`
- **URL**: `={{ $json.data.generated[0] }}` (lấy URL video từ API).
- **Lưu ý**: Node này **tải video** dưới dạng Base64 để chuẩn bị upload.

##### **I. Upload to Google Drive1 (Google Drive)**
- **Operation**: `Upload`
- **Name**: `=video - {{ $('Get prompt from google sheet').item.json.Name }} - {{ $('Duplicate Rows2').item.json.run }}`
  - **Ví dụ**: Nếu `Name` là "Video 1" và `run` là `1`, thì tên file sẽ là `video - Video 1 - 1.mp4`.
- **Drive ID**: `My Drive`
- **Folder ID**: Lấy từ folder Google Drive đã tạo trước đó.
- **Credentials**: Chọn `"googleDriveOAuth2Api"`.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Nhấn **Run Workflow** và chọn **Test** để chạy với dữ liệu mẫu.
- **Active Workflow**: Sau khi kiểm tra, nhấn **Active** để workflow chạy tự động.
- **Lưu ý**:
  - Nếu workflow bị **timeout**, tăng **Timeout** trong node `Get Video URL`.
  - Nếu gặp **lỗi API**, kiểm tra **API Key** của Freepik có đúng không.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Tích Hợp Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi video hoàn thành.
   - Ví dụ: Gửi tin nhắn `"Video '{{ $json.Name }}' đã hoàn thành!"` khi trạng thái là `COMPLETED`.

2. **Lưu Log vào Google Sheets**:
   - Thêm node **Google Sheets** sau node **Switch** để ghi log trạng thái (thành công/thất bại).
   - Cột mới có thể là `Status`, `Video URL`, `Time Completed`.

3. **Tự Động Xóa Video Thất Bại**:
   - Sử dụng node **Code** để xóa video từ Google Drive nếu trạng thái là `FAILED`.

4. **Tạo Video với Kích Thước Khác**:
   - Thay đổi URL API trong node **Create Video** để tạo video với độ phân giải khác (ví dụ: `720p` thay vì `768p`).

5. **Kết Hợp với YouTube**:
   - Sau khi upload lên Google Drive, thêm node **YouTube Upload** để tự động đăng video lên kênh YouTube.

6. **Tự Động Tạo Playlist**:
   - Sử dụng node **Google Drive** để tạo một **playlist** (folder) và thêm video mới vào đó.

7. **Báo Cáo Định Kỳ**:
   - Thêm node **Google Sheets** hoặc **Email** để gửi báo cáo hàng tuần về số lượng video tạo thành công/thất bại.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần tự động hóa **sáng tạo video AI bulk** một cách hiệu quả, không cần code. Bằng cách tích hợp **Freepik Minimax Hailuo**, **Google Sheets** và **Google Drive**, các sếp có thể:
✔ **Tiết kiệm thời gian** lên đến 80% so với thủ công.
✔ **Đảm bảo chất lượng** với quy trình tự động hóa.
✔ **Quản lý dễ dàng** với video được lưu tự động vào Google Drive.

**Hành động ngay hôm nay!**
1. Chuẩn bị tài khoản và credentials theo hướng dẫn.
2. Import workflow và cấu hình chi tiết.
3. Chạy thử và **tận hưởng sự tự động hóa hoàn toàn**!

---
:::note[CHÚ Ý]
- **Giám sát workflow**: Để tránh lỗi, các sếp nên **check log** trong n8n định kỳ.
- **API Rate Limit**: Freepik có giới hạn API. Nếu gặp lỗi, giảm **Batch Size** trong node `Split in Batches`.
- **Mở rộng**: Workflow này có thể được **customize** để sử dụng với các API video AI khác (ví dụ: Synthesia, Pictory).
:::

---
👉 **Cần hỗ trợ thêm?** Liên hệ với tác giả:
📧 [robert@ynteractive.com](mailto:robert@ynteractive.com)
🔗 [LinkedIn](https://www.linkedin.com/in/robert-breen-29429625/)

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::