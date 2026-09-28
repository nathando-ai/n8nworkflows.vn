---
title: "🚀 Tự động tạo ảnh Mockup sản phẩm cực đỉnh với Gemini 2.5 Flash Image và OpenRouter trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tạo ảnh mockup sản phẩm chuyên nghiệp từ hình ảnh gốc và template sử dụng AI đa phương thức Gemini 2.5 thông qua OpenRouter."
slug: "tao-anh-mockup-san-pham-gemini-openrouter-n8n"
tags: [n8n, automation, ai, gemini, openrouter, content-creation, multimodal]
keywords: [n8n workflow, tạo ảnh mockup, gemini 2.5 flash, openrouter api, tự động hóa thiết kế, ai đa phương thức]
---

# 🚀 Tự động tạo ảnh Mockup sản phẩm với Gemini 2.5 Flash Image qua OpenRouter

Các sếp làm trong ngành thương mại điện tử, thiết kế hay marketing chắc chắn hiểu rõ nỗi khổ: việc tạo ra hàng loạt hình ảnh mockup sản phẩm (như áo thun, cốc, banner quảng cáo...) vừa tốn kém chi phí thuê designer, vừa mất nhiều thời gian chờ đợi. Thay vì làm thủ công từng cái, tại sao không để AI lo toàn bộ?

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ, kết hợp Form thông minh và mô hình AI đa phương thức **Gemini 2.5 Flash Image** qua **OpenRouter** để tự động "biến hóa" ảnh sản phẩm của các sếp vào template có sẵn chỉ trong chớp mắt!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chỉ cần tải ảnh sản phẩm, ảnh template và nhập yêu cầu vào Form, AI sẽ tự động xử lý.
- **Tiết kiệm chi phí khủng:** Không cần tốn tiền thuê designer chỉnh sửa ảnh thủ công cho từng chiến dịch.
- **Chất lượng đỉnh cao:** Sử dụng mô hình AI tiên tiến `google/gemini-2.5-flash-image-preview` thông qua OpenRouter để ghép ảnh và tạo mockup cực kỳ chân thực.
- **Tối ưu thời gian:** Chuyển đổi từ ý tưởng sang ảnh thành phẩm chỉ trong vài giây, sẵn sàng tải về hoặc đưa vào chiến dịch marketing.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (phiên bản cloud hoặc self-hosted).
- **OpenRouter Account:** Tài khoản OpenRouter có API Key và đã nạp tiền để gọi mô hình Gemini Flash.
- **Dữ liệu đầu vào:** 
  - 1 ảnh sản phẩm (User Asset - ví dụ: logo, hình in trên áo).
  - 1 ảnh mẫu template (Template Model - ví dụ: người mẫu mặc áo thun trống).
  - Câu lệnh mô tả (Prompt) hướng dẫn AI cách ghép ảnh.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ n8n (Link gốc: [n8n.io/workflows/8194](https://n8n.io/workflows/8194)), sau đó chọn **Import from File** hoặc copy trực tiếp mã JSON và dán vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 7 nodes chính được liên kết chặt chẽ với nhau. Các sếp cần chú ý cấu hình các điểm sau:

- **Node `On form submission` (Form Trigger):** 
  - Tạo giao diện form thân thiện để người dùng (hoặc team marketing) tải lên ảnh sản phẩm, ảnh template và nhập prompt yêu cầu.
- **Node `User Asset Base64` & `Template Base64` (Extract From File):** 
  - Sử dụng thao tác `binaryToProperty` để chuyển đổi các file ảnh tải lên từ form thành định dạng Base64, giúp mô hình AI dễ dàng đọc hiểu dữ liệu đa phương thức.
- **Node `Assemble Final Data` & `Edit Fields` (Set):** 
  - Tổng hợp các dữ liệu gồm prompt của người dùng và các chuỗi Base64 của ảnh sản phẩm, ảnh template vào chung một cấu trúc JSON chuẩn bị gửi đi.
- **Node `HTTP Request` (HTTP Request):** 
  - **Quan trọng nhất:** Thiết lập kết nối đến OpenRouter API sử dụng Credentials `openRouterApi`.
  - Cấu hình body request gọi mô hình `google/gemini-2.5-flash-image-preview` với payload chứa cả 2 hình ảnh dạng Base64 kèm theo câu lệnh mô tả chi tiết công việc cần làm.
- **Node `Convert to File` (Convert To File):** 
  - Chuyển đổi kết quả trả về từ dạng dữ liệu thô của API thành file ảnh nhị phân (`toBinary`) để người dùng có thể xem trước và tải về ngay lập tức.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử điền thông tin vào form để test run với ảnh mẫu.
- Kiểm tra kết quả đầu ra xem ảnh mockup đã được tạo chính xác chưa.
- Sau khi test thành công, bật công tắc **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Kết nối thêm node Telegram hoặc Slack sau bước tạo ảnh thành công để tự động gửi ảnh mockup về group chat cho team duyệt.
- **Lưu trữ tự động:** Đẩy file ảnh kết quả (`Convert to File`) thẳng lên Google Drive hoặc AWS S3 để làm thư viện lưu trữ tài nguyên marketing lâu dài.
- **Tự động hóa hàng loạt (Batch Processing):** Thay vì dùng Form Trigger đơn lẻ, các sếp có thể đổi thành Google Sheets Trigger để tạo hàng trăm ảnh mockup sản phẩm tự động từ danh sách dữ liệu có sẵn.

### 📌 Kết luận
Việc ứng dụng AI đa phương thức như Gemini 2.5 Flash thông qua OpenRouter vào n8n sẽ giúp doanh nghiệp giải phóng sức lao động, tăng tốc độ sản xuất nội dung hình ảnh lên gấp nhiều lần. Hãy áp dụng ngay workflow này vào quy trình kinh doanh của các sếp để tối ưu hóa hiệu suất ngay hôm nay!