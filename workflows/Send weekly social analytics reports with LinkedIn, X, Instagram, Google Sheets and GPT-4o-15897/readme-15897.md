---
title: "📊 Tự động hóa báo cáo phân tích mạng xã hội hàng tuần với LinkedIn, X, Instagram, Google Sheets và GPT-4o"
description: "Hướng dẫn chi tiết cách tự động thu thập dữ liệu từ LinkedIn, X (Twitter) và Instagram, tính toán điểm tương tác trọng lượng (WES), tạo báo cáo AI và gửi email hàng tuần. Giải pháp hoàn toàn không cần code cho các chuyên gia marketing và nghiên cứu thị trường."
slug: "tu-dong-hoa-bao-cao-phan-tich-mang-xa-hoi-hang-tuan"
tags: [n8n, automation, no-code, marketing, social-media, ai, google-sheets, linkedin, twitter, instagram]
keywords: [n8n workflow, tự động hóa báo cáo, phân tích mạng xã hội, WES scoring, AI insights, marketing automation]
---

# 📊 Tự động hóa báo cáo phân tích mạng xã hội hàng tuần với LinkedIn, X, Instagram, Google Sheets và GPT-4o

[Các sếp marketing và chuyên gia nghiên cứu thị trường thường phải tốn nhiều thời gian để thu thập dữ liệu từ nhiều nền tảng mạng xã hội, tính toán các chỉ số quan trọng và tạo báo cáo hàng tuần. Workflow này giúp tự động hóa toàn bộ quy trình này trong vòng 90 giây mỗi tuần, mang lại dữ liệu chính xác và báo cáo chuyên nghiệp hàng tuần mà không cần can thiệp thủ công.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động thu thập dữ liệu từ 3 nền tảng lớn trong 90 giây mỗi tuần.
- **Dữ liệu chính xác**: Tính toán điểm tương tác trọng lượng (WES) dựa trên trọng số do các sếp cấu hình.
- **Báo cáo chuyên nghiệp**: Nhận báo cáo hàng tuần với dữ liệu phân tích và gợi ý chiến lược từ AI.
- **Hoạt động liên tục**: Workflow chạy tự động mỗi thứ Hai lúc 9h sáng mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản LinkedIn, X (Twitter) và Instagram với quyền truy cập dữ liệu.
- API keys cho LinkedIn, X, Instagram, OpenAI và Google Sheets.
- Địa chỉ email SMTP để gửi báo cáo.
- Google Sheets để lưu trữ dữ liệu thô.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15897](https://n8n.io/workflows/15897)
2. Nhấn nút "Import" và chọn "Import from URL"
3. Dán link workflow vào ô nhập liệu
4. Nhấn "Import" để tải workflow vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Every Monday 9 AM"**:
   - Đảm bảo múi giờ của n8n server trùng với múi giờ mong muốn (UTC+2 cho Helsinki).

2. **Node "WES Config"**:
   - Điều chỉnh trọng số tương tác (likes, comments, shares, saves) theo nhu cầu của các sếp.
   - Mặc định: likes 1, comments 3, shares 5, saves 4.

3. **Node "Get LinkedIn Posts"**:
   - Thiết lập biến môi trường `LINKEDIN_OWNER_URN` với URN của tài khoản LinkedIn.
   - Kết nối credentials LinkedIn OAuth2.

4. **Node "Search Tweets"**:
   - Thiết lập biến môi trường `TWITTER_SEARCH_QUERY` với truy vấn tìm kiếm mong muốn.
   - Kết nối credentials X (Twitter) OAuth2.

5. **Node "Get media"**:
   - Kết nối credentials Instagram.

6. **Node "Log Raw Posts to Sheets"**:
   - Thiết lập biến môi trường `ANALYTICS_SPREADSHEET_ID` với ID của Google Sheet.
   - Kết nối credentials Google Sheets.
   - Đảm bảo Google Sheet có các cột: Date, Platform, Content Preview, Impressions, Engagement Score, URL.

7. **Node "AI Strategy Insights"**:
   - Kết nối credentials OpenAI.
   - Có thể điều chỉnh prompt trong node này để phù hợp với nhu cầu phân tích.

8. **Node "Email Weekly Report"**:
   - Cập nhật địa chỉ email gửi và nhận trong node này.
   - Kết nối credentials SMTP/email.

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Execute Workflow" để kiểm tra dữ liệu mẫu.
2. Sau khi kiểm tra thành công, nhấn nút "Activate" để kích hoạt workflow.
3. Workflow sẽ chạy tự động mỗi thứ Hai lúc 9h sáng.

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Teams**: Thêm node để gửi báo cáo đến kênh Slack/Teams của nhóm.
2. **Lưu log chi tiết**: Thêm node để lưu log chi tiết của quá trình chạy workflow.
3. **Báo cáo định kỳ**: Có thể điều chỉnh lịch trình để gửi báo cáo theo tuần, tháng hoặc quý.
4. **Tùy chỉnh báo cáo**: Điều chỉnh template email để phù hợp với nhu cầu của các sếp.

### 📌 Kết luận
Workflow này giúp các sếp marketing và chuyên gia nghiên cứu thị trường tiết kiệm thời gian quý giá, thu thập dữ liệu chính xác và nhận báo cáo chuyên nghiệp hàng tuần. Với việc tự động hóa toàn bộ quy trình, các sếp có thể tập trung vào việc phân tích dữ liệu và đưa ra quyết định chiến lược hiệu quả hơn. Hãy áp dụng ngay để nâng cao hiệu quả làm việc của nhóm!