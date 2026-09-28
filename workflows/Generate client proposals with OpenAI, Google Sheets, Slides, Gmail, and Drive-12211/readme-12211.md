---
title: "🚀 Tự động hóa tạo Proposal khách hàng bằng AI, Google Slides và Gmail trong n8n"
description: "Xây dựng hệ thống tạo hồ sơ năng lực và đề xuất dự án (proposal) tự động bằng OpenAI, điền dữ liệu vào Google Slides, chuyển PDF và gửi qua Gmail."
slug: "tu-dong-hoa-tao-client-proposal-ai-google-slides-gmail-n8n"
tags: [n8n, automation, openai, google-workspace, crm]
keywords: [n8n workflow, tạo proposal tự động, openai n8n, google slides automation, tự động hóa gửi email]
---

# 🚀 Tự động hóa tạo Proposal khách hàng bằng AI, Google Slides và Gmail trong n8n

Các sếp có bao giờ cảm thấy mệt mỏi mỗi khi kết thúc một cuộc họp sale (sales call) thành phố, lại phải hì hụi ngồi gõ lại yêu cầu của khách, soạn slide báo giá, viết email chào hàng và kiểm tra từng con số? Công việc thủ công này không chỉ ngốn hàng giờ đồng hồ quý báu mà đôi khi còn dễ dẫn đến sai sót, khiến cơ hội chốt đơn trôi qua tay đối thủ.

Giải pháp ở đây chính là workflow **AI Proposal Engine** – một hệ thống tự động hóa 100% không cần code (no-code), giúp các sếp biến các thông tin thô từ form đăng ký hoặc cuộc họp thành một bản Proposal chỉn chu trên Google Slides, tự động xuất file PDF và gửi thẳng đến email khách hàng!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn phải copy-paste thủ công thông tin khách hàng vào các template slide.
- **Cá nhân hóa thông minh:** OpenAI sẽ phân tích ngữ cảnh, yêu cầu và chi phí để viết nội dung proposal chuẩn xác, chuyên nghiệp nhất.
- **Quy trình kiểm soát linh hoạt:** Dữ liệu được lưu trữ tập trung trên Google Sheets; hệ thống chỉ tự động chuyển thành PDF và gửi email khi các sếp bật trạng thái sẵn sàng ("Ready").
- **Hoạt động liên tục 24/7:** Quản lý toàn bộ vòng đời từ lúc nhận form yêu cầu đến khi gửi email báo giá hoàn thành.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản OpenAI API Key** (Dùng cho các node tạo dữ liệu proposal và email draft).
- **Google Account (Google Cloud Console OAuth2)** cấp quyền truy cập các dịch vụ:
  - Google Sheets (Lưu trữ và theo dõi database proposal).
  - Google Drive (Quản lý template slide và lưu file PDF được xuất ra).
  - Google Slides (Template báo giá).
  - Gmail (Gửi email tự động tới khách hàng).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này, paste trực tiếp vào n8n Editor hoặc import file JSON thông qua giao diện quản lý workflow.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các thành phần sau:

- **Cấu hình Google Credentials:** Sử dụng chung một OAuth2 Credential cho toàn bộ các node thuộc hệ sinh thái Google (`Google Sheets Trigger`, `Copy Template`, `Move to Folder`, `Inject generated Text`, `Append In Database`, `Download Proposal in PDF`, `Send Email`, `Update Status`) để tránh lỗi xác thực.
- **Cấu trúc Google Drive & Google Sheets:** 
  - Tạo cấu trúc thư mục trên Drive gồm thư mục chứa Template Slides và thư mục `Generated Proposals/` để chứa các file xuất ra.
  - Chuẩn bị Google Sheet làm cơ sở dữ liệu (`Proposal Generation Tracker`). Copy **Sheet ID** từ URL và dán vào các node Google Sheets tương ứng.
- **Cấu hình OpenAI Nodes (`Generate Proposal Data`, `Generate Email Draft`):**
  - Tạo Credentials cho OpenAI bằng API Key của các sếp.
  - Tinh chỉnh Prompt bên trong node AI để hệ thống hiểu đúng văn phong công ty và định dạng dữ liệu trả về chuẩn JSON.
- **Xử lý dữ liệu (`Parse Json for Proposal Data`, `Parse Email Data`):**
  - Các node Code có nhiệm vụ bóc tách dữ liệu JSON sạch sẽ từ OpenAI để chuyển tiếp sang Google Slides và Gmail một cách chính xác.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng nút `Execute Workflow` để kiểm tra từ bước điền form (`On form submission` / `Google Sheets Trigger`) cho đến khâu tạo slide.
- Sau khi kiểm tra dữ liệu hiển thị đúng trên Google Sheets và các bản nháp email đã sẵn sàng, hãy bật công tắc **Active** để workflow hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ngay sau bước `Append In Database` để đội ngũ Sale nhận được thông báo ngay khi có một proposal mới vừa được tạo xong và chờ duyệt.
- **Phê duyệt tự động qua Slack Interactive:** Tích hợp nút bấm "Approve" trực tiếp trên Slack, khi bấm vào sẽ tự động cập nhật trạng thái trong Google Sheets để kích hoạt luồng gửi email tự động mà không cần vào bảng tính.
- **Quản lý nhiều template:** Dùng node Switch hoặc If dựa theo ngành nghề của khách hàng để tự động chọn Template Slide phù hợp nhất trên Google Drive.

### 📌 Kết luận
Workflow **AI Proposal Engine** là mảnh ghép hoàn hảo giúp tự động hóa toàn bộ khâu chuẩn bị tài liệu kinh doanh của doanh nghiệp. Hãy thiết lập ngay hôm nay để tăng tốc độ phản hồi khách hàng lên gấp 10 lần và nâng tầm chuyên nghiệp cho thương hiệu của các sếp!