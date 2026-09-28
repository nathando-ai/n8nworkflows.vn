---
title: "🚀 Tự động tạo video bằng AI với mô hình Google Veo 3 Fast qua Replicate API trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tạo video chất lượng cao từ văn bản (Text-to-Video) sử dụng mô hình Google Veo 3 Fast thông qua Replicate API."
slug: "tu-dong-tao-video-ai-google-veo-3-fast-replicate-n8n"
tags: [n8n, automation, ai-video, replicate, google-veo, content-creation]
keywords: [n8n workflow, tao video ai, google veo 3 fast, replicate api, tu dong hoa content, text to video]
---

# 🚀 Tự động tạo video bằng AI với Google Veo 3 Fast Model qua Replicate API

Các sếp có đang tốn quá nhiều thời gian và công sức để thuê animator hoặc tự mày mò dựng video thủ công cho các chiến dịch marketing, mạng xã hội không? Việc sản xuất video ngắn (Reels, TikTok, Shorts) liên tục đòi hỏi nguồn lực lớn nhưng đôi khi kết quả lại không như ý.

Đừng lo, giải pháp ở đây rồi! Bài viết này sẽ hướng dẫn các sếp cách thiết lập một workflow n8n tự động hóa toàn bộ quy trình tạo video từ văn bản (Text-to-Video) sử dụng mô hình **Google Veo 3 Fast** cực kỳ mạnh mẽ thông qua **Replicate API**. Chỉ cần nhập câu lệnh (prompt), hệ thống sẽ tự động tạo video cho các sếp mà không cần đụng tay chân!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chuyển đổi ý tưởng dạng văn bản thành video hoàn chỉnh mà không cần thao tác thủ công trên giao diện web.
- **Tiết kiệm chi phí & thời gian:** Tận dụng tốc độ xử lý của mô hình Google Veo 3 Fast để sản xuất hàng loạt video chỉ trong vài phút.
- **Dễ dàng tích hợp:** Có thể kết hợp workflow này với Telegram, Google Sheets hoặc Slack để tự động tạo video khi có yêu cầu mới.
- **Quy trình thông minh:** Workflow tự động gửi yêu cầu, kiểm tra trạng thái render và trả về kết quả video khi hoàn tất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản trên **Replicate** và **Replicate API Token** hợp lệ.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ thư viện chính thức của n8n (Link gốc: [n8n Workflow #7101](https://n8n.io/workflows/7101)) và chọn **Import from File** hoặc copy trực tiếp mã JSON vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 8 nodes chính được bố trí logic để xử lý quá trình gọi API bất đồng bộ (gửi yêu cầu -> chờ xử lý -> kiểm tra trạng thái -> nhận kết quả):

1. **On clicking 'execute' (`manualTrigger`):** Điểm khởi chạy thủ công để test. Các sếp có thể thay thế bằng Webhook hoặc Google Sheets Trigger nếu muốn tự động hóa hoàn toàn.
2. **Set API Key (`set`):** Nơi các sếp cấu hình Replicate API Key của mình. Hãy tạo một biến chứa API Key hoặc điền trực tiếp token để các node HTTP Request phía sau có thể xác thực.
3. **Create Prediction (`httpRequest`):** Node này gửi prompt của các sếp tới endpoint API của mô hình `google/veo-3-fast` trên Replicate. Hãy đảm bảo truyền đúng định dạng JSON body bao gồm prompt video.
4. **Extract Prediction ID (`code`):** Sử dụng Javascript để bóc tách `prediction_id` từ phản hồi của Replicate, phục vụ cho bước kiểm tra trạng thái tiếp theo.
5. **Wait (`wait`):** Do việc render video mất một khoảng thời gian ngắn, node này tạm dừng workflow một vài giây trước khi gọi kiểm tra trạng thái để tránh làm nghẽn API.
6. **Check Prediction Status (`httpRequest`):** Gửi yêu cầu kiểm tra tiến độ render của video dựa trên `prediction_id` đã lấy ở bước trước.
7. **Check If Complete (`if`):** Kiểm tra xem video đã render xong chưa (`status === "succeeded"`). Nếu chưa, workflow có thể được cấu hình vòng lặp quay lại bước Wait; nếu rồi, chuyển sang bước xử lý kết quả.
8. **Process Result (`code`):** Node code cuối cùng để trích xuất đường dẫn URL tải video hoàn thiện từ dữ liệu trả về của Replicate.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với một prompt mẫu (ví dụ: *"A cinematic drone shot of a futuristic city at sunset"*).
- Theo dõi quá trình chạy qua các node và kiểm tra kết quả video đầu ra ở node cuối cùng.
- Sau khi test thành công, bật nút **Active** để đưa workflow vào trạng thái sẵn sàng hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Google Sheets:** Thay vì dùng Trigger thủ công, hãy kết nối Google Sheets để đọc danh sách prompt theo hàng, giúp tạo hàng loạt video tự động.
- **Nhận kết quả qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để bot tự động gửi video hoàn thành thẳng về chat cho các sếp.
- **Lưu trữ tự động:** Thêm node HTTP Request tải video về và đẩy trực tiếp lên Google Drive hoặc Cloudinary để lưu trữ lâu dài.

### 📌 Kết luận
Việc tích hợp AI Video Generation vào hệ thống tự động hóa n8n chưa bao giờ dễ dàng đến thế với mô hình Google Veo 3 Fast. Hãy áp dụng ngay để tối ưu hóa quy trình sản xuất nội dung hình ảnh cho doanh nghiệp của các sếp ngay hôm nay!