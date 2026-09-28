---
title: "🚀 Tự động hóa tìm việc hàng tuần với Gemini 1.5 Pro và Decodo Scraper"
description: "Workflow n8n tự động tìm kiếm việc làm, phân tích nội dung bằng AI và so khớp CV - giải pháp tiết kiệm thời gian 100% không cần code cho nhà tuyển dụng và ứng viên."
slug: "tu-dong-hoa-tim-viec-hang-tuan-voi-gemini-decodo"
tags: [n8n, automation, no-code, AI, HR, web-scraping]
keywords: [n8n workflow, tự động hóa tìm việc, AI phân tích công việc, Decodo scraper, Gemini 1.5 Pro]
---

# 🚀 Tự động hóa tìm việc hàng tuần với Gemini 1.5 Pro và Decodo Scraper

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải tra cứu hàng chục trang web tuyển dụng mỗi tuần để tìm việc làm phù hợp? Hay phải tốn thời gian đọc từng bài đăng tuyển dụng dài dòng để so khớp với CV của mình? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này trong vòng 15 phút - chỉ với một lần cài đặt!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động thu thập hàng trăm bài đăng tuyển dụng mỗi tuần
- **Phân tích thông minh**: AI tóm tắt nội dung công việc phức tạp thành thông tin ngắn gọn
- **So khớp chính xác**: AI so khớp CV với yêu cầu tuyển dụng một cách chuyên nghiệp
- **Báo cáo tự động**: Nhận email báo cáo hàng tuần với danh sách việc làm phù hợp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với API key cho Google Gemini
- Tài khoản Decodo với API key (cần gói Web Scraping API Advanced)
- Tài khoản Gmail để gửi báo cáo
- CV của bạn dưới dạng văn bản (đã sẵn sàng để so khớp)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/11125](https://n8n.io/workflows/11125)
2. Nhấn nút "Import" để tải workflow về máy
3. Trong n8n Editor, nhấn "Import from File" và chọn file JSON đã tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
**Group A: Cấu hình tìm kiếm việc làm**
- **Set Search Config1**: Chỉnh sửa các tham số tìm kiếm:
  - `query`: Từ khóa tìm kiếm (ví dụ: "Nhân viên kinh doanh Hà Nội")
  - `location`: Địa điểm (ví dụ: "Hà Nội")
  - `job_type`: Loại công việc (ví dụ: "Full-time")
  - `num_results`: Số lượng kết quả trả về (gợi ý: 50-100)

- **Google Search Jobs1**: Cấu hình credentials cho Decodo API
  - Tạo mới credential "Decodo Credentials API" và nhập API key từ tài khoản Decodo

**Group B: Scrape và xử lý nội dung**
- **Scrape Page HTML1**: Đảm bảo đã cấu hình proxy trong tài khoản Decodo để tránh bị chặn

**Group C: Phân tích và so khớp CV**
- **Job Matcher Agent1**: Cấu hình credentials cho Google Gemini
  - Tạo mới credential "Google Gemini Credentials" và nhập API key từ Google Cloud
  - Chỉnh sửa prompt để phù hợp với CV của bạn (ví dụ: "So khớp CV với yêu cầu tuyển dụng, đánh giá mức độ phù hợp từ 1-10")

- **Send Email Report1**: Cấu hình credentials cho Gmail
  - Tạo mới credential "Gmail OAuth2 API" và cấu hình OAuth2
  - Chỉnh sửa địa chỉ email nhận báo cáo

#### 3. Kích hoạt ⚡️
1. Chạy test với nút "Execute Workflow"
2. Kiểm tra kết quả ở node cuối cùng (Send Email Report1)
3. Bật "Active" workflow để chạy tự động hàng tuần

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy chỉnh báo cáo**: Chỉnh sửa template email để bao gồm các thông tin quan trọng nhất
- **Lọc kết quả**: Thêm node để lọc các công việc không phù hợp trước khi gửi email
- **Kết hợp với Slack**: Thêm node để gửi báo cáo lên kênh Slack của team
- **Lưu log**: Thêm node để lưu trữ lịch sử tìm kiếm cho phân tích dài hạn

### 📌 Kết luận
Workflow này không chỉ tiết kiệm thời gian mà còn nâng cao chất lượng tìm việc bằng cách sử dụng công nghệ AI. Các sếp chỉ cần cài đặt một lần và sau đó có thể ngồi lại thư giãn trong khi hệ thống làm việc cho bạn! Hãy thử ngay và biến quy trình tìm việc hàng tuần thành một công việc tự động hoàn toàn.