---
title: "🚀 Tự động hóa tổng hợp tin tức quy định với NewsAPI, Gemini và Google Sheets"
description: "Hướng dẫn chi tiết cách tự động hóa việc lấy tin tức từ NewsAPI, tổng hợp bằng AI Gemini và lưu kết quả vào Google Sheets cùng cảnh báo lỗi qua email"
slug: "tu-dong-hoa-tong-hop-tin-tuc-quy-dinh-voi-newsapi-gemini-google-sheets"
tags: [n8n, automation, no-code, AI, Google Sheets, NewsAPI]
keywords: [n8n workflow, tự động hóa, tổng hợp tin tức, AI, Google Sheets, NewsAPI]
---

# 🚀 Tự động hóa tổng hợp tin tức quy định với NewsAPI, Gemini và Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp đang gặp khó khăn khi phải theo dõi hàng nghìn tin tức quy định hàng ngày từ nhiều nguồn khác nhau? Khi phải tốn thời gian và công sức để đọc, phân tích và tổng hợp thông tin từ các bài báo dài dòng? Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này chỉ trong vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động lấy và xử lý hàng nghìn tin tức mỗi ngày
- Tăng hiệu quả: Nhận được bản tóm tắt chất lượng cao từ AI Gemini
- Dễ theo dõi: Tất cả dữ liệu được lưu trữ và cập nhật tự động trên Google Sheets
- Đảm bảo chất lượng: Hệ thống cảnh báo lỗi giúp phát hiện và xử lý vấn đề kịp thời
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với API Gemini được kích hoạt
- Tài khoản Google Sheets với bảng tính đã tạo sẵn
- API Key từ NewsAPI
- Tài khoản Gmail để nhận cảnh báo lỗi
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15326](https://n8n.io/workflows/15326)
2. Click vào nút "Import" ở góc trên bên phải
3. Trong n8n Editor, chọn "Import from URL" và dán link trên
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Workflow Config & Variables** (Node "set"):
   - Cấu hình các biến quan trọng:
     - `newsApiKey`: API Key từ NewsAPI
     - `query`: Từ khóa tìm kiếm (ví dụ: "regulatory news")
     - `articleLimit`: Số lượng bài báo tối đa cần xử lý
     - `delayTime`: Thời gian chờ giữa các bài báo (để tránh bị giới hạn API)
     - `spreadsheetId`: ID của Google Sheet đã tạo

2. **Fetch News from NewsAPI** (Node "httpRequest"):
   - Đảm bảo URL API là `https://newsapi.org/v2/everything`
   - Kiểm tra các tham số query bao gồm:
     - `q`: Sử dụng biến `{{$node["Workflow Config & Variables"].json["query"]}}`
     - `apiKey`: Sử dụng biến `{{$node["Workflow Config & Variables"].json["newsApiKey"]}}`
     - `sortBy`: Thiết lập thành "publishedAt" để lấy tin mới nhất

3. **Generate Summary & Key Changes (AI)** (Node "googleGemini"):
   - Kết nối với tài khoản Google Cloud của bạn
   - Cấu hình prompt cho AI (ví dụ: "Summarize the main points of this article about regulatory news")

4. **Update Sheet with AI Results** và **Store Raw Articles to Sheet** (2 Node "googleSheets"):
   - Kết nối với tài khoản Google của bạn
   - Đảm bảo các cột trong Google Sheet đã được tạo sẵn:
     - Title, Source, Published Date, Content, Summary, Key Changes

5. **Email Error Alert** (Node "gmail"):
   - Kết nối với tài khoản Gmail của bạn
   - Cấu hình email nhận cảnh báo (ví dụ: admin@congty.com)

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Node" trên node "Run Workflow Manually" để test chạy dữ liệu mẫu
2. Sau khi test thành công, click vào nút "Activate" ở góc trên bên phải để bật workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thiết lập lịch chạy tự động hàng ngày để nhận tin tức mới nhất
- Kết hợp với Slack để nhận thông báo tức thời khi có tin tức mới
- Thêm node để lưu log hoạt động của workflow
- Tạo báo cáo định kỳ từ dữ liệu trong Google Sheets
- Thiết lập cảnh báo khi có từ khóa quan trọng xuất hiện trong tin tức

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình theo dõi và tổng hợp tin tức quy định hàng ngày. Với sự kết hợp của NewsAPI, AI Gemini và Google Sheets, các sếp có thể tiết kiệm thời gian đáng kể và nhận được thông tin chất lượng cao để đưa ra quyết định nhanh chóng. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của đội ngũ!