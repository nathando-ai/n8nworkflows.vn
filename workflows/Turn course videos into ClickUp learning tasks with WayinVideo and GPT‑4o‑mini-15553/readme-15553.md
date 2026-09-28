---
title: "🎓 Tự động hóa học tập: Chuyển video khóa học thành danh sách nhiệm vụ ClickUp với WayinVideo và GPT-4o-mini"
description: "Hướng dẫn tự động hóa quy trình chuyển đổi video khóa học thành danh sách nhiệm vụ ClickUp bằng công nghệ AI, tiết kiệm thời gian và nâng cao hiệu quả học tập"
slug: "tu-dong-hoa-hoc-tap-video-khoa-hoc-clickup-wayinvideo-gpt4o"
tags: [n8n, automation, no-code, project management, ai summarization]
keywords: [n8n workflow, tự động hóa học tập, video khóa học, ClickUp, AI summarization]
---

# 🎓 Tự động hóa học tập: Chuyển video khóa học thành danh sách nhiệm vụ ClickUp với WayinVideo và GPT-4o-mini

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải xem hàng loạt video khóa học, sau đó phải tự tay tạo danh sách nhiệm vụ học tập trên ClickUp? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài phút, giúp tiết kiệm thời gian quý giá và nâng cao hiệu quả học tập.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa quy trình chuyển đổi video thành nhiệm vụ học tập
- **Chính xác cao**: Sử dụng công nghệ AI GPT-4o-mini để phân tích và tạo nhiệm vụ học tập chính xác
- **Quản lý hiệu quả**: Tất cả nhiệm vụ học tập được lưu trữ và quản lý trên ClickUp và Google Sheets
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công sau khi thiết lập
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản ClickUp với danh sách (list) đã tạo
- Tài khoản Google với Google Sheets đã tạo
- API Key từ WayinVideo
- API Key từ OpenAI
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15553](https://n8n.io/workflows/15553)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node 2. WayinVideo — Submit Summarization**:
   - Thay thế `YOUR_WAYINVIDEO_API_KEY` bằng API Key thực tế từ tài khoản WayinVideo của bạn
   - Đảm bảo API Key có quyền truy cập vào dịch vụ Summarization

2. **Node 4. WayinVideo — Get Summary Results**:
   - Thay thế `YOUR_WAYINVIDEO_API_KEY` bằng API Key thực tế từ tài khoản WayinVideo của bạn
   - Đảm bảo API Key có quyền truy cập vào dịch vụ Summarization

3. **Node 9. OpenAI — GPT-4o-mini Model**:
   - Kết nối với credential OpenAI của bạn
   - Đảm bảo tài khoản OpenAI có đủ credit để sử dụng mô hình GPT-4o-mini

4. **Node 11. ClickUp — Create Task**:
   - Kết nối với credential OAuth2 của ClickUp
   - Thay thế `YOUR_CLICKUP_LIST_ID` bằng ID thực tế của danh sách (list) trong ClickUp
   - Để lấy ID danh sách, các sếp có thể:
     1. Mở danh sách trong ClickUp
     2. Click chuột phải vào danh sách
     3. Chọn "Copy link"
     4. ID danh sách sẽ là phần cuối cùng của URL (ví dụ: `https://app.clickup.com/123456/v/l/abc123` → ID là `abc123`)

5. **Node 12. Google Sheets — Log Tasks**:
   - Kết nối với credential OAuth2 của Google Sheets
   - Thay thế `YOUR_GOOGLE_SHEET_ID` bằng ID thực tế của Google Sheet
   - Tạo một tab mới trong Google Sheet với tên "Course Tasks Log"
   - Thêm các cột sau: Course Title, Module Title, Video URL, Task Number, Task Title, Task Type, Estimated Minutes, Total Tasks in Module, ClickUp Task ID, ClickUp Task URL, Assigned To, Due Date, Priority, Generated On

#### 3. Kích hoạt ⚡️
1. Sau khi đã cấu hình tất cả các node, các sếp có thể test workflow bằng cách:
   - Click vào nút "Execute Workflow" ở góc trên bên phải
   - Hoặc gửi dữ liệu mẫu thông qua form để kiểm tra toàn bộ quy trình

2. Sau khi test thành công, các sếp có thể kích hoạt workflow bằng cách:
   - Click vào nút "Activate" ở góc trên bên phải
   - Chọn "Manual" hoặc "Schedule" tùy theo nhu cầu

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack/Teams**: Thêm node gửi thông báo đến Slack hoặc Teams khi có nhiệm vụ học tập mới được tạo
2. **Lưu log chi tiết**: Mở rộng Google Sheet để lưu trữ thêm thông tin như thời gian hoàn thành, đánh giá, v.v.
3. **Tự động nhắc nhở**: Thêm node gửi email hoặc thông báo nhắc nhở khi nhiệm vụ sắp đến hạn
4. **Phân tích hiệu suất**: Tạo báo cáo định kỳ về tiến độ học tập và hiệu suất của các nhiệm vụ

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình chuyển đổi video khóa học thành danh sách nhiệm vụ học tập trên ClickUp, tiết kiệm thời gian và nâng cao hiệu quả học tập. Với sự kết hợp của công nghệ AI và quản lý dự án, các sếp có thể tập trung vào việc học và phát triển kỹ năng một cách hiệu quả hơn. Hãy áp dụng ngay để trải nghiệm sự khác biệt!