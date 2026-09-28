---
title: "🚀 Tự động theo dõi xu hướng hashtag Instagram và gửi báo cáo qua Email với n8n, Apify và Gmail"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu hashtag Instagram qua Apify, phân tích xu hướng bằng code, lưu trữ và gửi báo cáo email định kỳ qua Gmail."
slug: "tu-dong-theo-doi-xu-huong-hashtag-instagram-n8n-apify-gmail"
tags: [n8n, automation, instagram, apify, gmail, marketing, market-research]
keywords: [n8n workflow, tự động hóa instagram, apify instagram scraper, gửi email báo cáo tự động, nghiên cứu thị trường]
---

# 🚀 Tự động theo dõi xu hướng hashtag Instagram và gửi báo cáo qua Email

Việc theo dõi các xu hướng hashtag trên Instagram bằng tay để làm nghiên cứu thị trường (Market Research) hay phân tích đối thủ tốn rất nhiều thời gian và công sức. Các Marketer thường xuyên phải lướt, lọc và tổng hợp dữ liệu thủ công mỗi ngày. 

Giải pháp? Workflow n8n tự động hóa 100% này sẽ thay bạn làm tất cả: tự động quét các từ khóa/hashtag từ bảng dữ liệu, gọi API của Apify để cào bài viết Instagram, sắp xếp, chấm điểm xu hướng bằng code, lưu trữ dữ liệu và gửi một bản báo cáo chi tiết trực tiếp qua Gmail cho bạn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Không cần thủ công tìm kiếm và thống kê bài viết trên Instagram nữa.
- **Báo cáo định kỳ tự động:** Nhận email tổng hợp xu hướng hashtag ngay trong hộp thư theo lịch hẹn (hàng ngày/hàng tuần).
- **Dữ liệu được lưu trữ chuẩn chỉnh:** Mọi kết quả phân tích được tự động lưu vào Data Table để tiện tra cứu lịch sử.
- **Tùy biến linh hoạt:** Dễ dàng thay đổi thuật toán chấm điểm, sắp xếp bài viết theo ý muốn thông qua các code node.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Apify Account:** Tài khoản Apify và Apify API Key để gọi Scraper Instagram.
- **Gmail Account:** Tài khoản Gmail để cấu hình gửi email báo cáo (OAuth2).
- **Data Table:** n8n Data Table chứa danh sách các từ khóa/hashtag Instagram cần theo dõi.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của bạn, hoặc copy toàn bộ mã JSON và dán (Paste) vào màn hình làm việc của n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Scheduled Run Trigger:** Cấu hình tần suất chạy mong muốn (ví dụ: Chạy mỗi ngày một lần vào lúc 8h sáng, hoặc mỗi tuần...).
- **Read Queries from Table (`dataTable`):** Trỏ tới Data Table chứa danh sách các từ khóa/hashtag Instagram mà các sếp muốn hệ thống theo dõi.
- **Loop Over Queries1 (`splitInBatches`):** Thiết lập kích thước batch (số lượng từ khóa xử lý trong một lần chạy) để tránh vượt quá giới hạn API.
- **Fetch Instagram Posts via Apify1 (`httpRequest`):** 
  - Thêm **Apify API Key** vào cấu hình xác thực (Credentials: `apifyApi` hoặc `httpHeaderAuth`).
  - Cấu hình URL endpoint của Actor Apify chuyên cào Instagram.
- **Sort Instagram Results & Rank Instagram Posts1 (`code`):** Các sếp có thể tinh chỉnh logic code bên trong các node này nếu muốn thay đổi cách tính điểm (score) hoặc bộ lọc bài viết nổi bật.
- **Save Results to Data Table (`dataTable`):** Trỏ tới Data Table đích để lưu trữ kết quả bài viết đã được phân tích.
- **Send Instagram Report Email (`gmail`):** 
  - Kết nối tài khoản Gmail của bạn thông qua `gmailOAuth2`.
  - Điền địa chỉ email nhận báo cáo và cấu hình tiêu đề/nội dung email hiển thị dữ liệu thống kê.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm (Test Run) với dữ liệu mẫu xem email có gửi về và data có lưu đúng không.
- Nếu mọi thứ chạy mượt mà, hãy bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Chat App:** Nối thêm node Telegram hoặc Slack để nhận thông báo nhanh ngay khi có báo cáo hoàn thành.
- **Mở rộng nguồn dữ liệu:** Thay vì chỉ đọc từ Data Table của n8n, các sếp có thể kết nối với Google Sheets để dễ dàng thêm/sửa danh sách hashtag cần quét.
- **Phân tích AI chuyên sâu:** Kết nối thêm OpenAI hoặc Anthropic Claude node để AI đọc nội dung các bài viết hàng đầu và viết tóm tắt xu hướng thị trường (Market Trend Summary) trước khi gửi email.

### 📌 Kết luận
Workflow này là trợ thủ đắc lực cho các team Marketing, Agency hoặc nhà sáng tạo nội dung muốn nắm bắt xu hướng Instagram nhanh chóng mà không tốn một chút sức lực thủ công nào. Hãy "lên đồ" và cài đặt ngay hôm nay để tối ưu hóa hiệu suất công việc của các sếp!