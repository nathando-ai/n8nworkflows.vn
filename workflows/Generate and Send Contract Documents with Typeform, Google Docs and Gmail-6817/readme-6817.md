---
title: "🚀 Tự Động Hóa Tạo và Gửi Hợp Đồng với Typeform, Google Docs và Gmail trong n8n"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình tạo hợp đồng PDF từ form đăng ký và gửi email trực tiếp cho khách hàng bằng n8n, Google Docs và Gmail."
slug: "tu-dong-hoa-tao-va-gui-hop-dong-typeform-google-docs-gmail"
tags: [n8n, automation, no-code, google-docs, typeform, gmail]
keywords: [n8n workflow, tạo hợp đồng tự động, typeform google docs, gửi gmail tự động, tự động hóa tài liệu]
---

# 🚀 Tự Động Hóa Tạo và Gửi Hợp Đồng từ Form đến Email Khách Hàng

Các sếp có bao giờ cảm thấy mệt mỏi mỗi khi có khách hàng mới đăng ký, đội ngũ lại phải hì hục copy thông tin, điền tay vào file Word/Google Docs mẫu, xuất ra PDF rồi mở Gmail gửi đi từng người? Quy trình thủ công này không chỉ ngốn hàng giờ đồng hồ mà còn rất dễ xảy ra sai sót ngớ ngẩn (như nhầm tên, sai điều khoản, quên gửi file).

Đừng lo, bài toán đó sẽ được giải quyết triệt để với workflow n8n cực kỳ thông minh này! Hệ thống sẽ tự động bắt dữ liệu từ form, điền vào mẫu hợp đồng, chuyển đổi thành PDF và gửi thẳng vào hộp thư của khách hàng ngay lập tức.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Ngay khi khách hàng bấm Submit trên Typeform, hợp đồng được tạo và gửi đi mà không cần con người nhúng tay.
- **Chính xác tuyệt đối:** Loại bỏ hoàn toàn sai sót do copy-paste thủ công thông tin khách hàng.
- **Tốc độ chớp nhoáng:** Khách hàng nhận được hợp đồng dưới dạng PDF chuyên nghiệp chỉ trong tích tắc, nâng tầm trải nghiệm dịch vụ.
- **Hoạt động không nghỉ:** Hệ thống làm việc 24/7, kể cả lúc các sếp đang ngủ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn các tài khoản và quyền truy cập sau:
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Typeform** với một Form thu thập thông tin khách hàng (Họ tên, Email, Công ty, Chi tiết gói dịch vụ...).
- Tài khoản **Google Drive / Google Docs** với một file Template hợp đồng mẫu (có sẵn các biến cần điền).
- Tài khoản **Gmail** để gửi email tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ n8n (ID: `6817`) và tiến hành Import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Typeform Trigger**: Kết nối tài khoản Typeform của các sếp và chọn đúng Form đăng ký dịch vụ/hợp đồng đã tạo. Node này sẽ đóng vai trò là "ngòi nổ" kích hoạt toàn bộ quy trình khi có phản hồi mới.
- **Set Variables**: Node này dùng để làm sạch và ánh xạ dữ liệu thô từ Typeform sang các biến chuẩn (như tên khách hàng, email, ngày tháng, giá trị hợp đồng) để các node phía sau dễ dàng đọc hiểu.
- **Fill Contract Template (Google Docs)**: 
  - Kết nối `Google API Credentials`.
  - Chọn file Google Docs Template mẫu của các sếp.
  - Điền các giá trị từ node `Set Variables` vào các trường tương ứng trong tài liệu mẫu.
- **Export as PDF (Google Drive)**: 
  - Sử dụng chung `Google API Credentials`.
  - Cấu hình thông số `Operation` là `Export` để chuyển đổi file Google Docs vừa điền thông tin thành định dạng `.pdf` chuẩn chỉnh.
- **Send via Email (Gmail)**:
  - Kết nối `Gmail OAuth2 Credentials`.
  - Cấu hình người nhận (lấy email từ Typeform), tiêu đề email và đính kèm tệp PDF hợp đồng vừa được xuất ra từ Google Drive. Viết một lời nhắn chuyên nghiệp để gửi kèm file cho khách hàng.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử submit một bản ghi mẫu trên Typeform để kiểm tra xem email có về đúng inbox với file PDF chuẩn xác chưa.
- Sau khi test ngon lành, các sếp bật nút **Active** ở góc trên cùng bên phải để workflow chính thức vào ca trực!

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống xịn sò hơn nữa, các sếp có thể cân nhắc mở rộng workflow:
- **Thêm thông báo nội bộ:** Gắn thêm node Telegram hoặc Slack để bắn tin nhắn về group nội bộ thông báo: *"ừa, vừa có khách hàng X ký hợp đồng, hệ thống đã gửi mail xong!"*.
- **Lưu trữ dữ liệu:** Thêm node Google Sheets để lưu lại lịch sử tạo hợp đồng phục vụ việc thống kê, báo cáo doanh thu.
- **Tích hợp ký số:** Thay vì chỉ gửi PDF thông thường, có thể kết hợp thêm các API ký điện tử để khách hàng ký xác nhận trực tuyến luôn.

### 📌 Kết luận
Việc tự động hóa quy trình tạo và gửi hợp đồng không chỉ giúp tiết kiệm hàng đống thời gian mà còn tạo ấn tượng cực kỳ chuyên nghiệp trong mắt đối tác và khách hàng. Hãy triển khai ngay workflow này vào hệ thống của các sếp để tối ưu hóa vận hành ngay hôm nay!