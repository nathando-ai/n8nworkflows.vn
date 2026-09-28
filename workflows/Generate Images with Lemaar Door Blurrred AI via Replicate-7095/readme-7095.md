---
title: "🚀 Tự động tạo hình ảnh AI chất lượng cao với Replicate và Lemaar Door Blurrred trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tạo hình ảnh AI sử dụng mô hình Lemaar Door Blurrred trên Replicate, giúp tiết kiệm thời gian thiết kế và sáng tạo nội dung."
slug: "tao-hinh-anh-ai-lemaar-door-blurrred-replicate-n8n"
tags: [n8n, automation, replicate, ai-image-generation, content-creation, no-code]
keywords: [n8n workflow, tạo hình ảnh ai, replicate api, lemaar door blurrred, tự động hóa n8n, generative ai]
---

# 🚀 Tự động tạo hình ảnh AI với Lemaar Door Blurrred và Replicate trong n8n

Các sếp có đang tốn hàng giờ đồng hồ để tạo ra các hình ảnh độc đáo phục vụ cho việc thiết kế, marketing hay sáng tạo nội dung nhưng vẫn chưa ưng ý? Việc thao tác thủ công trên các nền tảng AI tẻ nhạt và khó tích hợp vào quy trình làm việc hàng ngày thực sự là một điểm nghẽn lớn.

Giải pháp là đây! Workflow n8n này sẽ giúp các sếp tự động hóa hoàn toàn quy trình gọi API đến mô hình **`creativeathive/lemaar-door-blurrred`** trên **Replicate**. Chỉ với một cú click, hệ thống sẽ tự động tạo, kiểm tra trạng thái và trả về kết quả hình ảnh sắc nét mà không cần can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Loại bỏ thao tác thủ công copy/paste prompt lên nền tảng Replicate.
- **Quy trình thông minh:** Tự động gửi yêu cầu, chờ xử lý (polling), kiểm tra trạng thái và trích xuất kết quả mượt mà.
- **Tiết kiệm thời gian:** Tối ưu hóa tốc độ tạo nội dung hình ảnh cho các chiến dịch marketing, thiết kế sản phẩm.
- **Dễ dàng mở rộng:** Có thể tích hợp thêm các bước lưu trữ vào Google Drive, gửi qua Telegram/Slack hoặc đăng thẳng lên mạng xã hội.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản **Replicate** và **API Token** cá nhân để xác thực.
- Kiến thức cơ bản về cách điền prompt tiếng Anh để mô hình AI hiểu và cho ra hình ảnh đẹp nhất.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ thư viện n8n (Link gốc: [n8n.io/workflows/7095](https://n8n.io/workflows/7095)) hoặc copy/paste trực tiếp đoạn JSON vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 8 nodes được sắp xếp logic từ kích hoạt đến xử lý kết quả. Các sếp cần chú ý cấu hình các node sau:

- **Set API Key**: Node này dùng để lưu trữ thông tin cấu hình ban đầu. Các sếp cần điền `Replicate API Key` của mình vào đây để các node HTTP Request có quyền gọi API.
- **Create Prediction** (HTTP Request): Node này gửi lệnh tạo hình ảnh đến Replicate sử dụng mô hình `creativeathive/lemaar-door-blurrred`. Các sếp hãy kiểm tra phần Body để đảm bảo `prompt` được truyền vào đúng ý muốn.
- **Extract Prediction ID** (Code): Node JavaScript nhỏ giúp trích xuất mã ID của tiến trình tạo ảnh từ kết quả trả về của Replicate.
- **Wait**: Node tạm dừng một khoảng thời gian ngắn (ví dụ: vài giây) để mô hình kịp xử lý hình ảnh trên server của Replicate.
- **Check Prediction Status** (HTTP Request): Node kiểm tra tiến độ xử lý dựa vào Prediction ID đã lấy ở bước trên.
- **Check If Complete** (If): Node rẽ nhánh kiểm tra xem hình ảnh đã render xong chưa (`succeeded` hay chưa). Nếu chưa, vòng lặp sẽ tiếp tục chờ; nếu rồi, chuyển sang bước tiếp theo.
- **Process Result** (Code): Node xử lý dữ liệu đầu ra cuối cùng, trích xuất đường dẫn URL của bức ảnh hoàn chỉnh để các sếp dễ dàng sử dụng.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** tại node **On clicking 'execute'** (Manual Trigger) để chạy thử nghiệm lần đầu với dữ liệu mẫu.
- Kiểm tra kết quả trả về ở node cuối cùng để đảm bảo link ảnh hiển thị chính xác.
- Bật công tắc **Active** ở góc trên cùng bên phải để đưa workflow vào trạng thái vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Telegram/Slack Bot:** Thay vì chỉ nhận kết quả trên n8n, các sếp có thể gắn thêm node Telegram để bot tự động gửi hình ảnh vừa tạo thẳng vào nhóm chat ngay khi hoàn tất.
- **Lưu trữ tự động:** Thêm node Google Drive hoặc AWS S3 để tải bức ảnh từ Replicate về lưu trữ lâu dài, tránh link ảnh bị hết hạn trên server nguồn.
- **Tạo Webhook Trigger:** Thay thế node `Manual Trigger` bằng `Webhook` hoặc `Google Sheets Trigger` để tự động tạo hàng loạt hình ảnh từ một danh sách prompt có sẵn.

### 📌 Kết luận
Workflow tạo hình ảnh AI với Lemaar Door Blurrred và Replicate là một công cụ tuyệt vời giúp các sếp tối ưu hóa quy trình sáng tạo nội dung hình ảnh bằng sức mạnh của Generative AI. Hãy import ngay vào n8n của các sếp và bắt đầu "lên đồ" những bức ảnh độc đáo ngay hôm nay!