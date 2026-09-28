---
title: "🎥 Tự động hóa YouTube: Tóm tắt video và lưu vào Obsidian qua Dropbox"
description: "Workflow n8n tự động hóa việc tóm tắt video YouTube, tạo ghi chú Obsidian và lưu vào Dropbox - tiết kiệm 80% thời gian xử lý nội dung"
slug: "tu-dong-hoa-youtube-tom-tat-video-luu-obsidian-qua-dropbox"
tags: [n8n, automation, no-code, obsidian, youtube, dropbox]
keywords: [n8n workflow, tự động hóa nội dung, tóm tắt video, obsidian, dropbox]
---

# 🎥 Tự động hóa YouTube: Tóm tắt video và lưu vào Obsidian qua Dropbox

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải tóm tắt video YouTube thủ công cho Obsidian. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian xử lý nội dung
- Tự động tạo ghi chú Obsidian chuẩn từ video YouTube
- Lưu trữ an toàn trên Dropbox với cấu trúc file rõ ràng
- Hoạt động liên tục theo lịch trình đã cài đặt
- Tóm tắt chính xác nhờ sử dụng mô hình AI tiên tiến
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản YouTube API (với quyền truy cập vào playlist cần xử lý)
- Tài khoản OpenAI API (để sử dụng các node xử lý ngôn ngữ tự nhiên)
- Tài khoản Dropbox (để lưu trữ file ghi chú)
- Tài khoản Obsidian (để đồng bộ file từ Dropbox)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Run Workflow on Schedule** (scheduleTrigger):
   - Cấu hình thời gian chạy workflow (ví dụ: mỗi ngày lúc 8h sáng)
   - Chọn múi giờ phù hợp

2. **Get Playlist Videos** (youTube):
   - Cấu hình credentials YouTube API
   - Nhập ID của playlist cần xử lý
   - Chọn số lượng video tối đa cần xử lý mỗi lần chạy

3. **Get Video Details** (httpRequest):
   - Đảm bảo endpoint API YouTube đang hoạt động
   - Kiểm tra các tham số truyền vào (video ID)

4. **Get Video Transcript** (httpRequest):
   - Cấu hình endpoint API để lấy transcript (nếu có)
   - Xử lý trường hợp video không có transcript

5. **Clean Transcript** (code):
   - Kiểm tra và chỉnh sửa code xử lý transcript nếu cần
   - Đảm bảo output đúng định dạng

6. **Summarize Video** (openAi):
   - Cấu hình credentials OpenAI API
   - Tối ưu prompt để tạo tóm tắt chất lượng cao
   - Điều chỉnh độ dài tóm tắt theo nhu cầu

7. **Create Frontmatter** (openAi):
   - Tối ưu prompt để tạo frontmatter Obsidian chuẩn
   - Đảm bảo các trường thông tin quan trọng được bao gồm

8. **Create Links** (openAi):
   - Tối ưu prompt để tạo các liên kết hữu ích
   - Kiểm tra định dạng output

9. **Assemble Note** (set):
   - Kiểm tra cấu trúc của ghi chú cuối cùng
   - Đảm bảo tất cả các phần (tóm tắt, frontmatter, links) được kết hợp đúng cách

10. **Create File** (convertToFile):
    - Kiểm tra định dạng file đầu ra (markdown)
    - Đảm bảo tên file chứa thông tin video (ID hoặc tiêu đề)

11. **Save Note to Dropbox** (dropbox):
    - Cấu hình credentials Dropbox
    - Chọn thư mục lưu trữ trên Dropbox
    - Kiểm tra quyền truy cập và dung lượng còn lại

12. **Remove from Source Playlist** (youTube):
    - Cấu hình credentials YouTube API
    - Chọn hành động cần thực hiện (xóa hoặc di chuyển video)
    - Kiểm tra quyền hạn của tài khoản API

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu với 1-2 video.
- Kiểm tra file ghi chú được tạo trên Dropbox.
- Đồng bộ với Obsidian và kiểm tra định dạng.
- Bật Active workflow sau khi đã kiểm tra kỹ.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow hoàn thành
- Lưu log hoạt động vào Google Sheets để theo dõi hiệu suất
- Tạo báo cáo định kỳ về số lượng video đã xử lý và thời gian trung bình
- Tích hợp với Notion để tạo database từ các ghi chú Obsidian
- Sử dụng node "Email" để gửi báo cáo hàng tuần

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm hàng giờ mỗi ngày trong việc xử lý nội dung từ YouTube. Bằng cách tự động hóa toàn bộ quy trình từ tóm tắt đến lưu trữ, các sếp có thể tập trung vào những nhiệm vụ quan trọng hơn. Hãy thử ngay và trải nghiệm sự thay đổi đáng kể trong hiệu suất làm việc của mình!