---
title: "🚀 Tự động quét khách hàng tiềm năng địa phương với SearchAPI Google Maps và Google Sheets"
description: "Hướng dẫn xây dựng hệ thống tự động tìm kiếm, trích xuất và lưu trữ lead doanh nghiệp địa phương lên Google Sheets chỉ với một form nhập liệu bằng n8n."
slug: "tim-kiem-lead-dia-phuong-searchapi-google-sheets"
tags: [n8n, automation, lead-generation, searchapi, google-sheets, no-code]
keywords: [n8n workflow, tim kiem lead, searchapi google maps, google sheets automation, outbound lead finder]
---

# 🚀 Tự động quét khách hàng tiềm năng địa phương với SearchAPI Google Maps và Google Sheets

Các sếp có đang đau đầu vì tốn hàng giờ đồng hồ lướt Google Maps, copy thủ công từng cái tên, số điện thoại, địa chỉ và website của các doanh nghiệp địa phương để làm danh sách telesales hoặc cold email? Công việc chân tay này không chỉ nhàm chán, tốn thời gian mà còn cực kỳ dễ sai sót.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một **Workflow n8n tự động hóa 100%**. Chỉ cần vài cú click điền loại hình kinh doanh và khu vực vào một Form trực tuyến, hệ thống sẽ tự động cào dữ liệu từ Google Maps thông qua SearchAPI và đổ thẳng toàn bộ thông tin chi tiết vào Google Sheets cho các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải copy-paste thủ công từ bản đồ.
- **Dữ liệu phong phú, chuẩn xác:** Thu thập đầy đủ tên doanh nghiệp, ngành nghề, địa chỉ, số điện thoại, website, điểm đánh giá (rating), số lượng review, khoảng giá và link Google Maps.
- **Tự động hóa toàn diện:** Hoạt động liền mạch từ khâu nhận yêu cầu qua Form đến khi lưu trữ dữ liệu.
- **Sẵn sàng cho Sale & Marketing:** Danh sách sạch, định dạng chuẩn trên Google Sheets giúp đội ngũ kinh doanh tiếp cận khách hàng ngay lập tức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản SearchAPI:** Lấy API key miễn phí tại [searchapi.io](https://searchapi.io).
- **Tài khoản Google:** Để kết nối Google Sheets OAuth2 và tạo sẵn một bảng tính (Spreadsheet) lưu dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON thông qua giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 5 nodes chính hoạt động nhịp nhàng với nhau. Các sếp cần chú ý cấu hình các điểm sau:

- **Node `Lead Search Form` (Form Trigger):** 
  - Nơi người dùng nhập thông tin tìm kiếm. Các sếp có thể tùy chỉnh các trường (dropdown hoặc input) như *Business Type* (Loại hình kinh doanh: ví dụ: Nhà hàng, Spa, Nha khoa...) và *Location* (Khu vực: ví dụ: Quận 1 TP.HCM, Hà Nội...).
- **Node `Build Search Variables` (Set):** 
  - Node này nhận dữ liệu từ Form và đóng gói lại thành câu lệnh truy vấn (Query pattern: `{Business Type} in {Location}`) để gửi sang SearchAPI.
- **Node `SearchAPI — Google Maps` (SearchAPI):** 
  - Cần kết nối **SearchAPI Credentials** bằng API Key lấy từ trang chủ searchapi.io. Chọn Resource là `google_maps` để hệ thống trích xuất dữ liệu bản đồ chính xác nhất.
- **Node `Parse Business Results` (Code):** 
  - Sử dụng đoạn mã JavaScript có sẵn để bóc tách, chuẩn hóa dữ liệu trả về từ API thành danh sách các trường rõ ràng:
    `Business Name` · `Category` · `Address` · `Phone` · `Website` · `Rating` · `Review Count` · `Price Range` · `Location` · `Business Type` · `Maps URL` · `Place ID` · `Run ID` · `Scraped At`
- **Node `Write to Google Sheet` (Google Sheets):** 
  - Kết nối **Google Sheets OAuth2** tài khoản của các sếp.
  - Chọn đúng File Spreadsheet và Sheet Tab muốn lưu trữ dữ liệu. Đảm bảo các tiêu đề cột trong Google Sheet khớp với các trường dữ liệu mà node Code xuất ra.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền thông tin vào form do n8n cung cấp để kiểm tra dữ liệu đã vào Google Sheets chưa.
- Sau khi test thành công, bật nút **Active** ở góc trên bên phải để đưa workflow vào trạng thái chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Thông báo:** Thêm node Telegram hoặc Slack ở cuối workflow để bắn thông báo về máy ngay khi quét xong một danh sách lead mới.
- **Làm sạch dữ liệu thông minh:** Kết hợp thêm các node AI (như OpenAI / Claude) để tự động phân loại mức độ tiềm năng của lead dựa trên số lượng review và điểm rating.
- **Tự động gửi Email/SMS:** Nối tiếp workflow này với các chiến dịch gửi email tự động (Cold Outreach) ngay khi lead được ghi nhận vào Google Sheets.

### 📌 Kết luận
Việc tìm kiếm khách hàng tiềm năng địa phương chưa bao giờ dễ dàng và tự động hóa đến thế. Hãy áp dụng ngay workflow này để giải phóng sức lao động cho đội ngũ của các sếp và bứt phá doanh số ngay hôm nay!