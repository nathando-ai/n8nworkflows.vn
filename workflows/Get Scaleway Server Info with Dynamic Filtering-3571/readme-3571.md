---
title: "🚀 Tự động truy vấn và lọc thông tin Scaleway Server động qua Webhook với n8n"
description: "Hướng dẫn cấu hình workflow n8n giúp lấy danh sách server và baremetal từ Scaleway API, hỗ trợ lọc động theo tên, tags, IP hoặc zone cực kỳ tiện lợi."
slug: "tu-dong-truy-van-loc-thong-tin-scaleway-server-n8n"
tags: [n8n, automation, devops, scaleway, webhook, api]
keywords: [n8n workflow, scaleway automation, quan ly server scaleway, webhook n8n, devops automation]
---

# 🚀 Tự động truy vấn và lọc thông tin Scaleway Server động qua Webhook với n8n

Việc quản lý hàng loạt máy chủ (Instances và Baremetal) trên đám mây Scaleway thủ công qua giao diện Console thường tốn rất nhiều thời gian, đặc biệt khi các sếp cần tra cứu nhanh theo các tiêu chí như tên, thẻ (tags), địa chỉ IP hay khu vực (zone). 

Giải pháp tuyệt vời nhất là tự động hóa toàn bộ quy trình này! Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n chuyên nghiệp giúp nhận yêu cầu qua Webhook, tự động gọi Scaleway API, xử lý dữ liệu phức tạp và trả về kết quả đã lọc một cách chuẩn xác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Truy xuất thông tin cả Server Instances và Baremetal từ nhiều zones khác nhau của Scaleway chỉ trong tích tắc.
- **Lọc dữ liệu thông minh:** Hỗ trợ tìm kiếm động theo `tags`, `name`, `public_ip`, hoặc `zone` thông qua HTTP POST request gửi tới Webhook.
- **Xử lý lỗi chuyên nghiệp:** Tự động trả về thông báo lỗi chi tiết nếu tham số tìm kiếm không hợp lệ.
- **Tích hợp linh hoạt:** Dễ dàng nhúng vào các ứng dụng nội bộ, chatbot hoặc các workflow tự động hóa khác của doanh nghiệp.
:::

### yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Scaleway Account:** Tài khoản Scaleway và API Token cá nhân (được tạo từ Scaleway Console).
- **Kiến thức cơ bản:** Biết cách gửi HTTP POST request (dùng Postman, cURL hoặc các hệ thống khác).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc sao chép mã nguồn JSON.
- Trong giao diện n8n Editor, chọn **New Workflow** -> Nhấp vào biểu tượng menu (3 chấm) ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru với tài khoản Scaleway của các sếp, hãy cấu hình các điểm sau:

- **Node `Edit Fields`:** 
  - Mở node này và tìm trường chứa `Scaleway-X-Auth-Token`.
  - Thay thế giá trị mặc định bằng **API Token cá nhân** của các sếp. *(Nếu chưa có, hãy đăng nhập vào Scaleway console, tạo API Token mới và copy dán vào đây).*
- **Node `Webhook`:**
  - Cấu hình xác thực Basic Auth (`httpBasicAuth`) để bảo mật điểm đầu cuối nhận request.
  - Lấy URL Webhook (Test/Production URL) để sử dụng khi gửi request từ ứng dụng bên ngoài.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** và gửi một POST request thử nghiệm bằng Postman với payload mẫu:
  ```json
  {
    "search_by": "tags",
    "search": "Apiv1"
  }
  ```
- Kiểm tra kết quả trả về, nếu mọi thứ hoạt động chính xác, hãy gạt công tắc sang **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot:** Kết nối Webhook này với Slack hoặc Telegram Bot để các sếp có thể chat trực tiếp (VD: `/server tag production`) là bot trả về danh sách server ngay lập tức.
- **Lưu Log báo cáo:** Kết hợp thêm node Google Sheets hoặc Notion để lưu lại lịch sử mỗi khi có yêu cầu tra cứu hệ thống.
- **Cảnh báo tự động:** Thêm điều kiện lọc nếu phát hiện server có trạng thái lỗi (error/stopped) để gửi cảnh báo khẩn cấp qua email hoặc Discord.

### 📌 Kết luận
Với workflow "Get Scaleway Server Info with Dynamic Filtering", việc tra cứu và quản lý tài nguyên hạ tầng trên Scaleway đã trở nên đơn giản, nhanh chóng và tự động hoàn toàn. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa thời gian vận hành DevOps nhé!