---
title: "🚀 Tự động hóa tạo video Sora AI từ Google Sheets và lưu trữ vào Google Drive"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động đọc prompt từ Google Sheets, tạo video bằng Sora AI, tối ưu tiêu đề SEO và lưu trữ kết quả lên Google Drive."
slug: "tu-dong-hoa-tao-video-sora-ai-tu-google-sheets-va-google-drive"
tags: [n8n, automation, sora-ai, openai, google-sheets, google-drive, video-generation]
keywords: [n8n workflow, tạo video sora ai, google sheets automation, openai sora api, tự động hóa n8n]
---

# 🚀 Tự động hóa tạo video Sora AI từ Google Sheets và lưu trữ vào Google Drive

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thủ công copy từng đoạn prompt, gửi yêu cầu tạo video, chờ đợi render rồi tải về máy và upload lên Google Drive chưa? Quá trình này không chỉ tốn hàng giờ đồng hồ mà còn dễ xảy ra sai sót khi xử lý số lượng lớn video.

Giải pháp ở đây là gì? Workflow n8n này sẽ tự động hóa **100%** quy trình từ A-Z: đọc prompt từ Google Sheets, gọi API tạo video bằng mô hình Sora mạnh mẽ của OpenAI, tự động kiểm tra trạng thái render, tối ưu tiêu đề chuẩn SEO bằng GPT-4, sau đó lưu video hoàn thiện thẳng lên Google Drive và cập nhật ngược lại trạng thái vào Google Sheets. Không cần code, chỉ cần cấu hình một lần và để hệ thống tự chạy!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Tự động hóa toàn bộ chuỗi tác vụ từ tạo video đến lưu trữ mà không cần can thiệp thủ công.
- **Xử lý hàng loạt mượt mà:** Đọc danh sách prompt từ Google Sheets và xử lý các video chưa được render.
- **Thông minh hóa nội dung:** Tự động tạo tiêu đề chuẩn SEO cho từng video nhờ trợ lý AI GPT-4.
- **Đồng bộ dữ liệu hai chiều:** Cập nhật trạng thái thành công/thất bại và đường dẫn video trực tiếp vào bảng tính để dễ dàng theo dõi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản OpenAI** (Yêu cầu API Key có quyền truy cập Sora API).
- **Tài khoản Google** (Google Sheets & Google Drive để kết nối OAuth2).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy đoạn mã JSON và paste trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Chuẩn bị Google Sheets:** Tạo một bảng tính Google Sheets với các cột bắt buộc: 
  `PROMPT`, `DURATION (In Seconds)`, `VIDEO RESOLUTION`, `VIDEO TITLE`, `VIDEO URL`, `STATUS`.
- **Get Video Prompts from Sheet, Update video status to failed, Add video URL and update video status:** Kết nối tài khoản Google Sheets thông qua `googleSheetsOAuth2Api` và điền chính xác **Sheet ID** của các sếp vào từng node này.
- **GPT-4 Model & Generate SEO Title with AI:** Kết nối `openAiApi` credentials và đảm bảo model được chọn là `gpt-4.1-mini` (hoặc phiên bản phù hợp).
- **Create Sora Video Job, Check Video Status, Download Completed Video:** Cấu hình các HTTP Request nodes để gọi API Sora của OpenAI, đính kèm API Key xác thực.
- **Wait 60s for Rendering:** Node này giúp chờ đợi quá trình render video hoàn tất trước khi kiểm tra lại trạng thái.
- **Upload to Google Drive:** Kết nối tài khoản Google Drive bằng `googleDriveOAuth2Api` để chọn thư mục lưu trữ video đầu ra.
- **Filter Unprocessed Videos & Route by Video Status:** Kiểm tra các điều kiện lọc prompt chưa xử lý và phân nhánh luồng khi video thành công hay thất bại.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** thông qua **Manual Trigger** để test chạy thử với một vài dòng dữ liệu mẫu trong Google Sheets.
- Sau khi kiểm tra mọi thứ chạy ngon lành, hãy bật nút **Active** để workflow tự động làm việc.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack vào nhánh thành công/thất bại để nhận thông báo ngay khi video được render xong.
- **Lên lịch chạy định kỳ:** Thay thế *Manual Trigger* bằng *Schedule Trigger* để hệ thống tự động quét Google Sheets và tạo video hàng ngày/hàng tuần.
- **Quản lý lỗi thông minh:** Tận dụng nhánh *Update video status to failed* để ghi log chi tiết lý do lỗi, giúp dễ dàng debug khi prompt quá dài hoặc không hợp lệ.

### 📌 Kết luận
Tự động hóa việc tạo video với Sora AI và Google Sheets chưa bao giờ dễ dàng đến thế. Hãy triển khai ngay workflow này để tối ưu hóa quy trình sáng tạo nội dung video cho doanh nghiệp của các sếp ngay hôm nay!