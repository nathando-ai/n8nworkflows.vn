---
title: "🎬 Tự động hóa chuyển đổi hình ảnh thành video AI và đăng lên YouTube/TikTok với MiniMax Hailuo 02"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình chuyển đổi hình ảnh thành video AI sử dụng MiniMax Hailuo 02 và đăng lên YouTube/TikTok hoàn toàn không cần code"
slug: "tu-dong-hoa-chuyen-doi-hinh-anh-thanh-video-ai-minimax-hailuo-02"
tags: [n8n, automation, no-code, AI, content-creation, social-media]
keywords: [n8n workflow, tự động hóa, video AI, MiniMax Hailuo 02, YouTube, TikTok]
---

# 🎬 Tự động hóa chuyển đổi hình ảnh thành video AI và đăng lên YouTube/TikTok với MiniMax Hailuo 02

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quy trình tạo video từ hình ảnh
- Tiết kiệm thời gian và công sức cho đội ngũ sáng tạo
- Tăng tốc độ xuất bản nội dung lên các nền tảng xã hội
- Tạo ra nội dung phong phú và đa dạng hơn
- Theo dõi và quản lý quá trình tạo video một cách hiệu quả
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive và Google Sheets
- API Key từ MiniMax Hailuo 02 (đăng ký tại [fal.ai](https://fal.ai/))
- API Key từ Upload-Post (đăng ký tại [Upload-Post](https://app.upload-post.com/))
- Tài khoản YouTube và TikTok
- Hình ảnh đầu vào và prompt mô tả cho video
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import" ở góc trên bên phải
3. Chọn file JSON chứa workflow hoặc copy/paste JSON vào editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "When clicking ‘Test workflow’" (manualTrigger)**:
   - Không cần cấu hình gì thêm

2. **Node "Get status" (httpRequest)**:
   - Cấu hình credentials "httpHeaderAuth"
   - Điền URL API của MiniMax Hailuo 02
   - Thêm header "Authorization" với giá trị "Key YOURAPIKEY"

3. **Node "Wait 60 sec." (wait)**:
   - Không cần cấu hình gì thêm

4. **Node "Schedule Trigger" (scheduleTrigger)**:
   - Cấu hình thời gian chạy workflow (khuyến nghị 5 phút/lần)

5. **Node "Completed?" (if)**:
   - Không cần cấu hình gì thêm

6. **Node "Update result" (googleSheets)**:
   - Cấu hình credentials "googleSheetsOAuth2Api"
   - Chọn Spreadsheet ID và Sheet Name chứa dữ liệu
   - Đảm bảo có cột "IMAGE", "PROMPT", "VIDEO", "YOUTUBE"

7. **Node "Set data" (set)**:
   - Không cần cấu hình gì thêm

8. **Node "Upload Video" (googleDrive)**:
   - Cấu hình credentials "googleDriveOAuth2Api"
   - Chọn thư mục lưu trữ video

9. **Node "Get Url Video" (httpRequest)**:
   - Cấu hình credentials "httpHeaderAuth"
   - Điền URL API để lấy URL video đã tạo

10. **Node "Generate title" (openAi)**:
    - Cấu hình credentials "openAiApi"
    - Điền prompt để tạo tiêu đề video

11. **Node "Get File Video" (httpRequest)**:
    - Không cần cấu hình gì thêm

12. **Node "Update Youtube URL" (googleSheets)**:
    - Cấu hình credentials "googleSheetsOAuth2Api"
    - Cập nhật URL video YouTube vào Google Sheet

13. **Node "Get new video" (googleSheets)**:
    - Cấu hình credentials "googleSheetsOAuth2Api"
    - Lấy dữ liệu mới từ Google Sheet

14. **Node "Create video" (httpRequest)**:
    - Cấu hình credentials "httpHeaderAuth"
    - Điền URL API của MiniMax Hailuo 02

15. **Node "Upload on Youtube" (httpRequest)**:
    - Cấu hình credentials "httpHeaderAuth"
    - Điền URL API của Upload-Post
    - Thêm header "Authorization" với giá trị "Apikey YOUR_API_KEY_HERE"

16. **Node "Upload on TikTok" (httpRequest)**:
    - Cấu hình credentials "httpHeaderAuth"
    - Điền URL API của Upload-Post
    - Thêm header "Authorization" với giá trị "Apikey YOUR_API_KEY_HERE"

#### 3. Kích hoạt ⚡️
1. Kiểm tra kết nối với tất cả các dịch vụ bên ngoài
2. Chạy test với dữ liệu mẫu
3. Kích hoạt workflow bằng cách nhấn nút "Active" trên mỗi node

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi thông báo qua Slack/Telegram khi workflow hoàn thành
- Tự động tạo thumbnail cho video từ hình ảnh đầu vào
- Thêm chức năng kiểm tra nội dung không phù hợp trước khi đăng lên
- Tích hợp với các công cụ phân tích dữ liệu để theo dõi hiệu suất video
- Tự động tạo phiên bản phụ đề cho video

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa quy trình tạo video từ hình ảnh và đăng lên các nền tảng xã hội. Bằng cách áp dụng workflow này, các sếp có thể tiết kiệm thời gian đáng kể, tạo ra nội dung chất lượng cao và duy trì sự hiện diện liên tục trên các nền tảng mạng xã hội. Hãy thử nghiệm và tối ưu hóa workflow theo nhu cầu cụ thể của doanh nghiệp để đạt được kết quả tốt nhất!