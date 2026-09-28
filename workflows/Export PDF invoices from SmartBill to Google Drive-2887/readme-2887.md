---
title: "🚀 Tự động xuất hóa đơn PDF từ SmartBill lưu thẳng vào Google Drive bằng n8n"
description: "Hướng dẫn xây dựng workflow tự động tải file hóa đơn PDF từ hệ thống SmartBill và đồng bộ an toàn vào các thư mục tương ứng trên Google Drive."
slug: "tu-dong-xuat-hoa-don-pdf-smartbill-google-drive-n8n"
tags: [n8n, automation, no-code, finance, google-drive, smartbill, pdf]
keywords: [n8n workflow, tự động hóa tài chính, smartbill google drive, export hóa đơn pdf n8n]
---

# 🚀 Tự động xuất hóa đơn PDF từ SmartBill lưu thẳng vào Google Drive

Việc quản lý, tải xuống từng hóa đơn từ hệ thống SmartBill và phân loại thủ công lên Google Drive là nỗi đau đầu của bộ phận kế toán mỗi dịp cuối tháng. Công việc này vừa tốn thời gian, dễ xảy ra sai sót lại vừa nhàm chán. 

Giải pháp hoàn hảo cho các sếp đây! Workflow n8n này sẽ tự động hóa 100% quy trình: gọi API lấy hóa đơn PDF từ SmartBill, kiểm tra hoặc tự động tạo thư mục trên Google Drive, và lưu trữ gọn gàng file PDF mà không cần một thao tác tay nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 99% thời gian:** Không còn cảnh download thủ công hàng trăm hóa đơn.
- **Tổ chức khoa học:** Tự động tạo và phân loại thư mục lưu trữ trên Google Drive một cách bài bản.
- **Hoạt động bền bỉ:** Xử lý hàng loạt qua vòng lặp thông minh (Loop), đảm bảo không bị gián đoạn hay nghẽn mạng.
- **Độ chính xác tuyệt đối:** Giảm thiểu tối đa rủi ro thất lạc chứng từ kế toán.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Hệ thống **n8n** (Cloud hoặc Self-hosted).
- Tài khoản và thông tin API (API Keys/Credentials) của **SmartBill**.
- Tài khoản **Google Drive** đã được cấp quyền kết nối với n8n (OAuth2).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn hoặc sao chép trực tiếp, sau đó paste vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:
- **Smartbill get invoice pdf (`httpRequest`):** Cấu hình lại Endpoint API của SmartBill, thêm các headers xác thực (API Key, Token) để hệ thống có thể kéo được file PDF về.
- **SetData (`set`) & Set mime (`code`):** Kiểm tra lại định dạng dữ liệu đầu ra, đảm bảo file nhận được đúng chuẩn MIME type của file PDF (`application/pdf`).
- **Search Drive Folder & Create Drive Folder (`googleDrive`):** Kết nối tài khoản Google Drive của các sếp. Node này sẽ kiểm tra xem thư mục lưu trữ hóa đơn đã tồn tại chưa, nếu chưa sẽ tự động tạo mới dựa trên cấu hình ở node **Set Default Folder Name**.
- **Loop Over Items (`splitInBatches`) & Wait a sec (`wait`):** Giúp xử lý danh sách hóa đơn theo từng lô nhỏ kèm độ trễ cần thiết để tránh việc vượt quá giới hạn API (Rate Limit) của Google Drive và SmartBill.
- **Upload file to Google Drive (`googleDrive`):** Nốt cuối cùng đẩy file PDF vào đúng ID thư mục đã được xác định ở node **Set Folder ID**.

#### 3. Kích hoạt ⚡️
- Nhấn nút **"Execute Workflow"** với một vài dữ liệu mẫu để kiểm tra toàn bộ luồng chạy.
- Sau khi test thành công, bật trạng thái **Active** để workflow tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node Telegram hoặc Slack ở cuối luồng để gửi báo cáo tổng kết mỗi khi xuất hóa đơn thành công.
- **Lưu log Google Sheets:** Thêm một node Google Sheets để ghi lại lịch sử các hóa đơn đã xuất thành công kèm đường link dẫn trực tiếp đến file trên Drive.
- **Định kỳ tự động:** Thay vì chạy thủ công, các sếp có thể gắn thêm node Schedule Trigger để n8n tự động chạy gom hóa đơn vào cuối mỗi ngày hoặc cuối tháng.

### 📌 Kết luận
Với workflow tự động hóa này, công việc kiểm soát tài chính và lưu trữ hóa đơn của doanh nghiệp sẽ trở nên chuyên nghiệp và nhanh chóng hơn bao giờ hết. Hãy cài đặt ngay hôm nay để giải phóng thời gian cho đội ngũ kế toán của các sếp!