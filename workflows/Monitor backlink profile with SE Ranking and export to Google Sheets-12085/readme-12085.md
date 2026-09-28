---
title: "🚀 Tự động giám sát Backlink Profile với SE Ranking và Google Sheets trên n8n"
description: "Hướng dẫn tự động hóa quy trình theo dõi backlink, phân tích đối thủ, tổng hợp backlink mới/mất và xuất báo cáo chuyên nghiệp vào Google Sheets."
slug: "tu-dong-giam-sat-backlink-profile-se-ranking-google-sheets"
tags: [n8n, automation, seo, se-ranking, google-sheets]
keywords: [n8n workflow, se ranking, backlink monitoring, google sheets automation, seo tool n8n]
---

# 🚀 Tự động giám sát Backlink Profile với SE Ranking và Google Sheets

Việc theo dõi sức khỏe website và hồ sơ backlink thủ công là một "cực hình" đối với các SEO chuyên nghiệp và chủ doanh nghiệp. Các sếp thường phải mất hàng giờ đăng nhập vào các công cụ SEO, xuất file Excel, lọc dữ liệu và tổng hợp báo cáo hàng tuần hoặc hàng tháng. 

Giờ đây, với workflow n8n này, các sếp có thể tự động hóa toàn bộ quy trình thu thập dữ liệu backlink từ SE Ranking và lưu trữ trực tiếp vào Google Sheets một cách mượt mà, chính xác 100% mà không cần tốn một giọt mồ hôi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bức tranh toàn cảnh về Backlink:** Tự động lấy tổng số backlink, referring domains, điểm domain authority và các chỉ số trust metrics.
- **Phát hiện Backlink Mới & Mất:** Nắm bắt ngay các backlink mới có được trong 30 ngày qua và các backlink đã mất (kèm lý do).
- **Phân tích chuyên sâu:** Thống kê anchor text, các trang có nhiều backlink nhất và xu hướng tăng trưởng theo ngày/tháng.
- **Báo cáo tự động hóa:** Đồng bộ toàn bộ dữ liệu vào Google Sheets để chia sẻ với team hoặc khách hàng dễ dàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Hệ thống n8n (Self-hosted khuyến nghị).
- SE Ranking Community Node đã được cài đặt (`@seranking/n8n-nodes-seranking`).
- SE Ranking API Token ([Lấy API key tại đây](https://online.seranking.com/admin.api.dashboard.html)).
- Tài khoản Google Sheets để lưu trữ dữ liệu xuất ra.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp tiến hành tải file JSON của workflow này và import trực tiếp vào giao diện n8n Editor của mình, hoặc sử dụng tính năng copy/paste JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru với website của các sếp, hãy chú ý cấu hình các điểm sau:
- **Cài đặt Community Node:** Đảm bảo n8n đã cài đặt node SE Ranking. Nếu chưa, hãy vào mục Settings > Community Nodes để cài đặt gói `@seranking/n8n-nodes-seranking`.
- **Cấu hình Credentials:** Thiết lập `seRankingApi` bằng API token của các sếp và `googleSheetsOAuth2Api` để kết nối với Google Drive/Sheets.
- **Thay đổi tên miền:** Trong tất cả các node liên quan đến SE Ranking (như *Get backlinks summary*, *Get new backlinks*, *Get lost backlinks*, v.v.), hãy thay thế domain mẫu `example.com` bằng domain thực tế của các sếp.
- **Node Export to Google Sheets:** Chọn file Google Sheets đích và định dạng Sheet phù hợp để nhận dữ liệu đã được xử lý từ node *Format for Sheet*.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** trên node **Manual Trigger** để chạy thử nghiệm và kiểm tra dữ liệu trả về ở các node.
- Nếu muốn chạy tự động định kỳ hàng tuần, các sếp có thể thay thế node *Manual Trigger* bằng node *Schedule Trigger*.
- Cuối cùng, gạt công tắc sang chế độ **Active** để hoàn tất.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp cảnh báo Telegram/Slack:** Thêm một node Telegram hoặc Slack vào sau chuỗi xử lý để bắn thông báo ngay khi website có backlink "khủng" mới hoặc bị mất backlink quan trọng.
- **Tự động hóa định kỳ:** Kết hợp Schedule Trigger để chạy workflow vào thứ Hai hàng tuần, giúp team SEO có sẵn báo cáo tuần mà không cần động tay.
- **Tùy chỉnh thời gian:** Thay đổi các tham số `dateFrom` và `dateTo` trong các node lịch sử để theo dõi mốc thời gian tùy chỉnh (90 ngày, 6 tháng...).

### 📌 Kết luận
Workflow giám sát backlink profile với SE Ranking và Google Sheets là trợ thủ đắc lực giúp các sếp tiết kiệm hàng giờ làm việc thủ công, quản lý chiến lược SEO chặt chẽ và chuyên nghiệp hơn. Áp dụng ngay để tối ưu hóa hiệu suất làm việc của team ngay hôm nay!