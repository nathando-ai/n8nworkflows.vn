---
title: "🚀 Tự động quét Lead LinkedIn chất lượng cao với Google Sheets và Serper API"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa tìm kiếm, lọc và lưu trữ thông tin lead tiềm năng từ LinkedIn trực tiếp vào Google Sheets, giúp tiết kiệm hàng chục giờ làm việc thủ công."
slug: "tu-dong-quet-lead-linkedin-voi-google-sheets-va-serper-api"
tags: [n8n, automation, no-code, lead-generation, linkedin, google-sheets]
keywords: [n8n workflow, quét lead linkedin, tự động hóa lead generation, serper api, google sheets automation]
---

# 🚀 Tự động quét Lead LinkedIn chất lượng cao với Google Sheets và Serper API

Các sếp có đang cảm thấy mệt mỏi và tốn quá nhiều thời gian mỗi ngày khi phải lên LinkedIn tìm kiếm từng khách hàng tiềm năng (lead), copy thông tin rồi dán thủ công vào Google Sheets? Việc này không chỉ nhàm chán, dễ sai sót mà còn khiến đội ngũ sale bỏ lỡ cơ hội tiếp cận khách hàng vàng.

Giải pháp ở đây là gì? Hãy để **n8n** thay các sếp làm việc đó! Bài viết này sẽ hướng dẫn chi tiết cách vận hành workflow tự động hóa hoàn toàn quy trình tìm kiếm, lọc, xử lý trùng lặp và lưu trữ lead từ LinkedIn thông qua Serper API và Google Sheets. Không cần biết lập trình phức tạp, chỉ cần vài bước cấu hình là hệ thống đã sẵn sàng "cày" lead 24/7 cho các sếp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Tự động hóa hoàn toàn từ khâu đọc tiêu chí tìm kiếm, gọi API tìm kiếm đến việc trích xuất thông tin profile.
- **Dữ liệu sạch, không trùng lặp:** Tích hợp logic xử lý thông minh (Deduplication) giúp loại bỏ các profile đã tồn tại trong Google Sheets hoặc bị trùng lặp trong quá trình quét.
- **Kiểm soát giới hạn (Rate Limit):** Tích hợp sẵn các node quản lý batch và độ trễ (delay) giúp tránh việc bị chặn (ban) từ phía nhà cung cấp API.
- **Hoạt động tự động 24/7:** Chạy ngầm liên tục, giúp đội ngũ sales luôn có nguồn lead mới mỗi khi bắt đầu ngày làm việc.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Google Sheets** chứa bảng dữ liệu mẫu về tiêu chí tìm kiếm và nơi lưu trữ lead.
- **Serper API Key** (hoặc API tương thích để thực hiện các truy vấn tìm kiếm web/LinkedIn).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ kho lưu trữ n8n.
- Trong giao diện n8n Editor, nhấn vào menu **Add workflow** -> Chọn **Import from File** và tải file JSON lên. Hoặc đơn giản là copy toàn bộ mã JSON và dán trực tiếp vào màn hình workflow của n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 14 nodes hoạt động nhịp nhàng với nhau. Các sếp cần chú ý cấu hình kỹ các điểm sau:
- **Get Search Criteria & Read Existing Profiles from Sheets (Google Sheets Nodes):** Kết nối tài khoản Google Sheets của các sếp. Trỏ đúng đến file Google Sheet chứa các tiêu chí tìm kiếm (từ khóa, chức danh, khu vực...) và bảng tính lưu danh sách profile đã quét.
- **Post to LinkedIn Search API (HTTP Request Node):** Cấu hình Endpoint, Method (`POST`/`GET`) và Header chứa API Key (Serper API hoặc API tìm kiếm tương đương) để hệ thống gửi yêu cầu truy vấn dữ liệu.
- **Batch Process 50 Pages & Wait for Rate Limit (Split In Batches & Wait Nodes):** Tinh chỉnh kích thước mỗi mẻ quét (mặc định xử lý theo lô 50 trang) và thời gian chờ (`Wait`) giữa các lần gọi API để tuân thủ giới hạn (Rate limit) của nhà cung cấp dịch vụ.
- **Append New Profiles to Sheets (Google Sheets Node):** Thiết lập operation là `append` để tự động đẩy các profile mới tinh (sau khi đã qua bộ lọc trùng lặp) vào bảng Google Sheets đích.
- **Deduplicate Profiles by URL & Filter New Profiles (Code Nodes):** Kiểm tra kỹ các đoạn mã JavaScript ngắn gọn trong các node này để đảm bảo biến lọc URL trùng lặp khớp chính xác với cột dữ liệu trên Google Sheets của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** tại node `Manual Start` để chạy thử nghiệm (Test run) với một vài tiêu chí mẫu.
- Kiểm tra kết quả trên Google Sheets xem dữ liệu đã được lọc và đổ về đúng định dạng chưa.
- Sau khi test thành công, gạt công tắc **Active** ở góc trên cùng bên phải để workflow chính thức tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node **Telegram** hoặc **Slack** ngay sau node `Append New Profiles to Sheets` để nhận thông báo tức thì về điện thoại mỗi khi có lead mới chất lượng được tìm thấy.
- **Tự động hóa lịch chạy:** Thay vì dùng `Manual Start`, các sếp có thể thay thế bằng node **Schedule Trigger** để hệ thống tự động quét lead vào 8h sáng mỗi ngày.
- **Mở rộng làm giàu dữ liệu (Data Enrichment):** Kết hợp thêm các AI Agent node (như OpenAI, Claude) để tự động phân tích chức danh và viết email chào hàng (cold email) cá nhân hóa cho từng lead ngay sau khi quét xong.

### 📌 Kết luận
Việc tự động hóa quy trình tìm kiếm khách hàng tiềm năng trên LinkedIn chưa bao giờ dễ dàng đến thế với sức mạnh của n8n và Google Sheets. Hãy cài đặt ngay workflow này để giải phóng thời gian cho đội ngũ sales và tối ưu hóa chi phí vận hành doanh nghiệp ngay hôm nay!