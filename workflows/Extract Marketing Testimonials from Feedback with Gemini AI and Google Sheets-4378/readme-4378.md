---
title: "🚀 Tự động trích xuất Testimonial Marketing từ Feedback khách hàng bằng Gemini AI & Google Sheets"
description: "Biến feedback thô của khách hàng thành những câu testimonial cảm xúc, chất lượng cao để làm marketing bằng n8n, Google Sheets và Google Gemini AI."
slug: "trich-xuat-testimonial-marketing-gemini-ai-google-sheets"
tags: [n8n, automation, ai, marketing, google-sheets, gemini, gmail]
keywords: [n8n workflow, trích xuất testimonial, google sheets trigger, gemini ai, marketing automation]
---

# 🚀 Tự động trích xuất Testimonial Marketing từ Feedback khách hàng bằng Gemini AI & Google Sheets

Các sếp có bao giờ cảm thấy mệt mỏi khi phải đọc qua hàng trăm dòng feedback, khảo sát (survey) của khách hàng để tìm ra những câu khen ngợi hay, sắc bén dùng làm đánh giá (testimonial) cho chiến dịch marketing chưa? Việc làm thủ công này không chỉ tốn thời gian mà còn dễ bỏ sót những "viên kim cương" ẩn giấu trong câu chữ của khách hàng.

Đừng lo, workflow n8n được thiết kế bởi chuyên gia **Yaron Been** này sẽ tự động hóa 100% quy trình đó cho các sếp! Hệ thống sẽ lắng nghe feedback mới, dùng sức mạnh của **Google Gemini AI** để chắt lọc, tinh chỉnh thành một đoạn quote cảm xúc ngắn gọn, lưu lại vào Google Sheets và ngay lập tức gửi thông báo qua Gmail.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần đọc thủ công từng feedback dài dòng của khách hàng.
- **Content Marketing chất lượng:** Luôn có sẵn nguồn testimonial đắt giá, đánh trúng tâm lý khách hàng để đưa lên Landing Page, Facebook Ads hay Social Media.
- **Quy trình liền mạch:** Tự động ghi nhận vào Google Sheets và báo cáo ngay qua Gmail để đội ngũ marketing kịp thời nắm bắt.
- **Hoạt động 24/7:** Chạy ngầm tự động mỗi khi có khách hàng điền form hoặc thêm dòng mới vào bảng tính.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn:
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- File **Google Sheets** chứa dữ liệu feedback của khách hàng (có Google Sheets Trigger).
- **Google Gemini API Key** để kết nối với mô hình ngôn ngữ AI.
- Tài khoản **Gmail** để nhận thông báo khi có testimonial mới được trích xuất.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ thư viện n8n (Link gốc: [n8n.io/workflows/4378](https://n8n.io/workflows/4378)) và import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các node quan trọng sau đây:

- **Google Sheets Trigger**: 
  - Chọn tài khoản Google Credentials.
  - Trỏ đến file Spreadsheet chứa dữ liệu phản hồi của khách hàng và chọn đúng Sheet Name/ID. Node này sẽ làm nhiệm vụ "lắng nghe" khi có dòng dữ liệu mới được thêm vào.
- **Basic LLM Chain & Google Gemini Chat Model**:
  - Thiết lập Gemini API Credentials.
  - Tại node LLM Chain, viết prompt hướng dẫn AI cách trích xuất (ví dụ: *"Hãy đóng vai một chuyên gia marketing, đọc đoạn feedback sau và trích xuất một câu testimonial ngắn gọn, đầy cảm xúc, làm nổi bật giá trị sản phẩm..."*).
- **Google Sheets (appendOrUpdate)**:
  - Chọn lại file Google Sheet lưu kết quả.
  - Map các trường dữ liệu đã được Gemini xử lý vào các cột tương ứng trên bảng tính (ví dụ: cột Testimonial, cột Trạng thái...).
- **Gmail**:
  - Kết nối tài khoản Gmail cá nhân hoặc của công ty.
  - Cấu hình nội dung email gửi đi (bao gồm feedback gốc và đoạn testimonial đã được AI tinh chỉnh đẹp mắt).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách thêm một dòng dữ liệu mẫu vào Google Sheets để kiểm tra xem AI đã xử lý và Gmail có nhận được thông báo hay không.
- Nếu mọi thứ chạy mượt mà, gạt công tắc sang **Active** để hệ thống tự động làm việc.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack / Telegram:** Thay vì chỉ nhận email qua Gmail, các sếp có thể nối thêm node Slack hoặc Telegram để bắn thông báo thẳng vào nhóm chat của đội ngũ Marketing, giúp anh em dễ dàng duyệt và lấy content đi đăng ngay.
- **Lọc điểm số (Rating Filter):** Thêm một node IF trước khi gọi AI để chỉ kích hoạt trích xuất testimonial với những feedback có đánh giá từ 4-5 sao, tránh lãng phí token cho những phản hồi tiêu cực.
- **Tự động đăng mạng xã hội:** Kết nối tiếp đoạn kết quả với các node như Buffer, Facebook, hoặc Twitter để tự động lên lịch đăng tải những câu testimonial hay nhất lên các kênh social.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ lợi hại cho các mác-két-tinh (Marketer) muốn tối ưu hóa hiệu suất làm việc bằng AI. Hãy cài đặt ngay hôm nay để biến những feedback thô sơ thành tài nguyên marketing giá trị!