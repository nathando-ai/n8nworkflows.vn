---
title: "🤖 **Tự Động Hóa Sản Xuất Lead B2B Tối Đa: Tìm Kiếm Google Places + Trích Xuất AI + Scrape.do**"
description: "Workflow tự động hóa tìm kiếm doanh nghiệp B2B trên Google Maps, đánh giá chất lượng lead, trích xuất thông tin liên lạc từ website bằng AI, và lưu dữ liệu vào Google Sheets - hoàn toàn không cần code! Giúp các sếp tiết kiệm 10-15 giờ/tháng trong việc tìm kiếm và phân tích lead."
slug: "tieu-dong-hoa-san-xuat-lead-b2b-google-places-ai-scraped"
tags: [n8n, automation, no-code, ai-workflow, google-places, scrape-do, lead-generation]
keywords: [n8n workflow lead generation, tự động hóa tìm kiếm doanh nghiệp, trích xuất thông tin liên lạc bằng AI, scrape website, google places api, google sheets automation]
---

# 🚀 **Tự Động Hóa Sản Xuất Lead B2B: Từ Google Places Đến Trích Xuất AI - Không Cần Code!**

### **Nỗi Đau Của Các Sếp Trong Tìm Kiếm Lead B2B**
Hàng ngày, các sếp phải:
- **Tìm kiếm thủ công** trên Google Maps hàng trăm doanh nghiệp trong ngành mục tiêu.
- **Lọc và đánh giá** chất lượng lead dựa trên đánh giá, website, và thông tin liên lạc.
- **Scrape website** để tìm email, số điện thoại, hoặc liên kết mạng xã hội (thường mất từ 30-60 phút/lead).
- **Ghi chép dữ liệu** vào Google Sheets hoặc Excel, dễ bị lỗi và mất thời gian.

**Workflow này giải quyết tất cả!** Nó tự động hóa toàn bộ quy trình từ tìm kiếm đến trích xuất thông tin liên lạc bằng AI, giúp các sếp **tiết kiệm 10-15 giờ/tháng** và **nâng cao chất lượng lead** với độ chính xác cao.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động tìm kiếm và lọc lead chất lượng trong vài phút thay vì nhiều giờ.
- **Chất lượng lead cao**: Đánh giá tự động dựa trên rating, website, và thông tin liên lạc.
- **Trích xuất thông tin liên lạc chính xác**: AI phân tích footer website để lấy email, số điện thoại, và mạng xã hội.
- **Dữ liệu tập trung**: Tất cả lead được lưu vào Google Sheets với định dạng nhất quán.
- **Hoạt động liên tục**: Chạy 24/7 trên VPS, không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản và API Key**:
   - [Google Places API](https://developers.google.com/places/web-service/get-api-key) (để tìm kiếm doanh nghiệp).
   - [Scrape.do](https://scrape.do/) (hoặc dịch vụ scrape khác như Apify) (để lấy HTML website).
   - [OpenAI API](https://platform.openai.com/api-keys) (để sử dụng AI trích xuất thông tin).
   - [Google Sheets](https://sheets.google.com) (để lưu dữ liệu lead).
2. **Thông tin cơ bản**:
   - Danh sách **thể loại doanh nghiệp** (ví dụ: "Cafe", "Công ty phần mềm").
   - **Vị trí** (thành phố, quận) để tìm kiếm.
   - **Google Sheet** đã chuẩn bị sẵn với các cột: `Name`, `Rating`, `Website`, `Email`, `Phone`, `Social Media`, `Lead Score`.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [link gốc](https://n8n.io/workflows/8448).
2. Trong n8n Editor, nhấn **Import** và chọn file JSON.
3. Hoặc copy toàn bộ JSON và dán vào **Import Workflow** trong giao diện.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Dưới đây là các node quan trọng cần cấu hình chi tiết:

##### **A. Cấu Hình Tìm Kiếm Doanh Nghiệp (Google Places)**
- **Node**: `2. Find Businesses (Google Places)`
  - **Credentials**: Chọn `httpHeaderAuth` và điền **API Key** từ Google Places API.
  - **Parameters**:
    - `searchCategory`: Điền thể loại doanh nghiệp (ví dụ: `cafe`, `software`).
    - `locationName`: Điền vị trí (ví dụ: `Hà Nội`, `Quận 1 TP.HCM`).
    - `radius`: Khoảng cách tìm kiếm (km), mặc định là `5000m`.

##### **B. Trích Xuất Thông Tin Liên Lạc Bằng AI**
- **Node**: `6d. Extract Contact Info with AI`
  - **Credentials**: Chọn `openAiApi` và điền **API Key** từ OpenAI.
  - **Prompt AI**:
    - Workflow đã cấu hình sẵn để AI phân tích `<footer>` của website và trích xuất:
      - Email (ví dụ: `contact@example.com`).
      - Số điện thoại (ví dụ: `+84 123 456 789`).
      - Liên kết mạng xã hội (Facebook, LinkedIn, Instagram).
    - **Lưu ý**: Nếu AI không trích xuất được, các sếp có thể chỉnh sửa prompt trong node `OpenAI Chat Model` để phù hợp với website cụ thể.

##### **C. Lưu Dữ Liệu Vào Google Sheets**
- **Node**: `7. Save Enriched Lead to Google Sheets`
  - **Credentials**: Chọn `googleSheetsOAuth2Api` và đăng nhập tài khoản Google.
  - **Parameters**:
    - Chọn **Google Sheet** và **Sheet** mục tiêu.
    - Đảm bảo các cột trong Sheet phù hợp với dữ liệu xuất ra (ví dụ: `Name`, `Email`, `Phone`, `Lead Score`).

##### **D. Cấu Hình Lọc Lead Chất Lượng**
- **Node**: `4. Filter High-Quality Leads`
  - **Threshold**: Mặc định là `leadScore > 50`. Các sếp có thể điều chỉnh để lọc lead cao hơn (ví dụ: `leadScore > 70`).

#### **3. Kích Hoạt ⚡️**
1. **Test Run**: Nhấn **Execute Workflow** để kiểm tra với dữ liệu mẫu.
2. **Bật Active**: Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động.
3. **(Tùy Chọn)**: Cài đặt **Schedule Trigger** để chạy định kỳ (ví dụ: hàng ngày lúc 8h sáng).

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** sau node `7. Save Enriched Lead` để thông báo khi có lead mới.
   - **Cách làm**: Sử dụng node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` và cấu hình webhook.

2. **Lưu Log Hoạt Động**:
   - Thêm node **Google Drive** hoặc **AWS S3** để lưu log của workflow (ví dụ: lỗi scrape, lead bị bỏ qua).
   - **Cách làm**: Sử dụng node `n8n-nodes-base.googleDrive` hoặc `n8n-nodes-base.awsS3`.

3. **Tự Động Gửi Báo Cáo**:
   - Kết hợp với **Google Apps Script** để tự động gửi báo cáo hàng tuần qua email.
   - **Cách làm**: Sau khi lưu lead vào Google Sheets, sử dụng Apps Script để tạo báo cáo và gửi qua Gmail.

4. **Cải Thiện AI Trích Xuất**:
   - Nếu AI không trích xuất được thông tin, các sếp có thể:
     - Chỉnh sửa **prompt** trong node `OpenAI Chat Model` để cụ thể hơn.
     - Thêm node **Function** để xử lý lỗi (ví dụ: nếu website không có footer, bỏ qua lead đó).

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quy trình tìm kiếm và trích xuất lead B2B một cách **chính xác, tiết kiệm thời gian và không cần code**. Bằng cách kết hợp **Google Places API**, **Scrape.do**, và **AI OpenAI**, nó giúp các sếp:
✅ **Tìm kiếm hàng ngàn lead** trong vài phút.
✅ **Trích xuất thông tin liên lạc** từ website tự động.
✅ **Lưu dữ liệu** vào Google Sheets với định dạng nhất quán.
✅ **Hoạt động 24/7** trên VPS, không cần can thiệp thủ công.

**Hành động ngay hôm nay!**
1. Import workflow vào n8n của mình.
2. Cấu hình các API Key và thông tin cần thiết.
3. Bật workflow và bắt đầu tự động hóa lead generation!

---
**Có thắc mắc?** Liên hệ với tác giả [Onur](https://n8n.io/workflows/8448) qua email hoặc comment bên dưới! 🚀