---
title: "🚀 Tự động hóa theo dõi chi tiêu SaaS từ hóa đơn email với AgentMail, JigsawStack và Postgres"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình xử lý hóa đơn email, trích xuất dữ liệu và lưu trữ vào cơ sở dữ liệu Postgres bằng n8n"
slug: "tu-dong-hoa-theo-doi-chi-tieu-saas-tu-hoa-don-email"
tags: [n8n, automation, no-code, SaaS, Postgres, AgentMail, JigsawStack]
keywords: [n8n workflow, tự động hóa hóa đơn, xử lý email, Postgres, SaaS, AgentMail, JigsawStack]
---

# 🚀 Tự động hóa theo dõi chi tiêu SaaS từ hóa đơn email với AgentMail, JigsawStack và Postgres

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi phải xử lý thủ công hàng nghìn hóa đơn email hàng tháng. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian xử lý hóa đơn thủ công hàng tháng
- Tự động trích xuất dữ liệu từ hóa đơn PDF với độ chính xác cao
- Lưu trữ dữ liệu hóa đơn trong cơ sở dữ liệu Postgres để phân tích chi tiêu
- Theo dõi chi tiêu SaaS theo thời gian thực thông qua bảng tổng hợp
- Tự động hóa quy trình xử lý hóa đơn mới đến từ email
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản AgentMail để nhận và xử lý email hóa đơn
- API Key từ JigsawStack để xác minh loại tài liệu
- Cơ sở dữ liệu Postgres đã cấu hình
- Tài khoản LlamaCloud để xử lý trích xuất dữ liệu từ PDF
- (Tùy chọn) Redis instance cho quản lý phiên
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [trang workflow gốc](https://n8n.io/workflows/14997)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **AgentMail Webhook Trigger**:
   - Cấu hình URL webhook trong tài khoản AgentMail của bạn
   - Đường dẫn webhook: `/spendbase-inbound`
   - Phương thức HTTP: POST

2. **Post to JigsawStack API**:
   - Tạo credential mới với tên "jigsawStackApi"
   - Nhập API Key từ tài khoản JigsawStack của bạn

3. **Postgres Credentials**:
   - Tạo credential mới với tên "postgres"
   - Nhập thông tin kết nối đến cơ sở dữ liệu Postgres của bạn

4. **HTTP Request Nodes**:
   - Cấu hình các credential HTTP cần thiết (httpBearerAuth, httpHeaderAuth)
   - Đối với node "Post to LlamaCloud Extraction":
     - Base URL: `https://api.cloud.llamaindex.ai`
   - Đối với node "Download Email Attachment":
     - Base URL: `https://api.agentmail.to`

5. **Redis Advanced Processing** (nếu sử dụng):
   - Tạo credential mới với tên "redis"
   - Nhập thông tin kết nối đến Redis instance của bạn

#### 3. Kích hoạt ⚡️
1. Chạy workflow một lần với dữ liệu mẫu để kiểm tra kết nối
2. Sau khi tất cả các node được cấu hình đúng, bật chế độ Active cho workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tối ưu hóa xử lý hàng loạt**:
   - Điều chỉnh kích thước batch trong node "Loop Over Batch Items" để phù hợp với tải xử lý của hệ thống

2. **Báo cáo định kỳ**:
   - Kết nối workflow với các dịch vụ báo cáo như Google Sheets hoặc Slack để gửi báo cáo tổng hợp chi tiêu hàng tháng

3. **Xử lý lỗi nâng cao**:
   - Cấu hình email thông báo khi có lỗi xảy ra trong quá trình xử lý

4. **Tích hợp với các công cụ khác**:
   - Kết nối với các công cụ phân tích dữ liệu như Tableau hoặc Power BI để tạo báo cáo chi tiết về chi tiêu SaaS

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa quy trình xử lý hóa đơn SaaS từ email đến lưu trữ dữ liệu. Bằng cách triển khai workflow này, các sếp có thể tiết kiệm thời gian đáng kể, giảm thiểu lỗi xử lý và có được dữ liệu chi tiêu chính xác để đưa ra quyết định kinh doanh tốt hơn.