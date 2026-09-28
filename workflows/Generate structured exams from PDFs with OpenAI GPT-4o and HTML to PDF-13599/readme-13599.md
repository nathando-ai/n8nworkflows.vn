---
title: "🚀 Tự động tạo bộ đề thi chuẩn hóa từ file PDF với OpenAI GPT-4o và n8n"
description: "Hướng dẫn chi tiết cách xây dựng hệ thống tự động biến tài liệu PDF thành đề thi trắc nghiệm, tự luận và đáp án chi tiết bằng AI, xuất file PDF chuyên nghiệp."
slug: "tu-dong-tao-de-thi-tu-pdf-voi-openai-gpt-4o-n8n"
tags: [n8n, automation, ai, openai, pdf-processing, telegram]
keywords: [n8n workflow, tạo đề thi tự động, pdf to exam, openai gpt-4o n8n, automation no-code, xử lý pdf n8n]
---

# 🚀 Biến tài liệu PDF thành bộ đề thi chuẩn hóa tự động với AI

Các thầy cô giáo, các trung tâm đào tạo hay đội ngũ nhân sự thường xuyên phải tốn hàng giờ đồng hồ để đọc tài liệu, chắt lọc kiến thức và biên soạn đề thi (cả trắc nghiệm lẫn tự luận kèm đáp án)? Việc làm thủ công này cực kỳ tốn thời gian và dễ xảy ra sai sót.

Giải pháp là đây! Workflow **ExamForge AI** trên n8n sẽ giúp các sếp tự động hóa 100% quy trình này: chỉ cần tải file PDF tài liệu lên, hệ thống sẽ tự động bóc tách văn bản, kiểm tra token an toàn, gọi OpenAI GPT-4o để phân tích và tạo ra bộ đề thi cấu trúc rõ ràng, sau đó xuất ra file PDF riêng biệt cho đề thi và đáp án, thậm chí gửi thẳng qua Telegram. Không cần viết code phức tạp, tự động hóa hoàn toàn!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, xử lý các file PDF nặng mà không bị gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- ⏱️ **Tiết kiệm 95% thời gian:** Giảm từ vài tiếng biên soạn xuống chỉ còn vài giây xử lý tự động.
- 🎯 **Chính xác & Tùy biến linh hoạt:** Tự động tạo số lượng câu hỏi trắc nghiệm (MCQ) và tự luận (Essay) theo đúng yêu cầu, phân loại độ khó (Easy/Medium/Hard) và ngôn ngữ tùy chỉnh.
- 📄 **Xuất file chuyên nghiệp:** Tự động định dạng HTML thành 2 file PDF riêng biệt: một bản Đề thi sạch sẽ và một bản Đáp án chi tiết.
- 📲 **Tích hợp linh hoạt:** Nhận yêu cầu qua Webhook và trả kết quả trực tiếp hoặc gửi qua Telegram Bot tiện lợi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **OpenAI Account:** Cần có API Key đang hoạt động và có số dư để gọi mô hình (khuyên dùng GPT-4o).
- **PDF Munk / HTML-to-PDF API:** Tài khoản và API Key để chuyển đổi HTML sang PDF (`htmlcsstopdfApi`).
- **Telegram Bot (Tùy chọn):** Nếu muốn gửi file PDF kết quả trực tiếp qua Telegram.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy toàn bộ nội dung JSON và dán trực tiếp vào giao diện n8n Editor của mình. Workflow bao gồm 16 nodes được sắp xếp logic từ khâu nhận file, xử lý, gọi AI đến xuất file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần chú ý cấu hình các node cốt lõi sau:

- **Webhook Node:** Đóng vai trò nhận request `POST` với định dạng `multipart/form-data`. Các tham số bắt buộc truyền lên gồm:
  - `file`: File tài liệu định dạng PDF.
  - `mcq_count`: Số lượng câu hỏi trắc nghiệm mong muốn.
  - `essay_count`: Số lượng câu hỏi tự luận.
  - `difficulty`: Mức độ khó (`easy` / `medium` / `hard`).
  - `language`: Ngôn ngữ đầu ra (ví dụ: `Vietnamese`, `English`).

- **Validate Parameter & PDF / Code Nodes:** Các node này thực hiện việc kiểm tra kích thước file (mặc định dưới 5MB), làm sạch văn bản (`Clean Text`), ước tính dung lượng token (`Length Estimation Layer`) và nhánh điều kiện (`Condition Valid`, `Validate Token > 8.000`) để tránh vượt quá giới hạn của AI.

- **Message a model (OpenAI Node):** 
  - Chọn credentials `openAiApi` và điền OpenAI API Key của các sếp.
  - Chọn model xử lý (khuyên dùng `gpt-4o`). Node này sẽ nhận văn bản đã làm sạch và trả về cấu trúc JSON chứa bộ câu hỏi chuẩn xác.

- **Convert HTML to PDF - Exam & Convert HTML to PDF - Answer:**
  - Sử dụng dịch vụ chuyển đổi HTML sang PDF (`htmlcsstopdf`).
  - Cần cấu hình credentials `htmlcsstopdfApi` bằng API Key tương ứng. Các node này nhận dữ liệu từ JSON được parse và tạo ra 2 file PDF riêng biệt cho đề thi và đáp án.

- **Send a text message / Telegram Nodes (Tùy chọn):**
  - Cấu hình `telegramApi` với Bot Token từ BotFather và Chat ID của sếp để nhận thông báo và file PDF hoàn chỉnh ngay trên điện thoại.

#### 3. Kích hoạt ⚡️
- Thực hiện test run bằng cách gửi một request `POST` mẫu thông qua Postman hoặc lệnh `curl`:
```bash
curl -X POST https://your-n8n-domain/webhook/cd37ea38-9ff5-4518-a17d-5f443ef4ad3b \
  -F "file=@document.pdf" \
  -F "mcq_count=10" \
  -F "essay_count=2" \
  -F "difficulty=medium" \
  -F "language=Vietnamese"
```
- Kiểm tra kết quả trả về, sau đó gạt công tắc **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ Cloud Storage:** Thay vì chỉ gửi qua Telegram hoặc trả về Webhook, các sếp có thể gắn thêm node **Google Drive** hoặc **Supabase/S3** để lưu trữ tự động mọi đề thi được tạo ra.
- **Bổ sung thông báo Slack/Email:** Tích hợp thêm node gửi thông báo qua Slack hoặc Gmail cho đội ngũ giáo viên khi có một bộ đề mới được biên soạn xong.
- **Tinh chỉnh Prompt AI:** Tại node gọi OpenAI, các sếp có thể điều chỉnh System Prompt để AI định dạng câu hỏi theo đúng form chuẩn của trường hoặc công ty mình (thêm phần giải thích chi tiết cho đáp án chẳng hạn).

### 📌 Kết luận
Workflow **ExamForge AI** là một mảnh ghép tuyệt vời giúp tự động hóa hoàn toàn quy trình số hóa tài liệu thành đề thi chất lượng cao. Chúc các sếp cài đặt thành công và tiết kiệm được thật nhiều thời gian cho công việc chuyên môn! Nếu gặp khó khăn trong quá trình cấu hình, đừng ngần ngại triển khai ngay trên VPS riêng để tối ưu hiệu năng nhé.