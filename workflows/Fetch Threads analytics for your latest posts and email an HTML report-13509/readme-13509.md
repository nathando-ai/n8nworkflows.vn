---
title: "🚀 Tự động hóa đo lường và gửi báo cáo Threads Analytics qua Email với n8n"
description: "Hướng dẫn cài đặt workflow n8n tự động lấy dữ liệu 100 bài đăng Threads mới nhất, phân tích tương tác và gửi báo cáo HTML qua Gmail."
slug: "tu-dong-hoa-threads-analytics-va-gui-bao-cao-email-n8n"
tags: [n8n, automation, threads, marketing, gmail, api]
keywords: [n8n workflow, threads analytics, tự động hóa marketing, threads api, báo cáo email n8n]
---

# 🚀 Tự động hóa đo lường và gửi báo cáo Threads Analytics qua Email với n8n

Các sếp làm nội dung trên Meta Threads chắc hẳn đều hiểu cảm giác "mỏi tay" khi phải liên tục kiểm tra lượt xem, lượt thích, bình luận và chia sẻ của từng bài viết để đo lường hiệu quả. Việc tổng hợp thủ công này vừa tốn thời gian vừa khó nhìn ra bức tranh tổng thể về hiệu suất kênh.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực xịn xò giúp tự động hóa 100% quy trình: lấy danh sách bài đăng mới nhất từ Threads Graph API, bóc tách số liệu tương tác, tổng hợp thành bảng báo cáo HTML đẹp mắt và gửi thẳng vào hộp thư Gmail của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoàn toàn:** Không cần tốn một phút nào copy/paste số liệu thủ công từ ứng dụng Threads.
- **Báo cáo trực quan:** Nhận ngay báo cáo HTML định dạng sạch sẽ, sắp xếp theo thời gian mới nhất kèm tổng kết số liệu (views, likes, replies, reposts, quotes).
- **Linh hoạt thời gian:** Chạy tự động theo lịch (mặc định 2 ngày/lần) hoặc kích hoạt thủ công bất cứ lúc nào sếp muốn.
- **Tối ưu vận hành:** Nắm bắt nhanh nội dung nào đang viral để kịp thời điều chỉnh chiến lược content.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Threads Access Token:** Token truy cập dài hạn (Long-lived Threads Access Token) từ Meta for Developers.
- **Tài khoản Google/Gmail:** Để cấu hình node gửi email báo cáo tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn gốc hoặc copy toàn bộ cấu trúc nodes được cung cấp để dán trực tiếp vào giao diện làm việc của n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 10 nodes phối hợp nhịp nhàng với nhau. Các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Node `Get Threads Token` (Data Table):** Nơi lưu trữ token truy cập Threads của các sếp. Hãy đảm bảo tạo một Data Table với Platform là `"Threads"` và lưu token dài hạn lấy từ Meta for Developers.
- **Node `Fetch Threads Posts` & `Fetch Post Insights` (HTTP Request):** Gọi trực tiếp vào Threads Graph API để lấy tối đa 100 bài đăng gần nhất cùng các chỉ số tương tác chi tiết. *(Lưu ý: API Threads giới hạn tối đa 500 requests/ngày, việc lấy 100 bài sẽ tiêu tốn khoảng 100 request insights).*
- **Node `Email Analytics Report` (Gmail):** Kết nối tài khoản Google cá nhân hoặc doanh nghiệp của các sếp, sau đó điền địa chỉ email nhận báo cáo.
- **Node `Schedule Trigger (Every 2 Days)` & `Manual Trigger`:** Mặc định lịch chạy là 11 giờ đêm mỗi 2 ngày. Các sếp có thể thay đổi thời gian này tùy theo nhu cầu theo dõi của đội ngũ.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm thủ công với dữ liệu mẫu, kiểm tra xem email HTML đã được gửi về hộp thư chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo phụ:** Kết hợp thêm node **Telegram** hoặc **Slack** để bắn một tin nhắn nhanh tóm tắt số liệu ngay khi email báo cáo được gửi đi.
- **Lưu trữ dữ liệu lịch sử:** Thêm node **Google Sheets** hoặc **Supabase** để lưu lại các chỉ số theo từng đợt chạy, phục vụ việc vẽ biểu đồ tăng trưởng kênh về lâu dài.
- **Mở rộng hệ thống:** Nếu các sếp muốn tự động lên lịch đăng bài lên Threads từ Notion, hãy tham khảo thêm gói giải pháp tự động hóa nội dung đa nền tảng.

### 📌 Kết luận
Việc đo lường hiệu suất mạng xã hội chưa bao giờ dễ dàng và tự động hóa đến thế. Hãy cài đặt ngay workflow này để tiết kiệm thời gian phân tích và tập trung hoàn toàn vào việc sáng tạo nội dung đỉnh cao cùng Threads!