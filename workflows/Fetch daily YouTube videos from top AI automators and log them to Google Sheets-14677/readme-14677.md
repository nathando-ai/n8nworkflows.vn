---
title: "🚀 Tự Động Cào Video YouTube Hàng Ngày Từ Các Kênh AI Automation & Lưu Vào Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động quét video mới từ các chuyên gia AI hàng đầu trên YouTube, lọc trùng lặp và lưu trữ vào Google Sheets mỗi ngày."
slug: "tu-dong-cao-video-youtube-ai-automation-google-sheets"
tags: [n8n, automation, youtube, google-sheets, market-research]
keywords: [n8n workflow, tự động hóa youtube, cào video youtube, google sheets automation, nghiên cứu thị trường ai]
---

# 🚀 Tự Động Cào Video YouTube Hàng Ngày Từ Các Kênh AI Automation & Lưu Vào Google Sheets

Các sếp có đang tốn hàng giờ mỗi tuần để vào thủ công các kênh YouTube của các chuyên gia AI hàng đầu nhằm cập nhật xu hướng, video mới hay ý tưởng content không? Việc này vừa nhàm chán, tốn thời gian lại rất dễ bỏ lỡ thông tin quan trọng.

Đừng lo, workflow n8n được thiết kế bởi **Koulikas Giannis** (Founder & CEO của Coreflow Automation) sẽ giúp các sếp tự động hóa 100% quy trình này. Hệ thống sẽ tự động quét video mới từ danh sách các kênh AI Automation nổi tiếng, lọc bỏ các video đã tồn tại và lưu trữ gọn gàng vào Google Sheets mỗi ngày.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Không cần thủ công kiểm tra từng kênh YouTube nữa, mọi thứ diễn ra hoàn toàn tự động.
- **Nghiên cứu thị trường nhanh chóng:** Tổng hợp toàn bộ video mới nhất từ Nate Herk, Nick Saraev, Cole Medin... vào một bảng Google Sheets duy nhất.
- **Thông tin sạch, không trùng lặp:** Cơ chế kiểm tra thông minh giúp loại bỏ hoàn toàn các video đã được ghi nhận trước đó.
- **Hoạt động 24/7:** Chạy ngầm theo lịch trình định sẵn, sẵn sàng báo cáo dữ liệu bất cứ lúc nào các sếp cần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Sheets Credentials:** Tài khoản Google kết nối với n8n để đọc và ghi dữ liệu.
- **YouTube API Credentials:** Khóa API hoặc tài khoản kết nối YouTube để n8n gọi dữ liệu kênh.
- **Google Sheet mẫu:** Chuẩn bị sẵn một Google Sheet để lưu trữ danh sách video (gồm các cột ID video, tiêu đề, kênh, ngày đăng...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc copy toàn bộ JSON và paste trực tiếp vào màn hình n8n).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các node quan trọng sau đây để workflow hoạt động mượt mà:

- **Scheduled Daily Trigger:** Cấu hình mốc thời gian chạy tự động mỗi ngày (ví dụ: 8:00 sáng hàng ngày).
- **Các node lấy dữ liệu YouTube (Fetch Nate Herk Videos, Fetch Nick Saraev Videos, v.v.):** 
  - Chọn tài khoản kết nối YouTube (Credentials).
  - Cấu hình ID kênh hoặc từ khóa tương ứng của từng chuyên gia AI (Nate Herk, Cole Medin, Jack Roberts, Ed Hill, v.v.) tại phần tham số của node `resource: video`.
- **Read Rows in Sheets & Append Rows to Sheets:** 
  - Kết nối tài khoản Google Sheets.
  - Trỏ đúng đến file Google Sheet và Sheet Name mà các sếp dùng để lưu trữ dữ liệu video.
- **Execute Custom Code & Process Merged Data:** Kiểm tra nhanh các đoạn mã JavaScript có sẵn trong node `code` để đảm bảo định dạng trường dữ liệu (video ID, title, URL) khớp với cấu trúc bảng Google Sheets của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm lần đầu (Test run) và kiểm tra dữ liệu trả về từ YouTube xem đã đổ vào Google Sheets chuẩn chỉnh chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm một node Telegram hoặc Slack ngay sau bước `Append Rows to Sheets` để bắn thông báo mỗi khi có video AI mới xuất hiện, giúp các sếp cập nhật tin tức "nóng hổi" ngay lập tức.
- **Tóm tắt nội dung bằng AI:** Kết hợp thêm OpenAI/Claude node để tự động đọc tiêu đề/transcript của video và tóm tắt ý chính trước khi lưu vào Google Sheets.
- **Chia nhóm kênh:** Tách các kênh YouTube thành nhiều luồng theo chủ đề (Ví dụ: No-code Automation, LLM Development, AI Marketing) để quản lý dữ liệu chuyên sâu hơn.

### 📌 Kết luận
Workflow tự động cào video YouTube này là công cụ đắc lực cho các nhà sáng tạo nội dung, marketer và các nhà phát triển muốn nghiên cứu đối thủ hoặc cập nhật xu hướng AI automation mỗi ngày. Hãy triển khai ngay hôm nay để tối ưu hóa thời gian nghiên cứu thị trường của các sếp!