---
title: "🚀 Tự động hóa kiểm tra thăng tiến học thuật với GPT-4o, quy tắc chính sách và Gmail"
description: "Giải pháp tự động hóa 100% không cần code giúp các sếp HR tiết kiệm 70% thời gian kiểm tra thăng tiến bằng cách kết hợp AI và quy tắc chính sách."
slug: "tu-dong-hoa-kiem-tra-thang-tien-hoc-vu"
tags: [n8n, automation, no-code, HR, AI]
keywords: [n8n workflow, tự động hóa, kiểm tra thăng tiến, AI, HR]
---

# 🚀 Tự động hóa kiểm tra thăng tiến học thuật với GPT-4o, quy tắc chính sách và Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp HR khi phải kiểm tra thủ công hàng trăm hồ sơ thăng tiến hàng năm. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code kết hợp AI và quy tắc chính sách.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm **70% thời gian** kiểm tra thủ công
- Đảm bảo **chính xác** trong việc áp dụng quy tắc chính sách
- **Tự động hóa hoàn toàn** quy trình phê duyệt
- **Giảm thiểu rủi ro** sai sót trong quá trình đánh giá
- **Tích hợp liền mạch** với hệ thống HR hiện tại
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI với API key (để sử dụng GPT-4o)
- Quyền truy cập dữ liệu hiệu suất từ hệ thống quản lý nhân sự
- Tài khoản Gmail với mật khẩu ứng dụng (để gửi email cảnh báo)
- Google Sheets (để lưu trữ dữ liệu phê duyệt và nhật ký kiểm toán)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13432](https://n8n.io/workflows/13432)
2. Nhấn nút "Import" trên trang workflow
3. Trong n8n Editor, chọn "Import from URL" và dán link trên
4. Hoặc tải file JSON về máy và import từ file

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Schedule Trigger"**:
   - Cấu hình lịch trình phù hợp với chu kỳ đánh giá của tổ chức (hàng quý/hàng năm)

2. **Node "Workflow Configuration"**:
   - Cập nhật các tham số cấu hình chung như:
     - Thời gian chờ cho quá trình đánh giá
     - Ngưỡng quyết định phê duyệt/loại bỏ

3. **Node "Fetch Performance Data"**:
   - Cấu hình endpoint API để lấy dữ liệu hiệu suất từ hệ thống HR

4. **Node "Fetch Policy Rules"**:
   - Cập nhật endpoint API để lấy quy tắc chính sách hiện hành

5. **Các node OpenAI Model**:
   - Đảm bảo đã tạo credentials "openAiApi" trong n8n
   - Xác minh model "gpt-4o" có sẵn trong tài khoản OpenAI

6. **Node "Route by Decision"**:
   - Cấu hình logic phân luồng cho các trường hợp:
     - Phê duyệt tự động
     - Cần xem xét lại
     - Từ chối

7. **Node "Wait for HR Review"**:
   - Cấu hình thời gian chờ phù hợp cho quá trình xem xét lại

8. **Node "Send HR Escalation Email"**:
   - Cấu hình thông tin email gửi đi:
     - Địa chỉ email người nhận
     - Tiêu đề email
     - Nội dung email mẫu

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra toàn bộ quy trình
2. Kiểm tra các node quan trọng để đảm bảo dữ liệu được xử lý đúng
3. Bật chế độ Active cho workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Teams**: Thêm node để gửi thông báo qua các nền tảng này thay vì email
2. **Lưu log chi tiết**: Thêm node để ghi lại toàn bộ quá trình đánh giá vào Google Sheets
3. **Tự động báo cáo**: Thiết lập gửi báo cáo định kỳ về các trường hợp phê duyệt/từ chối
4. **Tích hợp với hệ thống đánh giá 360 độ**: Kết nối với dữ liệu đánh giá từ các đồng nghiệp

### 📌 Kết luận
Workflow này mang lại giải pháp toàn diện cho việc tự động hóa kiểm tra thăng tiến học thuật, giúp các sếp HR tiết kiệm thời gian và đảm bảo tính công bằng trong quá trình đánh giá. Hãy áp dụng ngay để nâng cao hiệu quả quản lý nhân sự của tổ chức!