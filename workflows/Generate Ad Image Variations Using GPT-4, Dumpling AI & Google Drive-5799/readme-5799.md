---
title: "🚀 Tự động tạo hàng loạt biến thể ảnh quảng cáo bằng GPT-4, Dumpling AI và Google Drive"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tạo 10 biến thể ảnh quảng cáo sáng tạo từ hình ảnh gốc và thông tin thương hiệu bằng AI."
slug: "tao-bien-the-anh-quang-cao-tu-dong-n8n-gpt4-dumpling-ai"
tags: [n8n, automation, ai, gpt-4, google-drive, content-creation]
keywords: [n8n workflow, tự động hóa marketing, tạo ảnh quảng cáo AI, gpt-4o, dumpling ai, google sheets automation]
---

# 🚀 Tự động tạo hàng loạt biến thể ảnh quảng cáo bằng GPT-4, Dumpling AI và Google Drive

Việc tạo ra các biến thể hình ảnh quảng cáo (ad variations) để chạy A/B Testing thường ngốn rất nhiều thời gian của các nhà thiết kế và đội ngũ marketing. Các sếp thường phải mất hàng giờ chỉnh sửa bối cảnh, ánh sáng, góc chụp thủ công mà đôi khi vẫn chưa tìm được mẫu ưng ý. 

Workflow n8n này sẽ giải quyết triệt để nỗi đau đó bằng cách tự động hóa 100%: Nhận thông tin thương hiệu và hình ảnh gốc qua Form, phân tích bằng GPT-4o, sau đó gọi **Dumpling AI** để tạo ra 10 biến thể ảnh quảng cáo độc đáo, giữ nguyên chủ thể sản phẩm nhưng thay đổi bối cảnh, ánh sáng và phong cách một cách mượt mà, đồng thời tự động lưu trữ kết quả vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Biến 1 hình ảnh gốc thành 10 biến thể quảng cáo chỉ với 1 lần submit form.
- **AI thông minh phân tích đa phương thức:** GPT-4o phân tích chi tiết phong cách hình ảnh và website thương hiệu để tạo prompt chuẩn xác.
- **Tối ưu A/B Testing:** Cung cấp đa dạng phong cách, ánh sáng, background giúp các chiến dịch quảng cáo không bị nhàm chán.
- **Quản lý tập trung:** Toàn bộ lịch sử tạo ảnh và đường dẫn (URL) được lưu trữ tự động vào Google Sheets để dễ dàng tải về sử dụng.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **OpenAI API Key** (Sử dụng cho GPT-4o phân tích hình ảnh và LangChain Agent).
- **Dumpling AI API Key** (Dùng để tạo biến thể hình ảnh).
- **Google Drive & Google Sheets Account** (Để lưu trữ hình ảnh gốc, tải ảnh và ghi log kết quả).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cung cấp hoặc copy trực tiếp mã JSON, sau đó paste vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các credentials và tham số cho từng node quan trọng sau:

- **Submit Brand Info + Image (`formTrigger`):** Node khởi chạy giao diện nhận thông tin thương hiệu, website và hình ảnh gốc từ người dùng.
- **Upload Ad Image to Google Drive (`googleDrive`) & Download Ad Image for Analysis (`googleDrive`):** Kết nối tài khoản Google Drive qua OAuth2 để tải và lưu trữ ảnh gốc làm căn cứ phân tích.
- **Describe Visual Style of Image & Analyze Brand Website Style (`openAi`):** Kết nối OpenAI Credentials, node này sử dụng khả năng thị giác của GPT-4o để bóc tách bố cục, chủ thể, ánh sáng và nhận diện thương hiệu từ website.
- **LangChain Agent: Generate Variation Prompts & GPT-4o (`agent` & `lmChatOpenAi`):** Cấu hình model `gpt-4o-mini` hoặc `gpt-4o` để tổng hợp dữ liệu và viết ra 10 câu lệnh (prompt) tạo ảnh biến thể khác nhau.
- **Parse Prompts into JSON Array (`outputParserStructured`):** Giúp ép cấu trúc đầu ra của AI thành dạng mảng JSON chuẩn xác để các bước sau dễ dàng xử lý.
- **Dumpling AI: Generate Image Variation (`httpRequest`):** Cấu hình Header Auth chứa API Key của Dumpling AI để thực hiện gọi API tạo ảnh dựa trên các prompt đã sinh ra.
- **Log Image Variation URLs to Google Sheets (`googleSheets`):** Kết nối tài khoản Google Sheets, chọn đúng file bảng tính và Sheet Name để ghi lại lịch sử các URL hình ảnh biến thể vừa tạo.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng một biểu mẫu và hình ảnh mẫu để kiểm tra toàn bộ luồng dữ liệu.
- Sau khi kiểm tra thấy các ảnh được tạo và ghi log thành công, hãy gạt công tắc sang chế độ **Active workflow**.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối luồng để gửi thông báo ngay khi bộ 10 ảnh quảng cáo được tạo xong kèm theo link Google Sheets.
- **Mở rộng số lượng biến thể:** Có thể điều chỉnh LangChain Agent để tạo ra 15 hoặc 20 biến thể tùy theo nhu cầu kiểm tra quảng cáo quy mô lớn.
- **Lưu ảnh tự động về Drive:** Kết hợp thêm node upload ảnh kết quả từ Dumpling AI trực tiếp vào một thư mục riêng trên Google Drive thay vì chỉ lưu URL.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ mạnh mẽ giúp tối ưu hóa quy trình sản xuất nội dung hình ảnh cho các đội ngũ Performance Marketing. Hãy thiết lập ngay hôm nay để tiết kiệm hàng chục giờ thiết kế thủ công cho doanh nghiệp của các sếp!