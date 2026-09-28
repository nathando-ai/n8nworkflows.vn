---
title: "🚀 Tự động xuất danh sách tên miền Cloudflare, bản ghi DNS và cấu hình ra Google Sheets"
description: "Hướng dẫn sử dụng workflow n8n giúp tự động hóa việc trích xuất toàn bộ domain, bản ghi DNS và cài đặt từ Cloudflare lưu thẳng vào Google Sheets."
slug: "tu-dong-xuat-cloudflare-domains-dns-google-sheets"
tags: [n8n, automation, cloudflare, google-sheets, devops, api]
keywords: [n8n workflow, export cloudflare dns, cloudflare to google sheets, tự động hóa devops, n8n cloudflare api]
---

# 🚀 Tự động xuất danh sách tên miền Cloudflare, bản ghi DNS và cấu hình ra Google Sheets

Các sếp quản lý hàng chục hay hàng trăm tên miền trên Cloudflare chắc chắn đã từng đau đầu khi phải kiểm tra thủ công từng bản ghi DNS, cài đặt SSL, hay cấu hình bảo mật. Việc sao chép thủ công ra Excel hay Google Sheets vừa mất thời gian, dễ sai sót lại chẳng thể cập nhật kịp thời khi có thay đổi.

Đừng lo, workflow n8n được thiết kế bởi chuyên gia *KPendic* sẽ giúp các sếp giải quyết triệt để bài toán này. Workflow tự động kết nối với Cloudflare API để quét toàn bộ tên miền (TLDs), bóc tách các bản ghi DNS, lấy các thông số cài đặt và đồng bộ toàn bộ dữ liệu này vào Google Sheets một cách mượt mà, hoàn toàn không cần viết code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 99% thời gian:** Thay vì mất hàng giờ đồng hồ kiểm tra từng trang quản trị Cloudflare, toàn bộ dữ liệu được tổng hợp chỉ trong vài phút.
- **Dữ liệu trực quan, tập trung:** Quản lý toàn bộ danh sách tên miền, bản ghi A, CNAME, TXT... và các thiết lập quan trọng ngay trên Google Sheets.
- **Dễ dàng kiểm toán (Audit):** Thuận tiện cho việc rà soát bảo mật, kiểm tra hạn SSL hoặc backup cấu hình hệ thống định kỳ.
- **Tùy biến linh hoạt:** Dễ dàng mở rộng thêm các endpoint API khác của Cloudflare nếu cần lấy thêm thông tin chi tiết.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Cloudflare API Token:** Token cần có quyền truy cập đầy đủ (Full Access) để đọc thông tin tên miền và DNS [tại đây](https://dash.cloudflare.com/:account/api-tokens).
- **Google Sheets Template:** Copy [mẫu Google Spreadsheet này](https://docs.google.com/spreadsheets/d/1jt6od8FMt-Yo7A_CPGuyfqWzL7HJk6SZmQQFO6kkWBo/edit?usp=sharing) vào tài khoản Google Drive cá nhân của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc copy toàn bộ mã JSON từ n8n, sau đó paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 15 nodes được sắp xếp logic. Các sếp cần chú ý cấu hình các điểm sau:
- **Node `Get TLDs`, `Get DNS`, `Get Settings` (HTTP Request):** 
  - Cần tạo `credentials` kiểu **Header Auth** hoặc **Custom Auth** với API Token lấy từ Cloudflare của các sếp.
  - Cấu hình header xác thực theo chuẩn Cloudflare API (`Authorization: Bearer <API_TOKEN>`).
- **Node `Export` (Google Sheets):**
  - Kết nối tài khoản Google qua `Google Sheets OAuth2 API`.
  - Trỏ đúng đến file Google Sheet mà các sếp đã copy ở phần chuẩn bị bằng cách điền **Spreadsheet ID** và chọn đúng tên Sheet (Sheet Name).
- **Các node `Filter` & `Flatten` (Code nodes):** Các node này dùng JavaScript cơ bản để chuẩn hóa cấu trúc JSON trả về từ Cloudflare trước khi đẩy vào bảng. Các sếp có thể tinh chỉnh lại nếu muốn lấy thêm các trường dữ liệu đặc thù khác.

#### 3. Kích hoạt ⚡️
- Nhấn nút **`When clicking ‘Test workflow’`** (`manualTrigger`) để chạy thử lần đầu tiên và kiểm tra dữ liệu trả về xem đã khớp với Google Sheets chưa.
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, các sếp có thể bật trạng thái **Active** cho workflow hoặc gắn thêm Trigger theo lịch (Schedule Trigger) để hệ thống tự động chạy định kỳ hàng tuần/hàng tháng.

### ✍️ Mẹo & gợi ý nâng cao
- **Cảnh báo qua Telegram/Slack:** Kết hợp thêm node Telegram hoặc Slack ở cuối luồng để gửi thông báo tóm tắt số lượng domain đã quét thành công hoặc báo lỗi nếu Cloudflare API phản hồi lỗi.
- **Tự động hóa định kỳ:** Thay vì dùng `manualTrigger`, các sếp có thể thay bằng `Schedule Trigger` để tự động backup cấu hình DNS mỗi tuần một lần vào lúc nửa đêm.
- **Mở rộng endpoint:** Dựa vào [Cloudflare API Docs](https://developers.cloudflare.com/api/), các sếp có thể bổ sung thêm các HTTP Request node để lấy thêm thông tin về Firewall rules, Page rules hoặc SSL settings.

### 📌 Kết luận
Việc quản lý hệ thống hạ tầng và tên miền quy mô lớn sẽ trở nên vô cùng đơn giản và chuyên nghiệp khi áp dụng tự động hóa. Hãy triển khai ngay workflow này để tối ưu hóa quy trình DevOps của các sếp ngày hôm nay!