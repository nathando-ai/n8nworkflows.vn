---
title: "🚀 Tự động trích xuất sản phẩm tốt nhất từ mọi website với Dumpling AI và GPT-4o"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa nghiên cứu thị trường, cào dữ liệu website, chụp ảnh màn hình và phân tích bằng AI để tìm top sản phẩm giá trị."
slug: "trich-xuat-top-san-pham-website-dumpling-ai-gpt-4o"
tags: [n8n, automation, ai, market-research, gpt-4o, dumpling-ai]
keywords: [n8n workflow, trích xuất sản phẩm, dumpting ai, gpt-4o vision, tự động hóa nghiên cứu thị trường]
---

# 🚀 Tự động trích xuất sản phẩm tốt nhất từ mọi website với Dumpling AI và GPT-4o

Các sếp có bao giờ đau đầu khi cần nghiên cứu thị trường, theo dõi sản phẩm bán chạy hay đối thủ cạnh tranh trên các sàn thương mại điện tử lớn (như Amazon, Shopee, Tiki...) chưa? Việc cào dữ liệu (scraping) thủ công hoặc dùng các công cụ truyền thống thường gặp lỗi do chống bot, thay đổi giao diện HTML liên tục, tốn hàng giờ đồng hồ ngồi lọc dữ liệu.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ thông minh: Chỉ cần nhập một đường dẫn (URL) website, hệ thống sẽ tự động cào trang, chụp ảnh màn hình, sử dụng mắt thần **GPT-4o (Multimodal AI)** để phân tích, chọn ra top 3 sản phẩm có giá trị tốt nhất, lưu thẳng vào Google Sheets và gửi email thông báo cho các sếp ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Thay vì lướt web thủ công chọn lọc, hệ thống tự động hoàn thành từ A-Z chỉ trong vài phút.
- **Phân tích hình ảnh thông minh:** Bất chấp giao diện web phức tạp hay chống bot, GPT-4o nhìn trực tiếp vào ảnh chụp màn hình để đọc tên, giá, số lượt đánh giá và thông tin giao hàng như con người.
- **Dữ liệu đồng bộ:** Tự động lưu trữ gọn gàng vào Google Sheets để tiện theo dõi, báo cáo.
- **Thông báo tức thì:** Nhận ngay link kết quả qua Gmail ngay khi tiến trình hoàn tất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy mượt mà, các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Dumpling AI Token** (Lưu dưới dạng HTTP Header Auth credentials).
- **OpenAI API Key** (Đã kích hoạt model GPT-4o).
- **Google Sheets & Gmail Credentials** (Để lưu dữ liệu và gửi email).
- **Google Sheet mẫu** với các cột: `product name`, `price`, `reviews no.`, `free_delivery_date`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ thư viện n8n (Link gốc: [n8n Workflow #8565](https://n8n.io/workflows/8565)) hoặc copy mã nguồn JSON và paste trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 8 nodes chính phối hợp nhịp nhàng với nhau. Các sếp chú ý cấu hình kỹ các điểm sau:

- **Receive Website URL (`formTrigger`):** Node khởi đầu dạng biểu mẫu (Form). Các sếp có thể tuỳ biến giao diện form để người dùng nhập URL website cần cào.
- **Crawl Website with Dumpling AI (`httpRequest`):** Kết nối với Dumpling AI thông qua `httpHeaderAuth` để thực hiện yêu cầu cào trang web từ URL đã nhận.
- **Split Crawled Pages (`splitOut`):** Tách dữ liệu trả về từ Dumpling AI thành các trang riêng biệt để xử lý tuần tự.
- **Take Screenshot of Page (`httpRequest`):** Tiếp tục gọi Dumpling AI (qua `httpHeaderAuth`) để chụp ảnh màn hình trang kết quả.
- **Analyze Screenshot with GPT-4o (`openAi`):** Sử dụng credential `openAiApi` với thao tác phân tích hình ảnh (`resource: image`, `operation: analyze`). Tại đây, các sếp viết Prompt hướng dẫn GPT-4o tìm ra top sản phẩm có giá trị tốt nhất (tên, giá, review, ngày giao hàng miễn phí).
- **Parse and Extract Product Data (`code`):** Node JavaScript xử lý dữ liệu JSON thô trả về từ AI, làm sạch và định dạng lại cấu trúc dữ liệu.
- **Save Products to Google Sheet (`googleSheets`):** Kết nối bằng `googleSheetsOAuth2Api`, chọn đúng file Google Sheet và mapping các trường dữ liệu tương ứng (`product name`, `price`, `reviews no.`, `free_delivery_date`).
- **Send Email with Product Link (`gmail`):** Sử dụng `gmailOAuth2` để tự động gửi email tổng hợp kèm link xem dữ liệu cho người yêu cầu.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** chạy thử với một URL mẫu (ví dụ: một trang danh mục sản phẩm trên Amazon).
- Kiểm tra xem dữ liệu đã đổ về Google Sheets và email đã được gửi đi chưa.
- Nếu mọi thứ chạy mượt, bật công tắc **Active** ở góc trên bên phải để đưa workflow vào trạng thái vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot:** Thay vì dùng Form Trigger, các sếp có thể đổi thành Telegram Trigger hoặc Slack Trigger để gửi URL qua chat và nhận kết quả ngay trong nhóm làm việc.
- **Mở rộng Prompt AI:** Tùy chỉnh câu lệnh trong node GPT-4o để trích xuất thêm các thông tin nâng cao như *chất liệu, màu sắc, điểm đánh giá trung bình, link chi tiết sản phẩm*.
- **Lưu lịch sử chạy:** Thêm một node Google Sheets hoặc Database phụ để ghi log mỗi lần chạy thành công/thất bại nhằm phục vụ việc kiểm toán (audit).

### 📌 Kết luận
Workflow "Extract Top Products from Any Website with Dumpling AI and GPT-4o" là một cỗ máy tự động hóa hoàn hảo cho các nhà nghiên cứu thị trường, nhà quản lý thương mại điện tử hoặc bất kỳ ai muốn nắm bắt xu hướng sản phẩm nhanh chóng. Hãy cài đặt ngay lên hệ thống n8n của các sếp để tối ưu hóa công việc hàng ngày!