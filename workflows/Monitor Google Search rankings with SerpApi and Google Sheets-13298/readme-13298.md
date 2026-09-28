---
title: "🚀 Tự Động Theo Dõi Thứ Hạng Từ Khóa SEO Trên Google Với SerpApi Và Google Sheets"
description: "Hướng dẫn cấu hình workflow n8n tự động check thứ hạng từ khóa SEO bằng SerpApi, lưu log chi tiết và cập nhật kết quả vào Google Sheets mỗi ngày."
slug: "tu-dong-theo-doi-thu-hang-tu-khoa-seo-serpapi-google-sheets"
tags: [n8n, automation, seo, serpapi, google-sheets, marketing]
keywords: [n8n workflow, seo rank tracking, serpapi google sheets, tu dong hoa seo, kiem tra thu hang tu khoa]
keywords: [n8n workflow, seo rank tracking, serpapi google sheets, tự động hóa seo, kiểm tra thứ hạng từ khóa]
---

# 🚀 Tự Động Theo Dõi Thứ Hạng Từ Khóa SEO Trên Google Với SerpApi Và Google Sheets

Các sếp làm SEO chắc chắn đã quá ngán ngẩm cảnh mỗi sáng phải ngồi check tay hàng chục, hàng trăm từ khóa trên Google, sau đó copy paste vào file Excel để báo cáo. Việc này vừa tốn thời gian, dễ sai sót lại chẳng mang lại giá trị sáng tạo nào. 

Hiểu được nỗi đau đó, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực xịn sò giúp tự động hóa 100% quy trình check rank SEO bằng **SerpApi** và lưu trữ kết quả trực tiếp vào **Google Sheets**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoàn toàn:** Lịch trình tự động chạy hàng ngày vào lúc 10h sáng (hoặc tùy chỉnh) mà không cần can thiệp thủ công.
- **Dữ liệu đồng bộ:** Lưu trữ toàn bộ lịch sử rank vào Google Sheets, giúp dễ dàng vẽ biểu đồ tăng trưởng.
- **Cấu hình linh hoạt:** Hỗ trợ tìm kiếm theo domain hoặc exact URL (đường dẫn chính xác), kèm giới hạn số trang quét.
- **Tránh rate limit:** Tích hợp sẵn cơ chế chờ thông minh giữa các request để không bị Google Sheets chặn API.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance **n8n** đang hoạt động.
- Tài khoản **SerpApi** (Đăng ký miễn phí tại [serpapi.com](https://serpapi.com/) và lấy API Key).
- Tài khoản **Google Sheets** đã kết nối với n8n.
- Mẫu Google Sheet quản lý từ khóa ([Link mẫu chuẩn từ tác giả](https://docs.google.com/spreadsheets/d/148gjSSqSY5x9Gz5JWE_FDXHOuB7ASTomSyxkZjrjuNc/edit?gid=1750873622#gid=1750873622)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ n8n template (ID: 13298) và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 10 nodes chính làm việc nhịp nhàng với nhau. Các sếp cần chú ý cấu hình các điểm sau:

- **Schedule Workflow:** Mặc định chạy lúc 10h UTC mỗi ngày. Các sếp có thể đổi lại múi giờ hoặc thời gian chạy tùy ý.
- **Get Keywords and Domains to Match (Google Sheets):** 
  - Chọn tài khoản Google Sheets của các sếp.
  - Trỏ tới file Google Sheet quản lý từ khóa đã chuẩn bị.
- **Set Page Limit & Match Type (Code Node):** 
  - `pagination_limit`: Mặc định check tới 10 trang Google. Có thể giảm xuống nếu muốn tiết kiệm credit SerpApi.
  - `match_type`: Chọn `'domain'` (tìm toàn bộ domain) hoặc `'page'` (tìm đúng URL chính xác).
- **Search Google (SerpApi):** Nhập SerpApi Credentials đã lấy từ tài khoản của các sếp.
- **Update Rank Log & Update Latest Run (Google Sheets):** 
  - Kết nối lại với file Google Sheet của các sếp ở cả 2 node này để ghi nhận lịch sử và cập nhật trạng thái mới nhất.
  - Đảm bảo các expression map đúng với các trường dữ liệu (`searched_at`, `target`, `keyword`, `rank`, `row_number`).
- **Wait Before Next Keyword (Wait Node):** Tạo độ trễ 4 giây giữa các từ khóa để tránh chạm giới hạn API của Google Sheets.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử với danh sách từ khóa mẫu xem dữ liệu đã đổ về Google Sheets chuẩn chỉnh chưa.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node **Slack** hoặc **Telegram** sau node cập nhật dữ liệu để bắn tin nhắn báo cáo thứ hạng mỗi khi check xong.
- **Lưu log lỗi:** Thêm nhánh Error Trigger để nếu SerpApi hết credit hoặc lỗi mạng, hệ thống sẽ gửi cảnh báo ngay lập tức.
- **Chia mẻ (Batching):** Nếu danh sách từ khóa lên tới hàng nghìn, hãy tinh chỉnh lại node `Split InBatches` để tối ưu tài nguyên VPS n8n.

### 📌 Kết luận
Với workflow n8n này, việc theo dõi biến động SEO hàng ngày không còn là gánh nặng thủ công nữa. Triển khai ngay hôm nay để tối ưu hóa thời gian và làm chủ thứ hạng từ khóa trên Google các sếp nhé!