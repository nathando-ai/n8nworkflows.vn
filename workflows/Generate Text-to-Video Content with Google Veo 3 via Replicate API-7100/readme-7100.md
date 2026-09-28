---
title: "🚀 Tự động tạo video AI chất lượng cao từ văn bản với Google Veo 3 và Replicate qua n8n"
description: "Hướng dẫn chi tiết xây dựng workflow n8n tự động hóa quy trình tạo video từ prompt văn bản sử dụng mô hình Google Veo 3 thông qua Replicate API."
slug: "tao-video-ai-google-veo-3-replicate-n8n"
tags: [n8n, automation, ai-video, google-veo, replicate, content-creation]
keywords: [n8n workflow, google veo 3, replicate api, text to video, tao video ai tu dong]
---

# 🚀 Tự động tạo video AI chất lượng cao từ văn bản với Google Veo 3 và Replicate

Các sếp có đang gặp khó khăn trong việc sản xuất nội dung video hàng loạt cho TikTok, YouTube Shorts hay Reels? Việc thuê editor hoặc tự ngồi render video thủ công vừa tốn kém thời gian, chi phí lại khó đáp ứng nhu cầu đăng tải liên tục. 

Giải pháp là đây! Bài viết này sẽ hướng dẫn các sếp cách thiết lập một workflow n8n cực kỳ mạnh mẽ, tự động hóa 100% quy trình chuyển đổi văn bản (text prompt) thành những thước phim chuyên nghiệp nhờ mô hình **Google Veo 3** thông qua **Replicate API**. Không cần biết lập trình, chỉ mất vài phút cài đặt là các sếp đã có ngay một "phòng dựng phim AI" tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Biến các ý tưởng chữ viết thành video sống động chỉ với một cú click chuột hoặc kích hoạt tự động.
- **Tiết kiệm chi phí tối đa:** Không cần đầu tư phần cứng khủng hay thuê đội ngũ dựng phim đắt đỏ.
- **Quy trình thông minh:** Workflow tự động gửi yêu cầu, chờ đợi (polling) trạng thái render và trả về kết quả video hoàn chỉnh.
- **Mở rộng dễ dàng:** Dễ dàng kết nối thêm Google Sheets để nhận danh sách prompt hàng loạt hoặc tự động đăng video lên mạng xã hội.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Replicate Account:** Tài khoản tại [Replicate](https://replicate.com/) kèm theo **API Token** để gọi mô hình Google Veo 3.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn cấp hoặc tạo một workflow mới trên n8n, sau đó copy toàn bộ cấu trúc JSON và paste trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 8 nodes hoạt động tuần tự. Các sếp cần chú ý cấu hình các điểm sau:

- **Node `Set API Key`**: Điền Replicate API Token của các sếp vào biến cấu hình để xác thực các yêu cầu gọi API tiếp theo.
- **Node `Create Prediction` (HTTP Request)**: 
  - Phương thức: `POST`
  - Endpoint: `https://api.replicate.com/v1/predictions`
  - Body: Cấu hình mô hình `google/veo-3` và truyền tham số `prompt` (nội dung mô tả video mà các sếp muốn tạo).
- **Node `Extract Prediction ID` (Code)**: Node này trích xuất mã định danh (prediction ID) từ phản hồi của Replicate để phục vụ cho việc kiểm tra tiến độ render.
- **Node `Wait`**: Thời gian chờ giữa các lần kiểm tra trạng thái video (mặc định được thiết lập để tránh gửi request quá dồn dập).
- **Node `Check Prediction Status` (HTTP Request)**: Gửi request kiểm tra xem video đã render xong chưa dựa trên Prediction ID.
- **Node `Check If Complete` (If)**: Kiểm tra trạng thái trả về. Nếu hoàn tất (`succeeded`), chuyển sang bước lấy kết quả; nếu chưa, quay lại vòng lặp chờ.
- **Node `Process Result` (Code)**: Lấy đường dẫn (URL) video đầu ra hoàn chỉnh để các sếp có thể tải xuống hoặc sử dụng cho các bước tiếp theo.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** tại node `On clicking 'execute'` (Manual Trigger) để test thử lần đầu với một prompt mẫu.
- Kiểm tra kết quả trả về ở node cuối cùng để đảm bảo video đã được tạo thành công.
- Bật công tắc **Active** để đưa workflow vào trạng thái sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
Để khai thác tối đa sức mạnh của workflow này, các sếp có thể mở rộng thêm:
1. **Kết nối Google Sheets:** Thay vì nhập prompt thủ công bằng tay, hãy đọc danh sách hàng chục ý tưởng video từ một file Google Sheets để tạo video hàng loạt (Batch Processing).
2. **Tự động lưu trữ:** Tự động tải file video về Google Drive hoặc AWS S3 ngay sau khi render xong.
3. **Phát hành tự động:** Kết hợp thêm các node đăng bài tự động để đẩy thẳng video vừa tạo lên TikTok, YouTube Shorts hoặc Facebook Reels qua API.

### 📌 Kết luận
Việc tích hợp AI Video Generation vào quy trình làm việc chưa bao giờ dễ dàng đến thế với n8n và Google Veo 3. Hãy nhanh tay thiết lập ngay workflow này để tối ưu hóa hiệu suất sản xuất nội dung của các sếp ngay hôm nay!