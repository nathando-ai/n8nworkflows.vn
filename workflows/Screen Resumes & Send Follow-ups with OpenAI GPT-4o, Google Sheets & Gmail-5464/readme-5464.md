---
title: "🚀 Tự Động Học Sàng Lọc CV & Gửi Lời Theo Dõi với OpenAI GPT-4o, Google Sheets & Gmail (Không Cần Code)"
description: "Workflow tự động hóa sàng lọc CV bằng AI, đánh giá phù hợp với yêu cầu công việc, lưu kết quả vào Google Sheets và gửi thông báo tự động qua Gmail. Giúp tiết kiệm thời gian tuyển dụng lên tới 80% và giảm thiểu sai sót trong quá trình sàng lọc."
slug: "tieu-dong-hoa-sang-loc-cv-voi-openai-gpt-4o"
tags: [n8n, automation, hr, ai-summarization, openai-gpt-4o, google-sheets, gmail]
keywords: [tự động hóa tuyển dụng, sàng lọc cv bằng ai, n8n workflow hr, openai gpt-4o tự động hóa, google sheets tuyển dụng, gửi thông báo tuyển dụng tự động]
---

# 🚀 **Tự Động Học Sàng Lọc CV & Gửi Lời Theo Dõi với AI (Không Cần Code)**

### **Nỗi Đau Của Các Sếp Trong Quá Trình Tuyển Dụng**
Tuyển dụng là một quá trình tốn thời gian và dễ mắc sai sót. Các sếp thường phải:
- **Đọc hàng trăm CV** để tìm ứng viên phù hợp.
- **Phân loại thủ công** giữa những ứng viên "Proceed" và "Reject".
- **Gửi thông báo theo dõi** một cách không đồng bộ, dễ quên hoặc trễ hạn.
- **Lưu trữ kết quả** một cách rối loạn, khó theo dõi sau này.

**Workflow này giải quyết tất cả những vấn đề trên bằng AI + Tự Động Hóa 100% Không Cần Code!**

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: AI tự động sàng lọc CV trong vài giây thay vì mất hàng giờ.
- **Đánh giá chính xác**: Dựa trên tiêu chí cụ thể của công ty, không bị chủ quan.
- **Tự động gửi thông báo**: Ứng viên được thông báo kết quả ngay lập tức qua email.
- **Lưu trữ hệ thống**: Kết quả được ghi vào Google Sheets, dễ theo dõi và báo cáo.
- **Cá nhân hóa thông báo**: AI tự động tạo tiêu đề và nội dung email phù hợp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối Google Sheets và Gmail API).
2. **Tài khoản OpenAI** (để sử dụng GPT-4o và GPT-4.1-mini).
3. **File Google Sheets** với 2 sheet: **"Accepted"** và **"Rejected"**, có cấu trúc header chuẩn.
4. **Email chính thức** của công ty (để gửi thông báo tự động).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/5464](https://n8n.io/workflows/5464) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **11 node** chính, các sếp cần chú ý cấu hình các node sau:

##### **A. Node "On form submission" (formTrigger)**
- **Mục đích**: Tạo form cho ứng viên upload CV (PDF), tên và email.
- **Lưu ý**:
  - Đảm bảo form có các trường: **File (PDF)**, **Tên**, **Email**, và tùy chọn **Số điện thoại**.
  - **Không cần chỉnh sửa** node này, chỉ cần kích hoạt form sau khi import.

##### **B. Node "Extracting CV data" (extractFromFile)**
- **Mục đích**: Trích xuất dữ liệu từ file PDF.
- **Lưu ý**:
  - Node này tự động đọc file PDF được upload.
  - **Không cần cấu hình thêm**, chỉ cần đảm bảo file CV là PDF.

##### **C. Node "Text Classifier" (textClassifier)**
- **Mục đích**: Phân loại nội dung CV (nếu cần).
- **Lưu ý**:
  - Nếu không cần phân loại, có thể **bỏ qua** hoặc đặt lại thành **pass-through**.

##### **D. Node "OpenAI 4o" & "OpenAI Chat Model" (lmChatOpenAi)**
- **Mục đích**: Sử dụng AI để đánh giá CV dựa trên tiêu chí của công ty.
- **Lưu ý**:
  - **Thay đổi prompt trong AI Agent** (node **"Screening & Evaluating Resume's"**) theo hướng dẫn dưới đây:
    ```plaintext
    • COMPANY NAME → "Tên Công Ty Của Các Sếp" (ví dụ: "TechCorp")
    • ROLE NAME → "Vị Trí Tuyển" (ví dụ: "Chuyên Viên Phát Triển Phần Mềm")
    • ROLE DESCRIPTION → "Mô tả ngắn gọn công việc" (ví dụ: "Làm việc với các công nghệ cloud và microservices")
    • CRITERIA 1–5 → Tiêu chí bắt buộc (ví dụ: "5 năm kinh nghiệm, bằng đại học CS, biết Python, Docker, AWS")
    • QUESTIONS 1–5 → Câu hỏi phù hợp với văn hóa công ty (ví dụ: "Có kinh nghiệm trong ngành công nghệ thông tin không?")
    • THRESHOLD → Điểm tối thiểu để "Proceed" (ví dụ: 75/100)
    ```
  - **Cấu hình API Key**:
    - Đi đến **Credentials** → **OpenAI API** → Nhập **API Key** từ tài khoản OpenAI.

##### **E. Node "Google Sheets" (googleSheets)**
- **Mục đích**: Lưu kết quả sàng lọc vào Google Sheets.
- **Lưu ý**:
  - **Chọn credentials**: `googleSheetsOAuth2Api`.
  - **Chọn sheet**: Chọn sheet **"Accepted"** hoặc **"Rejected"** tùy theo kết quả.
  - **Header phải chuẩn**: Các cột nên bao gồm: `Tên`, `Email`, `Điểm`, `Lý Do`, `Trạng Thái`.

##### **F. Node "Gmail" (gmail)**
- **Mục đích**: Gửi thông báo kết quả cho ứng viên.
- **Lưu ý**:
  - **Chọn credentials**: `gmailOAuth2`.
  - **Cấu hình email mẫu**:
    - **Tiêu đề**: AI tự động tạo (hoặc thay đổi thành tiêu đề cố định).
    - **Nội dung**: Có thể chỉnh sửa để cá nhân hóa (ví dụ: `Xin chào [Tên], CV của bạn đã được đánh giá...`).
  - **Đảm bảo email gửi từ tài khoản chính thức** của công ty.

##### **G. Node "Structured Output Parser1" (outputParserStructured)**
- **Mục đích**: Định dạng kết quả AI thành cấu trúc dễ đọc.
- **Lưu ý**:
  - **Không cần chỉnh sửa** nếu đã cấu hình prompt trong AI Agent đúng.

##### **H. Node "Screening & Evaluating Resume's" (agent)**
- **Mục đích**: AI tự động đánh giá CV dựa trên tiêu chí của công ty.
- **Lưu ý**:
  - **Prompt mẫu**:
    ```plaintext
    Bạn là một chuyên gia tuyển dụng của [Tên Công Ty]. Hãy đánh giá CV của ứng viên dựa trên tiêu chí sau:
    1. Kinh nghiệm: [Tiêu chí]
    2. Kỹ năng: [Tiêu chí]
    3. Giáo dục: [Tiêu chí]
    4. Trải nghiệm công việc: [Tiêu chí]
    5. Phù hợp văn hóa công ty: [Tiêu chí]

    Đánh giá điểm từ 0-100 và trả lời:
    - Điểm tổng: [Số]
    - Lý do: [Chi tiết]
    - Kết quả: Proceed/Reject
    ```

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run**:
   - Upload một CV mẫu (PDF) vào form.
   - Kiểm tra kết quả trong Google Sheets và email.
2. **Bật Active**:
   - Chuyển trạng thái workflow từ **Inactive** sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Sử dụng node **Slack Webhook** hoặc **Telegram Bot** để thông báo kết quả cho team tuyển dụng.
2. **Lưu Log Chi Tiết**:
   - Thêm node **StickyNote** để ghi lại các thay đổi hoặc lỗi phát sinh.
3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **Google Sheets + Gmail** để tự động gửi báo cáo tổng hợp hàng tuần.
4. **Cải Tiến Prompt AI**:
   - Nếu AI đánh giá không chính xác, hãy **cập nhật tiêu chí** trong prompt và test lại.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc mòn mỏi là sàng lọc CV thủ công. Với AI GPT-4o, Google Sheets và Gmail, quá trình tuyển dụng trở nên **chính xác, tự động và chuyên nghiệp**.

**Hãy áp dụng ngay và tiết kiệm thời gian lên tới 80% trong tuyển dụng!** 🚀

---
**Bạn có bất kỳ câu hỏi nào về cách cấu hình chi tiết? Hãy để lại comment bên dưới!** 👇