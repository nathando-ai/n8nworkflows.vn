---
title: "🚀 Tự Động Hoàn Chỉnh & Đăng Tất Cả Nội Dung Instagram (Image, Story, Reels, Carousel) Với Facebook Graph API - N8n"
description: "Workflow tự động hóa 100% không code để các sếp lên kế hoạch, chuẩn bị và đăng tất cả các loại nội dung Instagram (ảnh, story, video, carousel) lên Instagram Business Account thông qua Facebook Graph API, tiết kiệm thời gian lên tới 80% so với cách làm thủ công."
slug: "tu-dong-hoan-chinh-dang-tat-ca-noi-dung-instagram"
tags: [n8n, automation, marketing, instagram, facebook-graph-api, no-code]
keywords: [tự động hóa instagram, đăng bài instagram tự động, facebook graph api n8n, workflow instagram carousel, tự động hóa marketing social media]
---

# 🚀 **Tự Động Hoàn Chỉnh & Đăng Tất Cả Nội Dung Instagram (Image, Story, Reels, Carousel) Với Facebook Graph API**

### **Nỗi Đau Của Các Sếp**
Các sếp đang phải mất **giờ đồng hồ** mỗi ngày để:
- **Chuẩn bị nội dung** cho từng loại bài viết (ảnh, story, video, carousel) trên Instagram.
- **Chờ đợi** khi Instagram xử lý file (thời gian upload có thể kéo dài từ 5-30 phút).
- **Đăng thủ công** từng loại nội dung, dễ xảy ra lỗi hoặc quên lịch.
- **Không thể tự động hóa** vì không biết code hoặc không có API key hợp lệ.

**Workflow này giải quyết tất cả!** Các sếp chỉ cần **nhấp chuột** để lên kế hoạch, hoàn chỉnh và đăng **tất cả các loại nội dung Instagram** (ảnh, story, video, carousel) **tự động** qua Facebook Graph API, **không cần viết một dòng code nào!**

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên một VPS chuyên dụng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao, không lag)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên tới 80%** so với cách làm thủ công.
- **Đăng tự động** tất cả loại nội dung (ảnh, story, video, carousel) **không cần code**.
- **Kiểm tra trạng thái xử lý** và **retry tự động** nếu upload thất bại.
- **Lên lịch đăng** theo thời gian cụ thể (ví dụ: 9h sáng, 15h chiều).
- **Hỗ trợ cả API HTTP và Facebook Graph API**, linh hoạt cho nhiều tài khoản.
- **Lưu log đầy đủ** để theo dõi quá trình upload và xử lý.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Instagram Business** (đã kết nối với Facebook Page).
2. **Facebook Developer Account** và **API Access Token** (có quyền `instagram_basic`, `pages_show_list`, `pages_read_engagement`).
3. **API Key cho Instagram Business API** (cài đặt trong [Facebook Developer Dashboard](https://developers.facebook.com/)).
4. **Tài khoản n8n** (self-hosted hoặc dùng n8n.cloud).
5. **Danh sách nội dung sẵn sàng** (ảnh, video, carousel) được upload lên **Instagram Business Account** trước khi workflow chạy.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/4498) (hoặc sử dụng link gốc).
- Trong **n8n Editor**, nhấn **Import** → Chọn file JSON → **Load**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **22 node** và **2 hệ thống chính**:
- **Hệ thống xử lý container** (tạo, chờ xử lý, kiểm tra trạng thái).
- **Hệ thống đăng bài tự động** (sử dụng HTTP API hoặc Facebook Graph API).

##### **A. Cấu Hình Credentials (API Key)**
Các sếp cần **cấu hình credentials** cho các node **Facebook Graph API** và **HTTP Request**:
1. **Facebook Graph API**:
   - Trong **n8n**, đi đến **Credentials** → **Add Credential** → Chọn **Facebook Graph API**.
   - Điền:
     - **Access Token**: API Key từ [Facebook Developer](https://developers.facebook.com/) (có quyền `instagram_basic`).
     - **Page ID**: ID của Facebook Page đã kết nối với Instagram Business.
     - **Version**: Chọn **v18.0** (hoặc phiên bản mới nhất).
   - **Lưu** và **gán** cho các node:
     - `Container FB Image`
     - `Container FB Story Image`
     - `Container FB Reels`
     - `Container FB Story Video`
     - `📤 Publish via Facebook SDK`

2. **HTTP Header Auth (nếu sử dụng API HTTP)**:
   - Trong **Credentials**, thêm **HTTP Header Auth**.
   - Điền:
     - **URL**: `https://graph.instagram.com/...` (nếu sử dụng API HTTP).
     - **Headers**: Thêm `Authorization: Bearer {API_KEY}`.
   - **Gán** cho các node:
     - `Container HTTP Image`
     - `Container HTTP Reels`
     - `Container HTTP Story Image`
     - `Container HTTP Story Video`
     - `Container HTTP Carousel`
     - `📤 Publish via HTTP API`

##### **B. Cấu Hình Node Quản Lý Container**
Workflow sử dụng **các node `httpRequest` và `facebookGraphApi`** để:
1. **Tạo container** cho từng loại nội dung (ảnh, video, carousel).
2. **Chờ container xử lý xong** (thời gian ~5-30 phút).
3. **Kiểm tra trạng thái** và **retry tự động** nếu chưa hoàn thành.

**Cách cấu hình:**
- Mở node **⏰ Initial Processing Wait** → Đặt **thời gian chờ** (ví dụ: **30 giây**).
- Mở node **⏰ Retry Wait Loop** → Đặt **thời gian retry** (ví dụ: **5 phút**).
- Mở node **🔍 Check Processing Status** → Chọn **trạng thái "FINISHED"** để tiếp tục.

##### **C. Cấu Hình Node Đăng Bài Tự Động**
Workflow **auto-routing** dựa trên **prefix** của `post_type`:
- **`http_*`** → Sử dụng **HTTP Request**.
- **`fb_*`** → Sử dụng **Facebook Graph API**.

**Cách kiểm tra:**
- Mở node **🔀 HTTP vs FB API Router** → Đảm bảo **điều kiện if** đúng:
  - Nếu `post_type` bắt đầu bằng `http_` → Chạy **📤 Publish via HTTP API**.
  - Nếu `post_type` bắt đầu bằng `fb_` → Chạy **📤 Publish via Facebook SDK**.

##### **D. Cấu Hình Node Manual Trigger**
- Node **🚀 Manual Trigger - Start Workflow** cho phép các sếp **bắt đầu workflow thủ công** khi cần.
- **Không cần cấu hình thêm**, chỉ cần **nhấn "Execute"** khi muốn chạy.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với **dữ liệu mẫu**:
   - Sử dụng **node `Set`** để mock dữ liệu (ví dụ: `post_type: "fb_image"`, `media_url: "https://..."`).
   - Chạy **Test Execution** để kiểm tra workflow hoạt động như thế nào.
2. **Bật Active Workflow**:
   - Sau khi test thành công, **bật `Active`** và **lưu workflow**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram để báo cáo**:
   - Thêm **node `Slack`** hoặc **`Telegram Bot`** sau node **📤 Publish via Facebook SDK** để thông báo khi đăng bài thành công/thất bại.
   - **Cách làm**:
     ```json
     {
       "node": "slack",
       "type": "slack",
       "credentials": {
         "slackApiToken": "xoxb-your-token",
         "channel": "#n8n-instagram"
       },
       "options": {
         "text": "🚀 Bài {{ $node["📤 Publish via Facebook SDK"].json()["post_type"] }} đã đăng thành công!"
       }
     }
     ```

2. **Lưu log vào Google Sheets/Notion**:
   - Thêm **node `Google Sheets`** sau node **🔍 Check Processing Status** để ghi lại:
     - Thời gian upload.
     - Trạng thái thành công/thất bại.
     - Link bài đăng.
   - **Cách làm**:
     ```json
     {
       "node": "googleSheets",
       "type": "googleSheets",
       "credentials": {
         "apiKey": "your-api-key",
         "spreadsheetId": "your-spreadsheet-id",
         "sheetName": "Instagram_Logs"
       },
       "options": {
         "range": "A1",
         "values": [
           ["Thời gian", "Loại bài", "Trạng thái", "Link"],
           [new Date().toISOString(), "{{ $node["📤 Publish via Facebook SDK"].json()["post_type"] }}", "{{ $node["🔍 Check Processing Status"].json()["status"] }}", "{{ $node["📤 Publish via Facebook SDK"].json()["link"] }}"]
         ]
       }
     }
     ```

3. **Tự động gửi báo cáo hàng tuần**:
   - Sử dụng **node `Set`** + **`Date`** để tính ngày cuối tuần.
   - Thêm **node `Email`** (ví dụ: Gmail) để gửi báo cáo tổng hợp:
     ```json
     {
       "node": "email",
       "type": "email",
       "credentials": {
         "email": "your-email@gmail.com",
         "password": "your-app-password"
       },
       "options": {
         "to": "team@company.com",
         "subject": "Báo cáo nội dung Instagram tuần {{ $node["Date"].json()["week"] }}",
         "html": "Xin chào,\n\nDưới đây là báo cáo nội dung Instagram được đăng tự động:\n{{ $json["report"] }}"
       }
     }
     ```

4. **Optimize thời gian chờ**:
   - Nếu upload **video Reels** hoặc **carousel** mất nhiều thời gian, tăng **thời gian chờ** trong node **⏰ Retry Wait Loop** lên **10-15 phút**.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy marketing** thay vì **công việc thủ công lặp đi lặp lại**. Với **Facebook Graph API** và **n8n**, các sếp có thể:
✅ **Đăng tất cả loại nội dung** (ảnh, story, video, carousel) **tự động**.
✅ **Kiểm tra và retry tự động** nếu upload thất bại.
✅ **Lên lịch đăng** theo thời gian cụ thể.
✅ **Lưu log và báo cáo** để theo dõi hiệu quả.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình credentials** (API Key Facebook).
3. **Test run** với dữ liệu mẫu.
4. **Bật Active** và **đăng bài tự động**!

**Nếu gặp vấn đề**, các sếp có thể:
- **Comment trên video gốc** của Lakshit Ukani.
- **Giới thiệu trong cộng đồng Skool**: [AI Automation Club](https://www.skool.com/ai-automation-club-7843).
- **Liên hệ trực tiếp** qua LinkedIn: [Lakshit Ukani](https://www.linkedin.com/in/lakshit-ukani/).

**Chúc các sếp thành công với chiến dịch marketing tự động hóa!** 🚀