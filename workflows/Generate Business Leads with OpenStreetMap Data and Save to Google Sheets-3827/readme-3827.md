---
title: "🚀 Tự động quét và thu thập thông tin khách hàng tiềm năng (B2B Leads) từ OpenStreetMap vào Google Sheets bằng n8n"
description: "Hướng dẫn chi tiết cách xây dựng hệ thống tự động tìm kiếm doanh nghiệp, lọc thông tin liên hệ và lưu vào Google Sheets sử dụng OpenStreetMap và n8n."
slug: "tu-dong-thu-thap-business-leads-openstreetmap-google-sheets"
tags: [n8n, automation, no-code, sales, marketing, lead-generation, openstreetmap]
keywords: [n8n workflow, tạo lead b2b, openstreetmap api, google sheets automation, tự động hóa marketing]
---

# 🚀 Tự động quét và thu thập thông tin khách hàng tiềm năng (B2B Leads) từ OpenStreetMap vào Google Sheets

Các sếp làm trong lĩnh vực Sales và Marketing chắc chắn hiểu rõ nỗi đau khi phải đi tìm kiếm thông tin doanh nghiệp (leads) thủ công. Việc ngồi copy-paste từng tên công ty, số điện thoại, website từ bản đồ hay internet vừa tốn hàng chục giờ đồng hồ, vừa dễ sai sót lại nhanh chóng khiến đội ngũ "kiệt sức". 

Giải pháp là đây! Workflow n8n siêu việt này sẽ tự động hóa 100% quy trình truy xuất dữ liệu doanh nghiệp từ **OpenStreetMap**, làm sạch thông tin liên hệ (Website, Email) và tự động đồng bộ thẳng vào **Google Sheets** của các sếp. Không cần code phức tạp, chỉ cần cài đặt một lần và chạy mãi mãi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Tự động hóa hoàn toàn từ bước quét dữ liệu bản đồ đến khi lưu vào bảng tính.
- **Dữ liệu sạch & chất lượng:** Hệ thống tự động lọc các doanh nghiệp không có thông tin liên hệ và trích xuất email/website từ trang chủ.
- **Tập trung chốt sales:** Thay vì tốn thời gian tìm kiếm, đội ngũ sales của các sếp chỉ việc gọi điện và tư vấn cho danh sách lead đã sẵn sàng.
- **Hoạt động linh hoạt:** Có thể kích hoạt thủ công khi cần quét một khu vực mới hoặc tích hợp chạy ngầm tự động theo lịch trình.
:::

### ️🎯 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Self-hosted hoặc Cloud).
- Tài khoản Google (để kết nối và ghi dữ liệu vào Google Sheets).
- Một chút kiến thức cơ bản về cách cấu hình Node trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp hãy tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow này và dán trực tiếp vào giao diện n8n Editor (hoặc import file JSON gốc từ nguồn).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần lưu ý cấu hình chính xác các node quan trọng sau:

- **Google Sheets:** Node này chịu trách nhiệm lưu toàn bộ danh sách leads thu thập được. Các sếp bắt buộc phải kết nối tài khoản Google của mình, chọn đúng file Spreadsheet và Sheet Name để dữ liệu đổ về đúng chỗ.
- **HTTP Request (và Get Website HTML):** Node này dùng để gọi API lấy dữ liệu từ OpenStreetMap và cào dữ liệu từ website doanh nghiệp. Hãy kiểm tra lại cấu hình request, headers hoặc tham số truyền vào (nếu có thay đổi về khu vực hoặc ngành nghề tìm kiếm).
- **Loop Over Items / Loop Over Items1 (splitInBatches):** Quản lý việc chia nhỏ dữ liệu để xử lý hàng loạt mà không bị quá tải (rate limit) hay tràn bộ nhớ.
- **Clean Emails & Scrape HomePage (code):** Các node xử lý bằng mã Javascript (Node) giúp làm sạch định dạng email và bóc tách thông tin từ mã nguồn HTML của trang chủ doanh nghiệp.
- **Filter Away Items With No Contact Info (filter) & Has Email? / Has No Website? (if):** Các node điều kiện giúp lọc bỏ những bản ghi rác, không có giá trị chuyển đổi trước khi đưa vào bảng tính.

#### 3. Kích hoạt ⚡️
- Nhấn nút **‘Test workflow’** (thông qua node `When clicking ‘Test workflow’` hoặc `When Executed by Another Workflow`) để chạy thử với một lượng dữ liệu mẫu nhỏ.
- Kiểm tra lại kết quả hiển thị trên Google Sheets xem đã đúng ý các sếp chưa.
- Sau khi test thành công, gạt công tắc sang trạng thái **Active** để workflow sẵn sàng vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node **Telegram** hoặc **Slack** vào cuối workflow để nhận thông báo ngay lập tức về điện thoại mỗi khi có một mẻ leads mới được quét và lưu thành công.
- **Tự động hóa theo lịch:** Thay thế hoặc kết hợp node `manualTrigger` bằng node `Schedule Trigger` để hệ thống tự động quét leads theo tuần hoặc theo tháng.
- **Lưu trữ backup:** Kết hợp thêm các bước ghi log hoặc phân loại leads dựa trên ngành nghề/khu vực để chiến dịch gọi telesales hoặc gửi email marketing (như Email Outbound) đạt hiệu quả cao nhất.

### 📌 Kết luận
Việc xây dựng một hệ thống quét leads tự động từ OpenStreetMap chưa bao giờ dễ dàng đến thế với n8n. Hãy áp dụng ngay workflow này để tối ưu hóa nguồn lực, gia tăng danh sách khách hàng tiềm năng và bứt phá doanh số cho doanh nghiệp của các sếp ngay hôm nay!