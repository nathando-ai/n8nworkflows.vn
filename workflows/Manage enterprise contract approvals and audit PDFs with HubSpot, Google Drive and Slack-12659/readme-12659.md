---
title: "🚀 Tự động hóa quản lý hợp đồng doanh nghiệp: Phê duyệt, nén PDF & Đồng bộ HubSpot với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa toàn bộ quy trình duyệt hợp đồng doanh nghiệp, kiểm tra PDF, lưu trữ Google Drive và cập nhật HubSpot, Slack."
slug: "tu-dong-hoa-quan-ly-hop-dong-doanh-nghiep-hubspot-google-drive-slack"
tags: [n8n, automation, no-code, hubspot, google-drive, slack, document-extraction]
keywords: [n8n workflow, tự động hóa hợp đồng, hubspot deal update, google drive archive, slack finance alert, htmlcsstopdf]
---

# 🚀 Tự động hóa quy trình phê duyệt và lưu trữ hợp đồng doanh nghiệp với n8n

Việc quản lý và phê duyệt các hợp đồng doanh nghiệp (Enterprise Contracts) theo cách thủ công thường tốn rất nhiều thời gian: phải kiểm tra điều khoản phức tạp, xin chữ ký nhiều cấp, nén file PDF, lưu trữ lên Google Drive, cập nhật trạng thái trên HubSpot CRM và thông báo cho đội ngũ Tài chính/Pháp lý qua Slack. Chỉ cần một sai sót nhỏ, quy trình có thể bị đình trệ.

Giải pháp? Workflow n8n tự động hóa 100% này sẽ thay thế hoàn toàn các thao tác thủ công đó, giúp doanh nghiệp vận hành trơn tru, minh bạch và bảo mật tuyệt đối.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa luồng phê duyệt:** Xử lý logic phức tạp từ định tuyến hợp đồng đến kiểm tra kích thước file PDF.
- **Tối ưu hóa tài liệu:** Tự động nén file PDF hợp đồng để đáp ứng giới hạn dung lượng trước khi lưu trữ hoặc gửi đi.
- **Đồng bộ CRM thông minh:** Tự động cập nhật trạng thái Deal trên HubSpot khi hoàn tất quy trình.
- **Bảo mật và Minh bạch:** Lưu trữ Audit PDF trên Google Drive và gửi cảnh báo tức thì tới kênh Slack của phòng Tài chính.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **HubSpot CRM Account** (Cần API Token hoặc App Token để cập nhật Deal).
- **Google Drive Account** (Để lưu trữ file Audit PDF).
- **Slack Workspace** (Để gửi thông báo cho phòng Tài chính).
- **HTML/CSS to PDF API Credentials** (Dùng cho các node nén PDF).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 9 nodes chính thực hiện các nhiệm vụ từ xử lý logic, nén file đến đồng bộ dữ liệu. Các sếp cần chú ý cấu hình các node sau:

- **Các node Code (`Code: Approval Router`, `Code: Complexity Engine`, `Code: Size Validator`, `Code: Audit Metadata`):** Kiểm tra kỹ các đoạn mã JavaScript bên trong để đảm bảo logic tính toán điểm phức tạp (`Complexity Score`) và điều kiện phê duyệt khớp với chính sách của công ty.
- **Node `Compress PDF` & `Compress PDF1` (HTML/CSS to PDF):** Kết nối tài khoản `htmlcsstopdfApi` và thiết lập tham số nén PDF phù hợp với giới hạn dung lượng lưu trữ/gửi nhận.
- **Node `Drive: Archive Audit PDF` (Google Drive):** Chọn tài khoản Google Drive OAuth2 và chỉ định thư mục đích (`Folder ID`) dùng để lưu trữ file Audit PDF của hợp đồng.
- **Node `Update a deal` (HubSpot):** Kết nối bằng HubSpot App Token, cấu hình ánh xạ trường dữ liệu để tự động chuyển trạng thái Deal sang `'Executed'` (Đã thực thi) khi hợp đồng hoàn tất.
- **Node `Slack: Finance Alert` (Slack):** Kết nối Slack OAuth2 và cấu hình kênh (Channel) nhận thông báo tự động cho đội ngũ Tài chính/Pháp lý.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (`Test workflow`) với một bản ghi dữ liệu mẫu để kiểm tra toàn bộ luồng chạy từ xử lý code, nén PDF, lưu Drive đến cập nhật HubSpot và Slack.
- Sau khi kiểm tra dữ liệu trả về chính xác, gạt công tắc sang **Active** để workflow vận hành tự động 24/7.

### ✍️ Gợi ý nâng cao để tối ưu hóa
- **Tích hợp thêm Chatbot Telegram/Zalo:** Thay vì chỉ gửi thông báo qua Slack, các sếp có thể mở rộng nhánh thông báo sang Telegram để ban quản lý duyệt hợp đồng nhanh hơn trên điện thoại.
- **Lưu log vào Google Sheets/Airtable:** Tạo thêm một bảng ghi nhận lịch sử (Audit Trail) để dễ dàng tra cứu lại toàn bộ thông tin hợp đồng theo thời gian thực.
- **Cảnh báo lỗi tự động:** Thêm node Error Trigger để gửi email hoặc tin nhắn cảnh báo ngay lập tức cho đội ngũ kỹ thuật nếu có lỗi phát sinh trong quá trình nén PDF hoặc gọi API HubSpot.

### 📌 Kết luận
Workflow quản lý hợp đồng doanh nghiệp này là mảnh ghép hoàn hảo giúp tự động hóa toàn bộ quy trình từ kiểm duyệt, xử lý tài liệu đến đồng bộ CRM. Hãy triển khai ngay hôm nay để tối ưu hóa hiệu suất làm việc cho đội ngũ của các sếp!