---
title: "💊 Tự động hóa theo dõi tuân thủ thuốc bằng Google Sheets, OpenAI và Slack"
description: "Hướng dẫn chi tiết cách tự động nhắc nhở bệnh nhân uống thuốc, phân tích phản hồi bằng AI và cảnh báo bác sĩ khi có trường hợp nguy cấp"
slug: "tu-dong-hoa-theo-doi-tuan-thu-thuoc-google-sheets-openai-slack"
tags: [n8n, automation, no-code, google-sheets, openai, slack, healthcare]
keywords: [n8n workflow, tự động hóa y tế, theo dõi thuốc, AI phân tích phản hồi, cảnh báo bệnh nhân]
---

# 💊 Tự động hóa theo dõi tuân thủ thuốc bằng Google Sheets, OpenAI và Slack

[Đoạn mở đầu: Phân tích nỗi đau thực tế của bệnh viện/phòng khám khi theo dõi thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 50% thời gian theo dõi thủ công
- Phân tích tự động phản hồi bệnh nhân bằng AI
- Cảnh báo ngay khi có trường hợp nguy cấp
- Tự động cập nhật hồ sơ bệnh nhân
- Tăng cường tuân thủ thuốc thông qua nhắc nhở cá nhân hóa
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (để sử dụng Google Sheets)
- Tài khoản Slack (để gửi nhắc nhở và cảnh báo)
- API Key từ OpenAI (để phân tích phản hồi bệnh nhân)
- Dữ liệu bệnh nhân trong Google Sheets với các cột: Tên, Số điện thoại, Thời gian nhắc nhở, Số lần bỏ qua, Trạng thái nguy cấp
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/14860](https://n8n.io/workflows/14860)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "Import" để hoàn tất

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Trigger: Check Reminder Schedule**
   - Cấu hình lịch trình kiểm tra (ví dụ: mỗi 15 phút)
   - Đặt thời gian bắt đầu và kết thúc cho workflow

2. **Fetch Patient Records**
   - Chọn Google Sheets credentials đã cấu hình
   - Nhập ID của Google Sheet chứa dữ liệu bệnh nhân
   - Chỉ định tên sheet chứa dữ liệu (ví dụ: "Patients")

3. **Match Reminder Time**
   - Cấu hình điều kiện so sánh thời gian hiện tại với thời gian nhắc nhở trong dữ liệu
   - Sử dụng biểu thức: `{{$node["Fetch Patient Records"].json["Reminder Time"]}}`

4. **Send Medicine Reminder**
   - Cấu hình Slack credentials
   - Nhập channel ID hoặc tên channel để gửi nhắc nhở
   - Tùy chỉnh nội dung nhắc nhở với các biến từ dữ liệu bệnh nhân

5. **Receive Patient Response**
   - Đặt đường dẫn webhook (ví dụ: `/patient-reply`)
   - Chọn phương thức HTTP là POST
   - Lưu ý: Sau khi import, bạn cần cấu hình webhook endpoint trong Slack

6. **AI Response Classification**
   - Cấu hình OpenAI credentials
   - Chọn model "gpt-4-turbo" (hoặc model khác nếu có)
   - Tùy chỉnh prompt để phân loại phản hồi bệnh nhân thành các loại: Đã uống, Bỏ qua, Trễ, Không rõ

7. **Parse & Normalize AI Output**
   - Kiểm tra và điều chỉnh code JavaScript để chuyển đổi đầu ra AI thành định dạng JSON chuẩn
   - Đảm bảo các trường dữ liệu cần thiết được trích xuất đúng cách

8. **Load Patient Data**
   - Cấu hình tương tự như node "Fetch Patient Records"
   - Đảm bảo sử dụng cùng một Google Sheet để tránh sự cố

9. **Match Patient by Phone**
   - Cấu hình điều kiện so sánh số điện thoại từ phản hồi với dữ liệu bệnh nhân
   - Sử dụng biểu thức: `{{$node["Receive Patient Response"].json["phone"]}}`

10. **Update Missed Count**
    - Kiểm tra và điều chỉnh code để cập nhật số lần bỏ qua thuốc
    - Đảm bảo logic tăng số lần bỏ qua khi cần thiết

11. **Check Critical Condition**
    - Cấu hình điều kiện để xác định trường hợp nguy cấp
    - Có thể dựa trên số lần bỏ qua hoặc đầu ra từ AI

12. **Update Critical Status**
    - Cấu hình Google Sheets credentials
    - Chỉ định các cột cần cập nhật (ví dụ: "Critical Status")
    - Đảm bảo sử dụng đúng ID hàng để cập nhật

13. **Update Patient Record**
    - Cấu hình tương tự như node "Update Critical Status"
    - Cập nhật các thông tin khác như số lần bỏ qua, trạng thái uống thuốc

14. **Route Based on Response**
    - Cấu hình các trường hợp chuyển hướng dựa trên phân loại phản hồi
    - Đảm bảo tất cả các trường hợp được xử lý đúng cách

15. **Notify Missed Dose**
    - Cấu hình Slack credentials
    - Tùy chỉnh nội dung cảnh báo cho trường hợp bỏ qua thuốc

16. **Reminder for Later**
    - Cấu hình Slack credentials
    - Tùy chỉnh nội dung nhắc nhở cho trường hợp cần nhắc lại sau

17. **Acknowledge Compliance**
    - Cấu hình Slack credentials
    - Tùy chỉnh nội dung xác nhận cho trường hợp bệnh nhân đã uống thuốc

18. **Alert Doctor (Critical Case)**
    - Cấu hình Slack credentials
    - Chọn channel hoặc người nhận cảnh báo nguy cấp
    - Tùy chỉnh nội dung cảnh báo chi tiết

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình tất cả các node, thực hiện test run với dữ liệu mẫu
2. Kiểm tra các phản hồi từ Slack và Google Sheets để đảm bảo workflow hoạt động đúng
3. Khi đã kiểm tra xong, bật Active workflow để chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để gửi báo cáo hàng ngày về tình trạng tuân thủ thuốc cho quản lý
- Kết hợp với Telegram để gửi nhắc nhở bổ sung cho bệnh nhân
- Thêm tính năng lưu log các hoạt động quan trọng vào Google Sheets
- Tích hợp với hệ thống quản lý bệnh viện để cập nhật thông tin tự động
- Thêm tính năng gửi email nhắc nhở cho bệnh nhân không có tài khoản Slack

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc theo dõi tuân thủ thuốc, kết hợp sức mạnh của Google Sheets, OpenAI và Slack để tạo ra hệ thống tự động hóa hiệu quả. Với việc triển khai workflow này, các sếp có thể giảm thiểu công việc thủ công, tăng cường tuân thủ thuốc và đảm bảo chăm sóc sức khỏe tốt hơn cho bệnh nhân. Hãy áp dụng ngay để nâng cao hiệu quả quản lý bệnh viện của mình!