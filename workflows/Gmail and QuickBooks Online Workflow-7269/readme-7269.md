---
title: "🚀 Tự động hóa chuyển tiếp hóa đơn từ Gmail sang QuickBooks Online với n8n"
description: "Giải pháp tự động hóa 100% giúp quét hóa đơn, biên lai từ Gmail và chuyển tiếp trực tiếp vào QuickBooks Online một cách chính xác, loại bỏ hoàn toàn việc nhập liệu thủ công."
slug: "tu-dong-hoa-gmail-va-quickbooks-online-n8n"
tags: [n8n, automation, no-code, gmail, quickbooks, invoice-processing]
keywords: [n8n workflow, tự động hóa hóa đơn, gmail to quickbooks, qbo automation, xu ly hoa don n8n]
---

# 🚀 Tự động hóa chuyển tiếp hóa đơn từ Gmail và QuickBooks Online

Các sếp có đang mệt mỏi vì phải thủ công tải từng biên lai mua hàng, hóa đơn điện tử từ email lên QuickBooks Online (QBO)? Hay các quy tắc chuyển tiếp email (forwarding rules) mặc định quá cứng nhắc và kém tin cậy? 

Workflow n8n này sinh ra để giải quyết triệt để nỗi đau đó. Hệ thống sẽ tự động bắt các email biên lai, chuyển tiếp trực tiếp vào QBO, đồng thời quản lý nhãn (label) thông minh để tránh trùng lặp mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Tự động hóa 100% quy trình đưa biên lai vào phần mềm kế toán.
- **Không bỏ sót chứng từ:** Kết hợp giữa sự kiện thời gian thực (real-time trigger) và lịch chạy định kỳ (failsafe) đảm bảo không bao giờ lọt email.
- **Chống trùng lặp thông minh:** Tự động gỡ nhãn cũ và đánh dấu "Processed" sau khi xử lý thành công.
- **Vượt qua giới hạn:** Dễ dàng chuyển tiếp cả email của người khác vào QBO mà không vướng các giới hạn chia sẻ thông thường.
:::

### 📦 Các Use Cases thực tế
- Hóa đơn mua hàng online và thanh toán dịch vụ định kỳ (Subscriptions).
- Xác nhận chuyển khoản ngân hàng, E-transfer.
- Hóa đơn (Bills & Invoices) nhận từ nhà cung cấp.
- Báo cáo chi phí (Expense reports) từ nhân viên hoặc đối tác.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Gmail** đã được cấu hình OAuth2 Credentials trong n8n.
- **Tài khoản QuickBooks Online (QBO)** đã bật tính năng nhận hóa đơn qua email (Receipt Forwarding Email Address, ví dụ: `example@qbdocs.com`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n template (ID: 7269) và import trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node sau trong workflow:

- **New Email Receipt Received (`gmailTrigger`)**: 
  - Chọn `Credential` Gmail của các sếp.
  - Cấu hình điều kiện lọc email (ví dụ: tìm các email có nhãn "New E-Transfer" hoặc chứa tiêu đề phù hợp).
- **Every Day at 8 AM (`scheduleTrigger`)**: 
  - Node này đóng vai trò chạy dự phòng (failsafe) định kỳ hàng ngày để quét lại các email có thể bị bỏ lỡ.
- **Get New Receipt from Email (`gmail` - getAll)**: 
  - Kết nối credential và chọn đúng nhãn (label) chứa các hóa đơn mới cần xử lý.
- **Forward the Receipt to QBO (`gmail`)**: 
  - **CỰC KỲ QUAN TRỌNG**: Nhập địa chỉ email nhận biên lai QuickBooks Online của các sếp vào đây (Ví dụ: `your_company@qbdocs.com`). Node này sẽ thực hiện thao tác forward chính xác nội dung email sang QBO.
- **Remove the Old Label & Add the "Processed" Label (`gmail`)**: 
  - Cấu hình các thao tác gỡ nhãn "New Receipt" và thêm nhãn "Processed" để hệ thống đánh dấu email đã hoàn tất xử lý, tránh gửi trùng lặp sang QBO.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test step/Execute workflow) với một email mẫu để kiểm tra xem email đã được forward thành công sang QBO chưa.
- Bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng đính kèm:** Tùy chỉnh node Gmail để tự động tải xuống và xử lý các file PDF/hình ảnh đính kèm nếu nhà cung cấp gửi hóa đơn dạng file.
- **Phân loại thông minh:** Tạo nhiều workflow riêng biệt cho từng loại chi phí, hoặc thêm tên nhà cung cấp vào tiêu đề email để giúp QBO tự động hạch toán chính xác hơn.
- **Cảnh báo lỗi:** Thêm các node thông báo qua Telegram hoặc Slack vào nhánh lỗi (Error Trigger) để nắm bắt ngay lập tức nếu kết nối Gmail/QBO gặp sự cố.

### 📌 Kết luận
Việc tự động hóa quy trình chuyển tiếp hóa đơn từ Gmail sang QuickBooks Online sẽ giúp bộ phận kế toán giải phóng hàng giờ nhập liệu thủ công mỗi tuần, đảm bảo số liệu tài chính luôn minh bạch và cập nhật theo thời gian thực. Hãy áp dụng ngay vào hệ thống của các sếp nhé!