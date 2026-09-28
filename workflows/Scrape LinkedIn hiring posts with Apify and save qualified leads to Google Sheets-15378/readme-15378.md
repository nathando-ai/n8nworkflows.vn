---
title: "🚀 Tự Động Hóa Scrape Bài Đăng Tuyển Dụng LinkedIn & Lọc Lãnh Đạo Chất Lượng Sẵn Sàng Xuất Bán"
description: "Workflow tự động hóa scrape tất cả bài đăng tuyển dụng LinkedIn theo keyword cụ thể, lọc bỏ nội dung không liên quan, xác minh ý định tuyển dụng thật, và lưu dữ liệu lead chất lượng vào Google Sheets. Giúp freelancer, agency và nhà tuyển dụng tiết kiệm 10+ giờ/ngày so với cách làm thủ công."
slug: "tieu-dung-linkedin-scrape-va-lay-lead-chat-luong"
tags: [n8n, automation, lead-generation, scraping, google-sheets, apify]
keywords: [tự động hóa scrape LinkedIn, tìm kiếm tuyển dụng tự động, lead generation LinkedIn, n8n workflow, tự động hóa tuyển dụng]
---

# 🚀 **Tự Động Hóa Scrape Bài Đăng Tuyển Dụng LinkedIn & Lọc Lãnh Đạo Chất Lượng**

## **Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hàng ngày, các sếp phải:
- **Tìm kiếm thủ công** trên LinkedIn để theo dõi các bài đăng tuyển dụng liên quan đến ngành nghề, công cụ hoặc kỹ năng của mình.
- **Lọc bỏ hàng trăm bài đăng không liên quan** (tips, sự kiện, tự quảng cáo, tuyển dụng tạm thời).
- **Xác minh ý định tuyển dụng thật** (những bài đăng "hire me" hoặc "open to work" không phải là cơ hội thực sự).
- **Nhập liệu vào Google Sheets** để theo dõi và liên hệ sau.

**Kết quả?** Tốn **10-15 giờ/ngày** cho một công việc đơn giản, dễ bị bỏ quên, và không đảm bảo độ chính xác.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Scrape** tất cả bài đăng tuyển dụng từ LinkedIn theo keyword của bạn.
✅ **Lọc bỏ** nội dung không liên quan (tips, tự quảng cáo, tuyển dụng tạm thời).
✅ **Xác minh** ý định tuyển dụng thật (sử dụng AI + logic tự động).
✅ **Trích xuất** thông tin liên lạc (email, số điện thoại, WhatsApp, liên kết ứng tuyển).
✅ **Lưu vào Google Sheets** để bạn có thể xuất bản và liên hệ ngay.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-15 giờ/ngày** so với cách làm thủ công.
- **Lọc chính xác** chỉ những bài đăng tuyển dụng thật, không bị "nội dung rác".
- **Dữ liệu sạch** với email, số điện thoại, WhatsApp và liên kết ứng tuyển.
- **Hoạt động liên tục** (thiết lập chạy tự động mỗi 6 giờ).
- **Xuất bản lead chất lượng** vào Google Sheets để liên hệ ngay.
- **Cập nhật liên tục** mà không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Apify** (để scrape LinkedIn):
   - [Đăng ký miễn phí Apify](https://apify.com/) và lấy **API Key**.
   - Cài đặt **n8n-node-apify** trong n8n (nếu chưa có).
2. **Google Sheets OAuth2**:
   - Tạo một **Google Sheet mới** để lưu lead.
   - Cấu hình **Google Sheets OAuth2** trong n8n.
3. **DataTable (Google Sheets) để lưu trữ lịch sử**:
   - Tạo một **Google Sheet mới** với tên **"Post Job Scraper"** và một cột duy nhất: `post_ID` (dùng để tránh trùng lặp).
4. **Danh sách keyword tuyển dụng**:
   - Danh sách **công việc** và **công cụ/ngành nghề** bạn quan tâm (ví dụ: "n8n", "Zapier", "Make", "Developer", "Marketing").

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15378](https://n8n.io/workflows/15378) hoặc copy/paste JSON từ trang này.
- Mở **n8n Editor** → **Import Workflow** → Chọn file JSON đã tải.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **A. Cấu Hình Node "Get Posts" (Apify)**
- **Tham số quan trọng**:
  - **`urls`**: Điền **URL search LinkedIn** của bạn (ví dụ: `https://www.linkedin.com/search/results/people/?keywords=n8n%20developer&origin=SWITCH_SEARCH_VERTICAL`).
  - **`limitPerSource`**: Số bài đăng scrape mỗi URL (mặc định 150, có thể tăng giảm).
  - **Credentials**: Chọn **`apifyApi`** (đã cấu hình trước khi import).

##### **B. Cấu Hình Node "Append row in sheet" (Google Sheets)**
- **Tham số quan trọng**:
  - **Google Sheet ID**: Thay thế bằng **ID của Google Sheet** bạn muốn lưu lead (tìm trong URL của Sheet).
  - **Credentials**: Chọn **`googleSheetsOAuth2Api`** (đã cấu hình trước).

##### **C. Cấu Hình Node "Match Job Title" (Lọc theo keyword)**
- **Logic AND**:
  - **Bài đăng phải chứa tên công cụ** (ví dụ: `n8n`, `Zapier`).
  - **Bài đăng phải chứa ít nhất một trong các keyword tuyển dụng** (ví dụ: `Developer`, `Marketing`, `Sales`).
- **Cách chỉnh**:
  - Mở node này → Thay thế `n8n` bằng tên công cụ của bạn.
  - Thêm/bỏ keyword tuyển dụng theo nhu cầu.

##### **D. Cấu Hình Node "If Job Not in Database" (Tránh trùng lặp)**
- **DataTable liên kết**:
  - Chọn **Google Sheet "Post Job Scraper"** (đã tạo trước).
  - Cột `post_ID` phải khớp với cột trong DataTable.

##### **E. Cấu Hình Node "Check Hiring Intent" (Xác minh ý định tuyển dụng)**
- **Không cần chỉnh** (sử dụng logic AI mặc định với 35+ từ khóa tuyển dụng).

##### **F. Cấu Hình Node "Enrich Data" (Trích xuất thông tin liên lạc)**
- **Không cần chỉnh** (node này tự động trích xuất email, số điện thoại, WhatsApp, liên kết ứng tuyển).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn **Test Run** để kiểm tra workflow với dữ liệu mẫu.
   - Kiểm tra **Google Sheets** xem có xuất lead không.
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tăng tần suất scrape**:
   - Thay đổi **Schedule Trigger** từ 6 giờ/lần thành 1-2 giờ/lần (nếu cần cập nhật nhanh).
2. **Lưu log hoạt động**:
   - Thêm node **Slack/Telegram** để nhận thông báo khi có lead mới.
3. **Gửi báo cáo định kỳ**:
   - Sử dụng **Google Apps Script** để tự động gửi báo cáo lead mới qua email hàng tuần.
4. **Tích hợp CRM**:
   - Thay vì Google Sheets, có thể kết nối với **HubSpot**, **Salesforce** hoặc **Notion** để quản lý lead.
5. **Cập nhật keyword tự động**:
   - Sử dụng **AI (LLM)** để tự động cập nhật danh sách keyword tuyển dụng theo xu hướng mới.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc tẻ nhạt là scrape và lọc bài đăng tuyển dụng LinkedIn. Với **tự động hóa 100%**, bạn sẽ:
✔ **Nhận lead chất lượng** mỗi ngày.
✔ **Tiết kiệm hàng giờ** so với cách làm thủ công.
✔ **Xuất bản và liên hệ ngay** mà không cần can thiệp.

**Hãy áp dụng ngay!** Cài đặt workflow, cấu hình theo hướng dẫn, và bắt đầu **tự động hóa tuyển dụng** của mình từ hôm nay.

---
**💡 Lưu ý cuối cùng**:
- Nếu gặp vấn đề với **Apify**, kiểm tra **API Key** và **quota** (Apify có giới hạn scrape miễn phí).
- Nếu **Google Sheets không xuất dữ liệu**, kiểm tra **permissions** và **Sheet ID**.
- **Không cần code** – workflow đã sẵn sàng để chạy ngay!