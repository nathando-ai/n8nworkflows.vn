---
title: "🚀 Tự động hóa tạo Hồ sơ năng lực (Sales Proposal) từ JotForm và OpenAI với n8n"
description: "Hướng dẫn chi tiết cách xây dựng hệ thống tự động nhận thông tin từ JotForm, xử lý âm thanh bằng AI, tạo Google Docs proposal chuyên nghiệp và gửi email cho khách hàng."
slug: "tu-dong-hoa-tao-sales-proposal-jotform-openai-n8n"
tags: [n8n, automation, no-code, openai, google-docs, jotform]
keywords: [n8n workflow, tự động hóa sales proposal, jotform openai n8n, tạo báo giá tự động, ai document generator]
---

# 🚀 Tự động hóa tạo Hồ sơ năng lực (Sales Proposal) từ JotForm và OpenAI với n8n

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thủ công nghe lại file ghi âm cuộc gọi với khách hàng, tổng hợp thông tin, viết báo giá (Sales Proposal) vào Google Docs rồi mới gửi email không? Quá trình này không chỉ mất hàng giờ đồng hồ mà đôi khi còn khiến khách hàng phải chờ đợi lâu, làm giảm tỷ lệ chốt sale.

Giải pháp ở đây là gì? Workflow n8n này sẽ giúp các sếp **tự động hóa 100% quy trình từ A-Z**: Ngay khi khách hàng điền form trên JotForm (có đính kèm link ghi âm cuộc họp), hệ thống sẽ tự động dùng AI để transcribe (chuyển giọng nói thành văn bản), viết nội dung proposal chuẩn chỉnh, điền vào file template trên Google Docs, chuyển sang PDF và tạo bản nháp email gửi thẳng cho khách hàng hoặc sale phụ trách!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần nghe lại file ghi âm hay gõ phím viết proposal thủ công.
- **Cá nhân hóa sâu sắc:** Dựa trên nội dung trao đổi thực tế của khách hàng trong cuộc gọi để AI viết proposal trúng "nỗi đau".
- **Chuyên nghiệp & Tốc độ:** Khách hàng nhận được bản proposal chỉ vài phút sau khi submit form.
- **Hoạt động 24/7:** Chạy ngầm mượt mà, không bỏ lỡ bất kỳ lead tiềm năng nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **JotForm** (để tạo form thu thập thông tin lead và link ghi âm).
- Tài khoản **Google Drive / Google Docs** (chứa template proposal mẫu).
- Tài khoản **OpenAI API Key** (để dùng model Whisper transcribe âm thanh và GPT viết nội dung).
- Tài khoản **Gmail** (để tạo bản nháp/gửi email).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào n8n Editor của mình, hoặc import file JSON tải từ nguồn gốc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 8 nodes chính, các sếp cần cấu hình kỹ các điểm sau:

- **JotForm Trigger**: Kết nối tài khoản JotForm của các sếp. Thay đổi `form` ID thành ID form thực tế của sếp (mặc định trong template là `251206359432049`).
- **Google Drive**: Kết nối tài khoản Google Drive (OAuth2). Cập nhật `fileId` thành ID của file Google Docs Template mà sếp muốn dùng làm mẫu (mặc định: `1DSHUhq_DoM80cM7LZ5iZs6UGoFb3ZHsLpU3mZDuQwuQ`). Đặt tên file đầu ra tại trường `name` (mặc định: `={{ $json['Company Name'] }} | Ai Proposal`).
- **Google Drive1 (Download)**: Node này dùng để tải file âm thanh từ link mà khách hàng/sale cung cấp trong JotForm.
- **OpenAI (Transcribe)**: Sử dụng mô hình Audio Whisper của OpenAI để chuyển file ghi âm cuộc gọi thành văn bản. Cần cấu hình OpenAI credentials.
- **OpenAI1 (Text Generation)**: Sử dụng mô hình OpenAI (ví dụ: `gpt-4.1-mini`) kết hợp với prompt thông minh để soạn nội dung proposal dựa trên bản transcript cuộc gọi.
- **Google Docs (Update)**: Tự động điền nội dung mà OpenAI vừa viết vào file Google Docs đã được copy ở bước Google Drive.
- **Google Drive2 (Download as PDF)**: Tự động convert file Google Docs vừa tạo thành định dạng PDF để gửi cho chuyên nghiệp.
- **Gmail (Draft/Send)**: Tự động lấy email của khách hàng từ JotForm, đính kèm file PDF proposal và tạo bản nháp (hoặc gửi trực tiếp) cho khách.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test workflow**) với một dữ liệu JotForm giả lập để kiểm tra từng bước từ đọc form -> AI transcribe -> tạo Google Docs -> gửi Gmail.
- Sau khi test chạy mượt mà, các sếp bấm nút **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Gợi ý nâng cao để tối ưu hóa
- **Thêm Slack / Telegram Notification:** Gửi thông báo về nhóm nội dung ngay khi có proposal mới được tạo thành công để đội ngũ sale nắm bắt.
- **Lưu Log vào Google Sheets:** Ghi lại thông tin khách hàng, tên công ty và link Google Docs proposal vào một file quản lý chung để tiện theo dõi.
- **Phê duyệt thủ công (Human-in-the-loop):** Thay vì gửi email tự động hoàn toàn, hãy dừng ở bước tạo Gmail Draft để sếp hoặc nhân viên sale đọc lại, chỉnh sửa một chút rồi mới bấm nút gửi.

### 📌 Kết luận
Việc tự động hóa quy trình tạo Sales Proposal từ JotForm và OpenAI không chỉ giúp tiết kiệm thời gian tối đa mà còn nâng tầm chuyên nghiệp cho doanh nghiệp trong mắt khách hàng. Hãy "lên đồ" ngay cho hệ thống n8n của các sếp và tối ưu hóa quy trình bán hàng ngay hôm nay!