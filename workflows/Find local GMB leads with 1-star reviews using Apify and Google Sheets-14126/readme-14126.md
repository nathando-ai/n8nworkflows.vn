---
title: "🚀 Tìm kiếm khách hàng tiềm năng GMB có đánh giá 1 sao tự động với Apify và Google Sheets"
description: "Tự động hóa quy trình tìm kiếm doanh nghiệp địa phương có đánh giá 1 sao trên Google Maps thông qua Apify, lọc dữ liệu thông minh và lưu trữ vào Google Sheets phục vụ dịch vụ quản lý danh tiếng."
slug: "tim-kiem-khach-hang-gmb-1-sao-apify-google-sheets"
tags: [n8n, automation, no-code, apify, google-sheets, lead-generation]
keywords: [n8n workflow, apify google maps scraper, gmb lead finder, tu dong hoa lead generation, quan ly danh tieng doanh nghiep]
---

# 🚀 Tự Động Tìm Kiếm Khách Hàng Tiềm Năng GMB Có Đánh Giá 1 Sao

Các sếp làm dịch vụ Digital Marketing, Agency quản lý danh tiếng (Reputation Management) hay SEO Local chắc chắn đều hiểu việc tìm kiếm các doanh nghiệp đang gặp "phốt" hoặc có điểm đánh giá thấp trên Google My Business (GMB) thủ công cực kỳ tốn thời gian. Việc này đòi hỏi phải tra cứu từng doanh nghiệp, đọc từng review và lọc dữ liệu bằng tay.

Workflow n8n này sinh ra để giải quyết triệt để vấn đề đó! Nó tự động hóa toàn bộ quy trình: nhận yêu cầu từ Web Form, kích hoạt Apify để quét dữ liệu Google Maps bất đồng bộ, lọc ra các doanh nghiệp có đánh giá 1 sao (những đối tượng đang cực kỳ cần dịch vụ chăm sóc, cải thiện uy tín) và tự động ghi kết quả vào một tab riêng trên Google Sheets. Tất cả diễn ra hoàn toàn tự động 100% không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chỉ cần nhập loại hình kinh doanh và khu vực qua form, hệ thống tự động lo phần còn lại.
- **Tiếp cận đúng "nỗi đau":** Lọc chính xác các doanh nghiệp có đánh giá 1 sao — tệp khách hàng tiềm năng chất lượng cao cho dịch vụ quản lý danh tiếng.
- **Lưu trữ khoa học:** Tự động tạo một tab riêng kèm timestamp trên Google Sheets cho mỗi lần tìm kiếm, không lo bị đè dữ liệu.
- **Vận hành trơn tru:** Cơ chế lặp (polling) thông minh và xử lý lỗi tự động giúp đảm bảo không bỏ sót dữ liệu từ Apify.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Apify Account:** Tài khoản Apify kèm API Token để gọi dịch vụ Google Maps Scraper.
- **Google Sheets:** Tài khoản Google để kết nối OAuth2 và lưu trữ dữ liệu lead.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc copy toàn bộ JSON và dán trực tiếp vào giao diện làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số sau trong các node trọng điểm:

- **Node `Build Search Query` (Set):** 
  - Tại đây, các sếp cần dán **Google Sheet ID** của file Google Sheets chuẩn bị sẵn vào trường `googleSheetId`. ID này nằm trên URL của file Google Sheets (đoạn nằm giữa `/d/` và `/edit`).
- **Node `Start Apify Scraper Run` & `Poll Apify Run Status` & `Fetch Scraped Dataset` (HTTP Request):**
  - Cần thêm **Credentials loại HTTP Header Auth**. 
  - Header name: `Authorization`
  - Header value: `Bearer YOUR_APIFY_TOKEN` (Thay thế `YOUR_APIFY_TOKEN` bằng mã API Token thực tế từ tài khoản Apify của các sếp).
- **Node `Create Tab for This Run` & `Write Results to Sheet` (Google Sheets):**
  - Kết nối tài khoản **Google Sheets OAuth2 API** của các sếp.
  - Đảm bảo quyền truy cập vào file Google Sheet đã khai báo ở bước Set.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test run) bằng cách submit thông tin mẫu trên Web Form (`GMB Lead Form`).
- Kiểm tra dữ liệu trả về trên Apify và Google Sheets xem đã chính xác chưa.
- Sau khi mọi thứ chạy mượt mà, gạt công tắc sang **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node Telegram hoặc Slack sau bước ghi dữ liệu vào Google Sheets để nhận thông báo ngay lập tức mỗi khi có một danh sách lead mới được quét xong.
- **Mở rộng tệp dữ liệu:** Có thể tinh chỉnh thông số `maxCrawledPlacesPerSearch` và `maxReviews` trong cấu hình Apify để quét sâu hơn, lấy nhiều doanh nghiệp và nhiều đánh giá chi tiết hơn.
- **Tự động hóa outreach:** Kết hợp thêm các node AI (như OpenAI) để soạn thảo sẵn email chăm sóc cá nhân hóa dựa trên nội dung các đánh giá 1 sao mà doanh nghiệp đó đang gặp phải.

### 📌 Kết luận
Workflow tìm kiếm lead GMB này là một cỗ máy tự động hóa cực kỳ mạnh mẽ giúp các agency và đội ngũ sales tiết kiệm hàng chục giờ đồng hồ mỗi tuần. Hãy thiết lập ngay hôm nay để tối ưu hóa phễu tìm kiếm khách hàng tiềm năng của doanh nghiệp!