---
title: "🎤 Tự động hóa ghi chú cuộc gọi GoHighLevel với AI - Transcribe & Summarize"
description: "Hướng dẫn tự động hóa ghi chú cuộc gọi GoHighLevel bằng AI Whisper và GPT, tiết kiệm thời gian và nâng cao hiệu quả làm việc"
slug: "tu-dong-hoa-ghi-chu-cuoc-goi-go-highlevel-voi-ai"
tags: [n8n, automation, no-code, crm, ai]
keywords: [n8n workflow, tự động hóa, ghi chú cuộc gọi, GoHighLevel, AI transcribe]
---

# 🎤 Tự động hóa ghi chú cuộc gọi GoHighLevel với AI - Transcribe & Summarize

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp trong ngành bất động sản hay các doanh nghiệp dịch vụ thường phải đối mặt với tình trạng ghi chú cuộc gọi thủ công, tốn thời gian và dễ bị lỗi. Với workflow này, chúng ta sẽ tự động hóa toàn bộ quy trình từ ghi âm cuộc gọi đến tạo ghi chú tóm tắt trong CRM GoHighLevel, giúp tiết kiệm thời gian và nâng cao hiệu quả làm việc.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian ghi chú thủ công
- Tự động hóa toàn bộ quy trình từ ghi âm đến ghi chú
- Tăng tính chính xác và nhất quán trong ghi chú
- Tích hợp liền mạch với CRM GoHighLevel
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản GoHighLevel với quyền truy cập API
- API key từ OpenAI (hoặc các dịch vụ AI khác)
- Tài khoản n8n đã được cài đặt và cấu hình
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của bạn, các sếp làm theo các bước sau:

1. Truy cập vào trang workflow gốc: [Transcribe & Summarize GoHighLevel Call Recordings](https://n8n.io/workflows/10255)
2. Nhấp vào nút "Import" ở góc trên bên phải
3. Trong n8n Editor, chọn "Import from URL" và dán link workflow
4. Hoặc tải file JSON về máy và chọn "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Call Ended" (Webhook)**:
   - Cần thay đổi URL webhook thành endpoint của n8n của bạn
   - Đảm bảo phương thức HTTP là POST

2. **Node "GHL Get Audio", "GHL Get Conversation ID", "GHL Get Message ID" (HTTP Request)**:
   - Cần cấu hình credentials cho GoHighLevel
   - Điền đúng API key và userId từ tài khoản GoHighLevel

3. **Node "Transcribe a recording" (OpenAI)**:
   - Cần cấu hình credentials cho OpenAI
   - Đảm bảo API key có quyền truy cập vào dịch vụ Whisper

4. **Node "Message a model" (OpenAI)**:
   - Cần cấu hình credentials cho OpenAI
   - Có thể điều chỉnh prompt để phù hợp với nhu cầu ghi chú

5. **Node "Add note to contact" (HTTP Request)**:
   - Cần cấu hình credentials cho GoHighLevel
   - Đảm bảo cấu trúc JSON đầu ra phù hợp với API của GoHighLevel

#### 3. Kích hoạt ⚡️
Sau khi cấu hình xong các node quan trọng, các sếp cần thực hiện các bước sau:

1. Test run dữ liệu mẫu:
   - Gửi một cuộc gọi thử nghiệm qua GoHighLevel
   - Kiểm tra xem workflow có bắt được webhook không
   - Xác nhận ghi âm được tải xuống và chuyển đổi thành văn bản thành công
   - Kiểm tra ghi chú được thêm vào liên hệ trong GoHighLevel

2. Bật Active workflow:
   - Sau khi test thành công, chuyển workflow sang trạng thái Active
   - Đảm bảo workflow chạy ổn định trong 24 giờ trước khi sử dụng thực tế

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack/Telegram**:
   - Thêm node gửi thông báo qua Slack/Telegram khi có cuộc gọi mới
   - Cảnh báo khi có lỗi trong quá trình xử lý

2. **Lưu log hoạt động**:
   - Thêm node ghi log các cuộc gọi xử lý
   - Lưu trữ lịch sử xử lý để kiểm tra sau này

3. **Gửi báo cáo định kỳ**:
   - Thêm node tổng hợp báo cáo hàng tuần/tháng về các cuộc gọi quan trọng
   - Gửi báo cáo tự động qua email hoặc Slack

4. **Tùy chỉnh prompt AI**:
   - Điều chỉnh prompt để phù hợp với ngành nghề của bạn
   - Ví dụ: "Tóm tắt cuộc gọi bán bất động sản" thay vì "Tóm tắt cuộc gọi chung"

### 📌 Kết luận
Workflow này là giải pháp hoàn hảo cho các sếp muốn tự động hóa quy trình ghi chú cuộc gọi trong GoHighLevel. Bằng cách tích hợp AI Whisper và GPT, chúng ta có thể chuyển đổi ghi âm cuộc gọi thành văn bản và tóm tắt nội dung một cách nhanh chóng và chính xác. Hãy áp dụng ngay workflow này để tiết kiệm thời gian và nâng cao hiệu quả làm việc của đội ngũ!