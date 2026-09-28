---
title: "🚀 Tự Động Hóa Content LinkedIn: Nghiên Cứu Perplexity + GPT-4 + Google Sheets"
description: "Workflow n8n tự động tìm ý tưởng nội dung bằng Perplexity, viết bài LinkedIn chuyên nghiệp bằng GPT-4, lưu vào Google Sheets và thông báo qua Telegram mỗi ngày."
slug: "tu-dong-hoa-content-linkedin-perplexity-gpt4"
tags: [n8n, automation, no-code, linkedin, perplexity, gpt-4, google-sheets]
keywords: [n8n workflow, tự động hóa content, linkedin marketing, ai content creation, perplexity research]
---

# 🚀 Tự Động Hóa Content LinkedIn: Nghiên Cứu Perplexity + GPT-4 + Google Sheets

Việc duy trì lịch đăng bài đều đặn trên LinkedIn là một thách thức lớn đối với nhiều doanh nghiệp và cá nhân. Các sếp thường phải dành hàng giờ mỗi ngày để nghiên cứu xu hướng, tìm ý tưởng mới, và sau đó là quá trình viết lách tốn kém năng lượng. Làm thủ công không chỉ chậm mà còn dễ dẫn đến sự lặp lại, thiếu sự mới mẻ và nhất quán trong giọng văn thương hiệu.

Workflow này giải quyết triệt để vấn đề đó bằng cách kết hợp sức mạnh của **Perplexity AI** (để nghiên cứu sâu và tìm ý tưởng thực tế) và **GPT-4** (để viết nội dung chất lượng cao). Toàn bộ quy trình diễn ra tự động hàng ngày, không cần các sếp phải can thiệp thủ công, đảm bảo kênh LinkedIn luôn "sống" và thu hút tương tác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/tuần:** Tự động hóa hoàn toàn quy trình từ nghiên cứu đến viết bài.
- **Nội dung có chiều sâu:** Sử dụng Perplexity để lấy dữ liệu và xu hướng thực tế, tránh nội dung "sáo rỗng" của AI thông thường.
- **Quản lý tập trung:** Mọi ý tưởng và bài viết được lưu tự động vào Google Sheets, dễ dàng theo dõi lịch sử và hiệu suất.
- **Thông báo tức thì:** Nhận thông báo qua Telegram ngay khi bài viết mới được tạo, sẵn sàng để đăng hoặc chỉnh sửa nhẹ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị các credentials sau:
1. **OpenAI API Key:** Để sử dụng model `gpt-4.1-mini` (hoặc các model GPT-4 khác) cho việc viết bài.
2. **Perplexity API Key:** Để sử dụng model `sonar-pro` cho việc nghiên cứu và tìm ý tưởng.
3. **Google Sheets OAuth2:** Kết nối tài khoản Google để đọc và ghi dữ liệu vào Sheet.
4. **Telegram Bot Token & Chat ID:** Để nhận thông báo khi workflow hoàn tất.
5. **Google Sheet:** Tạo sẵn một Sheet với các cột tương ứng (ví dụ: Date, Topic, Idea, Image Prompt, Content).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ link gốc hoặc copy toàn bộ code JSON và dán vào n8n Editor.
- Mở n8n Editor.
- Chọn **Import from URL** hoặc **Import from File**.
- Dán link: `https://n8n.io/workflows/9185` hoặc file JSON đã tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Sau khi import, các sếp cần cấu hình các node sau để workflow chạy đúng ý đồ:

**1. Schedule Trigger**
- Mặc định workflow chạy hàng ngày. Các sếp có thể chỉnh giờ chạy (ví dụ: 08:00 sáng) để phù hợp với múi giờ và thời điểm đăng bài.

**2. Get row(s) in sheet (Google Sheets)**
- **Credentials:** Chọn credentials Google Sheets đã tạo.
- **Document ID & Sheet Name:** Điền ID của Google Sheet và tên Sheet chứa lịch sử bài viết.
- **Mục đích:** Node này lấy 3 bài viết gần nhất để đảm bảo nội dung mới không bị trùng lặp với các bài trước đó.

**3. Message a model (Perplexity)**
- **Credentials:** Chọn credentials Perplexity API.
- **Model:** Mặc định là `sonar-pro`. Các sếp có thể giữ nguyên hoặc đổi sang model khác nếu có.
- **Prompt:** Kiểm tra prompt để đảm bảo nó phù hợp với niche (ngách) của các sếp. Ví dụ: "Find 3 trending topics in [Your Niche] that are relevant to [Your Target Audience]".

**4. Idea Parser (Chain LLM)**
- **Model:** Chọn OpenAI Chat Model.
- **Prompt:** Đây là bước chuyển đổi kết quả nghiên cứu thô từ Perplexity thành các ý tưởng bài viết có cấu trúc. Các sếp nên tùy chỉnh prompt để yêu cầu AI đưa ra các góc nhìn cụ thể.

**5. Post Generator (Chain LLM)**
- **Model:** Chọn OpenAI Chat Model (khuyến nghị dùng model mạnh hơn như `gpt-4-turbo` hoặc `gpt-4.1` nếu ngân sách cho phép, mặc định là `gpt-4.1-mini`).
- **Prompt:** Đây là node quan trọng nhất. Các sếp cần chỉnh sửa prompt để định hình giọng văn (tone of voice), cấu trúc bài viết LinkedIn (hook, body, CTA) và độ dài mong muốn.
- **Structured Output Parser:** Đảm bảo output parser được cấu hình đúng để tách riêng nội dung bài viết và prompt hình ảnh (nếu có).

**6. Append row in sheet (Google Sheets)**
- **Credentials:** Chọn cùng credentials Google Sheets.
- **Mapping:** Kiểm tra ánh xạ các trường dữ liệu (Date, Topic, Idea, Image Prompt, Content) vào các cột tương ứng trong Sheet.

**7. Send a text message (Telegram)**
- **Credentials:** Chọn credentials Telegram Bot.
- **Chat ID:** Điền Chat ID của các sếp.
- **Message:** Tùy chỉnh thông báo để hiển thị tóm tắt bài viết mới được tạo.

#### 3. Kích hoạt ⚡️
1. **Test Run:** Chạy thử workflow với dữ liệu mẫu. Kiểm tra xem Perplexity có trả về ý tưởng hợp lý không, GPT-4 có viết bài đúng phong cách không và dữ liệu có được ghi vào Google Sheets chính xác không.
2. **Bật Active:** Sau khi kiểm tra kỹ, bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy theo lịch đã đặt.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Midjourney/DALL-E:** Workflow hiện tạo ra "Image Prompt". Các sếp có thể thêm node để gọi API Midjourney hoặc DALL-E để tự động tạo hình ảnh minh họa, sau đó lưu link ảnh vào Google Sheets.
- **Đa dạng hóa Niche:** Tạo nhiều workflow riêng cho từng kênh hoặc từng niche khác nhau, chỉ cần thay đổi prompt trong node Perplexity và Post Generator.
- **Phân tích hiệu suất:** Sau 1-2 tuần, các sếp có thể thêm node để đọc lại Google Sheets và phân tích loại bài viết nào có tương tác cao nhất (nếu có tích hợp LinkedIn API để lấy số liệu).
- **Cá nhân hóa hơn:** Thêm bước "Human-in-the-loop" bằng cách gửi bài viết qua Telegram và chờ phản hồi "Approve" trước khi tự động đăng lên LinkedIn (nếu có tích hợp LinkedIn API).

### 📌 Kết luận
Workflow này là một công cụ mạnh mẽ giúp các sếp biến LinkedIn thành một kênh marketing tự động, chuyên nghiệp và không ngừng nghỉ. Bằng cách kết hợp nghiên cứu sâu của Perplexity và khả năng viết lách của GPT-4, các sếp sẽ luôn có nội dung chất lượng cao, phù hợp với xu hướng và tiết kiệm được rất nhiều thời gian quý báu. Hãy import và tùy chỉnh ngay hôm nay để bắt đầu hành trình tự động hóa nội dung của mình!