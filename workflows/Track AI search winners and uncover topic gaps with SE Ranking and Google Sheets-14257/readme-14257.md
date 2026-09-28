---
title: "🚀 Theo dõi người chiến thắng tìm kiếm AI và phát hiện khoảng trống chủ đề với SE Ranking và Google Sheets"
description: "Tự động hóa nghiên cứu thị trường và chiến lược nội dung bằng cách theo dõi vị trí AI của bạn so với đối thủ và phát hiện khoảng trống chủ đề chưa được đáp ứng"
slug: "theo-doi-nguoi-chien-thang-tim-kiem-ai-voi-seranking-va-google-sheets"
tags: [n8n, automation, no-code, seo, market-research, ai-rag]
keywords: [n8n workflow, tự động hóa, nghiên cứu thị trường, seo, ai search]
---

# 🚀 Theo dõi người chiến thắng tìm kiếm AI và phát hiện khoảng trống chủ đề với SE Ranking và Google Sheets

[Các sếp đang gặp khó khăn khi phải theo dõi thủ công vị trí AI của mình trên các công cụ tìm kiếm như ChatGPT, Perplexity và Gemini. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình nghiên cứu thị trường và chiến lược nội dung, tiết kiệm thời gian quý giá và nhận được dữ liệu chính xác hơn.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảng xếp hạng AI tìm kiếm** với tỷ lệ thị phần trên ChatGPT, Perplexity, Gemini, AI Overviews và AI Mode
- **Khoảng trống từ khóa hữu cơ** nơi đối thủ xếp hạng nhưng bạn không, được sắp xếp theo lượng truy cập
- **Từ khóa câu hỏi** mà khán giả của bạn đặt ra xung quanh chủ đề hạt giống của bạn - sẵn sàng viết nội dung
- **Chủ đề AI** nơi bạn đã xuất hiện trong kết quả tìm kiếm AI
- **Chủ đề SEO** nơi đối thủ của bạn xuất hiện trong câu trả lời AI nhưng bạn không
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Node cộng đồng SE Ranking đã cài đặt
- Token API SE Ranking ([Lấy token tại đây](https://online.seranking.com/admin.api.dashboard.html))
- Tài khoản Google Sheets (tùy chọn)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/14257)
2. Click vào nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor của bạn, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Domain Input Form"**:
   - Không cần cấu hình gì, chỉ cần kích hoạt workflow

2. **Node "Configuration"**:
   - Thay đổi `volume_min` để tăng hoặc giảm ngưỡng lượng truy cập từ khóa
   - Thay đổi `source` cho cơ sở dữ liệu khu vực khác (us, uk, de, fr, es, etc.)
   - Thay đổi `seed_topic` bằng bất kỳ từ khóa nào mà doanh nghiệp của bạn nhắm đến để nhận một tập hợp mới các câu hỏi

3. **Node "Get AI leaderboard"**:
   - Chọn credentials "seRankingApi"
   - Không cần thay đổi tham số

4. **Node "Export to Sheets: AI Leaderboard"**:
   - Chọn credentials "googleSheetsOAuth2Api"
   - Thiết lập URL bảng tính Google Sheets của bạn

5. **Node "Get keyword gaps 1st Competitor" và "Get keyword gaps 2nd Competitor"**:
   - Chọn credentials "seRankingApi"
   - Không cần thay đổi tham số

6. **Node "Export to Sheets: Organic Gaps"**:
   - Chọn credentials "googleSheetsOAuth2Api"
   - Thiết lập URL bảng tính Google Sheets của bạn

7. **Node "Get question keywords"**:
   - Chọn credentials "seRankingApi"
   - Không cần thay đổi tham số

8. **Node "Export to Sheets: Questions"**:
   - Chọn credentials "googleSheetsOAuth2Api"
   - Thiết lập URL bảng tính Google Sheets của bạn

9. **Node "Get your AI topics"**:
   - Chọn credentials "seRankingApi"
   - Không cần thay đổi tham số

10. **Node "Export to Sheets: Your AI Topics"**:
    - Chọn credentials "googleSheetsOAuth2Api"
    - Thiết lập URL bảng tính Google Sheets của bạn

11. **Node "Get 1st competitor AI topics" và "Get 2nd competitor AI topics"**:
    - Chọn credentials "seRankingApi"
    - Không cần thay đổi tham số

12. **Node "Export to Sheets: Competitor AI Topics"**:
    - Chọn credentials "googleSheetsOAuth2Api"
    - Thiết lập URL bảng tính Google Sheets của bạn

#### 3. Kích hoạt ⚡️
1. Kiểm tra chạy thử với dữ liệu mẫu
2. Bật Active workflow
3. Mở node "Domain Input Form" và sao chép "Production URL"
4. Chia sẻ liên kết này với các thành viên trong nhóm để họ có thể nhập tên miền và đối thủ của họ

### ✍️ Mẹo & gợi ý nâng cao
- Thay đổi thời gian chờ trong các node "Wait" để điều chỉnh tốc độ xử lý
- Thêm node gửi email báo cáo tự động sau khi workflow hoàn thành
- Tích hợp với Slack để thông báo khi có thay đổi đáng kể trong vị trí AI
- Tạo báo cáo định kỳ bằng cách lập lịch chạy workflow hàng tuần

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian quý giá trong việc theo dõi vị trí AI của mình và phát hiện khoảng trống chủ đề chưa được đáp ứng. Bằng cách tự động hóa toàn bộ quá trình nghiên cứu thị trường và chiến lược nội dung, các sếp có thể tập trung vào việc tạo nội dung chất lượng cao và phát triển doanh nghiệp của mình.