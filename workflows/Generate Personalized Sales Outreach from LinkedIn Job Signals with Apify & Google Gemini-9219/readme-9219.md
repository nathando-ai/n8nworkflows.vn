---
title: "🚀 Tự động hóa tìm kiếm khách hàng tiềm năng LinkedIn và viết email cá nhân hóa với Apify, Apollo & Gemini"
description: "Hướng dẫn chi tiết xây dựng workflow n8n tự động quét tin tuyển dụng LinkedIn, lọc công ty, tìm decision-maker qua Apollo và viết email outreach bằng Google Gemini."
slug: "tu-dong-hoa-tim-kiem-khach-hang-linkedin-apify-gemini-n8n"
tags: [n8n, automation, no-code, apify, apollo, gemini, ai, sales-outreach]
keywords: [n8n workflow, tự động hóa sales, linkedin job scraper, apify n8n, google gemini ai, apollo.io, email outreach]
---

# 🚀 Tự động hóa tìm kiếm khách hàng tiềm năng LinkedIn và viết email cá nhân hóa với Apify, Apollo & Gemini

Việc tìm kiếm khách hàng tiềm năng (Lead Generation) và viết email outreach thủ công thường ngốn rất nhiều thời gian của đội ngũ sales. Các sếp phải mò mẫm trên LinkedIn tìm xem công ty nào đang tuyển dụng, lọc quy mô, tìm người ra quyết định (Decision-maker), tìm email rồi mới ngồi soạn nội dung cá nhân hóa.

Workflow n8n này sẽ thay thế toàn bộ quy trình thủ công đó bằng một hệ thống tự động hóa 100% kết hợp giữa **Apify**, **Apollo.io**, **Google Sheets** và **Google Gemini AI**. Hệ thống sẽ tự động quét tin tuyển dụng, lọc các công ty phù hợp, tìm kiếm người ra quyết định, tìm email xác thực và sử dụng AI để viết nội dung email chào hàng cực kỳ chuẩn xác và cá nhân hóa.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn từ A-Z:** Từ việc quét tín hiệu tuyển dụng trên LinkedIn đến khi ra được danh sách lead hoàn chỉnh có sẵn email và nội dung outreach.
- **Tiết kiệm 90% thời gian:** Không còn phải copy/paste thủ công từng công ty hay tra cứu thông tin người liên hệ.
- **Cá nhân hóa bằng AI:** Google Gemini sẽ phân tích dữ liệu tuyển dụng và thông tin công ty để viết email chào hàng sắc bén, trúng "nỗi đau" của khách hàng.
- **Dữ liệu lưu trữ đồng bộ:** Tự động đẩy toàn bộ lead và nội dung email được tạo vào Google Sheets để dễ dàng theo dõi và chiến dịch hóa.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow này chạy mượt mà, các sếp cần chuẩn bị sẵn:
1. **Tài khoản n8n** (Cloud hoặc Self-hosted).
2. **Tài khoản Apify:** Để chạy scraper quét tin tuyển dụng LinkedIn (`Run the LinkedIn Job Scraper`).
3. **Tài khoản Apollo.io:** Lấy API key để tìm kiếm nhân sự mục tiêu (`Apollo Get Targeted Personnel`) và tìm email (`Apollo Email Finder`).
4. **Google Gemini API Key / Google Cloud Account:** Cấu hình cho model `Google Gemini Chat Model`.
5. **Google Sheets:** File Google Sheets chuẩn bị sẵn các cột để lưu thông tin Lead và nội dung email trả về.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy đoạn mã JSON của workflow này hoặc tải file JSON từ nguồn gốc.
- Mở n8n Editor, chọn **Add workflow** -> Nhấn vào dấu `...` ở góc trên bên phải -> Chọn **Import from File / Clipboard** và dán đoạn JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các node cốt lõi sau để workflow kết nối đúng hệ thống:

- **Run the LinkedIn Job Scraper & Get dataset Items (Apify):** 
  - Kết nối Credentials của Apify.
  - Cấu hình URL tìm kiếm việc làm trên LinkedIn (LinkedIn Job Search URL) để scraper biết cần quét dữ liệu ngành nghề, khu vực nào.
- **Checks Company Size < 250 & Removes HR Related Industry (If nodes):** 
  - Tinh chỉnh điều kiện lọc quy mô nhân sự công ty và loại bỏ các công ty ngành Nhân sự (HR) nếu không phù hợp với chân dung khách hàng (ICP) của các sếp.
- **Apollo Get Targeted Personnel & Apollo Email Finder (HTTP Request):** 
  - Cung cấp API Key của Apollo.io trong phần Header của HTTP Request.
  - Kiểm tra endpoint gọi API tìm kiếm nhân sự theo domain công ty và tìm email cá nhân/doanh nghiệp.
- **Adding Leads to Sheets & Update Sheet with Email (Google Sheets):** 
  - Kết nối Google Account Credentials.
  - Chọn đúng File Google Sheets và Sheet Name dùng để lưu trữ dữ liệu lead (`Adding Leads to Sheets`) và cập nhật email (`Update Sheet with Email`).
- **Lead Email Generator & Google Gemini Chat Model:** 
  - Cấu hình Credentials cho Google Gemini.
  - Thiết lập Prompt trong node `Lead Email Generator` để hướng dẫn AI viết email outreach dựa trên thông tin người nhận, vị trí tuyển dụng và dịch vụ của doanh nghiệp các sếp.
  - Đảm bảo `Structured Output Parser` được cấu hình để trả về đúng định dạng JSON gồm `subject` (tiêu đề) và `email_body` (nội dung email).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** (hoặc dùng `When clicking ‘Execute workflow’` manual trigger) để chạy thử nghiệm với một lượng dữ liệu nhỏ (thông qua node `Limit Companies Search`).
- Kiểm tra kết quả trên Google Sheets xem dữ liệu lead và email do Gemini tạo ra đã chính xác chưa.
- Sau khi test thành công, bật công tắc **Active** góc trên cùng bên phải để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Thêm node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay về máy mỗi khi hệ thống tạo xong một loạt lead mới.
- **Tự động gửi email:** Kết nối node Gmail hoặc Outlook sau bước `Update Sheet with Email` nếu các sếp muốn hệ thống tự động gửi luôn chiến dịch email outreach (hoặc giữ lại ở trạng thái Draft để duyệt thủ công).
- **Lên lịch chạy định kỳ (Cron):** Thay thế `Manual Trigger` bằng `Schedule Trigger` để n8n tự động quét LinkedIn hàng tuần/hàng tháng mà không cần can thiệp thủ công.

### 📌 Kết luận
Workflow tích hợp Apify, Apollo và Google Gemini này là một "vũ khí tối tân" giúp tối ưu hóa toàn bộ phễu tìm kiếm khách hàng B2B. Hãy cài đặt ngay lên hệ thống n8n của các sếp để tiết kiệm hàng chục giờ làm việc mỗi tuần và bứt phá doanh số!