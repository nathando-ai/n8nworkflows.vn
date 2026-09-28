---
title: "🚀 Tự động quét danh thiếp từ Slack vào Google Sheets bằng GPT-4o OCR"
description: "Hướng dẫn xây dựng workflow n8n tự động trích xuất thông tin danh thiếp (business card) từ Slack, xử lý qua AI GPT-4o và lưu trữ gọn gàng vào Google Sheets."
slug: "tu-dong-quet-danh-thiep-slack-google-sheets-gpt-4o"
tags: [n8n, automation, no-code, openai, google-sheets, slack, ai-ocr]
keywords: [n8n workflow, quét danh thiếp tự động, slack to google sheets, gpt-4o ocr, trích xuất danh thiếp ai]
---

# 🚀 Tự động quét danh thiếp từ Slack vào Google Sheets với GPT-4o OCR

Các sếp có bao giờ cảm thấy mệt mỏi khi đi sự kiện, hội thảo về với một "núi" danh thiếp (business card) giấy và phải ngồi gõ thủ công từng cái tên, số điện thoại, email vào file quản lý không? Vừa tốn thời gian, dễ sai sót lại vừa nản lòng!

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n siêu việt này. Chỉ cần **chụp ảnh danh thiếp vàném lên Slack**, phần còn lại để AI và n8n lo. Thông tin sẽ được bóc tách chuẩn xác bằng sức mạnh của **GPT-4o**, tự động lưu vào **Google Sheets** và gửi thông báo xác nhận ngược lại cho các sếp trên Slack. Hoàn toàn tự động 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần gõ tay, AI đọc và phân loại thông tin danh thiếp chỉ trong vài giây.
- **Độ chính xác cao:** Ứng dụng mô hình thị giác máy tính GPT-4o đa phương thức (Multimodal AI) để nhận diện chữ trên ảnh cực tốt.
- **Dữ liệu đồng bộ tập trung:** Mọi liên hệ mới đều được cập nhật ngăn nắp vào Google Sheets để dễ dàng chăm sóc khách hàng (CRM).
- **Phản hồi tức thì:** Nhận thông báo xác nhận ngay trên Slack ngay khi dữ liệu được lưu thành công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã chạy ổn định (Cloud hoặc Self-hosted).
- **Tài khoản Slack:** Có quyền kết nối App/Bot để nhận trigger khi có ảnh tải lên channel.
- **Tài khoản Google:** Đã tạo sẵn một file Google Sheets để lưu thông tin danh thiếp.
- **OpenAI API Key:** Có số dư để sử dụng mô hình `gpt-4o`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, dán thẳng vào trình soạn thảo n8n (n8n Editor) hoặc import file JSON trực tiếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:
- **Slack Trigger:** Kết nối tài khoản Slack (`slackApi`) và chọn đúng Channel mà các sếp sẽ upload ảnh danh thiếp lên.
- **Fetch images (Node HTTP Request):** Cấu hình đúng credential Slack để n8n có quyền tải hình ảnh từ tin nhắn người dùng.
- **AI model (Node `lmChatOpenAi`):** Nhập OpenAI API Key, chọn model là `gpt-4o` để đảm bảo khả năng đọc ảnh (OCR) sắc bén nhất.
- **Scan Contact Information (Node `agent` & `Structure Output`):** Thiết lập cấu trúc dữ liệu đầu ra mong muốn (Ví dụ: Tên, Tên công ty, Email, Số điện thoại, Chức vụ...).
- **Append row in sheet (Node `googleSheets`):** Kết nối tài khoản Google Sheets OAuth2, chọn đúng file Spreadsheet và Sheet chứa danh sách liên hệ để map dữ liệu từ AI trả về.
- **Send a message (Node Slack):** Cấu hình kênh Slack nhận thông báo xác nhận danh thiếp đã được lưu thành công.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng cách gửi 1 bức ảnh danh thiếp lên kênh Slack đã chọn.
- Kiểm tra kết quả trên Google Sheets và Slack. Nếu mọi thứ xanh mướt, hãy gạt nút **Active** để workflow hoạt động tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp CRM:** Thay vì chỉ lưu Google Sheets, các sếp có thể nối thêm node HubSpot, Salesforce hoặc Notion để tạo lead tự động.
- **Gửi Email chào mừng tự động:** Nếu danh thiếp có kèm email, có thể dùng n8n gửi ngay một email giới thiệu dịch vụ/công ty đến khách hàng đó.
- **Lưu trữ ảnh gốc:** Lưu trữ ảnh danh thiếp lên Google Drive hoặc AWS S3 kèm theo dòng dữ liệu trong sheet để tiện tra cứu sau này.

### 📌 Kết luận
Việc số hóa danh thiếp chưa bao giờ dễ dàng và thông minh đến thế nhờ sự kết hợp giữa Slack, GPT-4o AI và Google Sheets trên n8n. Hãy thiết lập ngay hôm nay để tối ưu hóa quy trình networking của các sếp!