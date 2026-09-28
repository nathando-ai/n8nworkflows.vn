---
title: "🤖 **Tự Động Hoàn Chỉnh & Lưu Trữ Dữ Liệu Tin Tức từ Decodo + Gemini AI sang Google Sheets**"
description: "Workflow tự động hóa 100% không code giúp các sếp scrap dữ liệu tin tức từ diễn đàn, phân tích bằng AI Gemini, và lưu trữ kết quả vào Google Sheets với định dạng sạch sẽ. Giúp tiết kiệm thời gian nghiên cứu thị trường, theo dõi xu hướng, và phân tích dữ liệu hiệu quả."
slug: "tieu-dong-hoan-chinh-luu-tru-du-lieu-tin-tuc-decodo-gemini-google-sheets"
tags: [n8n, automation, no-code, AI-summarization, market-research, google-sheets, gemini-ai, decodo-api]
keywords: [n8n workflow tin tức, tự động hóa scrap dữ liệu, gemini ai phân tích tin tức, google sheets tự động hóa, decodo api n8n, nghiên cứu thị trường tự động]
---

# 🚀 **Tự Động Scrap, Phân Tích & Lưu Trữ Dữ Liệu Tin Tức bằng Decodo + Gemini AI**

## **💡 Giới Thiệu: Giải Pháp Cho Những Ai Cần Theo Dõi Xu Hướng Thị Trường Hiệu Quả**
Các sếp trong lĩnh vực **nghiên cứu thị trường, báo chí dữ liệu, hoặc AI automation** thường phải mất nhiều thời gian để:
✅ **Scrap** dữ liệu từ diễn đàn, forum, hoặc trang web.
✅ **Phân tích** nội dung để trích xuất thông tin quan trọng (tên bài, URL, tác giả, số lượt tương tác).
✅ **Lưu trữ** kết quả vào bảng tính để theo dõi và phân tích dài hạn.

**Workflow này giải quyết tất cả bằng cách:**
✔ **Tự động scrap** dữ liệu từ các diễn đàn bằng **Decodo API** (không cần viết code).
✔ **Phân tích bằng AI Gemini** để trích xuất thông tin theo định dạng JSON sạch sẽ.
✔ **Lưu trữ tự động** vào **Google Sheets** với định dạng cá nhân hóa.
✔ **Chạy 24/7** theo lịch trình tự động (ví dụ: mỗi ngày vào 00:00).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần scrap thủ công, phân tích bằng AI, và nhập liệu vào Sheets.
- **Dữ liệu chính xác**: Gemini AI tự động trích xuất thông tin quan trọng (tên bài, URL, tác giả, số lượt tương tác).
- **Lưu trữ tự động**: Dữ liệu được append vào Google Sheets theo định dạng sạch sẽ.
- **Theo dõi xu hướng**: Dễ dàng phân tích dữ liệu qua thời gian để ra quyết định kinh doanh.
- **Hoạt động liên tục**: Workflow chạy tự động theo lịch trình, không cần can thiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Decodo** (đăng ký [tại đây](https://visit.decodo.com/discount) để hưởng ưu đãi).
✔ **API Key Google Gemini** (cài đặt trong n8n dưới tên `googlePalmApi`).
✔ **Google Sheets OAuth 2.0** (cài đặt trong n8n dưới tên `googleSheetsOAuth2Api`).
✔ **Google Sheet mẫu** (cần có tab với cấu trúc cột phù hợp, ví dụ: `Title`, `URL`, `Author`, `Engagement`, `Scrape Date`).

---
:::note[CHUẨN BỊ CẦN THIẾT]
- **Decodo API Key**: Tạo tại [Decodo Dashboard](https://decodo.com/dashboard).
- **Google Sheets**: Tạo một bảng mới và chia sẻ với n8n (quyền chỉnh sửa).
- **Google Gemini API**: Khởi tạo tại [Google AI Studio](https://aistudio.google.com/).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/9965](https://n8n.io/workflows/9965) và import vào n8n Editor.
- **Copy/Paste JSON** từ link trên vào n8n Editor (đường dẫn: `https://n8n.io/workflows/9965/raw`).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này gồm **13 node**, các sếp cần chú ý cấu hình sau:

##### **A. Cấu Hình Credentials (API Keys)**
| Node | Yêu Cầu Cấu Hình | Ghi Chú |
|------|------------------|---------|
| **Scrape Forum Data** | `decodoApi` | Điền `API Key` từ Decodo Dashboard. |
| **Google Gemini Model** | `googlePalmApi` | Điền `API Key` từ Google AI Studio. |
| **Update Google Sheet (News)** | `googleSheetsOAuth2Api` | Chọn OAuth 2.0 credential đã cài đặt. |
| **Log Scrape Results** | `googleSheetsOAuth2Api` | Cùng credential với node trên. |

##### **B. Cấu Hình Node Quan Trọng**
1. **`Workflow Config` (Node `set`)**
   - **Điền tham số**:
     - `forumUrls`: Danh sách URL của các diễn đàn cần scrap (ví dụ: `["https://forum.example.com", "https://forum2.example.com"]`).
     - `geolocation`: Địa lý mục tiêu (ví dụ: `"US"`).
     - `sheetId`: ID của Google Sheet (lấy từ URL Sheet, ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
     - `sheetTab`: Tên tab trong Google Sheet (phải khớp với cấu trúc cột).

2. **`Schedule Trigger` (Node `scheduleTrigger`)**
   - **Chọn lịch trình**: Ví dụ: `0 0 * * *` (mỗi ngày vào 00:00 GMT).

3. **`Google Sheets` (Node `googleSheets`)**
   - **Chọn tab**: Đảm bảo tab trong Google Sheet có cột phù hợp với dữ liệu trích xuất (ví dụ: `Title`, `URL`, `Author`, `Engagement`).

##### **C. Test Run & Kích Hoạt**
- **Test run** với dữ liệu mẫu để kiểm tra:
  - Decodo có scrap được dữ liệu không?
  - Gemini có phân tích và trích xuất JSON chính xác không?
  - Google Sheets có append dữ liệu không?
- **Bật `Active`** workflow sau khi kiểm tra thành công.

---
#### **3. Kích Hoạt ⚡️**
1. **Chạy test run** với dữ liệu mẫu để đảm bảo mọi thứ hoạt động.
2. **Bật `Active`** workflow trong n8n Dashboard.
3. **Monitor** kết quả trong Google Sheets và log scrape.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**
   - Thêm node `slack` hoặc `telegram` để thông báo khi workflow hoàn tất hoặc gặp lỗi.
   - Ví dụ: Gửi tin nhắn `"Scrape thành công! Có [X] tin tức mới"` vào Slack.

2. **Lưu Log Chi Tiết**
   - Sử dụng node `googleSheets` để append log scrape (ví dụ: thời gian, số tin tức, lỗi nếu có) vào một tab riêng.

3. **Tự Động Gửi Báo Cáo**
   - Thêm node `email` hoặc `googleDrive` để gửi báo cáo định kỳ (ví dụ: mỗi tuần) về dữ liệu mới nhất.

4. **Cập Nhật Lịch Trình**
   - Nếu cần scrap thường xuyên hơn, điều chỉnh `Schedule Trigger` (ví dụ: `0 */6 * * *` để chạy mỗi 6 giờ).

5. **Optimize Decodo API**
   - Nếu Decodo trả về nhiều dữ liệu, sử dụng node `splitInBatches` để chia nhỏ và giảm tải.

---

### 📌 **Kết Luận: Áp Dụng Ngay Để Tiết Kiệm Thời Gian & Tăng Cường Dữ Liệu**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần:
✅ **Tự động hóa scrap tin tức** từ nhiều nguồn.
✅ **Phân tích bằng AI Gemini** để trích xuất thông tin chính xác.
✅ **Lưu trữ và theo dõi** dữ liệu một cách tự động.

**Hành động ngay:**
1. **Import workflow** và cấu hình credentials.
2. **Test run** để đảm bảo hoạt động.
3. **Bật Active** và theo dõi kết quả trong Google Sheets.

**🚀 Cùng tự động hóa công việc của mình ngay hôm nay!** 🚀

---
:::tip[LƯU Ý CUỐI CUNG]
- Nếu gặp lỗi, kiểm tra **log scrape** trong Google Sheets để debug.
- Để workflow ổn định, **cài n8n trên VPS** (không dùng phiên bản cloud).
- Nếu cần scrap nhiều nguồn, **tăng thời gian wait** giữa các scrape để tránh bị chặn.
:::

---
**📌 Cảm ơn các sếp đã đọc đến cuối!** Nếu có thắc mắc, hãy để lại comment dưới đây. 😊