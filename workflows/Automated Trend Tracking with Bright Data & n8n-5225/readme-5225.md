---
title: "🚀 Monthly Viral Trend Tracker: Tự Động Hàng Tháng Lấy Dữ Liệu Topics Viral Từ Quora Và Lưu Vào Google Sheets"
description: "Workflow tự động hóa hàng tháng để lấy dữ liệu các chủ đề viral từ Quora (như marketing, design) thông qua Bright Data, trích xuất tiêu đề, thống kê và lưu vào Google Sheets. Giúp các sếp tiết kiệm thời gian, theo dõi xu hướng thị trường và lấy ý tưởng nội dung một cách hiệu quả."
slug: "monthly-viral-trend-tracker-quora-n8n"
tags: [n8n, automation, no-code, ai, bright-data, google-sheets, trend-analysis]
keywords: [tự động hóa n8n, theo dõi xu hướng viral, quora scraper, bright data, google sheets automation, trend tracking]
---

# 🚀 Monthly Viral Trend Tracker: Lấy Dữ Liệu Viral Từ Quora Hàng Tháng Và Lưu Vào Google Sheets

## 📌 **Nỗi Đau Của Các Sếp**
Bạn có bao giờ phải **tìm kiếm thủ công** các chủ đề viral trên Quora để lấy ý tưởng nội dung, phân tích xu hướng thị trường hoặc chuẩn bị báo cáo hàng tháng? Thời gian và công sức tiêu tốn cho việc này có thể được tối ưu hóa bằng một **workflow tự động hóa hoàn toàn**!

Với **Monthly Viral Trend Tracker**, các sếp sẽ:
- **Tiết kiệm 10+ giờ/tháng** không phải tra cứu thủ công.
- **Nhận dữ liệu chính xác** từ Quora mỗi tháng, không phụ thuộc vào thời gian làm việc.
- **Lưu trữ dữ liệu** trong Google Sheets để phân tích, báo cáo hoặc chia sẻ với team.
- **Lấy ý tưởng nội dung** từ các chủ đề đang hot nhất trên Quora.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** và không bị gián đoạn, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) thay vì dùng phiên bản miễn phí trên cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần nhớ hoặc kích hoạt thủ công mỗi tháng.
- **Dữ liệu sạch và chuẩn**: Trích xuất tiêu đề, URL, số lượt tương tác và lưu vào Google Sheets.
- **Phân tích xu hướng**: So sánh dữ liệu giữa các tháng để phát hiện xu hướng mới.
- **Nguồn ý tưởng nội dung**: Lấy các chủ đề viral để viết bài blog, video hoặc chiến dịch marketing.
- **Chia sẻ dễ dàng**: Google Sheets cho phép team xem và phân tích dữ liệu cùng một lúc.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Bright Data**:
   - Đăng ký tại [Bright Data](https://get.brightdata.com/1tndi4600b25) (sử dụng link này để nhận commission nhỏ hỗ trợ nội dung).
   - Tạo **API Key** và **Proxy** trong tài khoản Bright Data.
2. **Tài khoản Google Sheets**:
   - Tạo một **Google Sheet mới** để lưu dữ liệu (ví dụ: `Monthly Quora Trends`).
   - Chia sẻ Google Sheet với n8n bằng cách tạo **OAuth 2.0 Credential** trong n8n.
3. **Tài khoản n8n**:
   - Nếu tự host, các sếp cần cài đặt n8n trên VPS (hướng dẫn tại [n8n.io](https://n8n.io/)).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### 1. **Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/5225) (nếu có link trực tiếp).
- **Copy JSON** từ canvas và dán vào n8n Editor:
  ```json
  // Dán JSON từ workflow gốc vào đây
  ```

#### 2. **Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **Node 1: Monthly Trend Trigger**
- **Cấu hình Cron Schedule**:
  - Thay đổi `0 0 1 * *` (ngày 1 hàng tháng) nếu muốn chạy vào ngày khác (ví dụ: `0 0 15 * *` để chạy vào ngày 15).
  - **Lưu ý**: Nếu workflow chạy trên VPS, đảm bảo máy chủ có thời gian đồng bộ (UTC).

##### **Node 2: Scrape Quora Trends (Bright Data)**
- **Thay đổi URL và Proxy**:
  - Thay `https://www.quora.com/search?q=marketing` thành chủ đề bạn muốn theo dõi (ví dụ: `design`, `ai`, `finance`).
  - **Cấu hình Bright Data**:
    - Vào **HTTP Request** → **Headers** → Thêm:
      ```
      User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36
      ```
    - **Body (JSON)**:
      ```json
      {
        "url": "https://www.quora.com/search?q=marketing",
        "proxy": "your-brightdata-proxy-url",
        "apiKey": "your-brightdata-api-key"
      }
      ```
    - **Lưu ý**: Proxy và API Key lấy từ tài khoản Bright Data.

##### **Node 3: Extract Post Titles & Stats**
- **Cấu hình CSS Selectors**:
  - Mở **Inspect Element** trên Quora (F12) để tìm các selector phù hợp.
  - Ví dụ:
    - **Tiêu đề**: `a.q-box.qu-mb--tiny` (lấy tiêu đề của câu hỏi).
    - **URL**: `a.q-box.qu-mb--tiny::attr(href)`.
    - **Số lượt tương tác**: `div.q-relative span.q-relative__text` (cần điều chỉnh theo cấu trúc mới nhất của Quora).
  - **Lưu ý**: Quora thường thay đổi CSS, các sếp cần **kiểm tra lại selector** sau mỗi lần update.

##### **Node 4: Save Trends to Sheet**
- **Chọn Google Sheet và Sheet Name**:
  - Vào **Google Sheets** → Chọn **Credentials** là `googleSheetsOAuth2Api`.
  - Thay `Sheet Name` thành tên sheet muốn lưu (ví dụ: `Trends`).
  - **Headers**: Đảm bảo các cột trong Google Sheet phù hợp với dữ liệu trích xuất (ví dụ: `Title`, `URL`, `Votes`, `Date`).
  - **Lưu ý**: Nếu sheet chưa có header, các sếp cần **tạo header trước** hoặc cấu hình `operation: "append"` để thêm dữ liệu vào cuối.

---

#### 3. **Kích Hoạt ⚡️**
- **Test Run**:
  - Kích hoạt **Manual Trigger** để kiểm tra workflow với dữ liệu mẫu.
  - Kiểm tra **Google Sheets** xem dữ liệu có được lưu đúng không.
- **Bật Active**:
  - Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động hàng tháng.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm **Node Slack/Telegram** sau `Save Trends to Sheet` để thông báo khi workflow hoàn thành.
   - Ví dụ: Gửi tin nhắn `"Monthly Quora Trends updated! Check Google Sheet: [link]"` mỗi khi workflow chạy.

2. **Lưu Log Dữ Liệu**:
   - Thêm **Node Set** trước `Save Trends to Sheet` để thêm cột `Date` và `Time` vào dữ liệu.
   - Cấu hình:
     ```json
     {
       "Date": "{{$now}}",
       "Time": "{{$datetime($now, 'HH:mm:ss')}}"
     }
     ```

3. **Tạo Báo Cáo Định Kỳ**:
   - Sử dụng **Google Apps Script** để tự động tạo báo cáo từ Google Sheets và gửi qua email hàng tuần.
   - Hướng dẫn: [Tạo báo cáo tự động với Google Apps Script](https://developers.google.com/apps-script).

4. **Theo Dõi Nhiều Chủ Đề**:
   - Sao chép **Node 2 (Scrape Quora Trends)** và thay đổi URL để theo dõi nhiều chủ đề khác nhau (ví dụ: `marketing`, `design`, `tech`).
   - Sau đó, dùng **Node Split** để chia dữ liệu thành nhiều sheet riêng biệt.

5. **Kết Hợp với AI (LLM)**:
   - Thêm **Node LLM** (n8n-nodes-ai) để tự động tổng hợp tóm tắt xu hướng từ dữ liệu trích xuất.
   - Ví dụ: Sử dụng **Prompt**:
     ```
     "Tóm tắt 3 xu hướng chính từ danh sách câu hỏi viral này và đề xuất 2 ý tưởng nội dung cho chủ đề marketing."
     ```

---

### 📌 **Kết Luận**
**Monthly Viral Trend Tracker** là công cụ **tự động hóa hoàn toàn** giúp các sếp:
✅ **Tiết kiệm thời gian** bằng việc loại bỏ công việc tra cứu thủ công.
✅ **Nhận dữ liệu chính xác** từ Quora mỗi tháng.
✅ **Phân tích xu hướng** để ra quyết định marketing thông minh.
✅ **Lấy ý tưởng nội dung** từ các chủ đề viral.

**Hành động ngay**:
1. **Cài đặt n8n trên VPS** (nếu chưa có).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và để nó làm việc cho bạn hàng tháng!

---
**Nếu có vấn đề**, liên hệ với tác giả Yaron Been qua:
🔗 [LinkedIn](https://www.linkedin.com/in/yaronbeen/)
📺 [YouTube](https://www.youtube.com/@YaronBeen/videos)