---
title: "🚀 Tự Động Hóa Chuyển Đổi Ảnh JPG/PNG Sang WebP Với n8n & APYHub"
description: "Workflow n8n tự động đọc danh sách ảnh từ Google Sheets, chuyển đổi sang định dạng WebP siêu nhẹ bằng APYHub và lưu trữ lên Google Drive. Giải pháp tối ưu tốc độ website không cần code."
slug: "tu-dong-hoa-chuyen-doi-anh-sang-webp-n8n"
tags: [n8n, automation, image-optimization, webp, google-drive, apyhub]
keywords: [n8n workflow, chuyển đổi ảnh webp, tối ưu ảnh tự động, apyhub api, google sheets automation]
---

# 🚀 Tự Động Hóa Chuyển Đổi Ảnh JPG/PNG Sang WebP Với n8n & APYHub

Trong kỷ nguyên tốc độ website quyết định thứ hạng SEO và trải nghiệm người dùng, việc tối ưu hóa hình ảnh là một bài toán nan giải. Các sếp thường phải mất hàng giờ để tải từng ảnh xuống, dùng phần mềm chuyển đổi sang định dạng WebP (nhẹ hơn 25-35% so với JPG/PNG), rồi lại tải lên hosting hoặc lưu trữ đám mây. Quy trình thủ công này không chỉ tốn thời gian mà còn dễ xảy ra sai sót, đặc biệt khi cần xử lý hàng trăm hoặc hàng nghìn ảnh.

Workflow n8n này chính là "trợ lý ảo" hoàn hảo giúp các sếp tự động hóa 100% quy trình đó. Chỉ cần liệt kê link ảnh trong Google Sheets, hệ thống sẽ tự động lấy ảnh, chuyển đổi sang WebP thông qua API của APYHub, và lưu kết quả vào Google Drive một cách liền mạch, không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tối đa:** Xử lý hàng loạt ảnh trong vài phút thay vì hàng giờ làm thủ công.
- **Tăng tốc độ website:** Định dạng WebP giúp giảm dung lượng file ảnh, cải thiện điểm PageSpeed Insights.
- **Chính xác & Không lỗi:** Loại bỏ hoàn toàn rủi ro con người trong quá trình chuyển đổi và lưu trữ.
- **Tích hợp liền mạch:** Kết nối trực tiếp giữa Google Sheets (dữ liệu đầu vào) và Google Drive (dữ liệu đầu ra).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Bản miễn phí hoặc Self-hosted.
2. **Tài khoản APYHub:** Đăng ký miễn phí tại [apyhub.com](https://apyhub.com/) để lấy API Key.
3. **Tài khoản Google:**
   - **Google Sheets:** Tạo hoặc clone sheet mẫu chứa danh sách URL ảnh (định dạng JPG, JPEG, PNG).
   - **Google Drive:** Nơi lưu trữ các file WebP đã chuyển đổi.
4. **Permissions:** Cấp quyền truy cập OAuth2 cho n8n đối với Google Sheets và Google Drive.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** hoặc **Import from File**.
3. Dán link workflow gốc: `https://n8n.io/workflows/3278` hoặc tải file JSON về và import.
4. Sau khi import, các sếp sẽ thấy một workflow với 10 nodes chính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Dưới đây là các node quan trọng cần cấu hình để workflow chạy đúng:

**1. Node: `Set API KEY`**
- Đây là node thiết lập biến môi trường cho API.
- **Thao tác:** Mở node này, tìm trường `value` (hoặc `apiKey` tùy phiên bản n8n) và dán **API Key** mà các sếp đã lấy từ APYHub vào đây.
- *Lưu ý:* Đảm bảo API Key đúng chính tả, không có khoảng trắng thừa.

**2. Node: `Get images` (Google Sheets)**
- Node này đọc danh sách ảnh từ Google Sheet.
- **Thao tác:**
  - Chọn **Credential** Google Sheets OAuth2 đã tạo.
  - Chọn **Sheet Name** (tên sheet chứa dữ liệu).
  - Đảm bảo cột chứa URL ảnh trong Sheet có tên là **"FROM"** (theo hướng dẫn gốc). Nếu các sếp đổi tên cột, cần chỉnh lại mapping trong node này.

**3. Node: `Get extension` & `JPG or PNG?`**
- Hai node này xử lý logic: xác định đuôi file và phân loại ảnh.
- **Thao tác:** Thường không cần chỉnh sửa gì nếu dữ liệu đầu vào chuẩn. Tuy nhiên, nếu các sếp muốn hỗ trợ thêm định dạng khác, cần sửa logic trong node `Code` (`Get extension`) và thêm nhánh trong node `Switch` (`JPG or PNG?`).

**4. Node: `From JPG to WEBP` & `PNG to WEBP` (HTTP Request)**
- Đây là các node gọi API APYHub để thực hiện chuyển đổi.
- **Thao tác:** Kiểm tra URL API và tham số gửi đi. Đảm bảo rằng URL API trong node khớp với tài liệu của APYHub. Thông thường, các tham số đã được cấu hình sẵn, chỉ cần đảm bảo API Key ở bước 1 là đủ.

**5. Node: `Get file image`**
- Node này tải file WebP đã chuyển đổi về dạng binary data.
- **Thao tác:** Kiểm tra URL trả về từ API APYHub. Đảm bảo node này nhận đúng response từ bước chuyển đổi.

**6. Node: `Upload image` (Google Drive)**
- Node cuối cùng lưu file WebP lên Google Drive.
- **Thao tác:**
  - Chọn **Credential** Google Drive OAuth2.
  - Chọn **Folder ID** (ID của thư mục đích trên Google Drive). Các sếp có thể lấy ID bằng cách mở thư mục trên Drive, nhìn vào URL, phần sau `/folders/` chính là ID.
  - Đặt tên file: Có thể cấu hình để tên file WebP giống tên file gốc (ví dụ: `anh1.jpg` -> `anh1.webp`).

**7. Node: `Update Sheet` (Google Sheets)**
- Node này cập nhật lại Google Sheet với link hoặc thông tin về file WebP đã lưu.
- **Thao tác:** Chọn **Credential** Google Sheets. Xác định cột cần cập nhật (ví dụ: cột "TO" hoặc "WEBP_URL") và giá trị cần ghi (thường là link trực tiếp hoặc ID file trên Drive).

#### 3. Kích hoạt ⚡️
1. **Test Run:** Nhấn nút **Test workflow** (hoặc "Execute Workflow") ở góc trên bên phải.
   - Kiểm tra xem dữ liệu có chạy qua các node không.
   - Kiểm tra xem file WebP có xuất hiện trong Google Drive không.
   - Kiểm tra xem Google Sheet có được cập nhật không.
2. **Bật Active:** Nếu test thành công, nhấn nút **Active** để workflow tự động chạy khi có dữ liệu mới (nếu các sếp thêm trigger khác như Webhook hoặc Schedule) hoặc chạy thủ công khi cần.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Trigger Webhook:** Thay vì chạy thủ công, các sếp có thể thêm node `Webhook` ở đầu workflow. Khi có yêu cầu chuyển đổi ảnh từ website hoặc ứng dụng khác, n8n sẽ tự động xử lý.
- **Gửi thông báo qua Telegram/Slack:** Thêm node `Telegram` hoặc `Slack` ở cuối workflow để gửi thông báo khi quá trình chuyển đổi hoàn tất, giúp các sếp nắm bắt tiến độ.
- **Lưu log chi tiết:** Thêm node `Google Sheets` hoặc `Database` để ghi lại lịch sử chuyển đổi (thời gian, tên file, dung lượng trước/sau) phục vụ báo cáo và theo dõi hiệu suất.
- **Tự động xóa ảnh gốc:** Nếu các sếp không cần giữ lại ảnh JPG/PNG gốc, có thể thêm node `Google Drive` (Delete) để xóa file gốc sau khi chuyển đổi thành công, giúp tiết kiệm dung lượng lưu trữ.

### 📌 Kết luận
Workflow **Automated Image Optimizer** là một công cụ mạnh mẽ giúp các sếp tự động hóa quy trình chuyển đổi ảnh sang định dạng WebP, tiết kiệm thời gian và nâng cao hiệu suất website. Với sự kết hợp giữa n8n, APYHub và Google Workspace, các sếp có thể dễ dàng xây dựng một hệ thống tối ưu hóa ảnh chuyên nghiệp mà không cần kiến thức lập trình. Hãy thử ngay hôm nay và trải nghiệm sự khác biệt!