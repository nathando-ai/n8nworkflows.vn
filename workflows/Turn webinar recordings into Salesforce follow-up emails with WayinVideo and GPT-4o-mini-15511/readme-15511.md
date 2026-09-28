---
title: "🚀 Tự động hóa Email theo dõi sau Webinar với WayinVideo + GPT-4o-mini + Salesforce"
description: "Tự động hóa quy trình gửi email theo dõi cá nhân hóa sau webinar bằng công nghệ AI, Salesforce và Gmail - tiết kiệm thời gian và tăng hiệu quả chăm sóc khách hàng"
slug: "tu-dong-hoa-email-theo-doi-sau-webinar"
tags: [n8n, automation, no-code, salesforce, gmail, ai, langchain]
keywords: [n8n workflow, tự động hóa, webinar, salesforce, gmail, ai, langchain]
---

# 🚀 Tự động hóa Email theo dõi sau Webinar với WayinVideo + GPT-4o-mini + Salesforce

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có biết rằng sau mỗi buổi webinar, việc gửi email theo dõi cá nhân hóa cho từng khách hàng tiềm năng là một công việc cực kỳ tốn thời gian và công sức? Với workflow này, các sếp có thể tự động hóa hoàn toàn quy trình này chỉ trong vài phút, giúp tiết kiệm thời gian quý giá và tăng hiệu quả chăm sóc khách hàng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa hoàn toàn quy trình gửi email theo dõi sau webinar
- Tăng hiệu quả: Gửi email cá nhân hóa cho từng khách hàng tiềm năng
- Tăng độ chính xác: Sử dụng công nghệ AI để tạo nội dung email phù hợp
- Hoạt động liên tục: Workflow chạy tự động 24/7, không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WayinVideo với API Key
- Tài khoản OpenAI với API Key
- Tài khoản Salesforce với quyền truy cập vào Lead object
- Tài khoản Gmail với quyền truy cập vào API
- Tài khoản Google Sheets với quyền truy cập vào API
- Salesforce Lead object có trường custom `Webinar_Name__c` để lưu tên webinar
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow, các sếp có thể thực hiện theo các bước sau:

1. Truy cập vào trang [n8n.io/workflows/15511](https://n8n.io/workflows/15511)
2. Nhấn vào nút "Import" để tải xuống file JSON của workflow
3. Trong n8n Editor, nhấn vào nút "Import from File" và chọn file JSON vừa tải xuống

Hoặc, các sếp cũng có thể copy/paste JSON của workflow vào n8n Editor bằng cách:

1. Truy cập vào trang [n8n.io/workflows/15511](https://n8n.io/workflows/15511)
2. Copy toàn bộ JSON của workflow
3. Trong n8n Editor, nhấn vào nút "Import from Clipboard" và dán JSON vào

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node 2. WayinVideo — Submit Summarization**:
   - Thay thế `YOUR_WAYINVIDEO_API_KEY` bằng API Key của tài khoản WayinVideo
   - Cấu hình các tham số khác như `webinarUrl`, `webinarTitle`, `hostName`, `companyName`, `webinarDate`, `ctaLink`

2. **Node 4. WayinVideo — Get Summary Results**:
   - Thay thế `YOUR_WAYINVIDEO_API_KEY` bằng API Key của tài khoản WayinVideo
   - Cấu hình các tham số khác như `webinarUrl`, `webinarTitle`, `hostName`, `companyName`, `webinarDate`, `ctaLink`

3. **Node 10. OpenAI — GPT-4o-mini Model**:
   - Kết nối với tài khoản OpenAI của các sếp
   - Đảm bảo rằng các sếp đã cấu hình đúng model là `gpt-4o-mini`

4. **Node 8. Salesforce — Query Registered Leads**:
   - Kết nối với tài khoản Salesforce của các sếp
   - Đảm bảo rằng trường `Webinar_Name__c` đã được tạo trong Salesforce Lead object
   - Nếu tên trường khác, các sếp cần chỉnh sửa truy vấn SOQL trong node này

5. **Node 12. Gmail — Send Follow-Up Email**:
   - Kết nối với tài khoản Gmail của các sếp
   - Cấu hình các tham số như `from`, `to`, `subject`, `body`

6. **Node 13. Salesforce — Log Email as Activity**:
   - Kết nối với tài khoản Salesforce của các sếp
   - Cấu hình các tham số như `WhoId`, `Subject`, `Description`

7. **Node 14. Google Sheets — Log Follow-Up**:
   - Kết nối với tài khoản Google Sheets của các sếp
   - Thay thế `YOUR_GOOGLE_SHEET_ID` bằng ID của Google Sheet
   - Đảm bảo rằng Google Sheet đã có tab `Follow-up Log` với các cột: `Webinar Title`, `Lead Email`, `Lead Name`, `Lead Company`, `Email Subject`, `Personalized Intro`, `Salesforce Lead ID`, `Salesforce Task ID`, `Sent Status`, `Sent On`

#### 3. Kích hoạt ⚡️
Sau khi các sếp đã cấu hình xong các node quan trọng, các sếp cần thực hiện các bước sau để kích hoạt workflow:

1. Test run dữ liệu mẫu:
   - Các sếp có thể tạo một bản ghi mẫu trong Salesforce Lead object với trường `Webinar_Name__c` được điền
   - Sau đó, các sếp có thể chạy workflow với dữ liệu mẫu để kiểm tra xem workflow có hoạt động đúng không

2. Bật Active workflow:
   - Sau khi đã kiểm tra và đảm bảo workflow hoạt động đúng, các sếp có thể bật Active workflow để workflow chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram: Các sếp có thể thêm các node để gửi thông báo qua Slack/Telegram khi workflow hoàn thành
- Lưu log chi tiết: Các sếp có thể thêm các node để lưu log chi tiết của workflow vào Google Sheets hoặc Salesforce
- Gửi báo cáo định kỳ: Các sếp có thể thêm các node để gửi báo cáo định kỳ về hiệu quả của workflow

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình gửi email theo dõi sau webinar, tiết kiệm thời gian và tăng hiệu quả chăm sóc khách hàng. Các sếp chỉ cần cấu hình một lần và workflow sẽ chạy tự động 24/7, không cần can thiệp thủ công. Hãy áp dụng ngay workflow này để nâng cao hiệu quả kinh doanh của các sếp!