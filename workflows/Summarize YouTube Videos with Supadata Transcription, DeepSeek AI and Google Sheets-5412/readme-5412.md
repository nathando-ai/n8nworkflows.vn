---
title: "🎬 Tự động hóa tóm tắt video YouTube với DeepSeek AI và Google Sheets"
description: "Hướng dẫn tự động hóa quy trình tóm tắt video YouTube bằng công cụ AI DeepSeek và lưu kết quả vào Google Sheets - tiết kiệm thời gian và nâng cao hiệu quả làm việc"
slug: "tu-dong-hoa-tom-tat-video-youtube-deepseek-google-sheets"
tags: [n8n, automation, no-code, AI, Google Sheets]
keywords: [n8n workflow, tự động hóa, tóm tắt video, DeepSeek AI, Google Sheets]
---

# 🎬 Tự động hóa tóm tắt video YouTube với DeepSeek AI và Google Sheets

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải xem hàng loạt video YouTube dài để tìm thông tin quan trọng? Với workflow này, các sếp có thể tự động hóa quy trình tóm tắt nội dung video chỉ trong vài bước đơn giản, giúp tiết kiệm thời gian quý giá và tập trung vào những thông tin thực sự quan trọng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xem video: Tự động tóm tắt nội dung video dài thành đoạn văn bản ngắn gọn
- Lưu trữ thông tin quan trọng: Tự động lưu transcript và summary vào Google Sheets
- Tăng cường hiệu quả làm việc: Tập trung vào những thông tin thực sự quan trọng thay vì phải xem toàn bộ video
- Hỗ trợ nghiên cứu: Tạo ra cơ sở dữ liệu nội dung video có cấu trúc dễ quản lý
- Tích hợp với các công cụ khác: Kết nối dễ dàng với các công cụ khác trong hệ sinh thái n8n
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets
- API Key từ DeepSeek AI (có thể đăng ký miễn phí tại [deepseek.com](https://deepseek.com))
- URL của video YouTube cần tóm tắt
- Google Sheets đã được tạo sẵn với cấu trúc phù hợp (bao gồm các cột cho URL, transcript và summary)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Nhấn vào nút "Import from URL" trên thanh công cụ
3. Dán link sau vào ô nhập liệu: `https://n8n.io/workflows/5412`
4. Nhấn "Import" để hoàn tất quá trình import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "When clicking ‘Execute workflow’" (manualTrigger)**:
   - Không cần cấu hình gì thêm

2. **Node "DeepSeek Chat Model" (lmChatDeepSeek)**:
   - Chọn credentials "deepSeekApi" đã được thiết lập trước đó
   - Đảm bảo tài khoản DeepSeek có đủ credit để thực hiện các yêu cầu

3. **Node "Generate Summary" (chainLlm)**:
   - Không cần cấu hình gì thêm

4. **Node "Adding Summary to file" (googleSheets)**:
   - Chọn credentials "googleSheetsOAuth2Api" đã được thiết lập
   - Chọn operation là "update"
   - Điền Sheet ID và tên Sheet cần cập nhật
   - Đảm bảo cấu trúc Sheet có cột "Summary" để lưu kết quả

5. **Node "Adding transcript to file" (googleSheets)**:
   - Chọn credentials "googleSheetsOAuth2Api" đã được thiết lập
   - Chọn operation là "update"
   - Điền Sheet ID và tên Sheet cần cập nhật
   - Đảm bảo cấu trúc Sheet có cột "Transcript" để lưu kết quả

6. **Node "Get URL to Transcript" (googleSheets)**:
   - Chọn credentials "googleSheetsOAuth2Api" đã được thiết lập
   - Điền Sheet ID và tên Sheet chứa URL video
   - Đảm bảo cấu trúc Sheet có cột "URL" chứa URL video YouTube

7. **Node "Generating transcript" (httpRequest)**:
   - Không cần cấu hình gì thêm

8. **Node "Clear code" (code)**:
   - Không cần cấu hình gì thêm

#### 3. Kích hoạt ⚡️
1. Sau khi đã cấu hình tất cả các node, nhấn vào nút "Execute workflow" để kiểm tra quá trình chạy
2. Kiểm tra kết quả trong Google Sheets để đảm bảo transcript và summary đã được lưu đúng cách
3. Nếu mọi thứ hoạt động tốt, nhấn vào nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tự động hóa định kỳ**: Thiết lập workflow chạy tự động theo lịch trình để cập nhật nội dung mới từ các video YouTube yêu thích
2. **Kết hợp với Slack/Teams**: Thêm node gửi thông báo qua Slack hoặc Microsoft Teams khi có nội dung mới được tóm tắt
3. **Phân tích cảm xúc**: Sử dụng các công cụ phân tích cảm xúc để đánh giá tone của nội dung video
4. **Tạo báo cáo định kỳ**: Tạo báo cáo tổng hợp nội dung từ nhiều video trong một khoảng thời gian nhất định

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện để tự động hóa quy trình tóm tắt video YouTube, giúp các sếp tiết kiệm thời gian và tập trung vào những thông tin quan trọng nhất. Với việc tích hợp DeepSeek AI và Google Sheets, các sếp có thể dễ dàng quản lý và truy xuất nội dung video một cách hiệu quả. Hãy thử ngay và trải nghiệm cách làm việc thông minh hơn với n8n!