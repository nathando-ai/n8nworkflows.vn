---
title: "🔥 Tự động hóa chia sẻ liên kết xem trước có thời hạn với UploadToURL, SendGrid và Google Sheets"
description: "Giải pháp an toàn cho các cơ quan truyền thông: Tạo liên kết xem trước tự hủy sau thời gian chỉ định, theo dõi hoạt động và gửi thông báo tự động."
slug: "chia-se-lien-ket-xem-truoc-co-thoi-han"
tags: [n8n, automation, no-code, file-management, email-marketing]
keywords: [n8n workflow, tự động hóa, quản lý file, email marketing, liên kết xem trước]
---

# 🔥 Tự động hóa chia sẻ liên kết xem trước có thời hạn với UploadToURL, SendGrid và Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các cơ quan truyền thông khi chia sẻ bản nháp quan trọng qua email thông thường. Giới thiệu workflow như giải pháp toàn diện giúp quản lý an toàn các liên kết xem trước.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo mật cao hơn**: Liên kết xem trước tự hủy sau thời gian chỉ định
- **Theo dõi hoạt động**: Ghi lại tất cả các liên kết đã chia sẻ trong Google Sheets
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công sau khi cài đặt
- **Thông báo tự động**: Gửi email thông báo khi liên kết hết hạn
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản UploadToURL (để lưu trữ file)
- Tài khoản SendGrid (để gửi email)
- Tài khoản Google (để truy cập Google Sheets)
- Biết cách tạo và quản lý API keys cho các dịch vụ trên
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13634](https://n8n.io/workflows/13634)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "Import" để hoàn tất quá trình

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Webhook - Create Burner Link**:
   - Đảm bảo đường dẫn "burner-link" là duy nhất và không bị trùng lặp
   - Kiểm tra phương thức HTTP là POST

2. **Upload to URL - Remote** và **Upload to URL - Binary**:
   - Cấu hình credentials "uploadToUrlApi" với API key của bạn
   - Đảm bảo operation được đặt là "uploadFile"

3. **Sheets - Log Active Link** và **Sheets - Mark Link Expired**:
   - Cấu hình credentials "googleSheetsOAuth2Api" với thông tin xác thực Google của bạn
   - Đặt operation là "append" cho node ghi log và "update" cho node cập nhật trạng thái

4. **SendGrid - Send Preview Email**, **SendGrid - Notify Client Expired** và **SendGrid - Agency Summary Email**:
   - Cấu hình credentials "sendGridApi" với API key của bạn
   - Kiểm tra các trường email (to, from, subject) để đảm bảo chúng được điền đúng

5. **Wait - Until Link Expires**:
   - Đặt thời gian chờ phù hợp với nhu cầu của bạn (mặc định là 24 giờ)

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Activate" ở góc trên bên phải
2. Test workflow bằng cách gửi một yêu cầu POST đến webhook của bạn với payload mẫu:
```json
{
  "email": "client@example.com",
  "expiryHours": 24,
  "fileUrl": "https://example.com/file.pdf",
  "projectName": "Project XYZ"
}
```
3. Kiểm tra email và Google Sheets để đảm bảo workflow hoạt động đúng

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack/Teams**: Thêm node để gửi thông báo đến các kênh chat khi liên kết hết hạn
2. **Lưu log chi tiết hơn**: Thêm các trường thông tin bổ sung vào Google Sheets như IP người truy cập, thời gian truy cập
3. **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo hàng tuần về các liên kết đã chia sẻ
4. **Xử lý lỗi nâng cao**: Thêm các node xử lý lỗi để gửi thông báo khi có vấn đề xảy ra trong workflow

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc chia sẻ liên kết xem trước có thời hạn một cách an toàn và tự động. Với khả năng theo dõi, thông báo tự động và bảo mật cao, nó là công cụ lý tưởng cho các cơ quan truyền thông muốn quản lý các bản nháp quan trọng một cách hiệu quả. Hãy thử ngay và nâng cao trải nghiệm chia sẻ file của bạn!