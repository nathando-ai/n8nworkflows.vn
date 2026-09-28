---
title: "🚀 Tối ưu hóa chuỗi cung ứng tự động với phân tích ABC & Pareto trên Google Sheets bằng n8n"
description: "Tự động hóa toàn bộ quy trình phân tích kho hàng ABC, XYZ và Pareto từ Google Sheets giúp doanh nghiệp quản lý tồn kho thông minh và tối ưu chi phí vận hành."
slug: "toi-uu-hoa-chuoi-cung-ung-phan-tich-abc-pareto-google-sheets-n8n"
tags: [n8n, automation, supply-chain, google-sheets, data-analysis, inventory-management]
keywords: [n8n workflow, phân tích ABC Pareto, quản lý tồn kho tự động, tối ưu chuỗi cung ứng, google sheets n8n]
---

# 🚀 Tối ưu hóa chuỗi cung ứng tự động với phân tích ABC & Pareto trên Google Sheets

Trong quản lý chuỗi cung ứng và kho hàng, việc phân loại nhóm hàng tồn kho theo phương pháp **ABC & Pareto (Quy tắc 80/20)** hay phân tích biến động **XYZ** đóng vai trò cực kỳ quan trọng giúp doanh nghiệp tập trung nguồn lực vào các mặt hàng mang lại giá trị cao nhất. Tuy nhiên, việc xử lý thủ công hàng ngàn dòng dữ liệu bán hàng trên Excel/Google Sheets mỗi tuần tốn rất nhiều thời gian và dễ xảy ra sai sót.

Workflow n8n này (được chia sẻ bởi chuyên gia Supply Chain **Samir Saci**) sẽ giúp các sếp tự động hóa 100% quy trình đọc dữ liệu bán hàng, tính toán phân tích Pareto, gom nhóm sản phẩm theo kho/cửa hàng và ghi kết quả trở lại Google Sheets một cách mượt mà và chính xác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Loại bỏ hoàn toàn các bước tính toán thủ công phức tạp trên bảng tính.
- **Phân tích chính xác:** Tự động thực hiện phân tích Pareto (Quy tắc 80/20) và phân loại ABC/XYZ cho từng mặt hàng và cửa hàng.
- **Quản lý đa cửa hàng hiệu quả:** Phân tách và tổng hợp dữ liệu doanh số theo từng Store (Store 1, Store 2, Multi-Store).
- **Cập nhật dữ liệu thời gian thực:** Kết quả phân tích được đẩy thẳng về Google Sheets để các bộ phận liên quan sử dụng ngay lập tức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google Drive / Google Sheets** có chứa sẵn file dữ liệu mẫu (Input Data) với các cột thông tin bán hàng, mã sản phẩm, cửa hàng, số lượng và doanh số.
- **Google Sheets OAuth2 API Credentials** để n8n có thể đọc và ghi dữ liệu vào file của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã JSON từ nguồn.
- Mở n8n Editor, chọn **Add workflow** -> Nhấn vào dấu `...` ở góc trên bên phải -> Chọn **Import from File** hoặc **Paste Workflow**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Node `Get row(s) in sheet`**: 
  - Kết nối tài khoản Google Sheets của các sếp tại phần **Credentials**.
  - Chọn đúng File Google Sheet chứa dữ liệu và trỏ tới sheet có tên **`Input Data`** (nơi chứa dữ liệu giao dịch bán hàng đầu vào).
- **Các Node ghi dữ liệu Google Sheets (`Sales Store 1`, `Sales Store 2`, `Multi-Store Sales`, `ABC XYZ Analysis`, `Update Pareto Sheet`)**:
  - Đảm bảo các node này đều sử dụng chung thông tin **Credentials** Google Sheets.
  - Kiểm tra lại Document ID và tên Sheet đích tương ứng trong file Google Sheets của các sếp để dữ liệu được append (thêm dòng mới) chính xác vào các tab báo cáo.
- **Các Node Code xử lý dữ liệu (`Transpose`, `Daily Sales per Store`, `Pareto Analysis`, `TO, QTY GroupBy ITEM`, `TO GroupBy (STORE, ITEM)`, `Demand Variability x Sales %`, `ABC Class Mapping`)**:
  - Các đoạn mã JavaScript bên trong đã được cấu hình sẵn các thuật toán phân tích chuỗi cung ứng tiêu chuẩn. Các sếp không cần sửa code trừ khi cấu trúc cột dữ liệu đầu vào của các sếp có tên gọi khác biệt.

#### 3. Kích hoạt ⚡️
- Nhấn nút **`When clicking ‘Execute workflow’`** để chạy thử nghiệm (Test Run) với dữ liệu mẫu.
- Kiểm tra lại các tab trên Google Sheets xem dữ liệu đã được tính toán và đổ về đầy đủ chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để hoàn tất.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp cảnh báo Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để gửi thông báo tóm tắt kết quả phân tích ABC hàng tuần cho ban quản lý.
- **Lên lịch chạy tự động (Cron/Schedule):** Thay thế node `Manual Trigger` bằng node `Schedule Trigger` để hệ thống tự động chạy phân tích vào mỗi đầu tuần hoặc đầu tháng.
- **Kết nối BI Tool:** Sử dụng Google Sheets kết nối trực tiếp với Looker Studio để vẽ biểu đồ Pareto trực quan cho đội ngũ vận hành.

### 📌 Kết luận
Workflow **Inventory ABC & Pareto Analysis with Google Sheets** là giải pháp "vàng" giúp các nhà quản lý chuỗi cung ứng tự động hóa các bài toán phân tích dữ liệu phức tạp chỉ bằng vài cú click. Áp dụng ngay hôm nay để nâng cao hiệu quả quản lý tồn kho và tối ưu hóa nguồn vốn cho doanh nghiệp của các sếp!