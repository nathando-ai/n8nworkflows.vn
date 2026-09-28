---
title: "🚀 Tạo bộ câu hỏi trắc nghiệm tương tác từ tài liệu PDF với Google Gemini và n8n"
description: "Tự động hóa hoàn toàn quy trình đọc sách giáo khoa/tài liệu PDF, dùng AI tạo câu hỏi trắc nghiệm (MCQ) và gửi qua Gmail dưới dạng trang web tương tác."
slug: "tao-bo-cau-hoi-trac-nghiem-tu-dong-tu-pdf-voi-n8n-gemini"
tags: [n8n, automation, ai, google-gemini, gmail, pdf-extraction, edtech]
keywords: [n8n workflow, tạo trắc nghiệm tự động, google gemini ai, trắc nghiệm từ pdf, tự động hóa n8n]
---

# 🚀 Tự Động Hóa Tạo Bộ Câu Hỏi Trắc Nghiệm (MCQ) Tương Tác Từ File PDF Bằng AI

Các sếp làm trong lĩnh vực giáo dục, đào tạo nội bộ hay tạo nội dung học tập chắc chắn hiểu cảm giác "mướt mồ hôi" khi phải ngồi đọc hàng trăm trang tài liệu PDF để soạn câu hỏi trắc nghiệm (MCQ). Việc này không chỉ tốn hàng giờ đồng hồ mà còn dễ nhàm chán và thiếu tính tương tác cho người học.

Đừng lo, workflow n8n cực đỉnh này sẽ giải quyết trọn gói bài toán đó! Chỉ với vài thao tác điền form đơn giản, hệ thống sẽ tự động trích xuất nội dung tài liệu, nhờ **Google Gemini AI** soạn thảo bộ câu hỏi chuẩn xác, biến nó thành một trang web trắc nghiệm tương tác đẹp mắt rồi tự động gửi thẳng vào email của người dùng. Tất cả diễn ra tự động 100% không cần đụng tay viết code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Biến tài liệu PDF dài dặc thành bộ câu hỏi trắc nghiệm chỉ trong tích tắc.
- **Trải nghiệm học tập hiện đại:** Tự động tạo trang web HTML tương tác có sẵn hiệu ứng đúng/sai, giải thích chi tiết và khóa đáp án.
- **Cá nhân hóa tự động:** Gửi trực tiếp link bài kiểm tra qua Gmail kèm tên riêng của từng học viên/người dùng.
- **Không cần hosting phức tạp:** Tích hợp dịch vụ UploadToURL giúp đưa trang web trắc nghiệm lên mạng ngay lập tức mà không cần cấu hình server.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Google Gemini API Key** (cho node Google Gemini Chat Model).
- **Tài khoản Gmail** (để cấu hình node gửi email qua OAuth2).
- **Tài khoản UploadToURL** (để lấy API Key upload file HTML lên mạng).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng mã JSON của workflow này từ kho lưu trữ n8n (Template ID: 15512) và import trực tiếp vào n8n Editor của mình bằng tính năng **Import from File** hoặc dán trực tiếp chuỗi JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 7 nodes chính được liên kết chặt chẽ với nhau. Các sếp cần cấu hình kỹ các điểm sau:

- **Get-Details (`formTrigger`):** Điểm khởi đầu hiển thị form cho người dùng nhập liệu (Tên, Email, File PDF, Số lượng câu hỏi: 10/20/30, và Độ khó: Easy/Medium/Hard).
- **Extract from File (`extractFromFile`):** Node tự động nhận file PDF từ form, sử dụng công cụ đọc PDF tích hợp sẵn để chuyển toàn bộ file thành dạng văn bản thuần túy (plain text).
- **Generate-MCQ (`chainLlm`) & Google Gemini Chat Model (`lmChatGoogleGemini`):** Nơi AI phát huy sức mạnh. Cấu hình credentials cho Gemini API, node sẽ tiếp nhận nội dung text từ file PDF cùng các thông số số lượng câu hỏi, độ khó từ form để yêu cầu AI tạo ra cấu trúc JSON các câu hỏi trắc nghiệm chuẩn xác.
- **Template (`code`):** Node xử lý mã JavaScript để:
  - Parse chuỗi JSON trả về từ AI thành JavaScript object an toàn.
  - Cá nhân hóa tên người dùng vào giao diện bài kiểm tra.
  - Xây dựng bố cục HTML hoàn chỉnh gồm: câu hỏi, các tùy chọn (radio buttons), đáp án kèm giải thích.
  - Viết sẵn mã JavaScript tương tác trực tiếp trên trang (khi người dùng chọn đáp án sẽ hiển thị ngay đúng/sai và khóa câu trả lời).
- **Upload a File (`uploadToUrl`):** Nhận file HTML được tạo từ code node và đẩy lên internet thông qua UploadToURL để tạo ngay một public shareable link (link xem trực tiếp không cần setup hosting).
- **Send a Message (`gmail`):** Node cuối cùng sử dụng tài khoản Gmail kết nối OAuth2 để gửi email thân thiện đến địa chỉ của người dùng, tự động chèn tên và đường link trang web trắc nghiệm vừa tạo.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test workflow**) bằng cách điền form mẫu để kiểm tra toàn bộ luồng từ việc đọc PDF đến nhận email.
- Sau khi kiểm tra mọi thứ chạy mượt mà, gạt công tắc sang trạng thái **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu lịch sử vào Google Sheets:** Thêm một node Google Sheets ngay sau form trigger hoặc trước khi gửi email để lưu lại thông tin người làm bài và điểm số/tài liệu họ đã chọn.
- **Thông báo qua Telegram/Slack:** Thêm node thông báo cho Admin mỗi khi có một bộ câu hỏi mới được tạo thành công.
- **Tùy biến giao diện HTML:** Chỉnh sửa phần CSS trong node `Template` để trang trắc nghiệm mang màu sắc nhận diện thương hiệu riêng của doanh nghiệp.

### 📌 Kết luận
Việc ứng dụng AI và tự động hóa vào giáo dục hay đào tạo nội bộ chưa bao giờ dễ dàng đến thế. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình ra đề kiểm tra chỉ trong vài nốt nhạc. Hãy cài đặt ngay lên hệ thống n8n của các sếp để tối ưu hóa năng suất làm việc nhé!