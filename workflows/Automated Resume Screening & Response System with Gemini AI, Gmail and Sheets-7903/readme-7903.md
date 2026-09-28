---
title: "🚀 Tự Động Sàng Lọc CV & Gửi Email Phản Hồi Với Gemini AI"
description: "Giải pháp tự động hóa quy trình tuyển dụng: AI đọc CV PDF, chấm điểm, phân loại ứng viên và gửi email phản hồi tự động qua Gmail, đồng bộ dữ liệu vào Google Sheets."
slug: "tu-dong-sang-loc-cv-gemini-ai"
tags: [n8n, automation, no-code, ai-recruitment, gemini-ai]
keywords: [n8n workflow, tự động hóa tuyển dụng, sàng lọc CV AI, gemini ai, gmail automation]
---

# 🚀 Tự Động Sàng Lọc CV & Gửi Email Phản Hồi Với Gemini AI

Trong bối cảnh thị trường lao động cạnh tranh gay gắt, các bộ phận nhân sự thường xuyên phải đối mặt với "núi" hồ sơ ứng tuyển. Việc đọc từng file PDF, đánh giá năng lực, phân loại ứng viên và soạn email phản hồi thủ công không chỉ tốn thời gian mà còn dễ dẫn đến sai sót hoặc phản hồi chậm trễ, gây mất thiện cảm với ứng viên tiềm năng.

Workflow này chính là "trợ lý AI" đắc lực giúp các sếp giải quyết triệt để nỗi đau đó. Bằng cách kết hợp sức mạnh của **Google Gemini AI**, **Gmail** và **Google Sheets**, quy trình tuyển dụng sẽ được tự động hóa 100%: Từ lúc ứng viên nộp đơn qua Form, AI sẽ tự động trích xuất nội dung CV, chấm điểm, đưa ra quyết định (Nhận/Từ chối), gửi email phản hồi cá nhân hóa và ghi log kết quả vào bảng tính. Tất cả diễn ra trong vài giây, không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi có lượng lớn ứng viên nộp đơn cùng lúc, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian khổng lồ:** Loại bỏ hoàn toàn công đoạn đọc CV thủ công và soạn email phản hồi hàng loạt.
- **Đánh giá nhất quán & khách quan:** AI chấm điểm dựa trên tiêu chí đã định nghĩa, tránh thiên kiến chủ quan của con người.
- **Trải nghiệm ứng viên tốt hơn:** Ứng viên nhận được phản hồi nhanh chóng (thường là tức thì) với nội dung được cá nhân hóa bởi AI.
- **Dữ liệu tập trung & dễ phân tích:** Toàn bộ hồ sơ, điểm số và trạng thái ứng viên được lưu tự động vào Google Sheets, thuận tiện cho việc báo cáo và lọc dữ liệu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị:
1. **Tài khoản Google Gemini:** Tạo API Key tại [Google AI Studio](https://aistudio.google.com/apikey).
2. **Tài khoản Gmail:** Để kết nối OAuth2 cho việc gửi email.
3. **Tài khoản Google Sheets:** Tạo một bảng tính mới với các cột: `Name`, `Job`, `Score`, `Status`, `Email`, `Email Status`.
4. **Tài khoản n8n:** Có quyền tạo và kích hoạt workflow.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Đăng nhập vào n8n.
2. Chọn **Import from File** hoặc **Import from URL**.
3. Tải file JSON của workflow này lên hoặc dán link gốc từ n8n.io.
4. Sau khi import, workflow sẽ hiển thị đầy đủ các node: Form Trigger, Extract File, AI Agent, Gmail, Google Sheets.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Dưới đây là các node quan trọng cần cấu hình chi tiết:

**1. Node: `On form submission` (Form Trigger)**
- Đây là điểm bắt đầu. Các sếp cần chỉnh sửa các trường (fields) trong form cho phù hợp với vị trí tuyển dụng.
- Các trường mặc định: `Name`, `Email Address`, `Job Role`, `Resume` (file upload).
- **Lưu ý:** Đảm bảo trường `Resume` được cấu hình để chấp nhận file `.pdf`.

**2. Node: `Extract from File`**
- Node này đã được cấu hình sẵn để xử lý file PDF.
- Không cần chỉnh sửa nhiều, nhưng hãy đảm bảo output của node này được kết nối đúng vào input của `AI Agent`.

**3. Node: `AI Agent` (Trái tim của workflow)**
- **Credentials:** Chọn hoặc tạo credentials cho **Google Gemini** (Google 2.5 Flash).
- **System Message:** Đây là phần quan trọng nhất. Các sếp cần chỉnh sửa prompt để định nghĩa rõ tiêu chí tuyển dụng.
  - *Ví dụ:* "Bạn là một chuyên gia tuyển dụng. Hãy đánh giá CV dựa trên kinh nghiệm, kỹ năng và độ phù hợp với vị trí [Tên Vị Trí]. Chấm điểm từ 1-10. Nếu điểm > 7, trạng thái là 'Accepted', ngược lại là 'Rejected'. Hãy viết email phản hồi lịch sự, chuyên nghiệp."
- **Tools:** Đảm bảo node `Information Extractor` được gắn vào đây để AI có thể truy xuất dữ liệu cấu trúc từ CV.

**4. Node: `Information Extractor`**
- Node này giúp AI chuyển đổi văn bản CV thô thành dữ liệu có cấu trúc (JSON).
- Kiểm tra schema output để đảm bảo các trường như `skills`, `experience`, `education` được trích xuất chính xác.

**5. Node: `Gmail`**
- **Credentials:** Kết nối tài khoản Gmail của công ty qua OAuth2.
- **To:** Chọn trường `Email` từ dữ liệu đầu vào (ứng viên).
- **Subject & Message:** Tham chiếu đến output của `AI Agent` để lấy tiêu đề và nội dung email đã được AI soạn thảo.

**6. Node: `Google Sheets`**
- **Credentials:** Kết nối tài khoản Google Sheets.
- **Operation:** Chọn `Append` (Thêm dòng mới).
- **Sheet Name:** Chọn bảng tính đã tạo ở bước chuẩn bị.
- **Mapping:** Ánh xạ các trường dữ liệu từ output của AI Agent vào các cột tương ứng trong Sheet (Name, Job, Score, Status, Email, Email Status).

#### 3. Kích hoạt ⚡️
1. **Test Run:** Nhấn nút **Execute Workflow** và điền dữ liệu mẫu vào Form Trigger (tên, email, tải lên một file CV PDF mẫu).
2. Kiểm tra xem AI có chấm điểm đúng không, email có được gửi không và dữ liệu có vào Sheet không.
3. Nếu mọi thứ ổn, bật công tắc **Active** ở góc trên bên phải để workflow bắt đầu chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thêm node `Slack` hoặc `Telegram` ngay sau node `Google Sheets` để gửi thông báo cho team tuyển dụng khi có ứng viên đạt điểm cao (Accepted).
- **Đa dạng định dạng file:** Hiện tại workflow chỉ xử lý PDF. Các sếp có thể cân nhắc thêm logic để xử lý cả file `.docx` nếu cần, hoặc yêu cầu ứng viên chuyển đổi sang PDF trước khi nộp.
- **Phân loại nhiều vị trí:** Thay vì một prompt chung, các sếp có thể dùng node `Switch` hoặc `IF` để chọn prompt đánh giá khác nhau tùy thuộc vào trường `Job Role` mà ứng viên chọn trong Form.
- **Lưu trữ CV:** Thêm node `Google Drive` để tự động lưu file CV gốc vào thư mục riêng theo tên ứng viên, giúp dễ dàng truy xuất lại hồ sơ sau này.

### 📌 Kết luận
Việc tự động hóa quy trình sàng lọc CV không chỉ giúp bộ phận nhân sự thoát khỏi những công việc lặp đi lặp lại mà còn nâng cao chất lượng tuyển dụng nhờ sự đánh giá nhất quán của AI. Với workflow này, các sếp có thể tập trung vào các ứng viên tiềm năng nhất và xây dựng trải nghiệm ứng viên chuyên nghiệp hơn. Hãy import workflow, cấu hình prompt theo tiêu chí của công ty và bắt đầu tiết kiệm hàng chục giờ làm việc mỗi tuần ngay hôm nay! 🚀