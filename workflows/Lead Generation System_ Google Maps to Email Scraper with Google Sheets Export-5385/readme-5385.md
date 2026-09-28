---
title: "🚀 Xây dựng hệ thống quét Leads tự động từ Google Maps và Email với n8n"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình tìm kiếm khách hàng tiềm năng (Leads) từ Google Maps, cào website và trích xuất email không cần API trả phí với n8n."
slug: "lead-generation-google-maps-email-scraper-n8n"
tags: [n8n, automation, no-code, lead-generation, google-maps, web-scraping, google-sheets]
keywords: [n8n workflow, cào dữ liệu google maps, lấy email tự động, lead generation system, n8n scraper, nick saraev]
---

# 🚀 Xây dựng hệ thống quét Leads tự động từ Google Maps và Email với n8n

Việc tìm kiếm khách hàng tiềm năng (Lead Generation) thủ công bằng cách tìm kiếm trên Google Maps, truy cập từng website và copy email là một công việc cực kỳ tốn thời gian, nhàm chán và không hiệu quả. 

Được xây dựng bởi chuyên gia tự động hóa **Nick Saraev**, workflow này giải quyết hoàn toàn bài toán trên bằng cách tự động hóa 100% quy trình: Quét Google Maps -> Lọc website doanh nghiệp -> Cào dữ liệu & Trích xuất Email -> Lưu trữ trực tiếp vào Google Sheets mà **không cần sử dụng bất kỳ API trả phí nào**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Thu thập hàng trăm thông tin doanh nghiệp và email chỉ với một cú click chuột.
- **Tiết kiệm chi phí:** Không tốn tiền mua các công cụ Lead Gen đắt đỏ hay sử dụng API Google Maps trả phí.
- **Thông minh & An toàn:** Tích hợp cơ chế chờ (Wait) và xử lý hàng loạt (Batching) giúp né tránh việc bị chặn IP (Rate Limiting) khi cào dữ liệu website.
- **Dữ liệu sạch:** Tự động lọc các domain rác, loại bỏ bản ghi trùng lặp và đồng bộ thẳng vào Google Sheets.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Google:** Để kết nối và ghi dữ liệu vào Google Sheets.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n.io (Template #5385) hoặc copy toàn bộ mã JSON và dán trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 15 nodes được chia thành 4 bước chính. Các sếp cần chú ý cấu hình các điểm sau:

- **Scrape Google Maps (HTTP Request Node):** 
  - Tại đây, các sếp cần thay đổi URL tìm kiếm mặc định thành từ khóa và khu vực mục tiêu của mình (Ví dụ: Thay đổi thành tìm kiếm "Digital Marketing Agency in Ho Chi Minh").
  - Node này sử dụng phương thức cào HTML trực tiếp mà không cần API key.
- **Xử lý JavaScript (Extract URLs & Extract Emails Nodes - Code Nodes):**
  - Các node dạng `code` sử dụng Regex để tự động bóc tách URL website chính xác từ mã nguồn Google Maps và tìm kiếm định dạng email chuẩn trong HTML của website đó. Không cần sửa code trừ khi muốn tùy chỉnh Regex.
- **Kiểm soát lưu lượng (Limit & Wait Nodes):**
  - Node `Limit` giúp giới hạn số lượng xử lý trong quá trình test (hãy tăng giới hạn này khi chạy thật).
  - Các node `Wait` và `Loop Over Items` (`splitInBatches`) cực kỳ quan trọng để tạo khoảng nghỉ giữa các lần cào website, tránh việc bị hệ thống đích chặn IP.
- **Lưu trữ dữ liệu (Add to Sheet - Google Sheets Node):**
  - Cần kết nối tài khoản Google (`googleSheetsOAuth2Api`).
  - Chọn file Google Sheets và Sheet tương ứng để hệ thống tự động append (thêm) dòng dữ liệu mới bao gồm tên doanh nghiệp, website và email thu thập được.

#### 3. Kích hoạt ⚡️
- Nhấn nút **When clicking ‘Test workflow’** để chạy thử với số lượng giới hạn nhằm kiểm tra dữ liệu trả về trong Google Sheets.
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, bật trạng thái **Active** cho workflow để bắt đầu sử dụng lâu dài.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack ở cuối workflow để nhận thông báo ngay khi hệ thống quét xong một danh sách leads mới.
- **Mở rộng nguồn quét:** Có thể nhân bản luồng đầu vào để quét thêm các nền tảng danh bạ doanh nghiệp khác ngoài Google Maps.
- **Tự động gửi Email Marketing:** Kết nối trực tiếp danh sách email vừa thu được vào các chiến dịch gửi email tự động (như Lemlist, Mailchimp hoặc qua SMTP node của n8n).

### 📌 Kết luận
Hệ thống Lead Generation từ Google Maps và Email Scraper này là một vũ khí cực kỳ mạnh mẽ giúp các sếp tự động hóa hoàn toàn khâu tìm kiếm khách hàng đầu phễu. Hãy thiết lập ngay hôm nay để giải phóng sức lao động và tối ưu hóa chi phí marketing cho doanh nghiệp!