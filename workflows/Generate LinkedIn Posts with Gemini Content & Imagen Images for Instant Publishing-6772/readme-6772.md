---
title: "🚀 Tự động hóa bài đăng LinkedIn chuyên nghiệp với Google Gemini và Imagen AI trên n8n"
description: "Hướng dẫn xây dựng workflow n8n kết hợp AI Agent (Google Gemini) và Imagen API để tự động tạo nội dung, hình ảnh chất lượng cao và đăng bài trực tiếp lên LinkedIn."
slug: "tu-dong-hoa-bai-dang-linkedin-gemini-imagen-n8n"
tags: [n8n, automation, content-creation, google-gemini, linkedin, ai-agent]
keywords: [n8n workflow, tự động hóa linkedin, google gemini n8n, imagen ai, tạo bài viết linkedin tự động]
---

# 🚀 Tự động hóa bài đăng LinkedIn chuyên nghiệp với Google Gemini và Imagen AI

Các sếp có thấy mệt mỏi khi mỗi ngày phải vắt óc nghĩ ý tưởng, viết bài, thiết kế hình ảnh rồi lại cặm cụi copy-paste lên LinkedIn không? Quy trình thủ công này ngốn rất nhiều thời gian quý báu mà lẽ ra các sếp có thể dùng để phát triển kinh doanh.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ xịn sò, giải quyết triệt để bài toán trên. Workflow này sẽ tự động hóa 100% từ khâu nhận chủ đề qua form, dùng **Google Gemini** viết nội dung cuốn hút kèm prompt vẽ tranh, gọi **Google Imagen API** tạo ảnh minh họa độc quyền, và tự động "xuất bản" bài viết lên trang cá nhân LinkedIn của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 không bị gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Chỉ cần nhập 1 dòng chủ đề (topic) vào form, AI sẽ lo từ A-Z.
- **Nội dung chuyên nghiệp:** Google Gemini tạo bài viết chuẩn SEO/Social với cấu trúc rõ ràng, thu hút tương tác.
- **Hình ảnh độc quyền:** Không cần dùng ảnh stock nhàm chán, Google Imagen sẽ vẽ hình minh họa riêng biệt dựa trên nội dung bài viết.
- **Đăng bài tức thì:** Tự động kết nối API và xuất bản trực tiếp lên feed LinkedIn mà không cần thao tác thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và thông tin sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Gemini API Key / Google Palm API Credentials** (cho node AI Agent & Google Gemini Chat Model).
- **Google Cloud Platform (Vertex AI)** API để sử dụng Imagen API (Text to Image).
- **LinkedIn Developer Account & App** với các quyền (scopes) đăng bài và upload ảnh qua API (cho các node HTTP Request tương tác với LinkedIn).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, vào giao diện n8n chọn **Add workflow** -> Click vào dấu ba chấm (...) ở góc trên bên phải -> Chọn **Import from Clipboard** và dán mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node cốt lõi sau:

- **On form submission (`formTrigger`):** Đây là điểm khởi đầu. Sau khi kích hoạt workflow, n8n sẽ cung cấp một đường link Form công khai. Các sếp có thể truy cập link này để nhập chủ đề bài viết bất cứ lúc nào.
- **Mapper (`set`) & AI Agent (`agent`):** Node Mapper nhận dữ liệu từ form và gán vào biến `chatInput`. AI Agent sẽ sử dụng biến này kết hợp với **Google Gemini Chat Model** để viết bài và tạo prompt vẽ ảnh.
- **Normalizer (`code`) & Code (`code`):** Các node này đóng vai trò "lọc" và định dạng lại dữ liệu đầu ra từ LLM (vốn thường chứa định dạng Markdown) để tách riêng phần Text bài viết và Prompt vẽ ảnh.
- **Text to image1 (`httpRequest`):** Gọi đến Google Imagen API để tạo ảnh dựa trên prompt của AI. *Lưu ý vùng địa lý (Geo Restrictions): Model tạo ảnh của Google có thể bị giới hạn ở một số quốc gia. Nếu gặp lỗi "Model not found", hãy kiểm tra lại vùng của API hoặc chuyển sang region được hỗ trợ.*
- **Convert to binary buffer (`code`):** Chuyển đổi dữ liệu ảnh nhận được từ dạng Base64 sang dạng Binary Buffer để chuẩn bị upload.
- **Register Image Upload & Upload Image to LinkedIn1 (`httpRequest`):** Thực hiện quy trình 2 bước của LinkedIn API để đăng ký và tải ảnh lên server của LinkedIn trước khi gắn vào bài viết.
- **Wait (`wait`):** Tạo khoảng thời gian chờ (30-60 giây) giữa lúc upload ảnh và lúc tạo bài viết để đảm bảo LinkedIn đã xử lý xong file ảnh.
- **HTTP Request (LinkedIn Post):** Node cuối cùng gửi payload gồm Nội dung text và ID hình ảnh đã upload để chính thức xuất bản bài viết lên LinkedIn cá nhân.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền một chủ đề bất kỳ vào Form.
- Kiểm tra kết quả trên terminal của n8n và trên trang LinkedIn của các sếp.
- Nếu mọi thứ chạy mượt, hãy gạt công tắc sang **Active** để chính thức tự động hóa!

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước Kiểm duyệt (Approval):** Thay vì đăng thẳng lên LinkedIn, các sếp có thể chèn thêm node Telegram hoặc Slack để gửi bản nháp (Text + Ảnh) kèm 2 nút bấm "Phê duyệt" hoặc "Chỉnh sửa". Chỉ khi sếp bấm Duyệt, workflow mới tiến hành gọi LinkedIn API để đăng bài.
- **Lưu lịch sử:** Thêm node Google Sheets hoặc Airtable để lưu lại toàn bộ chủ đề, nội dung bài viết và link LinkedIn đã đăng nhằm phục vụ việc đo lường hiệu suất (Analytics) sau này.
- **Đa kênh (Multi-platform):** Sau bước tạo nội dung, thay vì chỉ đăng LinkedIn, các sếp có thể nhân bản nhánh để đăng đồng thời lên Facebook Page, Twitter (X), hoặc Threads.

### 📌 Kết luận
Tự động hóa quy trình sáng tạo nội dung chưa bao giờ dễ dàng đến thế với sức mạnh của n8n và các mô hình Multimodal AI như Gemini & Imagen. Hãy cài đặt ngay workflow này để tối ưu hóa thời gian xây dựng thương hiệu cá nhân (Personal Branding) trên LinkedIn của các sếp ngay hôm nay!