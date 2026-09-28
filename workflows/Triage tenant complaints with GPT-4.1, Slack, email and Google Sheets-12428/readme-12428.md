---
title: "🚀 Tự động phân loại khiếu nại của người thuê nhà bằng AI, Slack, Email và Google Sheets"
description: "Hướng dẫn chi tiết cách tự động phân loại và xử lý khiếu nại của người thuê nhà bằng n8n, AI và các công cụ tích hợp phổ biến. Giảm thời gian xử lý, tăng hiệu quả và duy trì chất lượng dịch vụ."
slug: "tu-dong-phan-loai-khieu-nai-nguoi-thue-nha"
tags: [n8n, automation, no-code, ticket-management, ai-automation]
keywords: [n8n workflow, tự động hóa khiếu nại, xử lý khiếu nại, AI phân loại, quản lý khiếu nại]
---

# 🚀 Tự động phân loại khiếu nại của người thuê nhà bằng AI, Slack, Email và Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp quản lý tòa nhà khi phải xử lý hàng trăm khiếu nại hàng ngày. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp quản lý tòa nhà thường phải đối mặt với hàng trăm khiếu nại hàng ngày từ người thuê nhà. Từ việc ốm đau, hư hỏng thiết bị đến các vấn đề về dịch vụ, việc xử lý thủ công này không chỉ tốn thời gian mà còn dễ gây ra các trường hợp khiếu nại bị bỏ qua. Bằng cách tự động hóa quy trình này với n8n và công nghệ AI, các sếp có thể phân loại, xử lý và theo dõi các khiếu nại một cách hiệu quả hơn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động phân loại và xử lý khiếu nại trong vòng vài giây.
- **Chính xác cao**: Sử dụng AI để phân loại khiếu nại với độ chính xác cao.
- **Cá nhân hóa**: Tạo phản hồi và email xác nhận tự động dựa trên nội dung khiếu nại.
- **Hoạt động liên tục**: Workflow chạy 24/7 mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Slack để thông báo khiếu nại cấp cao.
- Tài khoản email để gửi email xác nhận.
- Tài khoản Google Sheets để lưu trữ và theo dõi các khiếu nại.
- API key từ OpenAI để sử dụng mô hình GPT-4.1.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/12428](https://n8n.io/workflows/12428).
3. Hoặc tải file JSON về và import từ máy tính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Tenant Complaint Webhook**:
   - Cấu hình path và HTTP method trong node "Tenant Complaint Webhook".
   - Ví dụ: Path: `tenant-complaint`, HTTP Method: `POST`.

2. **Workflow Configuration**:
   - Cấu hình các biến môi trường và tham số cần thiết trong node "Workflow Configuration".

3. **Normalize Complaint Data**:
   - Đảm bảo dữ liệu đầu vào từ webhook được chuẩn hóa đúng định dạng trong node "Normalize Complaint Data".

4. **AI Complaint Classifier**:
   - Cấu hình prompt và logic phân loại trong node "AI Complaint Classifier".
   - Ví dụ: Sử dụng mô hình GPT-4.1 để phân loại khiếu nại thành các mức độ ưu tiên (High, Medium, Low).

5. **OpenAI Chat Model**:
   - Thêm credentials cho OpenAI API trong node "OpenAI Chat Model".
   - Chọn mô hình `gpt-4.1-mini` trong danh sách mô hình.

6. **Route by Urgency**:
   - Cấu hình logic chuyển hướng trong node "Route by Urgency".
   - Ví dụ: Chuyển hướng khiếu nại cấp cao đến Slack, khiếu nại cấp trung bình tạo task, khiếu nại cấp thấp gửi email xác nhận.

7. **Notify Property Manager (High Priority)**:
   - Thêm credentials cho Slack trong node "Notify Property Manager (High Priority)".
   - Cấu hình kênh và thông báo cần thiết.

8. **AI Email Generator**:
   - Cấu hình prompt và logic tạo email trong node "AI Email Generator".
   - Ví dụ: Sử dụng mô hình GPT-4.1 để tạo email xác nhận tự động.

9. **OpenAI Chat Model for Email**:
   - Thêm credentials cho OpenAI API trong node "OpenAI Chat Model for Email".
   - Chọn mô hình `gpt-4.1-mini` trong danh sách mô hình.

10. **Send Acknowledgment Email**:
    - Thêm credentials cho email trong node "Send Acknowledgment Email".
    - Cấu hình địa chỉ email và nội dung cần thiết.

11. **Create Task Data (Medium Priority)**:
    - Cấu hình dữ liệu task trong node "Create Task Data (Medium Priority)".
    - Ví dụ: Tạo task với tiêu đề, mô tả và ngày hết hạn.

12. **Consolidate All Branches**:
    - Kết hợp dữ liệu từ các nhánh khác nhau trong node "Consolidate All Branches".

13. **Log to Google Sheets**:
    - Thêm credentials cho Google Sheets trong node "Log to Google Sheets".
    - Cấu hình Spreadsheet ID và tên sheet cần lưu trữ dữ liệu.

14. **AI Resolution Suggester**:
    - Cấu hình prompt và logic gợi ý giải pháp trong node "AI Resolution Suggester".
    - Ví dụ: Sử dụng mô hình GPT-4.1 để gợi ý giải pháp cho các khiếu nại.

15. **OpenAI Chat Model for Resolutions**:
    - Thêm credentials cho OpenAI API trong node "OpenAI Chat Model for Resolutions".
    - Chọn mô hình `gpt-4.1-mini` trong danh sách mô hình.

#### 3. Kích hoạt ⚡️
1. **Test run dữ liệu mẫu**:
   - Gửi một khiếu nại mẫu đến webhook để kiểm tra toàn bộ quy trình.
   - Kiểm tra các node để đảm bảo dữ liệu được xử lý đúng cách.

2. **Bật Active workflow**:
   - Sau khi kiểm tra và cấu hình xong, bật workflow để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack và Telegram**: Thêm các node để gửi thông báo đến Slack và Telegram cho các khiếu nại cấp cao.
- **Lưu log chi tiết**: Thêm các node để lưu trữ log chi tiết của các khiếu nại để theo dõi và phân tích.
- **Gửi báo cáo định kỳ**: Tạo các báo cáo định kỳ về các khiếu nại và gửi qua email hoặc Slack.
- **Tích hợp với các hệ thống quản lý task**: Kết nối với các hệ thống quản lý task như Trello, Asana để tạo task tự động.

### 📌 Kết luận
Workflow này giúp các sếp quản lý tòa nhà tự động phân loại và xử lý các khiếu nại của người thuê nhà một cách hiệu quả. Bằng cách sử dụng công nghệ AI và tự động hóa, các sếp có thể giảm thời gian xử lý, tăng độ chính xác và duy trì chất lượng dịch vụ. Hãy áp dụng ngay workflow này để nâng cao hiệu quả quản lý tòa nhà của bạn!