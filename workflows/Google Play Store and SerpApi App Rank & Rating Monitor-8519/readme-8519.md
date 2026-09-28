---
title: "🚀 Tự động theo dõi thứ hạng và đánh giá ứng dụng Google Play Store với n8n & SerpApi"
description: "Hướng dẫn xây dựng workflow tự động hóa kiểm tra thứ hạng SEO và điểm đánh giá trên Google Play Store bằng SerpApi và Google Sheets, giúp tiết kiệm thời gian nghiên cứu thị trường."
slug: "tu-dong-theo-doi-thu-hang-google-play-store-n8n-serpapi"
tags: [n8n, automation, serpapi, google-play, google-sheets, market-research]
keywords: [n8n workflow, theo dõi thứ hạng app, google play seo, serpapi google play, tự động hóa n8n]
---

# 🚀 Tự động theo dõi thứ hạng và đánh giá ứng dụng Google Play Store

Việc theo dõi thủ công thứ hạng từ khóa (App Store Optimization - ASO) và điểm đánh giá của ứng dụng trên Google Play Store là một công việc cực kỳ tẻ nhạt, mất thời gian và dễ bỏ sót số liệu. Các nhà phát triển và marketer thường phải tra cứu từng từ khóa mỗi ngày.

Workflow n8n này sẽ giải quyết hoàn toàn bài toán đó bằng cách tự động hóa 100% quy trình: quét thứ hạng, lấy rating, và cập nhật dữ liệu trực tiếp vào Google Sheets mỗi ngày mà không cần chạm tay vào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa ASO 24/7:** Lịch trình tự động chạy vào lúc 10 AM UTC mỗi ngày để cập nhật vị trí xếp hạng mới nhất.
- **Dữ liệu trực quan:** Tự động đồng bộ kết quả vào 2 trang tính (Google Sheets): một trang lưu log lịch sử và một trang dạng Dashboard cập nhật kết quả mới nhất.
- **Tránh lỗi Rate Limit:** Tích hợp bộ đếm độ trễ thông minh giữa các request để không vượt quá giới hạn API của Google Sheets.
- **Chính xác và nhanh chóng:** Sử dụng SerpApi chuyên dụng để bóc tách dữ liệu Google Play Store chuẩn xác tuyệt đối.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **SerpApi Account:** Tài khoản miễn phí tại [SerpApi](https://serpapi.com/) và lấy API Key.
- **Google Sheets:** Tài khoản Google kết nối với n8n và bản sao Google Sheet mẫu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy toàn bộ mã nguồn JSON dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node sau để hệ thống chạy mượt mà:

- **Schedule Trigger:** Mặc định chạy lúc 10 AM UTC mỗi ngày. Các sếp có thể điều chỉnh lại khung giờ cho phù hợp với múi giờ Việt Nam (UTC+7) hoặc chuyển sang chạy thủ công.
- **Get Keywords and Titles to Match (Google Sheets):** Đọc danh sách từ khóa và tên app cần theo dõi. Các sếp cần copy Google Sheet mẫu [tại đây](https://docs.google.com/spreadsheets/d/1DiP6Zhe17tEblzKevtbPqIygH3dpPCW-NAprxup0VqA/edit?gid=1750873622#gid=1750873622) về tài khoản của mình và kết nối tài khoản Google Sheets vào node này.
- **Search Google Play (SerpApi):** Tạo và thêm thông tin xác thực SerpApi API Key của các sếp vào node này để thực hiện truy vấn tìm kiếm.
- **Loop Over Keywords (Split In Batches) & Wait:** Vòng lặp duyệt qua từng từ khóa, kèm theo node **Wait** (độ trễ 4 giây) để không bị chạm trượt giới hạn gọi API của Google Sheets.
- **Update Rank & Rating Log & Update Latest Run (Google Sheets):** 
  - Ghi log lịch sử chạy và cập nhật bảng Dashboard mới nhất. 
  - Đảm bảo các mapping field khớp với dữ liệu đầu ra:
    - `searched_at`: `{{ $now.toISO() }}`
    - `app_title_to_match`: `{{ $('Loop Over Keywords').item.json.app_title_to_match }}`
    - `keyword`: `{{ $('Search Google Play').item.json.search_parameters.q }}`
    - `rank`: `{{ $json.rank }}`
    - `rating`: `{{ $json.rating }}`
  - Riêng node cập nhật dữ liệu mới nhất (`Update Latest Run`), nhớ set điều kiện match theo `title_keyword_pair`: `{{ $('Loop Over Keywords').item.json.title_keyword_pair }}`.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** để chạy thử nghiệm xem dữ liệu có đổ về Google Sheets thành công hay không.
- Bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp cảnh báo Telegram/Slack:** Thêm một node điều kiện (If) để kiểm tra nếu thứ hạng app rớt đột ngột (ví dụ tụt quá 10 hạng), hãy bắn tin nhắn ngay vào nhóm Telegram của team Product/Marketing.
- **Mở rộng nền tảng:** SerpApi không chỉ hỗ trợ Google Play mà còn hỗ trợ Apple App Store, giúp các sếp theo dõi đa nền tảng cùng lúc.
- **Lưu trữ dữ liệu dài hạn:** Định kỳ hàng tuần gửi một bản báo cáo tổng hợp (Weekly Report) qua Email cho ban lãnh đạo.

### 📌 Kết luận
Workflow này là trợ thủ đắc lực giúp các nhà phát triển ứng dụng và Digital Marketer tiết kiệm hàng giờ đồng hồ kiểm tra thủ công mỗi tuần. Hãy thiết lập ngay hôm nay để nắm bắt chính xác biến động thứ hạng app của mình trên Google Play Store các sếp nhé!