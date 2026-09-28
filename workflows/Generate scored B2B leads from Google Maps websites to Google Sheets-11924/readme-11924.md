---
title: "🚀 Tự động quét Lead B2B chất lượng cao từ Google Maps và lưu vào Google Sheets bằng n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động tìm kiếm doanh nghiệp trên Google Maps, quét website lấy email, chấm điểm chất lượng và đồng bộ vào Google Sheets."
slug: "tu-dong-quet-lead-b2b-tu-google-maps-vao-google-sheets"
tags: [n8n, automation, lead-generation, google-maps, google-sheets, web-scraping]
keywords: [n8n workflow, b2b lead generation, quét lead google maps, tự động hóa n8n, google maps api, scrape email website]
---

# 🚀 Tự động quét Lead B2B chất lượng cao từ Google Maps và lưu vào Google Sheets

Các sếp có đang mệt mỏi với việc tìm kiếm khách hàng tiềm năng (B2B) thủ công trên Google Maps? Copy từng tên công ty, click vào từng website để mò mẫm địa chỉ email, sau đó lại copy paste vào Excel? Công việc tẻ nhạt này vừa tốn hàng chục giờ đồng hồ, vừa dễ bỏ sót những khách hàng tiềm năng chất lượng.

Đừng lo, bài toán này sẽ được giải quyết triệt để 100% tự động với workflow **n8n** siêu việt được thiết kế bởi chuyên gia *Jannik Hiller*. Workflow này sẽ giúp các sếp càn quét Google Maps theo từ khóa, tự động truy cập website, bóc tách email, **chấm điểm chất lượng (score email)**, lọc ra địa chỉ tối ưu nhất và đẩy thẳng vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chỉ cần nhập từ khóa (ví dụ: *"Nhà hàng tại Quận 1"* hay *"Dentist New York"*), workflow tự động làm phần việc còn lại.
- **Chấm điểm thông minh (Email Scoring):** Phân loại email chuẩn xác (+30 điểm nếu trùng tên miền, +20 điểm email cá nhân, trừ điểm các email chung chung như info@ hay gmail miễn phí).
- **Lọc sạch dữ liệu rác:** Tự động loại bỏ doanh nghiệp đóng cửa, loại bỏ trùng lặp (deduplication) và chỉ giữ lại 1 email chất lượng nhất cho mỗi doanh nghiệp.
- **Đồng bộ thời gian thực:** Đổ dữ liệu sạch sẽ, gọn gàng trực tiếp vào Google Sheets để đội Sales bắt tay vào gọi điện/gửi email ngay lập tức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn (Self-hosted hoặc n8n Cloud).
- **Google Cloud Console Account:** Để lấy **Google Places API Key** (Kích hoạt Places API New).
- **Google Sheets Account:** Tạo sẵn một file Google Sheets để chứa danh sách lead.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow (hoặc tải file từ nguồn gốc) và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 25 nodes được chia thành 4 giai đoạn chính. Các sếp cần chú ý các điểm cấu hình quan trọng sau:

- **Node `Search Google Maps with query` (HTTP Request):** 
  - Cần cấu hình kết nối API của Google Places (New API). 
  - Đảm bảo truyền đúng từ khóa tìm kiếm (search queries) thông qua node `Loop over queries` (`splitInBatches`).
- **Node `Fetch Website HTML` & `Fetch Contact Page HTML` (HTTP Request):** 
  - Các node này chịu trách nhiệm truy cập vào trang chủ và trang liên hệ của doanh nghiệp để cào HTML tìm chuỗi email. Không cần đổi credentials nhưng cần đảm bảo VPS của các sếp có IP sạch để không bị chặn bởi Cloudflare/Firewall của mục tiêu.
- **Node `Score and Rank Emails` (Code):** 
  - Node này chạy mã xử lý logic chấm điểm (+30 domain match, +20 personal names, -40 generic prefixes như `info@`, `support@`, -25 free providers như `@gmail.com`). Các sếp có thể tùy chỉnh lại trọng số điểm trong code JS này nếu muốn ưu tiên loại email khác.
- **Node `Append to Google Sheets` (Google Sheets):** 
  - Kết nối tài khoản Google của các sếp.
  - Chọn đúng file Spreadsheet và Sheet Name để hệ thống tự động thêm dòng dữ liệu mới (`append`).

#### 3. Kích hoạt ⚡️
- Bấm nút `Execute Workflow` ở node `Run workflow` (`manualTrigger`) với một vài từ khóa mẫu để test thử.
- Kiểm tra xem dữ liệu có trả về đúng và đẩy lên Google Sheets thành công hay không.
- Nếu mọi thứ mượt mà, hãy bật nút **Active** ở góc trên bên phải để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack ở cuối workflow để mỗi khi quét xong một mẻ lead, hệ thống sẽ bắn thông báo số lượng lead mới về điện thoại cho các sếp.
- **Lọc theo vị trí địa lý hẹp:** Kết hợp thêm các tham số tọa độ (latitude, longitude) trong query Google Maps để quét chính xác các khu vực nhỏ hơn (phường/quận).
- **Gửi email tự động (Cold Outreach):** Nối tiếp Google Sheets bằng node Gmail hoặc Email Outreach để tự động gửi chuỗi email chăm sóc (Drip campaign) đến những email có điểm số cao nhất.

### 📌 Kết luận
Workflow quét lead B2B từ Google Maps này là một vũ khí cực kỳ lợi hại cho các đội ngũ marketing và sales thời đại số. Thay vì mất hàng tuần lễ để đi cóp nhặt data kém chất lượng, giờ đây các sếp chỉ cần vài phút thiết lập để có ngay một phễu khách hàng tiềm năng tự động, sạch sẽ và chuẩn xác. Chúc các sếp "lên đồ" thành công và chốt thật nhiều hợp đồng!