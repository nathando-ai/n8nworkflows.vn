---
title: "🚀 Tự động tạo Video AI từ Văn bản hoặc Hình ảnh với Veo3 API và VietVid trên n8n"
description: "Hướng dẫn chi tiết xây dựng workflow n8n tự động hóa quy trình tạo video AI chất lượng cao từ text hoặc hình ảnh sử dụng Veo3 API của VietVid, tiết kiệm chi phí và thời gian."
slug: "tao-video-ai-tu-van-ban-hoac-hinh-anh-veo3-vietvid-n8n"
tags: [n8n, automation, ai-video, content-creation, vietvid, veo3]
keywords: [n8n workflow, tạo video ai, text-to-video, veo3 api, vietvid automation, tự động hóa n8n]
---

# 🚀 Tự động tạo Video AI từ Văn bản hoặc Hình ảnh với Veo3 API và VietVid trên n8n

Việc sản xuất video thủ công cho các chiến dịch marketing, mạng xã hội hay giáo dục thường ngốn rất nhiều thời gian và chi phí. Với sự bùng nổ của AI, các sếp hoàn toàn có thể tự động hóa 100% quy trình này. Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ mạnh mẽ, cho phép tạo video AI chất lượng cao (hỗ trợ cả Text-to-Video và Image-to-Video) thông qua **VietVid.com Veo3 API** chỉ với một bảng điền thông tin (Form) đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Từ khâu nhập liệu qua Form đến khi nhận kết quả video hoàn chỉnh mà không cần thao tác thủ công.
- **Linh hoạt đa dạng đầu vào**: Hỗ trợ cả tạo video từ văn bản (Text-to-Video) hoặc kết hợp hình ảnh có sẵn (Image-to-Video).
- **Tiết kiệm chi phí**: Giá chỉ từ $0.4 cho mỗi clip 8 giây, gói credit không giới hạn thời gian sử dụng tại VietVid.
- **Tối ưu thời gian chờ**: Hệ thống tự động kiểm tra trạng thái (polling) ngầm định kỳ 10 giây cho đến khi video sẵn sàng trả về link tải 720p hoặc 1080p.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản và API Key tại [VietVid.com](https://vietvid.com/api) (dùng để xác thực các HTTP Request).
- Một chút ý tưởng prompt bằng tiếng Anh để AI hiểu và tạo video chính xác nhất.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo mới một workflow trống trong n8n, sau đó copy toàn bộ JSON của workflow hoặc sử dụng file template được cung cấp từ cộng đồng n8n (Workflow ID: 8213) để import trực tiếp vào trình soạn thảo n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 6 nodes chính hoạt động nhịp nhàng với nhau. Các sếp cần chú ý các điểm cấu hình sau:

- **Enter prompt infomation (`formTrigger`)**: Đây là điểm khởi đầu, tạo một giao diện Web Form để người dùng nhập các trường thông tin:
  - `prompt`: Mô tả ý tưởng video bằng tiếng Anh (ví dụ: *"A robot dancing under neon lights"*).
  - `imageUrl` (tùy chọn): Link ảnh JPG/PNG nếu muốn làm Image-to-Video, để trống nếu chỉ dùng Text-to-Video.
  - `aspectRatio`: Chọn tỷ lệ khung hình (16:9, 9:16, hoặc 1:1).
  - `seeds` (tùy chọn): Số ngẫu nhiên từ 10000–99999 để cố định kết quả.
  - `API Key`: Dán API Key lấy từ trang cá nhân VietVid.
- **Submit request (`httpRequest`)**: Gửi thông tin từ form lên hệ thống VietVid.
  - **Method**: `POST`
  - **URL**: `https://vietvid.com/api/n8n/generate`
  - **Headers**: `Authorization: Bearer {{ $json.api_key }}` và `Content-Type: application/json`
- **Wait for Video Processing (`wait`)**: Node tạm dừng 10 giây để chờ hệ thống AI xử lý video, tránh việc gọi liên tục gây quá tải API.
- **Check Video status (`httpRequest`)**: Gửi yêu cầu kiểm tra trạng thái xử lý video dựa trên `taskId` nhận được từ bước trước.
  - **Method**: `GET`
  - **URL**: `https://vietvid.com/api/n8n/video-status/{{ $json.taskId }}`
  - **Headers**: `Authorization: Bearer {{ $json.api_key }}`
- **Check video available (`if`)**: Kiểm tra xem trường `status` trả về đã là `"completed"` hay chưa. Nếu chưa (`processing`), vòng lặp sẽ quay lại node chờ (Wait) cho đến khi hoàn thành.
- **Return video link (`set`)**: Lưu trữ và hiển thị kết quả cuối cùng gồm link video chuẩn 720p (`videoUrl`) và bản HD 1080p (`hdVideoUrl` nếu có).

#### 3. Kích hoạt ⚡️
- Thực hiện chạy thử (Test execution) bằng cách mở form do n8n cung cấp, điền thử một prompt ngắn và API key của sếp.
- Kiểm tra kết quả trả về ở node cuối cùng.
- Bật công tắc **Active** để đưa workflow vào trạng thái vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Thay vì chỉ nhận kết quả trên n8n, các sếp có thể nối thêm node **Telegram** hoặc **Slack** để bot tự động bắn link video về group chat ngay khi render xong.
- **Lưu trữ tự động**: Thêm node **Google Sheets** hoặc **Airtable** để ghi lại lịch sử các prompt đã chạy kèm link video để tiện quản lý nội dung.
- **Tối ưu Prompt**: Thêm các từ khóa mô tả góc máy, phong cách nghệ thuật (cinematic, 3D animation, realistic) để chất lượng video đầu ra đạt mức cao nhất.

### 📌 Kết luận
Việc tích hợp Veo3 API của VietVid vào n8n mở ra một giải pháp sáng tạo nội dung vô cùng mạnh mẽ và tiết kiệm cho cá nhân lẫn doanh nghiệp. Hãy "lên đồ" ngay hôm nay để tự động hóa quy trình sản xuất video của các sếp!