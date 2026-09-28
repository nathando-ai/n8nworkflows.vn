---
title: "🚀 Tự động giám sát tài nguyên Azure, quản lý chi phí và xuất báo cáo thông minh với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động kết nối Azure subscription, phân tích chi phí, tracking tài nguyên và xuất báo cáo chi tiết sang Excel hoặc Power BI."
slug: "giam-sat-chi-phi-tai-nguyen-azure-n8n"
tags: [n8n, azure, devops, cost-management, automation, cloud-monitoring]
keywords: [n8n azure monitoring, tự động hóa azure cost, quản lý chi phí azure, n8n workflow devops, azure resource graph api]
---

# 🚀 Tự động giám sát tài nguyên Azure, quản lý chi phí và xuất báo cáo thông minh

Các sếp làm DevOps hoặc quản lý hệ thống Cloud chắc hẳn đã từng đau đầu với bài toán kiểm soát chi phí Azure (Azure Cost Management). Việc kiểm tra thủ công xem tài nguyên nào đang tiêu tốn nhiều tiền, dịch vụ nào lãng phí hay tổng hợp báo cáo hàng tháng thường tốn rất nhiều thời gian và dễ bỏ sót.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa toàn bộ quy trình kết nối vào Azure subscription, truy vấn danh sách tài nguyên, bóc tách chi phí, tổng hợp top 10 tài nguyên ngốn tiền nhất và xuất ra các định dạng báo cáo (Text, HTML, Excel hoặc đẩy lên Power BI) mà không cần tốn một giọt mồ hôi viết code phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Định kỳ quét toàn bộ tài nguyên (VM, Database, Storage...) và chi phí thực tế mà không cần human intervention.
- **Phát hiện lãng phí:** Nhanh chóng chỉ ra Top 10 tài nguyên "đốt tiền" nhiều nhất trong hệ thống.
- **Đa dạng định dạng báo cáo:** Tự động tổng hợp dữ liệu thành báo cáo HTML, Text, xuất file Excel hoặc đẩy trực tiếp lên dashboard Power BI.
- **Chủ động kiểm soát ngân sách:** Giúp đội ngũ tài chính và kỹ thuật nắm bắt chi phí kịp thời, tránh tình trạng "té ngửa" cuối tháng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Khuyên dùng Self-hosted trên VPS).
- **Azure Account:** Có quyền cấu hình trên Azure Active Directory (Microsoft Entra ID) và Azure Subscription.
- **Azure App Registration (Service Principal):** Được gán quyền `Reader` và `Cost Management Reader` trên subscription.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc copy toàn bộ mã nguồn JSON từ n8n template, sau đó paste trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà, các sếp cần cấu hình chính xác các điểm mấu chốt sau:

- **Thiết lập Credentials (`oAuth2Api`):**
  - Trong Azure AD, tạo App Registration để lấy `Client ID`, `Client Secret` và `Tenant ID`.
  - Cấu hình OAuth2 trong n8n với Grant Type là **Client Credentials**.
  - Token URL: `https://login.microsoftonline.com/{TENANT_ID}/oauth2/v2.0/token`
  - Scope: `https://management.azure.com/.default`
  - Áp dụng credentials này cho 2 node: **Query Azure Resources** và **Get Cost Data**.

- **Node `Set Configuration`:**
  - Điền chính xác `Subscription ID` và `Tenant ID` của các sếp vào đây.
  - Tùy chỉnh khoảng thời gian (Billing Period Dates) nếu muốn quét khoảng thời gian khác ngoài tháng hiện tại.

- **Các node xử lý dữ liệu (`Merge and Process Data`, `Format Report`):**
  - Chạy bằng code JavaScript thuần túy có sẵn trong workflow để join dữ liệu tài nguyên và chi phí, lọc ra top tài nguyên tốn kém nhất.

- **Node xuất dữ liệu (`Export to Excel`, `Send to Power BI`, `Respond to Webhook`):**
  - Tùy chọn bật/tắt các nhánh này tùy theo nhu cầu thực tế (ví dụ: muốn lưu file Excel, muốn đẩy dữ liệu vào Power BI hoặc trả về qua Webhook).

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** tại node **Manual Trigger** để test chạy thử với dữ liệu thực tế.
- Kiểm tra các nhánh dữ liệu xem đã trả về kết quả chính xác chưa.
- Gạt công tắc sang **Active** để bật chế độ tự động chạy theo lịch trình (Schedule) nếu muốn.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack vào sau bước **Format Report** để bắn tin nhắn cảnh báo ngay lập tức khi phát hiện chi phí vượt ngưỡng.
- **Lưu trữ lịch sử:** Kết hợp thêm node Google Sheets hoặc Airtable để lưu lại lịch sử chi phí từng tháng, phục vụ cho việc vẽ biểu đồ tăng trưởng chi phí dài hạn.
- **Chạy định kỳ tự động:** Thay thế node **Manual Trigger** bằng **Schedule Trigger** để workflow tự động chạy vào ngày 1 hàng tháng.

### 📌 Kết luận
Quản lý chi phí Cloud chưa bao giờ dễ dàng đến thế khi kết hợp sức mạnh của Azure APIs và sự linh hoạt của n8n. Hãy "lên đồ" ngay một con VPS, import workflow này vào và tối ưu hóa chi phí hạ tầng cho doanh nghiệp của các sếp ngay hôm nay!