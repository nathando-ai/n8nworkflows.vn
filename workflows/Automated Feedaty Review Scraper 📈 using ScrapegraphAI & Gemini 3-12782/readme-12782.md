---
title: "🚀 **Tự Động Hóa Scraping & Phân Tích Đánh Giá Feedaty (Giống Trustpilot) Với ScrapeGraphAI & Gemini 3 - Báo Cáo Reputation PDF Tự Động**"
description: "Workflow tự động hóa hoàn toàn **scraping đánh giá khách hàng từ Feedaty**, phân tích cảm xúc bằng Gemini 3, và tạo **báo cáo quản lý danh tiếng doanh nghiệp** dưới dạng PDF tự động upload lên Google Drive. Giúp các sếp tiết kiệm **10+ giờ/tháng** trong việc phân tích feedback và đưa ra quyết định chiến lược."
slug: "tieu-dong-hoa-scraping-phan-tich-danh-gia-feedaty"
tags: [n8n, automation, market-research, ai-summarization, scrapegraphai, gemini-3, google-drive, pdf-automation]
keywords: [n8n workflow tự động hóa, scrap reviews Feedaty, phân tích cảm xúc AI, Gemini 3 tự động hóa, báo cáo danh tiếng doanh nghiệp, PDF tự động hóa, Google Drive n8n]
---

# 🚀 **Tự Động Hóa Scraping & Phân Tích Đánh Giá Feedaty (Giống Trustpilot) Với ScrapeGraphAI & Gemini 3**

## **🔥 Nỗi Đau Của Các Sếp Khi Phân Tích Đánh Giá Khách Hàng**
Hàng ngày, các sếp phải **tốn thời gian thủ công** để:
- **Scraping** hàng trăm đánh giá từ Feedaty (hay Trustpilot) bằng cách copy-paste.
- **Phân loại** đánh giá theo cảm xúc (tích cực, trung lập, tiêu cực) bằng cách đọc từng bài.
- **Tạo báo cáo** bằng Excel/Google Sheets để gửi cho ban lãnh đạo, nhưng lại **không có cấu trúc** và **không tự động hóa**.
- **Mất thời gian** để theo dõi xu hướng và phản hồi khách hàng kịp thời.

**Kết quả?** Các sếp **chỉ có thời gian** để ra quyết định chiến lược khi đã **trễ mùa** vì thiếu dữ liệu chính xác và tự động hóa.

---
### **🎯 Kết Quả Các Sếp Nhận Được Khi Sử Dụng Workflow Này**
:::tip[**3 Lợi Ích Cốt Lõi**]
✅ **Tiết Kiệm 10+ giờ/tháng** – Scraping và phân tích tự động hóa hoàn toàn.
✅ **Báo Cáo Danh Tiếng Doanh Nghiệp Cấu Trúc** – AI phân tích cảm xúc và tổng hợp thành **PDF tự động**, dễ đọc và chia sẻ.
✅ **Dữ Liệu Chính Xác & Mới Nhất** – ScrapeGraphAI lấy dữ liệu **ngay từ trang web**, không phụ thuộc vào API hạn chế.
✅ **Hoạt Động 24/7** – Workflow chạy tự động sau khi cấu hình, không cần can thiệp thủ công.
:::

---
## **🔧 Yêu Cầu Cần Thiết Trước Khi Bắt Đầu**
:::info[**CHUẨN BỊ**]
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài Khoản & API Keys:**
- **ScrapeGraphAI** ([Đăng ký miễn phí](https://dashboard.scrapegraphai.com/?via=n3witalia)) – Dùng để scraping dữ liệu từ Feedaty.
- **Google Gemini API** ([Đăng ký](https://makersuite.google.com/)) – Dùng cho phân tích cảm xúc và tạo báo cáo.
- **ConvertAPI** ([Đăng ký](https://convertapi.com?ref=n3witalia)) – Chuyển HTML thành PDF.
- **Google Drive OAuth2** – Để upload báo cáo PDF tự động.

✔ **Thông Tin Cần Thiết:**
- **ID công ty Feedaty** (ví dụ: `maxisport`).
- **Số lượng trang đánh giá tối đa** (ví dụ: 5 trang).
- **Folder Google Drive** để lưu báo cáo PDF (cần chia sẻ quyền cho n8n).
:::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
#### **Cách 1: Import từ File JSON**
1. **Tải workflow** từ [n8n.io/workflows/12782](https://n8n.io/workflows/12782) (chọn **Export as JSON**).
2. **Mở n8n Editor** (trên VPS hoặc n8n.io).
3. Nhấn **Import** → Chọn file JSON vừa tải → **Import**.

#### **Cách 2: Copy/Paste JSON**
1. **Tải JSON** từ link trên.
2. Trong **n8n Editor**, nhấn **Import** → Chọn **Paste JSON** → Dán nội dung JSON → **Import**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **20 node**, nhưng các sếp **phải cấu hình cẩn thận** các node sau để hoạt động đúng:

#### **🔹 Node "Set Parameters" (Cấu Hình Tham Số)**
- **Điền:**
  - `companyIdentifier`: ID công ty Feedaty (ví dụ: `maxisport`).
  - `maxPages`: Số trang tối đa muốn scraping (ví dụ: `5`).

#### **🔹 Node "ScrapeGraphAI" (Scraping Dữ Liệu)**
- **Chọn credentials:** `scrapegraphAIApi` (đã cấu hình trước khi import).
- **Cấu hình:**
  - `url`: `https://feedaty.com/{companyIdentifier}/reviews` (thay `{companyIdentifier}` bằng ID công ty).
  - `maxPages`: Đặt theo tham số từ node "Set Parameters".

#### **🔹 Node "Google Gemini Chat Model" (Phân Tích Cảm Xúc & Tạo Báo Cáo)**
- **Chọn credentials:** `googlePalmApi` (API Key của Google Gemini).
- **Cấu hình Prompt:**
  - **Node "Sentiment Analysis"**: AI phân tích cảm xúc từng đánh giá thành **Positive/Neutral/Negative**.
  - **Node "Company Reputation Management"**: AI tổng hợp tất cả đánh giá thành **báo cáo quản lý danh tiếng** (cấu trúc như sau):
    ```json
    {
      "overallSentiment": "Positive/Neutral/Negative",
      "positiveReviews": 80,
      "negativeReviews": 15,
      "neutralReviews": 5,
      "keyThemes": ["Chất lượng sản phẩm", "Dịch vụ khách hàng", "Giao hàng"],
      "recommendations": ["Cải thiện điểm này...", "Tăng cường điểm này..."]
    }
    ```

#### **🔹 Node "HTML to PDF" (Chuyển HTML thành PDF)**
- **Chọn credentials:** `convertApi` (API Key của ConvertAPI).
- **Cấu hình:**
  - `inputFormat`: `html`.
  - `outputFormat`: `pdf`.
  - **Tham số tùy chọn:** Đặt `margin` và `orientation` theo yêu cầu.

#### **🔹 Node "Upload file" (Upload PDF lên Google Drive)**
- **Chọn credentials:** `googleDriveOAuth2Api`.
- **Cấu hình:**
  - **Folder ID**: Điền **ID folder Google Drive** (lấy từ liên kết folder: `https://drive.google.com/drive/folders/{FOLDER_ID}`).
  - **File Name**: `Báo cáo_Danh_Tiếng_{companyIdentifier}_{date}.pdf`.

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** (chọn **Test Workflow**).
   - Kiểm tra **log** để đảm bảo không có lỗi.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động khi kích hoạt.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::tip[**3 Ý Tưởng Mở Rộng**]
🔹 **Gửi Báo Cáo PDF qua Email Tự Động**
- Thêm **node `n8n-nodes-base.email`** sau node "Upload file" để gửi báo cáo PDF cho ban lãnh đạo hàng tuần.
- **Cấu hình:**
  - **SMTP Server**: Gmail/SendGrid.
  - **Người nhận**: `ban-lead@doanhnghiep.com`.
  - **Tiêu đề email**: `Báo cáo Danh Tiếng {Company Name} - Tuần {Week}`.

🔹 **Lưu Log Scraping vào Google Sheets**
- Thêm **node `n8n-nodes-base.googleSheets`** sau node "ScrapeGraphAI" để ghi lại tất cả đánh giá scraped vào bảng Google Sheets.
- **Cấu hình:**
  - **Sheet Name**: `Feedaty_Reviews`.
  - **Columns**: `Date`, `Rating`, `Review Text`, `Sentiment`.

🔹 **Kích Hoạt Workflow Tuần Hàng**
- Sử dụng **node `n8n-nodes-base.cron`** để chạy workflow tự động **mỗi thứ 2 hàng tuần** (hoặc theo lịch khác).
- **Cấu hình:**
  - `cronExpression`: `0 0 0 * * 2` (chạy lúc 00:00 thứ 2 hàng tuần).
:::

---
## **📌 Kết Luận: Tự Động Hóa Phân Tích Đánh Giá Khách Hàng Ngay Hôm Nay!**
Workflow này **giải quyết hoàn toàn** vấn đề **scraping, phân tích và báo cáo danh tiếng doanh nghiệp** một cách tự động hóa. Các sếp **không cần viết code** mà vẫn có được:
✅ **Dữ liệu chính xác** từ Feedaty.
✅ **Báo cáo PDF tự động** với phân tích cảm xúc sâu sắc.
✅ **Hoạt động 24/7** mà không tốn thời gian thủ công.

**🚀 Hành Động Ngay:**
1. **Cài đặt n8n trên VPS** (Self-hosted) để workflow chạy ổn định.
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **Import workflow** và **cấu hình API keys** theo hướng dẫn trên.
3. **Kích hoạt** và **theo dõi báo cáo** hàng tuần!

**💡 Lời Khuyên Cuối:**
Nếu các sếp muốn **tối ưu hóa thêm**, có thể kết hợp với **Slack/Telegram** để thông báo khi có **đánh giá tiêu cực** hoặc **xu hướng mới** trong feedback khách hàng.

---
**🔗 Xem video hướng dẫn chi tiết từ tác giả Davide:**
👉 [YouTube @n3witalia](https://youtube.com/@n3witalia) (Đăng ký để không bỏ lỡ tutorial mới!)