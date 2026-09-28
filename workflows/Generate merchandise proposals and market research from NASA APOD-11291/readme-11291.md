---
title: "🚀 Tự động hóa sáng tạo sản phẩm Print-on-Demand & Nghiên cứu thị trường từ NASA APOD với n8n"
description: "Xây dựng quy trình tự động lấy ảnh thiên văn NASA hàng ngày, tạo mockup sản phẩm, nghiên cứu thị trường trên Etsy qua Apify, phân tích AI và quản lý phê duyệt qua Slack."
slug: "tu-dong-hoa-san-pham-nasa-apod-etsy-n8n"
tags: [n8n, automation, ai, print-on-demand, openai, apify, slack]
keywords: [n8n workflow, tự động hóa print-on-demand, nasa apod automation, nghiên cứu thị trường etsy, apify openai n8n]
---

# 🚀 Tự động hóa sáng tạo sản phẩm Print-on-Demand & Nghiên cứu thị trường từ NASA APOD

Các sếp làm trong lĩnh vực Print-on-Demand (POD) hoặc thương mại điện tử chắc chắn hiểu rõ việc tốn bao nhiêu thời gian để tìm kiếm ý tưởng thiết kế, nghiên cứu giá đối thủ trên Etsy, tính toán lợi nhuận và ra quyết định sản xuất mỗi ngày. Quy trình thủ công này vừa chậm, vừa dễ bỏ lỡ các xu hướng hình ảnh độc quyền.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n tự động hóa từ A-Z: biến bức ảnh thiên văn hàng ngày của NASA thành một ý tưởng sản phẩm hoàn chỉnh, phân tích thị trường Etsy tự động bằng AI, gửi đề xuất qua Slack để các sếp duyệt "Go/No-Go" và tự động lưu trữ tài liệu nếu được thông qua!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% nguồn cảm hứng**: Lấy ngay bức ảnh thiên văn đỉnh cao từ NASA APOD mỗi ngày làm chất liệu thiết kế độc quyền.
- **Nghiên cứu thị trường chớp nhoáng**: AI kết hợp Apify tự động quét giá đối thủ trên Etsy và tính toán biên độ lợi nhuận chuẩn xác.
- **Quy trình phê duyệt thông minh (Approval Loop)**: Gửi báo cáo chi tiết kèm hình ảnh trực tiếp lên Slack, các sếp chỉ cần bấm nút duyệt mà không cần mở nhiều tab.
- **Lưu trữ đồng bộ**: Tự động tải ảnh chất lượng cao lên Google Drive và ghi log thông tin sản phẩm vào Notion DB khi được phê duyệt.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **NASA API Key**: Để lấy dữ liệu Astronomy Picture of the Day.
- **OpenAI API Key**: Phục vụ việc sinh từ khóa SEO và lời khuyên marketing.
- **Cloudinary**: Dùng để xử lý hình ảnh và tạo mockup sản phẩm tự động.
- **Apify Account**: Sử dụng actor trích xuất dữ liệu từ Etsy (`dtrungtin/etsy-scraper`).
- **Slack App / Bot Token**: Để nhận thông báo và tương tác phê duyệt.
- **Google Drive & Notion**: Tài khoản để lưu trữ tài sản số và quản lý cơ sở dữ liệu sản phẩm.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, dán trực tiếp vào n8n Editor (hoặc import file JSON tải từ nguồn) để bắt đầu.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 15 nodes được chia thành 4 giai đoạn chính. Các sếp cần cấu hình kỹ các điểm sau:

- **Workflow Configuration1 (Set)**: Khai báo các biến cấu hình cơ bản như thông tin Cloudinary, chi phí sản xuất cơ bản, giá mục tiêu...
- **Get NASA APOD1 (NASA)**: Kết nối tài khoản NASA API để lấy dữ liệu ảnh thiên văn mỗi ngày.
- **Generate Keywords & Check Logo1 & AI Marketing Advisor1 (OpenAI)**: Cấu hình credentials OpenAI và kiểm tra prompt để AI tạo từ khóa chuẩn SEO và lời khuyên kinh doanh.
- **Create Mockup with Cloudinary1 (HTTP Request)**: Thiết lập API gọi tới Cloudinary để lồng ghép ảnh NASA vào template sản phẩm (ví dụ: áo thun).
- **Search Etsy Market1 (Apify)**: Chọn actor Etsy Scraper (`dtrungtin/etsy-scraper`) trên Apify và điền API Token để quét đối thủ cạnh tranh.
- **Send Slack Proposal1 (Slack)**: Trỏ tới Channel ID cụ thể trên Slack của team các sếp để gửi bản đề xuất sản phẩm kèm mockup.
- **Wait for User Decision1 & Check User Decision1 (Wait & Switch)**: Xử lý logic chờ phản hồi từ người dùng (Phê duyệt hoặc Từ chối).
- **Save to Google Drive1 & Save to Notion DB1 (Google Drive & Notion)**: Điền **Google Drive Folder ID** và **Notion Database ID** để hệ thống tự động lưu file ảnh gốc và thông tin sản phẩm khi có lệnh "Go".

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Test Workflow**) với node **Schedule Trigger1** để kiểm tra toàn bộ luồng dữ liệu từ đầu đến cuối.
- Kiểm tra kết quả trên Slack và xác nhận luồng lưu trữ vào Google Drive/Notion hoạt động chuẩn xác.
- Bật công tắc **Active workflow** để hệ thống tự động chạy theo lịch trình (Schedule).

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Thay vì chỉ dùng Slack, các sếp có thể tích hợp thêm node Telegram để nhận đề xuất sản phẩm mọi lúc mọi nơi trên điện thoại.
- **Tự động đăng bài lên mạng xã hội**: Thêm các node Social Media (như Facebook Page, Twitter/X, Instagram) vào nhánh "Đã phê duyệt" để tự động xuất bản sản phẩm lên các kênh bán hàng.
- **Lưu log lỗi**: Cắm thêm nhánh Error Trigger để nếu quá trình quét Etsy hoặc tạo Mockup gặp lỗi, hệ thống sẽ tự động bắn tin nhắn báo cáo về kênh Slack riêng của dev.

### 📌 Kết luận
Workflow này là một minh chứng tuyệt vời cho việc ứng dụng AI và No-Code vào thương mại điện tử. Thay vì tốn hàng giờ nghiên cứu thủ công, các sếp giờ đây có thể tự động hóa toàn bộ phễu từ ý tưởng đến nghiên cứu thị trường. Hãy triển khai ngay hôm nay để tối ưu hóa năng suất kinh doanh của các sếp!