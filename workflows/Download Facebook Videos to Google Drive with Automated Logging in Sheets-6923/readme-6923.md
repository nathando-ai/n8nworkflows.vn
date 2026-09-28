---
title: "🚀 Tự động tải video Facebook lưu Google Drive và ghi log Google Sheets bằng n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình nhập link Facebook, tải video, upload lên Google Drive, phân quyền chia sẻ và ghi log trạng thái vào Google Sheets."
slug: "tu-dong-tai-video-facebook-google-drive-n8n"
tags: [n8n, automation, no-code, google-drive, google-sheets, facebook-downloader]
keywords: [n8n workflow, tải video facebook, tự động hóa google drive, google sheets automation, rapidapi facebook downloader]
---

# 🚀 Tự động tải video Facebook lưu Google Drive và ghi log Google Sheets

Việc tải video từ Facebook về máy rồi upload thủ công lên Google Drive để lưu trữ, chia sẻ cho đồng nghiệp hoặc khách hàng thường tốn rất nhiều thời gian, đặc biệt khi số lượng video lớn. Các sếp có bao giờ cảm thấy phiền toái khi phải thao tác lặp đi lặp lại: Copy link -> Tìm tool tải -> Chờ đợi -> Upload Drive -> Đổi quyền chia sẻ -> Lưu file Excel quản lý?

Giải pháp ở đây chính là **workflow n8n** tự động hóa 100% quy trình này. Chỉ với một cú click điền form đơn giản, video Facebook sẽ tự động bay thẳng vào Google Drive của các sếp, tự động bật quyền chia sẻ công khai và ghi nhận toàn bộ lịch sử thành công hay thất bại vào Google Sheets một cách minh bạch!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần thao tác thủ công từng video, hệ thống tự động xử lý từ A-Z.
- **Lưu trữ tập trung:** Video được gom gọn gàng vào một thư mục định sẵn trên Google Drive, tự động tạo link chia sẻ nhanh chóng.
- **Quản lý minh bạch:** Google Sheets sẽ tự động ghi log lại toàn bộ link gốc kèm link Drive (hoặc đánh dấu thất bại `N/A` nếu link lỗi), giúp dễ dàng kiểm tra.
- **Hoạt động 24/7:** Chạy ngầm liên tục trên cloud, sẵn sàng phục vụ bất cứ lúc nào qua giao diện Form trực quan.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Hệ thống n8n:** Đã cài đặt và hoạt động ổn định (Self-hosted hoặc n8n Cloud).
- **Tài khoản RapidAPI:** Đăng ký và lấy API Key từ [Facebook Video Downloader API](https://rapidapi.com/skdeveloper/api/facebook-video-downloader11).
- **Google Account:** 
  - Kết nối Google Drive OAuth2 API (để upload video và set quyền chia sẻ file).
  - Kết nối Google Sheets API (để ghi log dữ liệu).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow (từ nguồn cung cấp) và dán trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không gặp lỗi, các sếp cần chú ý cấu hình các node cốt lõi sau:

- **On form submission (`formTrigger`):** Node này tạo sẵn một giao diện web form đơn giản với một trường nhập `URL`. Các sếp có thể nhấn vào để xem trước giao diện và lấy link chia sẻ form cho người dùng nhập liệu.
- **Facebook RapidAPI Request (`httpRequest`):** 
  - Điền RapidAPI Key của các sếp vào phần Header (`X-RapidAPI-Key`).
  - Đảm bảo endpoint nhận đúng URL truyền từ form submission qua biểu thức (expression).
- **If Node (`if`):** Node này kiểm tra xem API trả về có chứa mã lỗi hay không. 
  - 🟢 **True Path:** Nếu thành công, chuyển sang bước tải file MP4.
  - 🔴 **False Path:** Nếu lỗi, đi qua node Wait để chờ xử lý ghi log lỗi.
- **Upload To Google Drive (`googleDrive`):** 
  - Chọn Credentials Google Drive OAuth2 của các sếp.
  - Chọn thư mục đích (`Parent Folder`) trên Google Drive nơi chứa các video tải về.
- **Google Drive Set Permission (`googleDrive`):** 
  - Thiết lập quyền chia sẻ file là `Anyone with the link can view` (Bất kỳ ai có đường liên kết đều có thể xem) để tự động sinh ra link public `webViewLink`.
- **Google Sheets & Google Sheets Append Row (`googleSheets`):** 
  - Kết nối tài khoản Google API.
  - Chọn file Google Sheets quản lý, chỉ định đúng Sheet Name và map các cột dữ liệu:
    - Log thành công: Lưu `URL` gốc và `Drive_URL` (link chia sẻ video).
    - Log thất bại: Lưu `URL` gốc và `Drive_URL` điền giá trị `N/A`.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** chạy thử một link video Facebook mẫu để kiểm tra toàn bộ luồng.
- Sau khi kiểm tra mọi thứ chạy xanh mướt (success), các sếp gạt công tắc sang chế độ **Active** để workflow chính thức vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram Bot hoặc Slack vào nhánh thành công hoặc thất bại để nhận thông báo tức thời ngay khi có video mới được tải về Drive.
- **Tự động dọn dẹp file tạm:** n8n xử lý dữ liệu nhị phân (binary) trong bộ nhớ, tuy nhiên các sếp có thể cấu hình thêm bước thông báo qua email cho khách hàng khi video đã sẵn sàng.
- **Mở rộng nguồn video:** Thay vì chỉ dùng form nội bộ, có thể thay trigger thành Webhook nhận link từ Typeform, Google Forms hoặc trang web riêng của doanh nghiệp.

### 📌 Kết luận
Workflow tự động hóa tải video Facebook lưu Google Drive này là một trợ thủ đắc lực cho các nhà sáng tạo nội dung, marketer hay đội ngũ vận hành fanpage. Hãy cài đặt ngay lên hệ thống n8n của các sếp để tối ưu hóa thời gian và giải phóng sức lao động thủ công ngay hôm nay!