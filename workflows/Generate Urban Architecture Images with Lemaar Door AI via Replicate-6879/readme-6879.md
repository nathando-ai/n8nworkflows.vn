---
title: "🚀 Tự động tạo ảnh kiến trúc đô thị độc đáo với Lemaar Door AI và Replicate trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tạo ảnh kiến trúc đô thị thông minh bằng mô hình Lemaar Door AI trên nền tảng Replicate, giúp tiết kiệm thời gian và tối ưu hóa sáng tạo nội dung."
slug: "tao-anh-kien-truc-do-thi-lemaar-door-ai-replicate"
tags: [n8n, automation, replicate, ai-image-generation, content-creation, no-code]
keywords: [n8n workflow, tạo ảnh AI, Lemaar Door AI, Replicate API, tự động hóa kiến trúc đô thị]
---

# 🚀 Tự động tạo ảnh kiến trúc đô thị độc đáo với Lemaar Door AI và Replicate

Trong ngành thiết kế kiến trúc và sáng tạo nội dung, việc tạo ra các concept hình ảnh đô thị độc đáo, chân thực thường ngốn rất nhiều thời gian và chi phí cho các phần mềm dựng hình truyền thống. Nếu các sếp đang tìm kiếm một giải pháp tự động hóa quy trình tạo ảnh AI chất lượng cao mà không cần viết code phức tạp, thì workflow n8n tích hợp **Replicate (Lemaar Door AI)** này chính là câu trả lời hoàn hảo.

Được thiết kế bởi chuyên gia *Yaron Been*, workflow này sẽ tự động hóa toàn bộ quy trình: từ việc gửi yêu cầu (prompt) đến mô hình AI, theo dõi trạng thái xử lý bất đồng bộ (asynchronous) và trả về kết quả hình ảnh hoàn chỉnh một cách mượt mà.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Bỏ qua các bước thao tác thủ công trên giao diện web của Replicate, gọi API và nhận kết quả trực tiếp trong n8n.
- **Xử lý bất đồng bộ thông minh:** Tận dụng cơ chế `Wait` và `If` để kiểm tra trạng thái tiến trình tạo ảnh của AI cho đến khi hoàn thành mà không làm nghẽn hệ thống.
- **Tối ưu chi phí & thời gian:** Nhanh chóng sản xuất hàng loạt các concept kiến trúc đô thị phục vụ cho marketing, thiết kế hoặc nghiên cứu ý tưởng.
- **Linh hoạt mở rộng:** Dễ dàng kết nối đầu ra hình ảnh với Telegram, Slack, Google Drive hoặc hệ thống CRM của doanh nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn n8n (Self-hosted hoặc n8n Cloud).
- **Replicate Account:** Tài khoản trên [Replicate](https://replicate.com/) kèm theo **API Key** cá nhân để xác thực các request gọi mô hình `creativeathive/lemaar-door-urban`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ kho lưu trữ n8n (Template ID: 6879) hoặc copy mã nguồn JSON trực tiếp và dán vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 8 nodes chính hoạt động nhịp nhàng với nhau. Các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Node `Set API Key` (Type: `set`):** 
  - Tại đây, các sếp cần cấu hình biến chứa **Replicate API Key** của mình để các node gọi API phía sau có quyền xác thực.
- **Node `Create Prediction` (Type: `httpRequest`):** 
  - Kiểm tra endpoint gọi tới Replicate API. Đảm bảo model được truyền vào đúng là `creativeathive/lemaar-door-urban`.
  - Truyền tham số `prompt` mô tả ý tưởng kiến trúc đô thị mà các sếp muốn tạo.
- **Node `Extract Prediction ID` (Type: `code`):** 
  - Trích xuất mã ID định danh của tiến trình (Prediction ID) từ kết quả trả về của Replicate để phục vụ việc kiểm tra trạng thái ở các bước sau.
- **Node `Wait` & `Check Prediction Status` (Type: `wait` & `httpRequest`):** 
  - Các node này phối hợp để chờ hệ thống AI xử lý (vì tạo ảnh mất một khoảng thời gian ngắn). Node `Wait` tạo khoảng trễ hợp lý trước khi gọi lại API kiểm tra trạng thái (`Check Prediction Status`).
- **Node `Check If Complete` (Type: `if`):** 
  - Kiểm tra xem trạng thái trả về từ Replicate đã ở trạng thái `succeeded` (thành công) chưa. Nếu chưa, workflow có thể vòng lặp lại hoặc chờ tiếp; nếu rồi sẽ chuyển sang bước xử lý kết quả.
- **Node `Process Result` (Type: `code`):** 
  - Nhận link bức ảnh kiến trúc đô thị hoàn chỉnh và định dạng lại dữ liệu để các sếp dễ dàng sử dụng cho các bước tiếp theo.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** từ node thủ công (`On clicking 'execute'`) để chạy thử nghiệm với một prompt mẫu.
- Kiểm tra kết quả trả về ở node cuối cùng. Khi mọi thứ hoạt động trơn tru, hãy bật công tắc **Active** để đưa workflow vào trạng thái vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack vào sau node `Process Result` để tự động bắn ảnh vừa tạo về nhóm chat ngay khi hoàn thành.
- **Lưu trữ tự động:** Kết nối với node Google Drive hoặc AWS S3 để tải trực tiếp file ảnh về lưu trữ lâu dài thay vì chỉ dựa vào link tạm thời của Replicate.
- **Nhận prompt từ Google Sheets:** Thay thế trigger thủ công bằng Google Sheets Trigger để các sếp có thể nhập danh sách hàng chục prompt vào bảng tính và để n8n tự động "cày" xuyên đêm.

### 📌 Kết luận
Việc ứng dụng AI vào thiết kế và sáng tạo nội dung chưa bao giờ dễ dàng đến thế khi kết hợp sức mạnh của n8n và Replicate. Hãy triển khai ngay workflow này để tối ưu hóa quy trình làm việc và tạo ra những bức ảnh kiến trúc đô thị mãn nhãn chỉ trong vài nốt nhạc!