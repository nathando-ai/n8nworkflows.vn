---
title: "🚀 Tự động trích xuất dữ liệu từ link trong Gmail và lưu vào Google Sheets bằng n8n"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình đọc email Gmail, trích xuất link, cào dữ liệu từ trang web đích và lưu thẳng vào Google Sheets."
slug: "trich-xuat-du-lieu-tu-link-gmail-vao-google-sheets"
tags: [n8n, automation, no-code, gmail, google-sheets, web-scraping]
keywords: [n8n workflow, trích xuất dữ liệu gmail, lưu gmail vào google sheets, cào dữ liệu web n8n, tự động hóa email]
---

# 🚀 Tự động trích xuất dữ liệu từ link trong Gmail và lưu vào Google Sheets

Các sếp có bao giờ cảm thấy mệt mỏi khi phải mở từng email đến, click vào các đường link bên trong, copy thông tin từ trang web đó rồi thủ công dán vào file Google Sheets không? Công việc lặp đi lặp lại này không chỉ tốn hàng giờ đồng hồ mỗi ngày mà còn rất dễ sai sót.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ thông minh giúp tự động hóa 100% quy trình: Quét email trong **Gmail** ➔ Tìm link ẩn trong nội dung ➔ Truy cập trang web đích (`HTTP Request`) ➔ Trích xuất thông tin cần thiết (`HTML` & `Code`) ➔ Lưu trữ gọn gàng vào **Google Sheets**. Tất cả diễn ra hoàn toàn tự động mà không cần viết code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh "copy-paste" thủ công từ web vào bảng tính.
- **Dữ liệu thời gian thực:** Email vừa đến, link được xử lý và lưu trữ ngay lập tức.
- **Độ chính xác tuyệt đối:** Tránh tình trạng bỏ sót email hoặc nhập nhầm số liệu.
- **Hoạt động 24/7:** Chạy ngầm liên tục trên server, các sếp chỉ việc mở Google Sheets ra xem kết quả.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google (Gmail & Google Sheets)** để kết nối credentials.
- **Một file Google Sheets** trắng đã được định nghĩa sẵn các cột (Tiêu đề cột) để lưu dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON từ link gốc hoặc tạo mới workflow trên n8n và lần lượt thêm các nodes theo danh sách tiêu chuẩn. Workflow này bao gồm 8 nodes chính phối hợp nhịp nhàng với nhau.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà theo đúng ý đồ, các sếp cần cấu hình kỹ các node trọng điểm sau:

- **Node `Search Emails` (Gmail):** 
  - Chọn tài khoản kết nối (`gmailOAuth2`).
  - Cấu hình điều kiện tìm kiếm email (ví dụ: theo người gửi `from:example@domain.com`, theo nhãn, hoặc theo khoảng thời gian) trong phần thông số `Operation: Get Many (getAll)`.
- **Node `search for an element in the email body` (HTML):** 
  - Sử dụng thao tác `Extract HTML Content` để lọc ra đúng thẻ HTML hoặc đường dẫn URL chứa link đích bên trong nội dung email.
- **Node `open the link` (HTTP Request):** 
  - Nhận URL vừa trích xuất từ bước trước để gửi yêu cầu GET tới trang web mục tiêu.
- **Node `capture data` (HTML):** 
  - Tiếp tục dùng HTML Extractor để bóc tách các dữ liệu cụ thể (như tiêu đề bài viết, giá sản phẩm, nội dung chính...) dựa trên cấu trúc CSS Selector của trang web đó.
- **Node `processes information` (Code):** 
  - Node JavaScript tùy chỉnh để làm sạch dữ liệu, định dạng lại ngày tháng hoặc biến đổi cấu trúc dữ liệu thô thành dạng mảng/đối tượng chuẩn xác. Các sếp có thể sửa đoạn code này tùy thuộc vào nhu cầu thực tế.
- **Node `set variables` (Set):** 
  - Gán các biến dữ liệu đã xử lý vào các trường cụ thể trước khi đẩy lên Google Sheets.
- **Node `Save data in spreadsheet` (Google Sheets):** 
  - Chọn tài khoản (`googleSheetsOAuth2Api`), chọn file Spreadsheet và Sheet Name chính xác của các sếp, chọn Operation là `Append` để thêm dòng mới.

#### 3. Kích hoạt ⚡️
- Bấm nút **‘Test workflow’** (`manualTrigger`) để chạy thử nghiệm với dữ liệu email mẫu gần nhất và kiểm tra kết quả trả về ở Google Sheets.
- Nếu mọi thứ xanh mướt (success), các sếp bật công tắc **Active** góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm thông báo:** Nối thêm một node **Telegram** hoặc **Slack** vào cuối workflow để nhận thông báo tức thì mỗi khi có một dòng dữ liệu mới được lưu thành công vào Google Sheets.
- **Xử lý lỗi (Error Handling):** Thêm nhánh Error Trigger để bắt lỗi nếu email không chứa link hoặc trang web đích bị lỗi (HTTP 404/500).
- **Lọc trùng lặp:** Thêm một bước kiểm tra (If/Code node) để đảm bảo không lưu lại các URL đã từng được xử lý trước đó.

### 📌 Kết luận
Workflow "Extract Web Page Data from Gmail Links and Save to Google Sheets" là một trợ thủ đắc lực cho những ai thường xuyên phải tổng hợp thông tin từ email và các trang web bên ngoài. Hãy cài đặt ngay hôm nay để giải phóng sức lao động và tối ưu hóa hiệu suất công việc của các sếp!