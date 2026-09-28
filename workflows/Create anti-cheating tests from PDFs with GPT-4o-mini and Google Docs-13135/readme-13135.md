---
title: "🚀 Tự Động Hoàn Thành Bài Thi Trắc Nghiệm Phòng Chống Tràn Lợi Từ PDF Với GPT-4o-mini & Google Docs"
description: "Workflow tự động hóa chuyển đổi nội dung PDF thành bài thi trắc nghiệm 10 câu (5 nhóm A, 5 nhóm B) với AI, tạo tài liệu Google Docs và gửi email thông báo - tiết kiệm 60 phút công việc thủ công mỗi lần."
slug: "tieu-dong-hoan-thanh-bai-thi-phong-chong-tran-loi-tu-pdf"
tags: [n8n, automation, no-code, ai-gpt-4o-mini, google-docs, google-drive, email-automation, content-creation]
keywords: [tự động hóa bài thi trắc nghiệm, n8n workflow pdf, tạo bài thi từ pdf, gpt-4o-mini tự động, google docs automation, phòng chống tràn lợi]
---

# 🚀 **Tự Động Hoàn Thành Bài Thi Trắc Nghiệm Phòng Chống Tràn Lợi Từ PDF Với AI**

### **Giải pháp cho giáo viên, nhà tuyển dụng và doanh nghiệp**
Hiện nay, việc tạo bài thi trắc nghiệm từ tài liệu PDF thủ công không chỉ tốn thời gian (thường 30-60 phút/lần) mà còn dễ mắc sai sót về logic hoặc trùng lặp câu hỏi. Workflow này **tự động hóa toàn bộ quy trình** bằng AI GPT-4o-mini, tạo ra **10 câu hỏi đa dạng** (5 nhóm A, 5 nhóm B) từ nội dung PDF, xuất bản dưới dạng tài liệu Google Docs và gửi email thông báo cho bạn - **chỉ trong 60 giây!**

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 60 phút/lần** so với cách làm thủ công.
- **Câu hỏi đa dạng** (không trùng lặp) do AI phân tích ngữ cảnh từ PDF.
- **Tài liệu sẵn sàng sử dụng** với định dạng chuyên nghiệp trên Google Docs.
- **Chia sẻ dễ dàng** qua liên kết Google Drive.
- **Gửi email tự động** với thông tin chi tiết.
- **Chi phí thấp** (~$0.002/1 lần sử dụng).
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** với API Key (để sử dụng GPT-4o-mini).
2. **Tài khoản Google** với quyền:
   - **Google Docs** (để tạo và chỉnh sửa tài liệu).
   - **Google Drive** (để chia sẻ liên kết).
   - **Gmail** (để gửi email thông báo).
3. **File PDF mẫu** (để test trước khi áp dụng thực tế).
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/13135](https://n8n.io/workflows/13135) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/13135) và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **10 node** chính, các sếp cần chú ý cấu hình sau:

##### **📌 Node "Form Trigger" (Bắt đầu)**
- **Tên form:** Tùy chỉnh theo nhu cầu (ví dụ: "Upload PDF để tạo bài thi").
- **Fields cần thêm:**
  - **File Upload** (để người dùng chọn PDF).
  - **Email (optional)** (nếu muốn gửi kết quả về email cụ thể).

##### **📌 Node "Extract PDF" (Trích xuất nội dung)**
- **Không cần chỉnh sửa** (n8n tự động trích xuất toàn bộ văn bản từ PDF).

##### **📌 Node "AI Generate" (GPT-4o-mini tạo câu hỏi)**
- **Prompt mẫu (cần chỉnh sửa):**
  ```javascript
  const pdfText = $input.all().pdfText;
  return {
    prompt: `Tạo 10 câu hỏi trắc nghiệm (5 nhóm A, 5 nhóm B) từ nội dung sau:
  ${pdfText}
  Yêu cầu:
  1. Mỗi câu hỏi có 4 lựa chọn (A, B, C, D).
  2. Nhóm A và B phải khác nhau.
  3. Tránh trùng lặp câu hỏi.
  4. Cấu trúc câu hỏi phải rõ ràng và phù hợp với nội dung PDF.
  5. Đáp án đúng là A.
  Định dạng output theo JSON:
  {
    "groupA": ["Câu 1: ...", "Câu 2: ..."],
    "groupB": ["Câu 1: ...", "Câu 2: ..."]
  }`
  };
  ```
- **Model:** Chọn **GPT-4o-mini** (đảm bảo API Key đã cấu hình ở **Credentials**).

##### **📌 Node "Format Test" (Code - Xử lý dữ liệu)**
- **Mã JavaScript (không cần chỉnh sửa nếu dùng mặc định):**
  ```javascript
  const questions = JSON.parse($input.all().openAi.output.text);
  return {
    groupA: questions.groupA,
    groupB: questions.groupB
  };
  ```

##### **📌 Node "Create Doc" (Tạo tài liệu Google Docs)**
- **Chọn tài liệu mẫu:**
  - Nếu chưa có, **tạo một Google Doc mới** và sao chép liên kết.
  - Điền vào **Document ID** trong node này.
- **Tham số cần thiết:**
  - **Title:** "Bài thi tự động từ PDF - [Tên tài liệu]".
  - **Content:** Sử dụng **HTML template** để định dạng (có thể chỉnh sửa ở **Code Node** trước đó).

##### **📌 Node "Share Doc" (Chia sẻ liên kết)**
- **Chọn quyền chia sẻ:**
  - **"Anyone with the link"** (ai có liên kết cũng xem được).
  - **"Specific people"** (nếu muốn giới hạn).

##### **📌 Node "Insert Group A/B" (Chèn câu hỏi)**
- **Không cần chỉnh sửa** (n8n tự động chèn câu hỏi vào Google Docs theo nhóm).

##### **📌 Node "Send Email" (Gửi thông báo)**
- **Nội dung email mẫu (cần chỉnh sửa):**
  ```plaintext
  Chào [Tên người dùng],

  Bài thi đã được tạo thành công từ PDF của bạn! Để xem kết quả, vui lòng truy cập liên kết sau:
  [Liên kết Google Docs]

  Trân trọng,
  [Tên hệ thống]
  ```
- **Chọn tài khoản Gmail** đã cấu hình ở **Credentials**.

---
#### **3. Kích hoạt ⚡️**
1. **Test run với file PDF mẫu** để kiểm tra kết quả.
2. **Bật Active workflow** sau khi xác nhận mọi thứ hoạt động ổn định.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
- **Gửi email tự động đến nhiều người:** Sử dụng **Google Sheets** để lưu danh sách email và kết hợp với node **gmail** để gửi bulk.
- **Lưu log sử dụng:** Thêm node **StickyNote** để ghi lại lịch sử tạo bài thi.
- **Tích hợp Slack/Telegram:** Sử dụng node **Slack Webhook** để thông báo kết quả ngay khi hoàn thành.
- **Tự động lưu vào Google Drive:** Chỉnh node **Google Drive** để lưu bản sao của tài liệu vào thư mục cụ thể.
- **Cập nhật định kỳ:** Sử dụng **n8n Cron Trigger** để tự động tạo bài thi định kỳ (ví dụ: hàng tuần).
:::

---
### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công tạo bài thi, đồng thời **đảm bảo chất lượng cao** nhờ AI GPT-4o-mini. **Chỉ cần 60 giây**, bạn đã có một bài thi trắc nghiệm chuyên nghiệp, sẵn sàng chia sẻ và sử dụng.

👉 **Bắt đầu ngay!** Import workflow và thử với file PDF đầu tiên của mình. Nếu có vấn đề, hãy **cấu hình lại node "AI Generate"** để phù hợp với yêu cầu cụ thể của bạn.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Chúc các sếp thành công với tự động hóa!** 🚀