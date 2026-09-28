---
title: "🚀 Tự động hóa Nghiên cứu thị trường với Gemini & OpenAI: Tóm tắt nội dung đối thủ hàng tuần"
description: "Workflow n8n tự động thu thập, phân tích và tổng hợp nội dung từ trang web đối thủ hàng tuần, giúp các sếp tiết kiệm thời gian và nhận thông tin thị trường một cách chính xác và cá nhân hóa."
slug: "tu-dong-hoa-nghien-cuu-thi-truong-gemini-openai"
tags: [n8n, automation, no-code, ai, market-research]
keywords: [n8n workflow, tự động hóa, nghiên cứu thị trường, tóm tắt nội dung, ai]
---

# 🚀 Tự động hóa Nghiên cứu thị trường với Gemini & OpenAI: Tóm tắt nội dung đối thủ hàng tuần

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động thu thập và phân tích nội dung từ 10+ trang web đối thủ mỗi tuần
- Chính xác: Sử dụng AI Gemini và OpenAI để tóm tắt nội dung một cách chuyên nghiệp
- Cá nhân hóa: Nhận báo cáo hàng tuần theo định dạng và nội dung mà các sếp yêu cầu
- Hoạt động liên tục: Chạy tự động mỗi Chủ Nhật lúc 5AM mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Sheets (để lưu trữ dữ liệu đầu vào và kết quả)
- API Key từ Google Gemini và OpenAI
- API Key từ Firecrawl (dịch vụ thu thập nội dung web)
- Tài khoản Gmail (để gửi báo cáo)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/6637)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Input Links" (Google Sheets)**:
   - Chọn credentials Google Sheets OAuth2
   - Điền ID của Google Sheet chứa danh sách URL đối thủ
   - Đảm bảo Sheet có các cột: URL, Company

2. **Node "Firecrawl_Links" và "Firecrawl_Markdown"**:
   - Chọn credentials HTTP Header Auth
   - Thêm API Key của Firecrawl vào header Authorization
   - Lưu ý: Firecrawl Free Tier chỉ cho phép 10 request/phút (1 request/6 giây)

3. **Node "Gemini 2.5 Flash: Temp 0"**:
   - Chọn credentials Google Palm API
   - Điền API Key của Google Gemini
   - Tùy chỉnh prompt nếu cần

4. **Node "OpenAI o4-mini"**:
   - Chọn credentials OpenAI API
   - Điền API Key của OpenAI
   - Đảm bảo tài khoản có đủ credit để sử dụng model o4-mini

5. **Node "Append row in sheet"**:
   - Chọn credentials Google Sheets OAuth2
   - Điền ID của Google Sheet lưu kết quả
   - Đảm bảo Sheet có các cột: URL, Title, Author, Summary, Published Date, Company, Crawled Date

6. **Node "Send a message" (Gmail)**:
   - Chọn credentials Gmail OAuth2
   - Điền địa chỉ email nhận báo cáo
   - Tùy chỉnh nội dung email theo yêu cầu

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Chạy từng node từ đầu đến cuối với 1-2 URL mẫu
   - Kiểm tra kết quả ở mỗi node để đảm bảo dữ liệu được xử lý đúng
2. Bật Active workflow:
   - Sau khi test thành công, bật chế độ Active cho workflow
   - Đảm bảo workflow sẽ chạy tự động mỗi Chủ Nhật lúc 5AM

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Teams**:
   - Thêm node gửi báo cáo đến kênh Slack/Teams thay vì email
   - Sử dụng node "Slack" hoặc "Microsoft Teams" trong n8n

2. **Lưu log hoạt động**:
   - Thêm node ghi log hoạt động vào Google Sheets hoặc cơ sở dữ liệu
   - Giúp theo dõi lịch sử hoạt động và phát hiện lỗi

3. **Gửi báo cáo định kỳ**:
   - Tùy chỉnh thời gian chạy trong node "Schedule Trigger"
   - Có thể chạy hàng ngày/tháng một lần thay vì hàng tuần

4. **Xử lý lỗi tự động**:
   - Thêm node xử lý lỗi và gửi thông báo khi workflow gặp sự cố
   - Giúp các sếp nhận thông báo kịp thời khi có vấn đề xảy ra

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc nghiên cứu thị trường. Bằng cách tự động thu thập, phân tích và tổng hợp nội dung từ trang web đối thủ hàng tuần, các sếp có thể nhận được thông tin thị trường một cách chính xác và cá nhân hóa. Hãy áp dụng ngay để nâng cao hiệu quả làm việc của mình!