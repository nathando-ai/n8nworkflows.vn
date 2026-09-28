---
title: "🚀 Tự động hóa tạo video B-roll đỉnh cao từ video gốc bằng AI Veo và n8n"
description: "Hướng dẫn cài đặt workflow n8n giúp phân tích video gốc, chọn khoảnh khắc vàng bằng AI và tự động tạo các đoạn B-roll chuyên nghiệp."
slug: "tao-video-b-roll-ai-veo-n8n"
tags: [n8n, automation, ai-video, veomodel, openai, telegram, google-cloud-storage]
keywords: [n8n workflow, tạo b-roll bằng ai, veomodel n8n, tự động hóa video, openai n8n]
---

# 🚀 Tự động hóa tạo video B-roll đỉnh cao từ video gốc bằng AI Veo và n8n

Việc sản xuất video ngắn, video quảng cáo hay nội dung TikTok/Reels thường đòi hỏi rất nhiều thời gian để cắt ghép và tìm kiếm các phân cảnh B-roll minh họa (phân cảnh phụ chèn vào video chính). Nếu làm thủ công, các sếp sẽ mất hàng giờ để xem lại video, chọn khoảnh khắc và tạo dựng nội dung bổ trợ. 

Workflow n8n tuyệt vời này từ tác giả **Koulikas Giannis (Coreflow Automation)** sẽ giải quyết triệt để bài toán đó bằng cách kết hợp sức mạnh của **OpenAI**, **Google Cloud Storage** và **Veo Video API**, tự động hóa 100% quy trình từ việc phân tích video gốc, chọn khoảnh khắc đắt giá cho đến khi xuất xưởng những thước phim B-roll cực xịn xò và thông báo qua Telegram!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Không cần can thiệp thủ công từ khâu phân tích video đến tạo B-roll.
- **AI thông minh:** Sử dụng OpenAI để chọn ra các "khoảnh khắc vàng" đáng giá nhất từ video gốc để chuyển hóa thành B-roll.
- **Lưu trữ chuyên nghiệp:** Tự động đẩy file video thành phẩm lên Google Cloud Storage (GCS) an toàn, dễ quản lý.
- **Cập nhật tức thì:** Nhận thông báo trực tiếp qua Telegram ngay khi video B-roll được xử lý xong.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n instance** (phiên bản Cloud hoặc Self-hosted).
- Tài khoản và **API Key OpenAI** (cho các node `Select Key Moments with AI` và `AI B-Roll Selector`).
- Tài khoản **Google Cloud Platform (GCP)** với dịch vụ Google Cloud Storage để lưu trữ video.
- Thông tin xác thực **Google Cloud Service Account** (JWT, OAuth) để gọi các API phân tích/tạo video.
- **Telegram Bot Token** và Chat ID để nhận thông báo kết quả.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã nguồn JSON của workflow từ n8n template (hoặc file JSON được cung cấp), sau đó paste trực tiếp vào giao diện n8n Editor của mình thông qua tính năng Import từ Clipboard.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:
- **Set API Credentials**: Điền các thông tin xác thực API cần thiết cho hệ thống AI và dịch vụ tạo video của các sếp.
- **Generate JWT Token** & **Request OAuth Token**: Cấu hình thông tin kết nối Google Cloud Service Account của các sếp để cấp quyền gọi API.
- **Set Video URL**: Dán đường dẫn (`video URL`) của video gốc mà các sếp muốn phân tích và tạo B-roll.
- **Select Key Moments with AI** & **AI B-Roll Selector**: Kết nối credential OpenAI và kiểm tra lại System Prompt để đảm bảo AI hiểu đúng phong cách B-roll các sếp muốn hướng tới.
- **Upload File to GCS**: Cấu hình kết nối Google Cloud Storage (Bucket Name, Folder) để lưu trữ các video B-roll được tạo ra.
- **Send Telegram Message**: Điền Telegram Bot Token và Chat ID của các sếp để nhận link video hoàn thiện.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** tại node `Manual Trigger` để test chạy thử với video mẫu đầu tiên.
- Kiểm tra kỹ luồng dữ liệu đi qua các node `Split Moments into Items`, `Batch Process Items` và `Route Based on Status`.
- Sau khi test thành công không báo lỗi, hãy bật công tắc **Active** góc trên cùng bên phải để workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ gửi Telegram, các sếp có thể nối thêm node Slack hoặc Discord để gửi video B-roll vào nhóm chung cho team content cùng kiểm duyệt.
- **Lưu trữ dữ liệu:** Kết nối thêm Google Sheets hoặc Airtable để lưu lại lịch sử các video gốc đã tạo B-roll và đường dẫn file trên GCS nhằm dễ dàng tra cứu về sau.
- **Tối ưu batch:** Điều chỉnh thông số ở node `Batch Process Items` nếu các sếp xử lý các video có thời lượng quá dài để tránh vượt quá giới hạn thời gian chạy của server (timeout).

### 📌 Kết luận
Workflow "Generate AI B-roll clips from videos with Veo 3" là một "vũ khí bí mật" giúp các nhà sáng tạo nội dung và agency tối ưu hóa gấp nhiều lần tốc độ sản xuất video. Hãy cài đặt ngay hôm nay để giải phóng sức lao động và để AI làm thay những công việc nặng nhọc nhất!