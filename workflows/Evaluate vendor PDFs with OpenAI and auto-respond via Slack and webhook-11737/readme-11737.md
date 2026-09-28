---
title: "🚀 Tự động đánh giá hồ sơ năng lực nhà cung cấp (PDF) bằng OpenAI và Slack trên n8n"
description: "Xây dựng hệ thống tự động nhận file PDF đề xuất từ nhà cung cấp, phân tích rủi ro bằng AI OpenAI và tự động phản hồi hoặc cảnh báo qua Slack."
slug: "tu-dong-danh-gia-ho-so-nha-cung-cap-pdf-openai-slack-n8n"
tags: [n8n, automation, openai, slack, ai-summarization, document-extraction]
keywords: [n8n workflow, tự động hóa tài liệu, đánh giá nhà cung cấp, openai pdf, webhook n8n]
---

# 🚀 Tự động đánh giá hồ sơ năng lực nhà cung cấp bằng OpenAI và Slack

Mỗi khi doanh nghiệp mở thầu hoặc nhận hồ sơ năng lực (proposal/PDF) từ đối tác, việc đọc, sàng lọc và đánh giá thủ công thường ngốn rất nhiều thời gian của đội ngũ mua hàng (Procurement). Chưa kể, việc bỏ sót các điều khoản rủi ro hay chậm trễ phản hồi có thể khiến doanh nghiệp mất đi cơ hội hợp tác vàng.

Workflow n8n này sẽ giải quyết triệt để bài toán trên bằng cách **tự động hóa 100% quy trình**: Nhận file PDF qua Webhook $\rightarrow$ Trích xuất & làm sạch dữ liệu $\rightarrow$ Phân tích rủi ro bằng OpenAI $\rightarrow$ Cảnh báo qua Slack nếu có rủi ro hoặc tự động phê duyệt nếu an toàn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tăng tốc xử lý 90%**: Rút ngắn thời gian đánh giá hồ sơ từ vài tiếng xuống còn vài giây.
- **Quyết định minh bạch, chuẩn xác**: AI đánh giá dựa trên tiêu chí đồng nhất, đảm bảo nguyên tắc 1 file PDF = 1 quyết định duy nhất, không trùng lặp.
- **Cảnh báo thông minh**: Tự động gửi thông báo chi tiết qua Slack khi phát hiện rủi ro hoặc thông tin mập mờ để đội ngũ quản lý can thiệp kịp thời.
- **Hoạt động 24/7**: Hệ thống tự động tiếp nhận hồ sơ qua Webhook bất kể ngoài giờ hành chính.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance** (Self-hosted hoặc n8n Cloud).
- **Tài khoản OpenAI** (để lấy API Key tích hợp vào node OpenAI).
- **Workspace Slack** (để tạo Bot/App và lấy Slack API Credentials gửi cảnh báo).
- **Tool test API** (Postman, cURL hoặc một form HTML đơn giản để gọi Webhook).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow (hoặc tải file JSON từ nguồn gốc) và dán trực tiếp vào giao diện n8n Editor thông qua tính năng Import từ Clipboard.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 11 nodes chính được chia làm các cụm xử lý thông minh:

- **Proposal Upload (Webhook)**: 
  - Cấu hình đường dẫn (Path) nhận dữ liệu: `vendor-proposal-upload`
  - Phương thức HTTP Method: `POST` (nhận file PDF hoặc URL file PDF từ hệ thống bên ngoài gửi đến).
- **Download Proposal PDF (HTTP Request)**: 
  - Đảm bảo node này nhận đúng URL file PDF được truyền từ Webhook đầu vào để tiến hành tải file xuống.
- **Parse PDF (Extract From File)**: 
  - Chọn Operation là `PDF` để chuyển đổi toàn bộ tài liệu thành dạng văn bản thô (raw text).
- **Proposal Evaluation (OpenAI)**: 
  - Chọn hoặc tạo mới **OpenAI API Credentials**.
  - Thiết lập System Prompt/User Prompt chuẩn xác để AI phân tích cấu trúc hồ sơ, trả về kết quả dưới dạng JSON có cấu trúc rõ ràng (bao gồm cờ rủi ro - risk flag).
- **Risks? (If Node)**: 
  - Thiết lập điều kiện kiểm tra biến rủi ro từ kết quả trả về của OpenAI. Nhánh `True` sẽ chuyển đến việc tạo tóm tắt rủi ro và gửi cảnh báo, nhánh `False` chuyển sang tự động phê duyệt.
- **SEND ALERT (Slack)**: 
  - Chọn **Slack API Credentials**, cấu hình kênh (Channel) nhận thông báo khẩn cấp khi phát hiện rủi ro trong hồ sơ nhà cung cấp.
- **Respond to Webhook**: 
  - Trả về kết quả phản hồi (thành công/được duyệt) cho bên gửi yêu cầu (requester).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng một file PDF mẫu thông qua Postman bắn vào URL Webhook của n8n.
- Kiểm tra kỹ luồng dữ liệu chạy qua các node Code (`Clean Text`, `Parse OpenAI JSON`, `Build Risk Summary`, `Auto Approve Payload`).
- Sau khi test thành công, gạt công tắc **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ lịch sử**: Kết nối thêm node Google Sheets hoặc Airtable ngay sau bước phân tích để lưu lại toàn bộ lịch sử nộp hồ sơ và kết quả đánh giá của AI vào bảng dữ liệu quản lý.
- **Gửi Email tự động cho nhà cung cấp**: Tích hợp thêm node Gmail hoặc SMTP để tự động gửi email cảm ơn hoặc thông báo trúng thầu cho nhà cung cấp khi hồ sơ vượt qua vòng kiểm duyệt (No Risk).
- **Tích hợp bảng điểm động**: Thay vì chỉ kiểm tra rủi ro dạng Có/Không, các sếp có thể yêu cầu OpenAI chấm điểm theo thang điểm 100 để lọc ra top nhà cung cấp tốt nhất.

### 📌 Kết luận
Với workflow n8n tích hợp OpenAI và Slack này, quy trình thẩm định nhà cung cấp thủ công chậm chạp sẽ được thay thế bằng một hệ thống thông minh, tự động hóa hoàn toàn. Hãy triển khai ngay hôm nay để tối ưu hóa hiệu suất vận hành cho đội ngũ của mình các sếp nhé!