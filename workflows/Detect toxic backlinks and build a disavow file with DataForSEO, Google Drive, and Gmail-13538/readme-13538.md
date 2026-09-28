---
title: "🚀 Tự động phát hiện Backlink độc hại và tạo file Disavow với DataForSEO, Google Drive & Gmail"
description: "Tự động quét backlink spam, lọc link độc hại bằng DataForSEO API, tạo file disavow chuẩn Google, lưu Google Drive và gửi thông báo qua Gmail."
slug: "tu-dong-phat-hien-toxic-backlinks-dataforseo-google-drive-gmail"
tags: [n8n, automation, seo, dataforseo, google-drive, gmail]
keywords: [n8n workflow, toxic backlinks, disavow file, DataForSEO API, tự động hóa SEO, Google Search Console]
---

# 🚀 Tự động phát hiện Backlink độc hại và tạo file Disavow với DataForSEO, Google Drive & Gmail

Các sếp làm SEO chắc chắn đều hiểu cảm giác "đau đầu" khi website bị tấn công bởi hàng loạt backlink bẩn (spam backlinks) từ các trang web độc hại, khiến từ khóa tụt hạng không phanh trên Google Search Console. Việc phải thủ công rà soát từng link, lọc ra các domain độc hại rồi format lại theo chuẩn `domain:example.com` để nộp cho Google thực sự là một cơn ác mộng tốn hàng tá thời gian.

Giải pháp ở đây là gì? Workflow n8n tự động hóa 100% này sẽ thay các sếp làm toàn bộ quy trình: quét toàn bộ backlink, lọc spam, đóng gói thành file `.txt` chuẩn chỉnh, đẩy lên Google Drive và bắn thông báo qua Gmail ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải thủ công xuất Excel, lọc điểm spam hay copy-paste hàng nghìn dòng link.
- **Bảo vệ website chuyên nghiệp:** Phát hiện kịp thời các chiến dịch SEO bẩn nhắm vào website của các sếp.
- **Chuẩn hóa 100%:** File `disavow.txt` được tạo tự động tuân thủ tuyệt đối cấu trúc mà Google yêu cầu để nộp lên Search Console.
- **Cảnh báo thông minh:** Hệ thống tự động kiểm tra dung lượng file, số lượng link và gửi email cảnh báo nếu có bất kỳ điểm bất thường nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **DataForSEO Account:** Cần có API login và password (lấy tại [DataForSEO API Access](https://app.dataforseo.com/api-access)).
- **Google Drive Account:** Dùng để lưu trữ file `disavow.txt` được sinh ra.
- **Gmail Account:** Dùng để gửi thông báo kết quả và đường dẫn file cho quản trị viên.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy đoạn mã JSON từ n8n.io và paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node cốt lõi sau:

- **Get spam backlinks (`n8n-nodes-dataforseo.dataForSeoBacklinksApi`):**
  - Kết nối tài khoản thông qua **DataForSEO API credentials** (sử dụng Login và Password từ trang quản trị DataForSEO).
  - Điền Domain mục tiêu (`Target Domain`) của các sếp và cấu hình bộ lọc điểm spam (mặc định >50).
- **Create file from text (`googleDrive`):**
  - Kết nối tài khoản Google Drive qua OAuth2.
  - Chọn thư mục đích (`Destination Folder`) trên Google Drive nơi file `disavow.txt` sẽ được lưu trữ.
- **Các node gửi thông báo (`Send a message (success)`, `Send a message (too many links)`, `Send a message (file too large)` - `gmail`):**
  - Kết nối tài khoản Gmail qua OAuth2.
  - Cấu hình địa chỉ Email nhận thông báo kết quả hoặc cảnh báo lỗi.

#### 3. Kích hoạt ⚡️
- Bấm **"Execute workflow"** thủ công tại node `When clicking ‘Execute workflow’` để test chạy thử với domain của các sếp.
- Kiểm tra kết quả trên Google Drive và Gmail xem file đã được tạo và gửi về đúng ý chưa.
- Gạt công tắc sang **Active** để bật chế độ sẵn sàng hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa định kỳ:** Thay vì dùng `manualTrigger`, các sếp có thể thay thế bằng node `Schedule Trigger` để chạy quét backlink tự động hàng tháng.
- **Tích hợp Slack/Telegram:** Thêm các node chatwork để nhận cảnh báo ngay lập tức trên nhóm nội bộ khi có file disavow mới được tạo.
- **Lưu lịch sử vào Google Sheets:** Ghi lại log các lần quét backlink, số lượng link độc hại bị loại bỏ theo thời gian để tiện theo dõi sức khỏe website.

### 📌 Kết luận
Việc kiểm soát backlink độc hại nay đã trở nên hoàn toàn tự động nhờ sự kết hợp giữa n8n và DataForSEO. Hãy áp dụng ngay workflow này để tiết kiệm thời gian vận hành và bảo vệ thứ hạng từ khóa của website các sếp trước các đối thủ cạnh tranh không lành mạnh!