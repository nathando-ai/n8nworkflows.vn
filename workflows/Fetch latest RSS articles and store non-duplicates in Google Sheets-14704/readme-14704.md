---
title: "🚀 Tự Động Thu Thập Bài Viết RSS Và Lọc Trùng Lặp Vào Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n giúp tự động quét danh sách URL, tìm nguồn RSS hợp lệ, lọc bỏ bài viết trùng lặp và lưu trữ thông minh vào Google Sheets."
slug: "tu-dong-thu-thap-bai-viet-rss-google-sheets"
tags: [n8n, automation, rss, google-sheets, market-research, no-code]
keywords: [n8n workflow, tự động hóa rss, crawl rss google sheets, lọc bài viết trùng lặp n8n, market research automation]
---

# 🚀 Tự Động Thu Thập Bài Viết RSS Và Lọc Trùng Lặp Vào Google Sheets

Các sếp làm trong lĩnh vực nghiên cứu thị trường (*Market Research*), làm nội dung hay tổng hợp tin tức chắc chắn đều hiểu cảm giác "ngợp thở" khi phải hàng ngày thủ công đi kiểm tra hàng chục website, đọc RSS feed, lọc xem bài nào đã đăng rồi, bài nào chưa để đưa lên bảng quản lý. Công việc này vừa nhàm chán, tốn thời gian lại rất dễ bỏ sót thông tin.

Hiểu được nỗi đau đó, workflow n8n **"Fetch latest RSS articles and store non-duplicates in Google Sheets"** do *WeblineIndia* phát triển sẽ thay các sếp làm toàn bộ quy trình này một cách tự động 100%: từ quét nguồn, kiểm tra RSS, lấy bài viết mới nhất, lọc trùng lặp thông minh cho đến lưu trữ gọn gàng vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Không cần click thủ công, tự động quét nguồn định kỳ.
- **Lọc trùng lặp thông minh:** Hệ thống tự đối chiếu tiêu đề mới với dữ liệu cũ trong Google Sheets, đảm bảo không có bài viết bị lưu lặp lại.
- **Tiết kiệm thời gian cực lớn:** Giảm từ vài tiếng đồng hồ tổng hợp tin tức xuống 0 phút mỗi ngày.
- **Dữ liệu sạch sẽ, trực quan:** Mọi bài viết mới đều được phân loại và lưu trữ gọn gàng để phục vụ cho các chiến dịch content hoặc phân tích thị trường tiếp theo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đã được cấu hình sẵn.
- Tài khoản Google có quyền truy cập **Google Sheets**.
- Chuẩn bị sẵn 1 file Google Sheets chứa danh sách các website/URL cần kiểm tra nguồn RSS và một bảng/sheet để lưu trữ kết quả bài viết.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, sau đó dán (Paste) trực tiếp vào giao diện n8n Editor của mình hoặc import file JSON tải về từ thư viện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình các node cốt lõi sau:
- **Node `RSS URLs` & `Fetch title` & `Add data in sheets` & `Append row in sheet` (Google Sheets):** 
  - Kết nối tài khoản Google thông qua **Credentials** (`googleSheetsOAuth2Api`).
  - Chọn chính xác file Google Spreadsheet ID và Sheet Name chứa danh sách URL nguồn và nơi lưu trữ dữ liệu bài viết mới.
- **Node `Get Website Data` & `RSS Read` & `Fetch Each URL`:** Các node này thực hiện nhiệm vụ HTTP request để tìm kiếm xem URL nào có hỗ trợ RSS feed. Các sếp có thể giữ nguyên cấu trúc code JavaScript có sẵn trong các node `Code` (*Check RSS URLs*, *Get Titles List*, *Check if title exits in sheet*...) vì tác giả đã viết sẵn thuật toán xử lý mảng và so khớp chuỗi rất tối ưu.
- **Node `Stop if no Article found` & `Stop if no Url found` (`stopAndError`):** Giúp dừng workflow ngay lập tức nếu không tìm thấy URL hợp lệ hoặc không có bài viết mới, tránh tốn tài nguyên chạy ngầm.

#### 3. Kích hoạt ⚡️
- Bấm nút **"When clicking ‘Execute workflow’"** (`manualTrigger`) để test thủ công lần đầu xem dữ liệu đổ về Google Sheets có chuẩn chỉnh chưa.
- Sau khi test xanh mướt (success), các sếp có thể thay đổi Trigger thành **Schedule Trigger** (chạy định kỳ hàng giờ/hàng ngày) và bấm **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node Telegram hoặc Slack ở cuối workflow để mỗi khi có bài viết mới được lưu vào Google Sheets, hệ thống sẽ bắn một tin nhắn thông báo tóm tắt tiêu đề bài viết về điện thoại cho các sếp.
- **Xử lý lỗi:** Cấu hình thêm đường dẫn lỗi (Error Trigger) để nếu Google Sheets quá tải hoặc lỗi mạng, hệ thống sẽ tự động gửi email cảnh báo.
- **Mở rộng nguồn:** Thêm các từ khóa lọc hoặc phân loại chuyên ngành ngay trong các node `Code` để tự động gán nhãn (tag) cho từng bài viết trước khi ghi vào sheet.

### 📌 Kết luận
Workflow **Fetch latest RSS articles and store non-duplicates in Google Sheets** là một trợ thủ đắc lực cho những ai làm trong ngành truyền thông, nghiên cứu thị trường hoặc quản lý nội dung. Hãy áp dụng ngay vào hệ thống n8n của các sếp để giải phóng sức lao động thủ công ngay hôm nay!