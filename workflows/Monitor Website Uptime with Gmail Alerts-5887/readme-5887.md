---
title: "🚀 Giám sát Uptime Website tự động và cảnh báo qua Gmail với n8n"
description: "Hướng dẫn thiết lập hệ thống giám sát tình trạng website tự động 24/7, phát hiện website sập trước khách hàng và gửi cảnh báo ngay lập tức qua Gmail."
slug: "giam-sat-website-uptime-gmail-alerts"
tags: [n8n, automation, devops, website-monitoring, gmail, no-code]
keywords: [n8n workflow, giám sát uptime website, check website down tự động, cảnh báo qua gmail, n8n devops]
---

# 🚀 Tự động giám sát Uptime Website và cảnh báo qua Gmail với n8n

Các sếp có đang quản lý nhiều website, cửa hàng trực tuyến hay landing page không? Sẽ thật thảm họa nếu website bị sập mà khách hàng phát hiện trước, còn mình thì hay tin cuối cùng qua những lời than phiền (hoặc mất đơn hàng tiền triệu). Việc kiểm tra thủ công mỗi ngày là bất khả thi và cực kỳ tốn thời gian.

Giải pháp ở đây là gì? Hãy để n8n gánh vác việc này giúp các sếp! Workflow tự động hóa **Monitor Website Uptime with Gmail Alerts** này sẽ tự động kiểm tra sức khỏe các trang web của các sếp theo lịch trình, cơ chế double-check thông minh để tránh báo động giả, và gửi email cảnh báo ngay lập tức qua Gmail khi có sự cố xảy ra. 100% không cần code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phát hiện sự cố tức thì:** Biết ngay khi website "lăn đùng ra chết" trước khi khách hàng kịp phàn nàn.
- **Cơ chế chống báo động giả:** Tích hợp node chờ (`Wait`) và kiểm tra lại lần 2 trước khi bắn email cảnh báo, tránh trường hợp mạng chập chờn nhất thời.
- **Giám sát hàng loạt:** Dễ dàng cấu hình nhiều website cùng một lúc chỉ trong một node cài đặt.
- **Hoạt động 24/7 không mệt mỏi:** Chạy ngầm tự động theo lịch trình (Schedule) do các sếp tự định nghĩa.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản Google/Gmail để cấu hình OAuth2 gửi cảnh báo.
- Danh sách các URL website mà các sếp muốn giám sát.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy mã JSON của workflow này (hoặc tải file từ nguồn gốc) và dán trực tiếp vào n8n Editor của mình. Workflow gồm 14 nodes được thiết kế tối ưu với các chức năng kiểm tra, định tuyến (`Switch`), gộp dữ liệu (`Merge`) và chờ (`Wait`).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy đúng ý muốn, các sếp nhớ cấu hình kỹ các node trọng điểm sau:
- **Node `Config` / `Websites to Array`:** Đây là nơi các sếp thêm danh sách các URL website cần theo dõi. Có thể thêm nhiều website cùng lúc bằng cấu trúc mảng mà node này hỗ trợ.
- **Node `Wait before Second Attempt`:** Cấu hình thời gian chờ (ví dụ: vài chục giây) giữa lần kiểm tra đầu tiên thất bại và lần kiểm tra thứ hai để xác nhận chính xác website thực sự sập.
- **Node `Send Email Alert`:** Kết nối tài khoản Gmail của các sếp thông qua **OAuth2** (chỉ mất 1 cú click chuột xác thực với Google). Đồng thời, cấu hình địa chỉ email nhận thông báo cảnh báo.
- **Node `Schedule Trigger`:** Tùy chỉnh lịch chạy kiểm tra (ví dụ: chạy mỗi 5 phút, 15 phút hay 1 tiếng một lần tùy nhu cầu quan trọng của website).

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để chạy thử nghiệm thủ công với danh sách website mẫu.
- Kiểm tra kết quả trả về ở các node HTTP Request và Gmail xem đã trơn tru chưa.
- Sau khi test thành công, gạt công tắc sang **Active** để workflow chính thức gác cổng 24/7 cho các sếp.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Ngoài Gmail, các sếp có thể gắn thêm node Telegram Bot hoặc Slack để nhận tin nhắn pop-up ngay trên điện thoại cho nhanh gọn.
- **Lưu Log vào Google Sheets:** Thêm một node Google Sheets ở cuối luồng để ghi lại lịch sử uptime/downtime của website, phục vụ việc đánh giá độ ổn định của nhà cung cấp hosting/VPS sau mỗi tháng.
- **Cảnh báo phục hồi (Recovery Alert):** Mở rộng workflow để khi website "sống lại", hệ thống tự động gửi một email thông báo "Website đã hoạt động bình thường trở lại" để các sếp yên tâm.

### 📌 Kết luận
Một hệ thống giám sát uptime tưởng chừng phức tạp và tốn kém nay đã được tự động hóa hoàn toàn chỉ trong vài phút thiết lập với n8n. Đừng để website sập làm mất tiền oan của doanh nghiệp—hãy cài đặt ngay workflow này hôm nay các sếp nhé!