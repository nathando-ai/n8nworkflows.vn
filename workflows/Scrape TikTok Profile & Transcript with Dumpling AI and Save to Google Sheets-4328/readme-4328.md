---
title: "🚀 Tự Động Hóa Scrape TikTok + Trích Lời Chuyển Thể & Lưu Trữ Trên Google Sheets (Không Cần Code)"
description: "Workflow tự động theo dõi Google Sheet để lấy liên kết TikTok mới, trích xuất thông tin tài khoản và lời thoại video bằng Dumpling AI, rồi lưu kết quả vào Sheet. Giúp các sếp tiết kiệm 10+ giờ/tháng và có dữ liệu chi tiết cho phân tích nội dung."
slug: "tieu-dong-hoa-scrape-tiktok-dumpling-ai-google-sheets"
tags: [n8n, automation, tiktok-scraper, ai, google-sheets, dumpling-ai]
keywords: [tự động hóa tiktok, scrape tiktok bằng n8n, dumpling ai tiktok, lưu trữ tiktok trên google sheets, tự động hóa nội dung social media]
---

# 🚀 **Tự Động Hóa Scrape TikTok + Trích Lời Chuyển Thể & Lưu Trữ Trên Google Sheets**

### **Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Các sếp thường phải:
- **Tìm kiếm và sao chép** liên kết TikTok từ hàng ngàn video.
- **Trích xuất thông tin tài khoản** (số follower, video count, engagement) bằng cách truy cập từng profile.
- **Lấy lời thoại video** bằng cách xem trực tiếp hoặc sử dụng công cụ third-party.
- **Ghi chép dữ liệu vào Google Sheets** một cách thủ công, dễ bị lỗi và mất thời gian.

**Workflow này giải quyết tất cả bằng tự động hóa 100% không cần code!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 mà không gián đoạn, các sếp nên **self-host n8n** trên VPS ổn định.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
- **Tiết kiệm 10+ giờ/tháng** bằng việc loại bỏ công việc trích xuất thủ công.
- **Dữ liệu chính xác và cập nhật liên tục** khi mới có liên kết TikTok trong Sheet.
- **Lời thoại video được trích xuất tự động**, không cần xem trực tiếp.
- **Thông tin tài khoản (stats) được tổng hợp** (follower, video count, engagement).
- **Hoạt động 24/7** mà không cần can thiệp người dùng.

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** với quyền chỉnh sửa file chứa liên kết TikTok.
2. **API Key Dumpling AI** (đăng ký tại [Dumpling AI](https://dumpling.ai/)).
3. **Credentials OAuth2 cho Google Sheets** (cài đặt trong n8n).
4. **File Google Sheet** có cột chứa liên kết TikTok (ví dụ: `TikTok_URL`).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/4328](https://n8n.io/workflows/4328).
- Trong **n8n Editor**, nhấn `Import` và chọn file JSON.
- **Hoặc** copy toàn bộ JSON và paste vào `Import Workflow` trong Editor.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **Node 1: Watch for New TikTok Links in Sheet**
- **Chọn Sheet và Sheet Name** trong `googleSheetsTrigger`.
- **Chọn cột chứa liên kết TikTok** (ví dụ: `TikTok_URL`).
- **Lưu ý**: Sheet phải có **trạng thái "Active"** để workflow phát hiện thay đổi.

##### **Node 2: Extract Username from TikTok URL**
- **Không cần chỉnh sửa** vì node này tự động trích xuất username từ URL bằng Regex.
- **Kiểm tra**: Sau khi chạy test, username sẽ được trích xuất từ URL ví dụ `https://www.tiktok.com/@username/video/123456` → `@username`.

##### **Node 3 & 4: Get TikTok Profile Data & Transcript (Dumpling AI)**
- **Thêm `httpHeaderAuth`** (nếu chưa có):
  - `URL`: `https://api.dumpling.ai/v1/...` (đăng ký API key tại Dumpling AI).
  - **Headers**:
    - `Authorization`: `Bearer <API_KEY>`.
    - `Content-Type`: `application/json`.
  - **Body (Request Payload)**:
    - **Profile Data**:
      ```json
      {
        "username": "{{ $node["Extract Username from TikTok URL"].json["username"] }}"
      }
      ```
    - **Transcript**:
      ```json
      {
        "url": "{{ $node["Watch for New TikTok Links in Sheet"].json["TikTok_URL"] }}"
      }
      ```
- **Lưu ý**:
  - Dumpling AI có **hạn chế free tier** (kiểm tra tài liệu API).
  - Nếu API bị lỗi, kiểm tra **API Key** và **URL endpoint** trong Dumpling AI.

##### **Node 5: Save Profile Stats and Transcript to Google Sheet**
- **Chọn Sheet và Sheet Name** tương tự Node 1.
- **Chọn cột mục tiêu** (ví dụ: `Profile_Stats`, `Transcript`).
- **Kiểm tra `operation: append`** để dữ liệu mới được thêm vào cuối Sheet.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Thêm 1 liên kết TikTok vào Sheet.
  - Chạy **Manual Trigger** trong Node 1 để kiểm tra kết quả.
  - Kiểm tra Sheet xem dữ liệu đã được cập nhật chưa.
- **Bật Active**:
  - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` để thông báo khi có dữ liệu mới.
   - **Cách làm**:
     ```json
     {
       "operation": "sendMessage",
       "text": "🚀 TikTok Video: {{ $node["Watch for New TikTok Links in Sheet"].json["TikTok_URL"] }} đã được scrape!"
     }
     ```

2. **Lưu Log Dữ Liệu**:
   - Thêm node `n8n-nodes-base.set` để lưu **thời gian scrape** và **status** (thành công/thất bại).
   - **Cột mới trong Sheet**: `Scrape_Time`, `Status`.

3. **Lọc Video Theo Keyword**:
   - Sử dụng **Google Apps Script** để tự động thêm chỉ những liên kết TikTok chứa từ khóa (ví dụ: `#marketing`) vào Sheet.

4. **Tự Động Xóa Dữ Liệu Trùng Lặp**:
   - Thêm node `n8n-nodes-base.if` để kiểm tra xem URL đã tồn tại trong Sheet trước khi scrape.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào phân tích nội dung TikTok thay vì làm thủ công. **Chỉ cần thêm liên kết vào Sheet, toàn bộ quá trình scrape, trích xuất và lưu trữ sẽ tự động hóa!**

**Hành động ngay**:
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Thêm liên kết TikTok** vào Sheet để test.
3. **Bật Active** và theo dõi kết quả!

👉 **Cần hỗ trợ?** Đăng ký **VPS n8n** tại [TinoHost](https://tino.vn/vps-n8n?affid=388) để workflow chạy ổn định 24/7!