---
title: "🚀 Tự động hóa Sales Lead Pipeline từ Job Postings với Scrape.do, Apollo.io & OpenAI"
description: "Xây dựng hệ thống tìm kiếm khách hàng tiềm năng tự động từ các tin tuyển dụng trên Indeed, làm giàu dữ liệu qua Apollo.io và cá nhân hóa tin nhắn bằng OpenAI."
slug: "tu-dong-hoa-sales-lead-pipeline-scrape-do-apollo-openai"
tags: [n8n, automation, lead-generation, apollo-io, openai, scrape-do]
keywords: [n8n workflow, sales lead pipeline, scrape indeed jobs, apollo.io enrichment, openai personalized message]
---

# 🚀 Tự động hóa Sales Lead Pipeline từ Job Postings với Scrape.do, Apollo.io & OpenAI

Việc thủ công tìm kiếm khách hàng tiềm năng (leads) từ các trang tuyển dụng, tra cứu thông tin công ty và tìm kiếm người ra quyết định (decision-makers) tốn rất nhiều thời gian của đội ngũ sales. Chưa kể việc phải viết từng tin nhắn kết nối mang tính cá nhân hóa cho từng khách hàng lại càng ngốn thời gian. 

Workflow n8n này sẽ giải quyết triệt để bài toán trên bằng cách tự động hóa 100% quy trình: Quét tin tuyển dụng trên Indeed bằng **Scrape.do**, làm giàu thông tin công ty và tìm kiếm nhân sự cấp cao qua **Apollo.io**, sử dụng **OpenAI** để soạn tin nhắn kết nối siêu cá nhân hóa, sau đó lưu toàn bộ vào **Google Sheets**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện**: Từ việc quét job, lọc công ty, tìm người ra quyết định (CTO, Founder...) đến tạo nội dung outreach.
- **Cá nhân hóa sâu sắc**: OpenAI tự động đọc ngữ cảnh tuyển dụng để viết tin nhắn kết nối LinkedIn cực kỳ bén và đúng trọng tâm.
- **Tiết kiệm 90% thời gian**: Đội ngũ sales chỉ việc nhận danh sách leads sạch và sẵn sàng outreach mỗi ngày.
- **Quản lý tập trung**: Dữ liệu công ty và leads được phân loại rõ ràng, lưu trữ ngăn nắp trên Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Tài khoản Scrape.do** (để cào dữ liệu Indeed qua API).
- **Tài khoản Apollo.io** (để tìm kiếm thông tin tổ chức và nhân sự).
- **Tài khoản OpenAI API** (để tạo tin nhắn cá nhân hóa).
- **Google Sheets API / Credentials** (để lưu trữ dữ liệu).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã nguồn JSON của workflow này và paste trực tiếp vào giao diện n8n Editor, hoặc import file JSON thông qua menu.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình các thành phần sau:
- **Form Trigger (Optional) / Manual Trigger**: Nơi khởi chạy quy trình. Các sếp có thể dùng Form để nhập nhanh vị trí tuyển dụng hoặc chạy thủ công.
- **Set Search Parameters**: Cập nhật các tham số tìm kiếm mục tiêu của các sếp như chức danh công việc (`Job Title`), địa điểm (`Location`), và khoảng thời gian đăng tin (`Days`).
- **Scrape.do Indeed API**: Điền `httpQueryAuth` credentials của Scrape.do để cào dữ liệu từ Indeed.
- **Google Sheets (Add New Company & Save Leads to Sheet)**: Chuẩn bị một file Google Sheets có 2 tab riêng biệt đặt tên là `Companies` và `Leads`. Cấu hình kết nối Google Sheets trong 2 node này để ghi dữ liệu đúng vào từng tab.
- **Apollo Organization Search & People Search**: Cấu hình API key của Apollo.io (`httpHeaderAuth`) để tìm kiếm thông tin chi tiết công ty và danh sách người ra quyết định (ví dụ: CTO, Founder).
- **Generate Personalized Message**: Chọn credential `openAiApi`, kiểm tra `prompt` để đảm bảo AI hiểu đúng văn phong và mục tiêu tiếp cận khách hàng.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (`Test workflow`) với một vài từ khóa mẫu để kiểm tra dữ liệu trả về ở từng node.
- Bật công tắc `Active` để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo**: Thêm node Slack hoặc Telegram ngay sau node `Save Leads to Sheet` để bắn thông báo về máy khi có lead mới chất lượng.
- **Chống trùng lặp**: Tận dụng tab `Companies` trên Google Sheets để lọc bớt các công ty đã quét trước đó, tránh gọi API lãng phí.
- **Xử lý Rate Limit**: Nếu cào số lượng lớn, hãy thêm node `Wait` giữa các bước gọi API Apollo để tránh bị khóa tính năng do vượt giới hạn request.

### 📌 Kết luận
Workflow này là một "vũ khí" cực mạnh mẽ giúp các đội ngũ Sales B2B tiếp cận đúng khách hàng tiềm năng ngay khi họ có nhu cầu tuyển dụng. Hãy thiết lập ngay hôm nay để tối ưu hóa phễu bán hàng của các sếp!