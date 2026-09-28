---
title: "🚀 Tự động trích xuất và phân tích cảm xúc bình luận Facebook bằng AI Gemini với n8n"
description: "Hướng dẫn tự động hóa quy trình thu thập toàn bộ bình luận từ bài viết Facebook, phân tích cảm xúc (Sentiment Analysis) bằng Google Gemini AI và lưu trữ trực tiếp vào Google Sheets."
slug: "tu-dong-trich-xuat-phan-tich-cam-xuc-binh-luan-facebook-gemini-n8n"
tags: [n8n, automation, facebook-graph-api, google-gemini, sentiment-analysis, google-sheets]
keywords: [n8n workflow, phân tích cảm xúc facebook, facebook graph api n8n, google gemini n8n, tự động hóa marketing, sentiment analysis n8n]
---

# 🚀 Tự động trích xuất và phân tích cảm xúc bình luận Facebook bằng AI Gemini

Các sếp có đang đau đầu khi phải thủ công đọc hàng trăm, hàng ngàn bình luận trên các bài đăng Facebook để xem khách hàng đang khen hay chê sản phẩm? Việc này không chỉ tốn hàng giờ đồng hồ mà còn dễ bỏ sót các phản hồi quan trọng, khiến việc đo lường sức khỏe thương hiệu (Brand Reputation) hay hiệu quả chiến dịch marketing trở nên chậm trễ.

Giải pháp ở đây là gì? Một hệ thống tự động hóa 100% không cần code (No-code) với **n8n**, giúp tự động kéo toàn bộ bình luận từ Facebook Page, sử dụng **Google Gemini AI** để phân loại cảm xúc (Tích cực, Tiêu cực, Trung tính) và lưu trữ gọn gàng vào **Google Sheets**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần copy-paste thủ công hay đọc từng bình luận một.
- **Phân tích thông minh:** AI Google Gemini tự động đánh giá chính xác sắc thái cảm xúc của khách hàng (Sentiment Analysis).
- **Quản lý dữ liệu trực quan:** Mọi bình luận, ID bài viết và kết quả phân tích được tự động đồng bộ vào Google Sheets, chống trùng lặp dữ liệu (append-or-update).
- **Hoạt động quy mô lớn:** Xử lý mượt mà các bài viết có lượng tương tác khổng lồ nhờ tính năng phân trang (Pagination) và chia lô (Batching).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** (Self-hosted hoặc n8n Cloud).
- **Facebook Graph API Credentials:** Token truy cập để lấy thông tin bài đăng và bình luận.
- **Google Gemini API Key / Google PaLM API:** Cho node AI phân tích cảm xúc.
- **Google Sheets:** Tài khoản cấu hình OAuth2 để ghi dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tạo một workflow mới trên n8n, sau đó copy toàn bộ mã nguồn JSON của workflow này và dán trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Node `Set Fb post ID`**: Nhập ID bài viết Facebook (`Facebook Post ID`) mà các sếp muốn phân tích vào đây.
- **Node `Get Fb Post` & `Get Fb comments`**: Cần kết nối tài khoản `Facebook Graph API` credentials hợp lệ để có quyền truy cập dữ liệu trang.
- **Node `Google Gemini Chat Model`**: Thêm thông tin xác thực API của Google AI (Gemini) để mô hình có nguyên liệu phân tích.
- **Node `Add comment` (Google Sheets)**: 
  - Clone mẫu Google Sheet tại [đường dẫn này](https://docs.google.com/spreadsheets/d/1xMLAtBgSdxh7Cc--J6fExGb2ul48QTvN-KgGitEGgZw/edit?usp=sharing).
  - Kết nối tài khoản Google Sheets OAuth2.
  - Đảm bảo các cột như `POST ID`, `COMMENT ID`, `COMMENT`, và `SENTIMENT` đã sẵn sàng để ghi dữ liệu theo cơ chế cập nhật tự động (Append or Update).
- **Node `Call 'Facebook'`**: Đảm bảo node này trỏ chính xác đến sub-workflow phụ trách việc xử lý từng batch bình luận.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute workflow** thủ công ở node `When clicking ‘Execute workflow’` với một ID bài viết mẫu để kiểm tra kết quả trả về.
- Sau khi test thành công, gạt công tắc **Active** để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo tức thời:** Nối thêm node **Telegram** hoặc **Slack** để nhận cảnh báo ngay lập tức khi có bình luận mang cảm xúc "Tiêu cực" (Negative) vượt ngưỡng cho phép, giúp xử lý khủng hoảng truyền thông kịp thời.
- **Báo cáo định kỳ:** Kết hợp thêm node **Schedule Trigger** để chạy quét tự động các bài viết hot mỗi ngày/tuần và gửi tổng hợp báo cáo qua Email cho đội ngũ marketing.
- **Lưu trữ Log lỗi:** Thêm nhánh xử lý lỗi (Error Trigger) để ghi nhận lại nếu gọi API Facebook bị quá giới hạn (Rate Limit).

### 📌 Kết luận
Việc thấu hiểu khách hàng trên mạng xã hội chưa bao giờ dễ dàng đến thế khi kết hợp sức mạnh tự động hóa của n8n và trí tuệ nhân tạo Gemini. Hãy áp dụng ngay workflow này để nâng tầm chiến lược chăm sóc khách hàng và quản trị thương hiệu của các sếp!