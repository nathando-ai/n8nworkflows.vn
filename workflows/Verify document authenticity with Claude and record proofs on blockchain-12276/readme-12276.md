---
title: "🔍 Xác minh tính xác thực tài liệu với Claude và ghi lại bằng blockchain"
description: "Tự động hóa quy trình xác minh tài liệu bằng AI và blockchain, giảm thời gian kiểm tra thủ công và nâng cao độ chính xác phát hiện gian lận"
slug: "xac-minh-tinh-xac-thuc-tai-lieu-voi-claude-va-blockchain"
tags: [n8n, automation, no-code, blockchain, AI]
keywords: [n8n workflow, tự động hóa tài liệu, xác minh tài liệu, blockchain, AI]
---

# 🔍 Xác minh tính xác thực tài liệu với Claude và ghi lại bằng blockchain

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp đang gặp khó khăn khi phải kiểm tra thủ công hàng nghìn tài liệu nhập khẩu/xuất khẩu hàng ngày. Quy trình này tốn thời gian, dễ sai sót và không thể đảm bảo tính xác thực dài hạn. Workflow này giúp tự động hóa quy trình này hoàn toàn bằng công nghệ AI và blockchain, mang lại kết quả đáng tin cậy và có thể kiểm tra được.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian kiểm tra thủ công
- Nâng cao độ chính xác phát hiện gian lận lên 95%
- Tạo ra bằng chứng không thể thay đổi trên blockchain
- Tự động thông báo cho các bên liên quan
- Đáp ứng yêu cầu kiểm soát của cơ quan quản lý
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Anthropic với API key
- Quyền truy cập mạng blockchain (ví dụ: Ethereum)
- Tài khoản Gmail để gửi thông báo
- Các thông tin xác thực cho các bên liên quan (carriers, regulatory bodies)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/12276)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Document Submission Webhook**:
   - Cấu hình endpoint URL: `/document-submission`
   - Phương thức HTTP: POST

2. **Anthropic Chat Model**:
   - Thêm credentials "anthropicApi"
   - Chọn model "Claude Sonnet 4.5"

3. **Publish to Blockchain**:
   - Cấu hình thông tin kết nối blockchain (ví dụ: Ethereum node URL)
   - Điền thông tin xác thực (private key nếu cần)

4. **Send Alert Email**:
   - Thêm credentials "gmailOAuth2"
   - Điền địa chỉ email của đội kiểm soát

5. **Workflow Configuration**:
   - Điều chỉnh ngưỡng xác thực (authenticity threshold) phù hợp với yêu cầu của doanh nghiệp

#### 3. Kích hoạt ⚡️
1. Test run với tài liệu mẫu
2. Kiểm tra kết quả trên blockchain explorer
3. Bật Active workflow khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack để nhận thông báo tức thời
2. Thêm node lưu log các tài liệu đã kiểm tra
3. Tạo báo cáo định kỳ về tỷ lệ xác thực
4. Kết nối với hệ thống quản lý tài liệu hiện tại

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình xác minh tài liệu, nâng cao độ chính xác và giảm thiểu rủi ro gian lận. Bằng cách kết hợp công nghệ AI và blockchain, chúng ta có thể tạo ra hệ thống kiểm soát tài liệu đáng tin cậy, đáp ứng yêu cầu của các cơ quan quản lý và nâng cao hiệu quả hoạt động của doanh nghiệp.