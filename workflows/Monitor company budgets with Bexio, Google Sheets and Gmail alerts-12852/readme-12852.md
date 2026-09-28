---
title: "🚀 Tự động giám sát ngân sách doanh nghiệp với Bexio, Google Sheets và Gmail"
description: "Hướng dẫn thiết lập workflow n8n tự động đồng bộ dữ liệu kế toán Bexio, so sánh với ngân sách trong Google Sheets và gửi cảnh báo qua Gmail."
slug: "tu-dong-giam-sat-ngan-sach-doanh-nghiep-bexio-google-sheets-gmail"
tags: [n8n, automation, no-code, bexio, google-sheets, gmail, financial-monitoring]
keywords: [n8n workflow, giám sát ngân sách, bexio api, google sheets automation, tự động hóa kế toán, cảnh báo email]
---

# 🚀 Tự động giám sát ngân sách doanh nghiệp với Bexio, Google Sheets và Gmail

Việc kiểm soát chi phí thủ công thường tốn rất nhiều thời gian và đôi khi chúng ta chỉ phát hiện ra việc vượt ngân sách khi đã quá muộn. Đối với các nhà quản lý vàanh em làm tài chính, việc dò dẫm giữa các bảng tính Excel hay Bexio để đối chiếu chi phí thực tế với kế hoạch là một "nỗi đau" thực sự.

Workflow n8n này sẽ giải quyết triệt để bài toán đó bằng cách tự động hóa 100%: lấy dữ liệu kế toán từ phần mềm Bexio, đối chiếu với ngân sách mục tiêu trên Google Sheets, tính toán chênh lệch và tự động gửi báo cáo tổng hợp qua Gmail. Giúp các sếp chuyển từ trạng thái **quản lý bị động** sang **kiểm soát chủ động** theo thời gian thực!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Định kỳ trích xuất dữ liệu từ Bexio API mà không cần can thiệp thủ công.
- **Cảnh báo vượt ngân sách kịp thời:** Phát hiện ngay các khoản chi phí vượt mức dự kiến theo từng tháng/giai đoạn.
- **Báo cáo chuyên nghiệp:** Tổng hợp số liệu và gửi email báo cáo chi tiết qua Gmail theo lịch trình (hàng tuần/hàng tháng).
- **Tiết kiệm thời gian:** Loại bỏ hoàn toàn công việc sao chép dữ liệu thủ công giữa các nền tảng kế toán và bảng tính.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Bexio:** Có quyền truy cập API (Bearer Token).
- **Google Sheets:** File Google Sheets chứa thông tin mục tiêu ngân sách (Budgets) và danh mục tài khoản (Accounts).
- **Gmail Account:** Tài khoản Gmail được cấu hình xác thực OAuth2 để gửi email báo cáo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này và import trực tiếp vào n8n Editor của mình thông qua tính năng "Import from File" hoặc copy/paste trực tiếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 19 nodes được chia thành các cụm chức năng rõ ràng. Các sếp cần chú ý cấu hình các node sau:

- **Schedule Trigger:** Thiết lập lịch chạy tự động (ví dụ: hàng tuần vào thứ Hai hoặc hàng tháng).
- **Get Records (HTTP Request Node):** Cần cấu hình `httpBearerAuth` kết nối với API của Bexio để lấy toàn bộ dữ liệu bút toán (journal entries) thông qua vòng lặp phân trang (pagination loop).
- **Update Records & Read Budgets & Get Debits & Get Credits (Google Sheets Nodes):** Kết nối tài khoản Google Sheets thông qua `googleSheetsOAuth2Api`. Trỏ đúng đường dẫn tới file Google Sheets quản lý ngân sách của công ty.
- **Calculate Credits, Calculate debit, Calculate Costs, Check Budgets, Compose Report (Code Nodes):** Các node này chạy mã JavaScript để xử lý logic tài chính, tính toán delta giữa ghi có (Credits) và ghi nợ (Debits), đồng thời so sánh với ngưỡng ngân sách.
- **Send Report (Gmail Node):** Chọn credentials `gmailOAuth2`. Tại trường **To**, điền địa chỉ email nhận báo cáo của các sếp hoặc đội ngũ tài chính.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng cách nhấn nút "Execute Workflow" để kiểm tra xem dữ liệu từ Bexio và Google Sheets có đồng bộ chính xác không.
- Kiểm tra email đến xem định dạng báo cáo đã chuẩn chỉnh chưa.
- Bật công tắc **Active** để workflow chạy tự động theo lịch đã hẹn.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa kênh nhận tin:** Thay thế hoặc bổ sung node Gmail bằng node **Slack** hoặc **Microsoft Teams** để bắn thông báo tức thì lên group chat khi có khoản chi vượt ngân sách.
- **Tùy chỉnh lịch chạy:** Thay đổi `Schedule Trigger` thành chạy hàng ngày (daily) nếu doanh nghiệp có tốc độ giao dịch lớn và cần kiểm soát chi phí ngặt nghèo hơn.
- **Lưu lịch sử báo cáo:** Thêm một node Google Sheets ở cuối luồng để ghi lại lịch sử các lần báo cáo nhằm phục vụ việc audit sau này.

### 📌 Kết luận
Workflow tích hợp Bexio, Google Sheets và Gmail này là một trợ thủ đắc lực giúp tự động hóa khâu kiểm soát tài chính cho các nhà sáng lập và quản lý. Hãy cài đặt ngay hôm nay để tối ưu hóa chi phí và quản trị doanh nghiệp thông minh hơn!