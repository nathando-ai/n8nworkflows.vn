---
title: "🚀 Tự động tạo ảnh quảng cáo theo phong cách đối thủ từ ảnh sản phẩm với Gemini AI"
description: "Hướng dẫn xây dựng workflow n8n tự động 'nhái' phong cách quảng cáo của đối thủ và tạo ảnh sản phẩm mới bằng Gemini Vision AI qua form upload."
slug: "tao-anh-quang-cao-doi-thu-bang-gemini-ai-n8n"
tags: [n8n, automation, no-code, gemini-ai, ai-image-generation, marketing]
keywords: [n8n workflow, tạo ảnh quảng cáo AI, Gemini Vision, tự động hóa marketing, clone ad style]
---

# 🚀 Tự động tạo ảnh quảng cáo theo phong cách đối thủ từ ảnh sản phẩm với Gemini AI

Các sếp làm marketing chắc chắn hiểu cảm giác mệt mỏi khi phải liên tục sáng tạo ý tưởng hình ảnh quảng cáo mới, hoặc tốn hàng giờ nghiên cứu xem vì sao banner của đối thủ lại chạy hiệu quả đến thế. Việc thiết kế thủ công từng biến thể (A/B testing) vừa tốn kém thời gian lại vừa chậm chạp trong cuộc đua "bắt trend".

Đừng lo, workflow n8n tuyệt vời này sẽ giải quyết triệt để nỗi đau đó! Bằng cách kết hợp sức mạnh của **Gemini Vision AI**, workflow tự động phân tích phong cách hình ảnh từ link quảng cáo của đối thủ, kết hợp với hình ảnh sản phẩm thực tế của các sếp để "tái sinh" ra một mẫu banner quảng cáo hoàn toàn mới, chuyên nghiệp và chuẩn chỉnh trong tích tắc.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian thiết kế**: Không cần mày mò bố cục hay blend màu từ đầu, AI tự động học theo phong cách đối thủ.
- **Sản xuất hàng loạt biến thể (A/B Testing)**: Dễ dàng tạo ra hàng chục mẫu quảng cáo chỉ với vài thao tác upload form đơn giản.
- **Cá nhân hóa theo sản phẩm thực**: Lồng ghép chính xác hình ảnh sản phẩm của doanh nghiệp vào concept của đối thủ một cách mượt mà.
- **Tự động hóa toàn diện**: Hoạt động 24/7 thông qua giao diện Web Form gọn gàng, trả kết quả trực tiếp cho người dùng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản API / Credentials kết nối với Generative AI (Gemini-style endpoints hỗ trợ multimodal và sinh ảnh).
- File workflow JSON gốc từ tác giả Pratyush Kumar Jha.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow `Generate competitor-style image ads from your product photos with Gemini` (Link gốc: [n8n workflow 13209](https://n8n.io/workflows/13209)).
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** và chọn file JSON vừa tải.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 10 nodes chính được chia thành các luồng xử lý từ input đến output:
- **`form_trigger`**: Điểm khởi đầu dạng Web Form, nơi người dùng (hoặc các sếp) sẽ nhập URL hình ảnh quảng cáo của đối thủ, upload file ảnh sản phẩm của mình, và ghi chú các yêu cầu thay đổi (nếu có).
- **`convert_product_image_to_base64`** & **`convert_ad_image_to_base64`**: Sử dụng node `extractFromFile` để chuyển đổi các định dạng file ảnh sản phẩm và ảnh đối thủ sang dạng chuỗi Base64 inline, chuẩn bị dữ liệu gửi cho mô hình AI.
- **`download_image`**: Node `httpRequest` thực hiện tải hình ảnh quảng cáo của đối thủ về từ URL được cung cấp trong form.
- **`build_prompt`**: Node `set` quan trọng giúp tổng hợp thông tin, ghép nối dữ liệu hình ảnh dạng Base64 và tạo câu lệnh (Prompt) chi tiết hướng dẫn AI cách kết hợp bố cục, ánh sáng, đổi CTA hoặc thêm bớt chi tiết theo ý muốn.
- **`generate_ad_image_prompt` & `generate_ad_image`**: Hai node `httpRequest` gọi trực tiếp đến các endpoint của Gemini/Generative AI (cần cấu hình chuẩn `httpBearerAuth` hoặc `httpHeaderAuth` tương ứng với API Key của các sếp). Node đầu chuẩn bị nội dung, node sau kích hoạt quá trình sinh ảnh.
- **`Wait`**: Tạm dừng luồng một khoảng thời gian ngắn để đảm bảo quá trình xử lý bất đồng bộ (async generation) của AI hoàn tất.
- **`set_result` & `get_image`**: Xử lý kết quả trả về từ AI, chuyển đổi dữ liệu nhị phân (`toBinary`) thành file ảnh hoàn chỉnh sẵn sàng để tải xuống hoặc trả về trực tiếp qua form.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và điền thử nghiệm thông tin vào form (`form_trigger`) để kiểm tra xem ảnh tạo ra có đúng kỳ vọng không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để đưa workflow vào trạng thái vận hành tự động thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack**: Thay vì chỉ trả kết quả về form, các sếp có thể nối thêm node Telegram hoặc Slack để bot tự động gửi ảnh quảng cáo vừa tạo vào group nhóm nội bộ ngay khi hoàn thành.
- **Lưu trữ Google Drive / Airtable**: Thêm node Google Drive để tự động lưu trữ tất cả các mẫu ad đã generate kèm theo prompt gốc để làm kho tư liệu marketing lâu dài.
- **Tối ưu Prompt**: Tinh chỉnh lại node `build_prompt` để bổ sung thêm các quy chuẩn về nhận diện thương hiệu (màu sắc chủ đạo, font chữ, logo) giúp ảnh AI tạo ra đồng bộ hơn với brand của doanh nghiệp.

### 📌 Kết luận
Tự động hóa quy trình sáng tạo nội dung và quảng cáo chưa bao giờ dễ dàng đến thế với sự trợ giúp của n8n và Gemini AI. Hãy áp dụng ngay workflow này vào đội ngũ marketing của các sếp để tối ưu hóa chi phí nhân sự và bứt phá doanh thu trong thời đại số!