---
title: "🚀 Tự động tạo Infographic chuyên sâu bằng AI: GPT-4, kie.ai và Gmail"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa hoàn toàn quy trình nghiên cứu chủ đề bằng GPT-4, tạo infographic chuyên nghiệp qua kie.ai và gửi email kết quả."
slug: "tu-dong-tao-infographic-voi-gpt-4-va-kie-ai-trong-n8n"
tags: [n8n, automation, ai-infographic, openai, kie-ai, gmail]
keywords: [n8n workflow, tạo infographic tự động, ai marketing automation, gpt-4 web search, kie.ai, n8n gmail integration]
---

# 🚀 Tự động tạo Infographic chuyên sâu bằng AI: GPT-4, kie.ai và Gmail

Các sếp có bao giờ cảm thấy mệt mỏi khi phải tốn hàng giờ liền lên ý tưởng, nghiên cứu số liệu, rồi lại chật vật thiết kế infographic trên Canva hay Photoshop cho mỗi bài đăng mạng xã hội hoặc chiến dịch marketing không? Việc này vừa ngốn thời gian, vừa đòi hỏi kỹ năng thiết kế mà kết quả đôi khi vẫn chưa được như ý.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một "vũ khí" tự động hóa cực kỳ mạnh mẽ trên n8n. Workflow này sẽ thay các sếp làm từ A-Z: Nghiên cứu nội dung bằng GPT-4 (có web search), tối ưu prompt, gửi sang **kie.ai** để render ảnh infographic sắc nét, và tự động gửi thẳng thành phẩm vào hòm thư Gmail chỉ với một vài cú click điền form!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần tự tay tra cứu số liệu hay thiết kế đồ họa phức tạp.
- **Dựa trên dữ liệu thực tế (Research-backed):** GPT-4 sẽ tìm kiếm thông tin mới nhất trước khi tạo prompt thiết kế.
- **Tự động hóa thông minh:** Cơ chế Polling (kiểm tra trạng thái) tự động theo dõi tiến độ render ảnh và gửi email đính kèm ngay khi hoàn tất.
- **Xử lý lỗi chuyên nghiệp:** Tự động gửi email thông báo chi tiết nếu quá trình tạo ảnh gặp sự cố hoặc timeout.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và thông tin sau:
- **n8n Instance:** Đã chạy ổn định (Self-hosted hoặc n8n Cloud).
- **OpenAI API Key:** Dành cho node AI Agent & Researcher (sử dụng model GPT-4).
- **kie.ai API (Bearer Token):** Nền tảng tạo ảnh AI chuyên dụng.
- **Gmail Account:** Để kết nối gửi email tự động chứa ảnh infographic hoàn thiện.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này hoặc copy trực tiếp mã JSON từ nguồn cấp.
- Mở giao diện n8n Editor, nhấn vào dấu **`+`** hoặc chọn **Add workflow** -> **Import from File / Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp nhớ cấu hình kỹ các điểm sau:
- **Node `Researcher` & `Build Image Prompt` (AI Agent):** Kết nối với OpenAI Credential và cấu hình model `gpt-4.1-mini` (hoặc model GPT-4 tương đương) hỗ trợ web search.
- **Node `Generate Infographic` & `Check Job Status` (HTTP Request):** Tạo một **Header Auth** credential với Bearer Token lấy từ tài khoản **kie.ai** của các sếp, sau đó gán vào các node này.
- **Node `Email Image to User` & `Send Error Email` (Gmail):** Kết nối tài khoản Gmail qua OAuth2 và nhớ cập nhật địa chỉ email nhận (To) hoặc lấy động từ form submit.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử submit dữ liệu mẫu qua form (`On form submission`) để test toàn bộ luồng chạy từ nghiên cứu, tạo ảnh đến gửi email.
- Kiểm tra xem ảnh đã về hòm thư Gmail chưa. Nếu mọi thứ OK, gạt công tắc sang **Active** để đưa workflow vào vận hành chính thức 24/7!

---

### 💡 Luồng hoạt động chi tiết qua 5 bước
1. **① User Input:** Người dùng điền form trực tuyến (tiêu đề, chủ đề, phong cách, màu sắc, độ phân giải...).
2. **② AI Prompt Engineering:** AI Agent (GPT-4 kèm web search) nghiên cứu sâu về chủ đề và viết prompt tối ưu hóa cho việc tạo ảnh.
3. **③ Generate & Poll:** Gửi request sang kie.ai (model nano-banana-pro), sau đó workflow sẽ tự động lặp kiểm tra trạng thái mỗi 15 giây (tối đa 20 lần thử / ~5 phút).
4. **④ Success:** Khi hoàn thành, tự động tải ảnh về và gửi kèm qua email cho người dùng.
5. **⑤ Error Handling:** Xử lý triệt để các trường hợp lỗi (lỗi tạo ảnh, timeout quá 20 lần thử, lỗi API) và gửi email thông báo chi tiết tình trạng lỗi.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng thông báo:** Kết nối thêm node Telegram hoặc Slack ở nhánh Success/Error để đội ngũ nội dung nhận được thông báo ngay khi có infographic mới ra lò.
- **Lưu trữ tự động:** Thêm node Google Drive hoặc Airtable để lưu trữ lại tất cả các infographic đã tạo kèm theo prompt gốc phục vụ cho việc tra cứu sau này.
- **Tạo bảng Dashboard:** Lưu lịch sử yêu cầu của khách hàng/nhân sự vào Google Sheets để dễ dàng theo dõi hiệu suất sử dụng.

### 📌 Kết luận
Workflow tự động hóa tạo Infographic kết hợp giữa GPT-4 và kie.ai là một giải pháp đột phá giúp cá nhân hóa và tăng tốc độ sản xuất nội dung hình ảnh cho các doanh nghiệp vừa và nhỏ. Hãy triển khai ngay hôm nay để tối ưu hóa hiệu suất làm việc của đội ngũ marketing nhé các sếp!