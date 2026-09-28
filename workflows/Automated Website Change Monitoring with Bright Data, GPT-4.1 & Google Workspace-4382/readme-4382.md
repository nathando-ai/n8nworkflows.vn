---
title: "🔍 **Tự Động Hóa Theo Dõi & Báo Cáo Thay Đổi Trang Web với Bright Data, GPT-4.1 & Google Workspace**"
description: "Workflow tự động hóa theo dõi thay đổi nội dung trên trang web hàng tuần, so sánh dữ liệu, tạo báo cáo tự động bằng AI (GPT-4.1), lưu trữ trên Google Drive và gửi email thông báo. Giúp các sếp SEO/Marketing tiết kiệm 10+ giờ/tháng so sánh thủ công."
slug: "tieu-dong-ho-tra-thay-doi-trang-web-voi-bright-data-gpt-4-1"
tags: [n8n, automation, seo, marketing, ai, google-workspace, bright-data, web-scraping]
keywords: [n8n workflow theo dõi trang web, tự động hóa SEO, báo cáo thay đổi trang web, GPT-4.1 trong n8n, Bright Data MCP, tự động hóa Google Sheets]
---

# 🚀 **Tự Động Hóa Theo Dõi & Báo Cáo Thay Đổi Trang Web Hàng Tuần**

## **💡 Giới Thiệu: Tại Sao Các Sếp SEO/CMO Cần Workflow Này?**
Hàng tuần, các sếp SEO phải **so sánh thủ công** hàng chục trang web để phát hiện thay đổi nội dung, meta tag, hoặc cấu trúc trang. Quá trình này tốn **5-10 giờ/tháng**, dễ mắc lỗi, và không thể hoạt động liên tục 24/7. **Workflow này giải quyết tất cả vấn đề đó bằng cách:**
✅ **Tự động hóa 100% theo dõi thay đổi** trên trang web (dùng Bright Data MCP).
✅ **So sánh dữ liệu** giữa tuần trước và tuần hiện tại bằng AI (GPT-4.1).
✅ **Tạo báo cáo tự động** dưới dạng Google Docs + Email thông báo.
✅ **Lưu trữ dữ liệu** trên Google Drive để theo dõi lịch sử.
✅ **Hoạt động tự động hàng tuần** mà không cần can thiệp thủ công.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 10+ giờ/tháng** so sánh thủ công.
- **Chính xác 100%** nhờ AI (GPT-4.1) phân tích thay đổi chi tiết.
- **Báo cáo tự động** gửi qua Email + Google Docs.
- **Lịch sử dữ liệu** được lưu trữ trên Google Drive.
- **Hoạt động 24/7** mà không cần can thiệp.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Lên Đồ**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Bright Data MCP** (dùng để web scraping):
   - [Tạo tài khoản Bright Data](https://brightdata.com/) (mã giảm giá: **BRIGHTDATA10**).
   - Cài đặt **Bright Data MCP Server** (hướng dẫn: [GitHub](https://github.com/luminati-io/brightdata-mcp)).
   - Cài đặt **n8n MCP Client Node** (community node):
     ```bash
     npm install n8n-nodes-mcp
     ```
2. **Tài khoản Google Workspace** (Google Sheets, Drive, Docs, Gmail).
3. **Tài khoản OpenAI** (để sử dụng GPT-4.1):
   - [Tạo API Key OpenAI](https://platform.openai.com/) (mã giảm giá: **N8N10**).
4. **File mẫu Google Sheets** (sẽ được copy và chỉnh sửa):
   - [Mẫu Sheets](https://docs.google.com/spreadsheets/d/1oPyAaTS8GMqlaBcyCO7G7MRtzMUUaOnA45JfWCzcCa8/edit?usp=sharing).
5. **Google Drive Folder** để lưu trữ dữ liệu tuần.
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/4382](https://n8n.io/workflows/4382).
- **Import vào n8n Editor**:
  - Nhấn **Import** → Chọn file JSON → **Import**.
  - **Hoặc** copy toàn bộ JSON vào **Import Workflow** (tab bên trái).

### **2. Các Lưu Ý Bắt Buộc Phải Chỉnh 📌**
Workflow này **không hoạt động được** nếu không cấu hình đúng các node sau:

#### **A. Cấu Hình Google Sheets & Drive**
1. **Node: "Read from comparison spreadsheets"**
   - **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).
   - **File ID**: Sử dụng ID của file Sheets đã copy (ví dụ: `1e4oheZjmxb3P7OXGY0uLWZKz2ENcp7XlEpIloOtRHEk`).
   - **Sheet Name**: Đặt là `"Sheet1"` (hoặc tên sheet của bạn).

2. **Node: "Upload current week JSON file"**
   - **Credentials**: `googleDriveOAuth2Api`.
   - **Folder ID**: Điền `DriveFolderID` (đã set trong **Set workflow variables**).
   - **File Name**: Đặt định dạng `week_{current_date}.json` (ví dụ: `week_2024-05-20.json`).

3. **Node: "Update comparison sheet with current week file data"**
   - **Credentials**: `googleSheetsOAuth2Api`.
   - **Range**: Điền `Sheet1!A1:Z100` (hoặc phạm vi của bạn).

#### **B. Cấu Hình Bright Data MCP**
1. **Node: "scrape_as_markdown"**
   - **Credentials**: `mcpClientApi`.
   - **MCP Server URL**: Điền URL của server MCP bạn cài đặt (ví dụ: `http://your-server-ip:8080`).
   - **API Key**: Điền API Key từ Bright Data.

2. **Node: "Web scraping and data extraction agent"**
   - **Tool**: Chọn `scrape_as_markdown`.
   - **URLs**: Lấy từ Google Sheets (cột `URL`).
   - **Prompt AI**: Đã được cấu hình sẵn trong node `agent`.

#### **C. Cấu Hình AI (GPT-4.1)**
1. **Node: "GPT-4.1"**
   - **Credentials**: `openAiApi`.
   - **Model**: Đặt là `gpt-4-1` (hoặc `gpt-4` nếu không có).
   - **API Key**: Điền API Key OpenAI.

2. **Node: "Detect changes between weeks" (Code Node)**
   - **Mã JavaScript**: Đã được viết sẵn, **không cần chỉnh sửa** (nếu muốn thay đổi logic, cần hiểu code).

#### **D. Cấu Hình Email & Google Docs**
1. **Node: "Send email of comparison results"**
   - **Credentials**: `gmailOAuth2`.
   - **Email To**: Điền địa chỉ Email của bạn (đã set trong `Set workflow variables`).
   - **Subject**: Đặt là `"Báo cáo thay đổi trang web - Tuần {current_date}"`.

2. **Node: "Create comparison document"**
   - **Credentials**: `googleDocsOAuth2Api`.
   - **Title**: Đặt là `"Báo cáo thay đổi trang web - Tuần {current_date}"`.

#### **E. Cấu Hình Biến Cần Đặt Trước**
1. **Node: "Set workflow variables"**
   - **Biến cần thiết**:
     | Biến | Giá Trị |
     |------|---------|
     | `DriveFolderID` | ID của folder Google Drive (lấy từ liên kết share) |
     | `ComparisonSpreadsheetFileID` | ID của file Sheets (ví dụ: `1e4oheZjmxb3P7OXGY0uLWZKz2ENcp7XlEpIloOtRHEk`) |
     | `ComparisonSpreadsheetSheetName` | `"Sheet1"` |
     | `Email` | Email nhận báo cáo (ví dụ: `seo@doanhnghiep.com`) |
     | `IsTest` | `true` (chỉ dùng để test) hoặc `false` (chế độ hoạt động thực) |

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run (Chế Độ Test)**
   - Đặt `IsTest = true`.
   - Chạy workflow **manual** để kiểm tra:
     - Dữ liệu scraping có đúng không?
     - AI có phân tích thay đổi chính xác không?
     - Email và Google Docs có tạo được không?

2. **Chuyển Sang Chế Độ Hoạt Động**
   - Đặt `IsTest = false`.
   - **Bật Schedule Trigger** (node cuối cùng):
     - Chọn **Weekly** (hàng tuần).
     - Thời gian chạy: Ví dụ **08:00 sáng thứ 2** (để có thời gian xử lý trước cuối tuần).

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**Cách Tối Ưu Hóa Workflow**]
1. **Thêm Slack/Telegram Notifications**
   - Sử dụng node `slack` hoặc `telegramBot` để gửi thông báo khi workflow hoàn thành.
   - Ví dụ:
     ```json
     {
       "name": "Notify Slack",
       "type": "slack",
       "credentials": "slackOAuth2",
       "parameters": {
         "text": "🚀 Báo cáo thay đổi trang web đã hoàn thành! Kết quả: {{ $json("summary") }}"
       }
     }
     ```

2. **Lưu Log Dữ Liệu**
   - Thêm node `googleSheets` để lưu **log hoạt động** (thời gian chạy, lỗi, thành công).
   - Ví dụ:
     ```json
     {
       "name": "Log Execution",
       "type": "googleSheets",
       "credentials": "googleSheetsOAuth2Api",
       "parameters": {
         "fileId": "{{ $json("ComparisonSpreadsheetFileID") }}",
         "range": "Log!A1:A",
         "valueInputOption": "RAW",
         "values": [
           ["{{ $node("Schedule Trigger").json("$.execution.date") }}", "{{ $node("Schedule Trigger").json("$.status") }}"]
         ]
       }
     }
     ```

3. **Tự Động Xóa File Cũ**
   - Thêm node `googleDrive` để **xóa file cũ** sau 6 tháng để tiết kiệm không gian.
   - Ví dụ:
     ```json
     {
       "name": "Delete Old Files",
       "type": "googleDrive",
       "credentials": "googleDriveOAuth2Api",
       "parameters": {
         "operation": "delete",
         "fileId": "{{ $json("oldFileId") }}"
       }
     }
     ```

4. **Kết Hợp với Google Analytics**
   - Sử dụng node `googleAnalytics` để **so sánh thay đổi traffic** cùng với thay đổi nội dung.
   - Ví dụ:
     ```json
     {
       "name": "Get GA Data",
       "type": "googleAnalytics",
       "credentials": "googleAnalyticsOAuth2",
       "parameters": {
         "viewId": "VIEW_ID_OF_YOUR_SITE",
         "metrics": "ga:sessions,ga:pageviews",
         "dimensions": "ga:date",
         "startDate": "{{ $date("YYYY-MM-DD").subtract(7, "days") }}",
         "endDate": "{{ $date("YYYY-MM-DD") }}"
       }
     }
     ```
---

## 📌 **Kết Luận: Áp Dụng Ngay Để Tiết Kiệm Thời Gian!**
Workflow này **giải phóng bạn khỏi công việc so sánh trang web thủ công**, giúp:
✔ **Tiết kiệm 10+ giờ/tháng**.
✔ **Nhận báo cáo chính xác** nhờ AI (GPT-4.1).
✔ **Hoạt động tự động** mà không cần can thiệp.

**Bước đầu tiên:**
1. **Cài đặt Bright Data MCP** và **n8n MCP Client Node**.
2. **Import workflow** và cấu hình các biến.
3. **Test chế độ `IsTest = true`** trước khi chuyển sang hoạt động thực.

**👉 [Tải Workflow Mẫu](https://n8n.io/workflows/4382) và bắt đầu tự động hóa ngay!**

---
:::note[**Lưu Ý Cuối Cùng**]
- **N8n Self-hosted** là lựa chọn tốt nhất để workflow **chạy 24/7** mà không bị giới hạn.
- **Nếu gặp lỗi**, kiểm tra:
  - API Key có đúng không?
  - Google Sheets/Drive có quyền truy cập không?
  - Node `agent` có chạy được không?
:::

---
**🚀 Cảm ơn các sếp đã đọc! Chúc các sếp thành công với tự động hóa SEO!** 🎉