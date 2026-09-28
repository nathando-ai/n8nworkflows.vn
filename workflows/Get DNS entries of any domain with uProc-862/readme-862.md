---
title: "🚀 Tự Động Tra Cứu Bản Ghi DNS Của Bất Kỳ Domain Nào Với uProc Trên n8n"
description: "Hướng dẫn xây dựng workflow tự động trỏ và lấy toàn bộ bản ghi DNS của domain bất kỳ nhanh chóng, tích hợp uProc API và n8n chỉ trong vài phút."
slug: "tu-dong-tra-cuu-dns-domain-uproc-n8n"
tags: [n8n, automation, it-ops, secops, dns, uproc]
keywords: [n8n workflow, tra cứu dns, uproc api, tự động hóa it, kiểm tra domain, n8n việt nam]
---

# 🚀 Tự Động Tra Cứu Bản Ghi DNS Của Bất Kỳ Domain Nào Với uProc

Các sếp làm trong ngành IT Ops, SecOps hay Digital Marketing chắc chắn đã từng tốn không ít thời gian để tra cứu hệ thống phân giải tên miền (DNS records) của các đối thủ hoặc khách hàng thủ công trên nhiều trang web khác nhau. Việc này không chỉ tốn thời gian mà còn khó tự động hóa khi cần kiểm tra danh sách lớn.

Giải pháp là gì? Trong bài viết này, em xin giới thiệu workflow n8n cực kỳ gọn nhẹ nhưng cực kỳ mạnh mẽ, kết hợp với dịch vụ **uProc** để tự động hóa toàn bộ quy trình truy vấn bản ghi DNS của bất kỳ domain nào chỉ bằng một cú click chuột!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Bỏ qua các bước tra cứu thủ công qua web công cụ rời rạc.
- **Tốc độ cực nhanh:** Lấy trọn bộ thông tin DNS (A, CNAME, MX, TXT...) ngay lập tức.
- **Dễ dàng mở rộng:** Có thể kết hợp thêm danh sách hàng trăm domain từ Google Sheets để quét hàng loạt.
- **Tiết kiệm nguồn lực:** Giúp đội ngũ SecOps và IT Ops kiểm tra thông tin cấu hình mạng của đối thủ hoặc hệ thống nội bộ chính xác.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **uProc Account:** Tài khoản uProc để lấy API Key kết nối với node uProc trong n8n.
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n Editor, sau đó copy toàn bộ mã nguồn JSON của workflow này (hoặc tải file JSON từ trang chủ n8n template #862) và dán trực tiếp vào giao diện làm việc của n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 3 node chính gọn gàng, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Node `On clicking 'execute'` (manualTrigger):** 
  - Đây là điểm khởi đầu thủ công. Các sếp có thể thay thế node này bằng *Webhook* hoặc *Schedule Trigger* nếu muốn tự động hóa theo lịch trình hoặc nhận request từ hệ thống khác.
- **Node `Create Domain Item` (functionItem):** 
  - Nơi các sếp định nghĩa tên domain cần kiểm tra. Hãy mở node này và thay đổi giá trị domain mẫu thành domain thực tế mà các sếp muốn truy vấn DNS.
- **Node `Get DNS records` (uproc):** 
  - Node cốt lõi kết nối với dịch vụ uProc. Các sếp cần tạo **uProc API Credentials** trong n8n bằng cách nhập API Key lấy từ tài khoản uProc của mình. Sau đó chọn đúng phương thức truy vấn bản ghi DNS cho domain được truyền từ node phía trước.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** để kiểm tra dữ liệu trả về từ node uProc xem đã hiển thị đầy đủ các thông tin bản ghi DNS chưa.
- Sau khi kiểm tra mọi thứ mượt mà, các sếp có thể bật công tắc **Active** để đưa workflow vào trạng thái sẵn sàng hoạt động.

---

### ✍️ Mẹo & gợi ý nâng cao
Để workflow này trở thành một "trợ thủ" đắc lực thực thụ trong hệ thống của các sếp, hãy thử các cải tiến sau:
1. **Kết hợp Google Sheets / Airtable:** Thay vì hard-code một domain ở node *Create Domain Item*, hãy đọc danh sách hàng trăm domain từ Google Sheets, chạy vòng lặp để quét DNS hàng loạt.
2. **Cảnh báo qua Telegram / Slack:** Tự động gửi kết quả phân tích DNS về kênh Telegram hoặc Slack của team khi hoàn tất quá trình quét.
3. **Lưu trữ lịch sử:** Lưu toàn bộ kết quả trả về vào cơ sở dữ liệu (PostgreSQL, Supabase) để theo dõi sự thay đổi cấu hình DNS của domain theo thời gian (rất hữu ích cho SecOps phát hiện thay đổi bất thường).

### 📌 Kết luận
Chỉ với 3 node cực kỳ tinh gọn, workflow này giúp các sếp tiết kiệm rất nhiều thời gian trong việc khai thác thông tin mạng của các domain. Hãy triển khai ngay vào hệ thống n8n của mình và tối ưu hóa quy trình IT Ops ngay hôm nay các sếp nhé!