---
title: "🚀 Xây dựng Trợ lý AI Tự động Ứng tuyển Công việc (Job Applying Agent) với n8n"
description: "Tự động hóa toàn bộ quy trình tìm kiếm thông tin doanh nghiệp, quét website, trích xuất dữ liệu liên hệ và gửi email ứng tuyển cá nhân hóa 100% nhờ AI Agent."
slug: "job-applying-agent-n8n"
tags: [n8n, automation, ai-agent, openai, google-sheets, gmail]
keywords: [n8n workflow, job applying agent, tự động hóa ứng tuyển, ai agent n8n, openai gpt-5]
---

# 🚀 Tự động hóa ứng tuyển công việc đỉnh cao với Job Applying Agent

Việc gửi đơn ứng tuyển thủ công, nghiên cứu từng website công ty, tìm kiếm thông tin liên hệ và viết email cá nhân hóa cho từng nhà tuyển dụng ngốn của bạn hàng giờ đồng hồ mỗi ngày. Chưa kể việc thiếu nhất quán và dễ bỏ sót cơ hội. 

Giải pháp ư? Hãy để **Job Applying Agent** trên n8n thay bạn làm toàn bộ quy trình nặng nhọc này: Từ việc tiếp nhận thông tin qua Form, quét website mục tiêu, trích xuất thông tin liên hệ bằng AI, đối chiếu dữ liệu kinh nghiệm cá nhân từ Google Sheets cho đến việc tự động gửi email ứng tuyển chuyên nghiệp qua Gmail.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các tác vụ AI nặng, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải copy/paste hay viết từng email thủ công cho hàng chục công ty.
- **Cá nhân hóa 100%:** AI Agent tự động phân tích website doanh nghiệp và kết hợp với dữ liệu kinh nghiệm thực tế của bạn để tạo ra bức thư ứng tuyển cực kỳ thuyết phục.
- **Tự động hóa toàn diện:** Từ Form đầu vào đến việc quét dữ liệu (HTTP Request, Information Extractor) và gửi email qua Gmail hoàn toàn tự động.
- **Hoạt động linh hoạt:** Dễ dàng tùy biến các vị trí công việc (Video Editor, SEO Expert, Full-Stack Developer, Social Media Manager...) ngay trên Form Trigger.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Phiên bản hỗ trợ LangChain / AI Nodes).
- **Tài khoản OpenAI API:** Để cấp quyền cho 2 node `OpenAI Chat Model` sử dụng mô hình GPT-5.
- **Google Sheets:** File Google Sheet chứa thông tin kỹ năng, portfolio, kinh nghiệm và thành tựu cá nhân của bạn.
- **Gmail Account:** Tài khoản Gmail đã kết nối OAuth2 để gửi email tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc copy trực tiếp mã nguồn JSON, sau đó dán vào n8n Editor của bạn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà, các sếp cần cấu hình kỹ các node sau:
- **On form submission (Form Trigger):** Tùy chỉnh các trường trong form (Website doanh nghiệp mục tiêu, Vị trí ứng tuyển). Thêm các vị trí công việc phù hợp vào danh sách dropdown (Ví dụ: Video Editor, SEO Expert, Full-Stack Developer, Social Media Manager...).
- **OpenAI Chat Model & OpenAI Chat Model1:** Kết nối tài khoản OpenAI API của bạn để cung cấp sức mạnh AI cho việc trích xuất thông tin và tạo nội dung email.
- **Get row(s) in sheet in Google Sheets:** Liên kết file Google Sheet chứa dữ liệu kinh nghiệm và portfolio của bạn. Đảm bảo các cột trong sheet khớp với dữ liệu mà AI cần đối chiếu cho từng loại công việc.
- **Send a message in Gmail (Gmail Tool):** Kết nối thông tin xác thực Gmail OAuth2. Nhớ cập nhật tên người gửi từ tên mặc định sang tên thực tế của các sếp trong cài đặt node này.
- **AI Agent:** Tinh chỉnh system prompt trong node này để phản ánh đúng thế mạnh độc bản (unique value proposition) và phong cách ứng tuyển riêng của bạn.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test workflow) bằng cách điền thông tin mẫu vào Form để kiểm tra luồng dữ liệu từ việc quét website, trích xuất đến soạn thảo email.
- Bật công tắc **Active workflow** để đưa hệ thống vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Kết nối thêm node Telegram hoặc Slack để nhận thông báo ngay lập tức mỗi khi Agent gửi thành công một email ứng tuyển.
- **Lưu log tự động:** Thêm một bước ghi lại lịch sử các công ty đã ứng tuyển vào Google Sheets để dễ dàng theo dõi trạng thái phản hồi (Follow-up).
- **Tạo danh sách đen (Blacklist):** Thêm node `If` để lọc ra các trang web không phù hợp hoặc trùng lặp trước khi tiến hành cào dữ liệu và gửi email.

### 📌 Kết luận
Với **Job Applying Agent**, quá trình tìm việc và gửi CV chưa bao giờ chuyên nghiệp và tự động hóa đến thế. Hãy triển khai ngay hôm nay để tối ưu hóa hành trình sự nghiệp của các sếp!