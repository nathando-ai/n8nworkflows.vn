---
title: "🚀 Tự Động Cào Dữ Liệu Sản Phẩm Amazon Bằng Scrape.do, GPT-4 & Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động trích xuất thông tin sản phẩm Amazon (giá, đánh giá, mô tả) bằng Scrape.do và AI, sau đó lưu trực tiếp vào Google Sheets."
slug: "tu-dong-cao-du-lieu-san-pham-amazon-scrape-do-gpt-4-google-sheets"
tags: [n8n, automation, no-code, amazon-scraper, scrape-do, openai, google-sheets]
keywords: [n8n workflow, cào dữ liệu amazon, scrape.do api, gpt-4o-mini, tự động hóa google sheets, market research]
---

# 🚀 Tự Động Cào Dữ Liệu Sản Phẩm Amazon Bằng Scrape.do, GPT-4 & Google Sheets

Các sếp làm nghiên cứu thị trường (Market Research) hay Dropshipping chắc chắn hiểu rõ nỗi đau khi muốn lấy dữ liệu từ Amazon: chống bot cực gắt, CAPTCHA xuất hiện liên tục và HTML của Amazon thay đổi chóng mặt khiến các code scraper truyền thống "gục ngã" chỉ sau vài ngày.

Việc copy/paste thủ công từng sản phẩm vừa tốn thời gian, vừa dễ sai sót. Giải pháp hoàn hảo ở đây chính là workflow n8n kết hợp **Scrape.do API** (vượt rào chống bot thông minh), **GPT-4o-mini** (lọc và cấu trúc hóa dữ liệu thông minh) và **Google Sheets** (lưu trữ tự động). Tất cả chạy tự động 100% không cần viết code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Vượt tường lửa Amazon dễ dàng:** Nhờ Scrape.do API tự động xoay vòng proxy và xử lý CAPTCHA mà không tốn công cấu hình phức tạp.
- **Trích xuất thông tin chuẩn xác:** AI (GPT-4o-mini) tự động làm sạch và bóc tách tên sản phẩm, giá, mô tả, đánh giá (rating & reviews) gọn gàng.
- **Tự động hóa toàn diện:** Lấy danh sách URL từ Google Sheets, xử lý hàng loạt và tự động ghi kết quả trả ngược lại Google Sheets.
- **Tiết kiệm 95% thời gian:** Thay vì mất hàng giờ liền cào tay, hàng trăm sản phẩm được xử lý chỉ trong vài phút.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Scrape.do:** Đăng ký tại [Scrape.do](https://scrape.do) để lấy API Token.
- **Tài khoản OpenAI:** Lấy API Key để sử dụng model `gpt-4o-mini`.
- **Google Sheets:** Chuẩn bị sẵn một file Google Sheet để đọc URL sản phẩm đầu vào và ghi kết quả đầu ra.
- **Credentials trong n8n:** Google Sheets OAuth2 API và OpenAI API.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor (hoặc import file JSON thông qua menu tuỳ chọn của n8n).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 10 nodes chính hoạt động nhịp nhàng với nhau. Các sếp cần chú ý cấu hình các điểm sau:

- **1. Get Product URLs from Google Sheets**: Chọn đúng Google Sheets Credentials. Trỏ tới file Google Sheet của các sếp và chọn đúng Tab chứa danh sách đường dẫn sản phẩm Amazon (cột chứa URL nên đặt tên là `url`).
- **3. Scrape Product Page HTML (HTTP Request)**: Thêm API Token của Scrape.do vào phần query parameters hoặc header theo tài liệu của Scrape.do để cào mã nguồn trang web Amazon.
- **OpenAI Chat Model & Structured Output Parser**: Kết nối OpenAI Credentials và chọn model `gpt-4o-mini`. Parser sẽ ép AI trả về dữ liệu chuẩn cấu trúc JSON (tên, giá, mô tả, đánh giá...).
- **7. Save Product Data to Google Sheets**: Chọn Google Sheets Credentials, trỏ tới Tab thứ hai trong file Google Sheet dùng để lưu trữ kết quả đầu ra (bao gồm: Tên sản phẩm, mô tả, rating, reviews, giá).

#### 3. Kích hoạt ⚡️
- Bấm nút **"When clicking Test workflow"** để chạy thử nghiệm với một vài dòng dữ liệu mẫu xem hệ thống đã nuốt trọn thông tin chưa.
- Kiểm tra lại Google Sheet xem dữ liệu đã được đổ về đẹp đẽ hay chưa.
- Gạt công tắc sang **Active** để workflow chính thức tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Thông báo:** Thêm node Telegram hoặc Slack vào cuối workflow để nhận tin nhắn báo cáo ngay khi cào xong danh sách sản phẩm.
- **Lên lịch chạy định kỳ (Cron/Schedule Trigger):** Thay thế node Manual Trigger bằng Schedule Trigger để tự động cào giá đối thủ hàng ngày/hàng tuần phục vụ phân tích thị trường.
- **Xử lý lỗi (Error Handling):** Thêm Error Trigger để bắt các URL bị lỗi hoặc hết hạn và ghi log lại, giúp workflow không bị dừng giữa chừng khi gặp URL bất hợp lệ.

### 📌 Kết luận
Workflow "Extract Amazon Product Data with Scrape.do, GPT-4 & Google Sheets" là một cỗ máy tự động hóa cực kỳ mạnh mẽ giúp các sếp giải quyết bài toán thu thập dữ liệu thương mại điện tử mà không lo ngại vấn đề chống bot. Nhanh tay setup ngay để tối ưu hóa quy trình nghiên cứu thị trường của doanh nghiệp nào!