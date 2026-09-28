---
title: "🚑 Tự động hóa Triage Bệnh nhân cấp cứu với GPT-4.1 và Hệ thống Bệnh viện"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình triage bệnh nhân cấp cứu bằng n8n, kết hợp AI và hệ thống bệnh viện. Tiết kiệm 60% thời gian xử lý, đảm bảo đánh giá chuẩn theo quy trình."
slug: "tu-dong-hoa-triage-benh-nhan-cap-cuu-voi-gpt-4-1"
tags: [n8n, automation, no-code, ai, hospital-management]
keywords: [n8n workflow, tự động hóa y tế, triage bệnh nhân, gpt-4.1, hệ thống bệnh viện]
---

# 🚑 Tự động hóa Triage Bệnh nhân cấp cứu với GPT-4.1 và Hệ thống Bệnh viện

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các bệnh viện khi xử lý hàng nghìn bệnh nhân cấp cứu mỗi ngày. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code kết hợp AI và hệ thống bệnh viện.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm **60% thời gian xử lý** bệnh nhân cấp cứu
- Đảm bảo đánh giá chuẩn theo quy trình y tế
- Tự động hóa quy trình từ tiếp nhận đến phân loại ưu tiên
- Ghi log toàn bộ quá trình để tuân thủ quy định
- Tích hợp liền mạch với hệ thống bệnh viện hiện tại
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI API (để truy cập mô hình GPT-4.1)
- Quyền truy cập API hệ thống bệnh viện (để đặt lịch hẹn và gửi thông báo)
- Cơ sở dữ liệu PostgreSQL để lưu trữ lịch sử tương tác
- Các quy trình y tế chuẩn để cấu hình mô hình AI
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/12986](https://n8n.io/workflows/12986)
2. Click vào nút "Import" trên trang workflow
3. Trong n8n Editor, chọn "Import from URL" và dán link trên
4. Hoặc tải file JSON về máy và chọn "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Patient Chat Interface**: Cấu hình giao diện chat cho bệnh nhân (có thể sử dụng Slack, Telegram hoặc webhook tùy chỉnh)
- **OpenAI Chat Model**:
  - Thêm credentials OpenAI API
  - Chọn model "gpt-4.1-mini" trong dropdown
- **Hospital Triage Agent**:
  - Cấu hình prompt theo quy trình y tế của bệnh viện
  - Định nghĩa các loại bệnh cần ưu tiên
- **Execute Appointment Action**:
  - Cấu hình endpoint API của hệ thống đặt lịch hẹn
  - Thiết lập các tham số yêu cầu (patient ID, department, priority...)
- **Send Notification**:
  - Cấu hình endpoint API của hệ thống thông báo
  - Thiết lập các tham số thông báo (recipient, message template...)
- **Log Interaction to Audit DB**:
  - Cấu hình kết nối PostgreSQL
  - Tạo bảng để lưu trữ lịch sử tương tác
- **Check Patient Eligibility** và **Retrieve Patient History**:
  - Viết các truy vấn SQL phù hợp với cơ sở dữ liệu bệnh viện
- **Calculate Priority Score** và **Validate Business Rules**:
  - Chỉnh sửa logic code theo quy trình ưu tiên của bệnh viện

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra toàn bộ luồng
2. Kiểm tra các thông báo và lịch hẹn được tạo
3. Xác nhận dữ liệu được ghi log vào cơ sở dữ liệu
4. Bật Active workflow khi đã sẵn sàng sản xuất

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để tạo kênh hỗ trợ 24/7 cho bệnh nhân
- Thêm node để gửi báo cáo hàng ngày về số lượng bệnh nhân được xử lý
- Tích hợp với hệ thống quản lý bệnh nhân (EHR) để cập nhật thông tin
- Thêm node để xử lý các trường hợp không chắc chắn (confidence < threshold)
- Tối ưu hóa prompt cho các tình huống đặc biệt (trẻ em, người cao tuổi...)

### 📌 Kết luận
Workflow này mang lại giải pháp toàn diện cho các bệnh viện cần tự động hóa quy trình triage bệnh nhân cấp cứu. Bằng cách kết hợp sức mạnh của AI với hệ thống bệnh viện hiện tại, các sếp có thể giảm tải công việc cho nhân viên y tế, đảm bảo đánh giá chuẩn theo quy trình và cải thiện trải nghiệm cho bệnh nhân. Hãy triển khai ngay để thấy sự khác biệt trong hiệu quả và hiệu suất của phòng khám cấp cứu!