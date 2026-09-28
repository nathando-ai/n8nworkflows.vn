---
title: "🎬 Tự động hóa tạo video giới thiệu cá nhân từ CV bằng AI (HeyGen + GPT)"
description: "Hướng dẫn tự động hóa quy trình chuyển đổi CV thành video giới thiệu cá nhân chuyên nghiệp bằng công nghệ AI, tiết kiệm 90% thời gian tuyển dụng"
slug: "tu-dong-hoa-tao-video-gioi-thieu-tu-cv-bang-ai"
tags: [n8n, automation, no-code, AI, HR, video-marketing]
keywords: [n8n workflow, tự động hóa tuyển dụng, video giới thiệu, AI tạo nội dung, HR automation]
---

# 🎬 Tự động hóa tạo video giới thiệu cá nhân từ CV bằng AI (HeyGen + GPT)

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 90% thời gian tuyển dụng bằng video tự động
- Tạo video giới thiệu cá nhân chuyên nghiệp từ CV trong 30 giây
- Tự động phân loại giới tính để chọn giọng nói phù hợp
- Lưu trữ video và thông tin ứng viên trong Google Sheets
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI API (cho mô hình GPT)
- Tài khoản HeyGen API (để tạo video)
- Tài khoản Google Sheets (để lưu trữ kết quả)
- Tài khoản n8n (đã cài đặt các credentials trên)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/6608)
2. Click vào nút "Import" ở góc trên bên phải
3. Copy toàn bộ JSON workflow và dán vào n8n Editor của bạn

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Upload Resume & Photo" (formTrigger)**
   - Cấu hình form để người dùng upload CV (PDF) và ảnh đại diện
   - Đảm bảo form có các trường: "Resume File", "Photo File"

2. **Node "OpenAI Chat Model" (lmChatOpenAi)**
   - Chọn credentials OpenAI API của bạn
   - Đảm bảo model được chọn là "gpt-4o-mini" (hoặc phiên bản mới nhất)

3. **Node "Avatar upload" (httpRequest)**
   - Cấu hình endpoint API của HeyGen để upload ảnh đại diện
   - Thêm header "Authorization" với API key của HeyGen

4. **Node "Generate Script & Find Gender" (openAi)**
   - Chọn credentials OpenAI API của bạn
   - Đảm bảo prompt được cấu hình để trích xuất thông tin từ CV và xác định giới tính

5. **Node "Append video" (googleSheets)**
   - Chọn credentials Google Sheets OAuth2 của bạn
   - Cấu hình Spreadsheet ID (có thể lấy từ [sample sheet](https://docs.google.com/spreadsheets/d/1jQtu4ZREsMge8elB-6xJoOMDMKsJLqof2dDmh0sxqWk/edit?usp=sharing))
   - Điền tên sheet và phạm vi cột để lưu trữ kết quả

6. **Node "Generate Male Voice Video" và "Generate Female Voice Video" (httpRequest)**
   - Cấu hình endpoint API của HeyGen để tạo video
   - Thêm header "Authorization" với API key của HeyGen
   - Đảm bảo body request chứa các tham số cần thiết: script, avatar_id, voice_id

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Upload một CV mẫu và ảnh đại diện
   - Kiểm tra xem hệ thống có trích xuất thông tin đúng không
   - Xác nhận video được tạo và lưu vào Google Sheets

2. Bật Active workflow:
   - Chọn "Activate" trên thanh công cụ
   - Đảm bảo workflow chạy ổn định trước khi sử dụng với dữ liệu thực tế

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Teams để thông báo khi video hoàn thành
- Thêm node gửi email tự động với video đính kèm
- Tạo báo cáo định kỳ về số lượng video đã tạo
- Tích hợp với hệ thống CRM để quản lý ứng viên
- Thêm chức năng chỉnh sửa video trước khi xuất bản

### 📌 Kết luận
Workflow này giúp các sếp HR tiết kiệm thời gian đáng kể trong quá trình tuyển dụng bằng cách tự động hóa việc tạo video giới thiệu cá nhân từ CV. Với công nghệ AI tiên tiến, hệ thống này đảm bảo chất lượng cao và hiệu suất tối ưu. Hãy áp dụng ngay để nâng cao trải nghiệm tuyển dụng của doanh nghiệp!