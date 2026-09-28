---
title: "🚀 **Tự Động Hóa SEO Audit Tối Đa Với Screaming Frog, PageSpeed & Báo Cáo PDF/Excel - Không Cần Code**"
description: "Workflow này tự động thực hiện SEO audit chuyên nghiệp cho website bằng công cụ Screaming Frog CLI, đánh giá PageSpeed Insights, tạo báo cáo PDF/Excel cá nhân hóa và gửi kết quả trực tiếp qua Slack. Giúp các sếp tiết kiệm 10-15h/tháng, giảm thiểu lỗi thủ công và tối ưu hóa SEO liên tục."
slug: "tieu-dong-hoa-seo-audit-screaming-frog-pagespeed"
tags: [n8n, automation, seo, screaming-frog, google-pagespeed, google-drive, slack-integration, no-code]
keywords: [n8n workflow seo audit, tự động hóa seo với screaming frog, báo cáo seo pdf excel, seo audit automation, n8n seo tools, google pagespeed insights api]
---

# 🚀 **SEO Audit Tự Động Hóa Tối Đa: Từ URL → Báo Cáo PDF/Excel Trong 5 Phút**

Hãy tưởng tượng một ngày không phải mất **3-5 tiếng** để chạy SEO audit thủ công cho website, không phải lo lắng về **lỗi nhầm lẫn trong dữ liệu**, và không phải **chờ đợi kết quả** để báo cáo cho khách hàng. Với workflow này, **các sếp** có thể:
✅ **Nhập URL qua Slack** với lệnh `#Audit [URL]` và nhận báo cáo hoàn chỉnh trong **5 phút**.
✅ **Tích hợp Screaming Frog CLI** để crawl toàn bộ website (bao gồm nội dung, meta tags, backlinks, lỗi 404...).
✅ **Đánh giá PageSpeed Insights** để tối ưu tốc độ trang (Core Web Vitals, LCP, FID, CLS).
✅ **Tạo báo cáo PDF/Excel** với **màu sắc phân loại lỗi** (critical, warning, info) và **branding cá nhân hóa**.
✅ **Lưu trữ tự động** báo cáo lên Google Drive và ghi log vào Google Sheets.
✅ **Gửi kết quả trực tiếp** về Slack với liên kết truy cập.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm **90% công việc thủ công** so với cách làm truyền thống.
- **Chính xác 100%**: Không còn lỗi copy-paste hoặc bỏ sót dữ liệu như khi làm bằng tay.
- **Cá nhân hóa**: Thêm logo, tên công ty và thông tin liên hệ vào báo cáo.
- **Hoạt động 24/7**: Workflow chạy tự động khi có yêu cầu từ Slack, không cần can thiệp.
- **Dễ dàng chia sẻ**: Báo cáo PDF/Excel được upload lên Google Drive và gửi liên kết qua Slack.
- **Theo dõi lịch sử**: Tất cả kết quả audit được ghi log vào Google Sheets.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Slack**:
   - Một **Slack App** được cấu hình với quyền `chat:write` và `files:write`.
   - **Channel ID** của channel muốn nhận báo cáo (ví dụ: `D0ATVN7D5B4`).
   - **Slack API Token** (tạo từ [Slack API Credentials](https://api.slack.com/apps)).

2. **API Screaming Frog**:
   - Một **server Python FastAPI** chạy Screaming Frog CLI (cần cài đặt và cấu hình trước).
   - **Bearer Token** để xác thực với API (cập nhật trong nodes `Start Crawl` và `Check Crawl`).

3. **Google API Keys**:
   - **Google PageSpeed Insights API Key** (mở khóa trong [Google Cloud Console](https://console.cloud.google.com/)).
   - **PDFEndpoint API Key** (đăng ký tại [pdfendpoint.com](https://pdfendpoint.com/)).

4. **Google Drive & Sheets**:
   - **Folder ID** của thư mục `SEO Audits` trên Google Drive (tạo trước và chia sẻ cho n8n).
   - **Document ID** của Google Sheet dùng để ghi log kết quả audit.

5. **Branding cá nhân hóa**:
   - Tên công ty, email liên hệ, website và logo (sẽ được thêm vào báo cáo PDF/Excel).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### 1. **Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/15252) và import vào n8n.
- **Hoặc copy** toàn bộ JSON và dán vào **Create Workflow** → **Import from JSON**.

:::note[LƯU Ý]
- **Không** sử dụng phiên bản n8n Community nếu cần tính năng **Google Drive/Sheets** hoặc **PDF generation**.
- **Khuyến nghị** cài n8n trên **VPS** để workflow hoạt động 24/7.
:::

---
### 2. **Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **💬 Slack Trigger & Input Cleaner**
- **Node `Slack Trigger`**:
  - Đảm bảo **Slack App** đã được re-authenticate trong n8n.
  - Cập nhật **Channel ID** trong node này (ví dụ: `D0ATVN7D5B4`).
  - **Watermark** (logo hoặc chữ nhạt) sẽ được thêm vào báo cáo PDF. Cập nhật trong node `Input Cleaner`.

- **Node `Extract URL`**:
  - Đã sử dụng **RegEx** để trích xuất URL từ lệnh Slack (`#Audit [URL]`). Không cần chỉnh sửa.

#### **🕷️ Screaming Frog Crawl Loop**
- **Nodes `Start Crawl` và `Check Crawl`**:
  - Cập nhật **Bearer Token** trong header của cả hai node này (nếu đổi mật khẩu API).
  - **Cấu trúc API** phải trả về trạng thái crawl (`done`, `timeout`, `failed`).

#### **📥 Fetch & Unpack**
- **Node `Fetch`**:
  - Thêm **Token** vào header để tải file `.zip` từ server Screaming Frog.
  - Sau khi download, file sẽ được **nén giải nén** tự động.

#### **🧠 Parsing & PageSpeed Insights**
- **Node `Page Speed Insights`**:
  - **Thay thế** `Your-psi-api-key` trong **Query Parameters** bằng **Google API Key** của mình.
  - Ví dụ:
    ```json
    "key": "AIzaSyD123ABC...",  // Thay thế bằng key của bạn
    "url": "{{$json.url}}"
    ```

- **Nodes `SEO Audit Parser` và `Full Data Parser`**:
  - Đây là **code nodes** sử dụng JavaScript để xử lý dữ liệu CSV từ Screaming Frog.
  - **Không cần chỉnh sửa** trừ khi muốn thay đổi logic phân loại lỗi.

#### **📊 Excel & PDF Generation**
- **Node `Report Builder` (Code)**:
  - Tìm dòng `const AGENCY = { ... }` (tầm dòng 125) và cập nhật:
    ```javascript
    const AGENCY = {
      name: "Tên Công Ty Của Bạn",
      email: "contact@congty.com",
      website: "https://congty.com",
      logo: "https://congty.com/logo.png"
    };
    ```

- **Node `HTML TO PDF`**:
  - Thêm **Bearer Token** của `pdfendpoint.com` vào header:
    ```json
    "Authorization": "Bearer YOUR_PDFENDPOINT_API_KEY"
    ```

#### **☁️ Google Drive, Sheets & Slack Delivery**
- **Nodes `Upload file` và `Upload to Drive`**:
  - Cập nhật **Folder ID** của thư mục `SEO Audits` trên Google Drive.
  - Ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz` (lấy từ liên kết chia sẻ thư mục).

- **Node `Append row in sheet`**:
  - Chọn **Google Sheet** đã tạo để ghi log kết quả audit.
  - Cập nhật **Document ID** trong node này.

- **Nodes `Send Failed Message` và `Send Report`**:
  - Đảm bảo **Slack API Token** đã được cấu hình đúng.

---
### 3. **Kích hoạt ⚡️**
1. **Test run** với một URL mẫu (ví dụ: `https://example.com`).
2. Kiểm tra **Slack** để xác nhận báo cáo đã được gửi.
3. **Bật Active** workflow khi đã kiểm tra xong.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC TÍNH NĂNG MỞ RỘNG]
1. **Tích hợp với Trello/Notion**:
   - Sau khi hoàn thành audit, workflow có thể tự động tạo **task mới** trong Trello/Notion để theo dõi các lỗi cần sửa.

2. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n Scheduler** để chạy audit tự động hàng tuần/tháng cho các website quan trọng.

3. **Lưu log chi tiết**:
   - Thêm **Google Sheets** để ghi log tất cả lỗi (critical, warning) và trạng thái sửa chữa.

4. **Tích hợp với Email**:
   - Thay vì Slack, workflow có thể gửi báo cáo qua **Email** (sử dụng node `n8n-nodes-base.email`).

5. **Cập nhật tự động**:
   - Sử dụng **n8n Webhook** để nhận yêu cầu từ website hoặc CRM (HubSpot, Salesforce) thay vì Slack.
:::

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần **SEO audit tự động hóa**, tiết kiệm thời gian và giảm thiểu lỗi. Với **cấu hình đơn giản** và **tích hợp đa nền tảng** (Slack, Google Drive, Sheets, PDF), các sếp có thể:
✔ **Nhận báo cáo PDF/Excel** chỉ trong **5 phút**.
✔ **Tối ưu hóa SEO** một cách chuyên nghiệp.
✔ **Chia sẻ kết quả** dễ dàng với khách hàng.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với một URL** để đảm bảo hoạt động.
3. **Bật workflow** và bắt đầu tự động hóa SEO!

---
:::note[CHÚ Ý CUỐI CÙNG]
- **N8n Self-hosted** là lựa chọn tối ưu để workflow hoạt động 24/7.
- **Không có giới hạn số lượng audit** (tùy thuộc vào API limits của Google và Screaming Frog).
- **Cập nhật định kỳ** API keys nếu hết hạn.
:::

👉 **Bắt đầu tự động hóa SEO ngay hôm nay!** 🚀