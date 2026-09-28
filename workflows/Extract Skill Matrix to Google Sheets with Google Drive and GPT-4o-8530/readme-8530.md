---
title: "🚀 Tự động trích xuất Ma trận Kỹ năng từ CV PDF vào Google Sheets với AI và GPT-4o"
description: "Hướng dẫn xây dựng workflow n8n tự động quét CV từ Google Drive, đọc file PDF, phân tích kỹ năng bằng Azure OpenAI GPT-4o-mini và lưu trữ ma trận kỹ năng vào Google Sheets."
slug: "trich-xuat-ma-tran-ky-nang-cv-google-sheets-gpt-4o"
tags: [n8n, automation, ai-agent, google-drive, google-sheets, gpt-4o, hr-automation]
keywords: [n8n workflow, tự động hóa tuyển dụng, trích xuất cv ai, google sheets automation, azure openai n8n]
---

# 🚀 Tự động trích xuất Ma trận Kỹ năng từ CV ứng viên vào Google Sheets bằng AI

Các nhà tuyển dụng và HR manager chắc chắn đã quá ngán ngẩm cảnh phải mở từng file CV PDF, đọc lướt qua hàng chục trang giấy để đánh giá kỹ năng của ứng viên, sau đó lại cặm cụi copy-paste từng dòng vào Excel để làm bảng ma trận kỹ năng (Skill Matrix). Việc này vừa tốn thời gian, dễ sai sót lại vừa làm gián đoạn các công việc nhân sự chiến lược khác.

Workflow n8n này sinh ra để giải quyết triệt để nỗi đau đó! Bằng cách kết hợp sức mạnh của **Google Drive**, **AI Agent (Azure OpenAI GPT-4o-mini)** và **Google Sheets**, toàn bộ quy trình từ quét CV, trích xuất văn bản, phân tích kỹ năng chuyên môn đến lưu trữ dữ liệu được tự động hóa 100% không cần code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Quét toàn bộ thư mục CV trên Google Drive mà không cần thao tác thủ công.
- **Phân tích thông minh bằng AI:** GPT-4o-mini tự động bóc tách các kỹ năng công nghệ (React, Python, AWS, Docker...) và chấm điểm mức độ thành thạo (thang điểm 1-5), cùng số năm kinh nghiệm.
- **Lọc dữ liệu thông minh:** Tự động lọc ra các kỹ năng từ mức độ trung bình trở lên (level > 2) trước khi lưu vào database.
- **Đồng bộ hóa tức thì:** Cập nhật kết quả gọn gàng vào Google Sheets, giúp HR dễ dàng sàng lọc và so sánh năng lực ứng viên.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Drive Account:** Đã tạo sẵn thư mục chứa CV (ví dụ: `Resume_store`).
- **Google Sheets Account:** Đã tạo sẵn bảng tính lưu ma trận kỹ năng (ví dụ: `Resume store` / `Sheet2`).
- **Azure OpenAI API Key:** Tài khoản Azure OpenAI có quyền gọi mô hình `gpt-4o-mini`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ nguồn cung cấp và dán trực tiếp vào giao diện n8n Editor (sử dụng phím tắt `Ctrl + V` hoặc `Cmd + V` trong không gian làm việc của n8n).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Search Resume (Google Drive):**
  - Kết nối tài khoản Google Drive (`googleDriveOAuth2Api`).
  - Chọn thư mục đích chứa CV (mặc định trong hướng dẫn là thư mục **`Resume_store`**).
- **Download Resume (Google Drive):**
  - Sử dụng chung credentials Google Drive để tải file PDF dựa trên ID file được tìm thấy ở bước trên.
- **Extract content from File:**
  - Cấu hình operation là **`pdf`** để trích xuất toàn bộ văn bản từ các tệp tin CV định dạng PDF.
- **Azure OpenAI Chat Model & Skill Analyser (AI Agent):**
  - Kết nối credentials `azureOpenAiApi`.
  - Chọn model chính xác là **`gpt-4o-mini`**.
  - Kiểm tra System Instructions của Agent để đảm bảo AI tập trung vào đúng các công nghệ mong muốn (React, Node.js, Python, Java, AWS, v.v.) và trả về đúng định dạng JSON.
- **Parse Structured JSON (Code Node):**
  - Kiểm tra đoạn mã JavaScript xử lý và lọc dữ liệu (chỉ lấy các kỹ năng có proficiency level > 2) để đảm bảo dữ liệu đầu ra khớp với cấu trúc bảng tính.
- **Update sheet with skill matrix (Google Sheets):**
  - Kết nối tài khoản Google Sheets (`googleSheetsOAuth2Api`).
  - Trỏ tới file Spreadsheet **`Resume store`** và Tab **`Sheet2`**.
  - Cấu hình operation là **`appendOrUpdate`** dựa trên cột `Name` để tránh trùng lặp dữ liệu ứng viên.

#### 3. Kích hoạt ⚡️
- Nhấn nút **`Execute workflow`** thủ công (thông qua node `When clicking ‘Execute workflow’`) để test thử với một vài file CV mẫu.
- Kiểm tra kết quả trên Google Sheets xem dữ liệu đã được điền chính xác chưa.
- Sau khi test thành công, bật công tắc **Active** để sẵn sàng sử dụng.

### ✍️ Mẹo & gợi ý nâng cao
- **Thay đổi Trigger:** Thay vì dùng Manual Trigger, các sếp có thể chuyển sang **Google Drive Trigger** để mỗi khi có ứng viên mới tải CV lên thư mục, workflow sẽ tự động chạy ngay lập tức.
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack vào cuối workflow để gửi thông báo tóm tắt về kết quả phân tích CV ngay vào nhóm tuyển dụng của công ty.
- **Lưu log lỗi:** Kết nối nhánh lỗi (Error Handling) để nếu file CV bị lỗi font hoặc hỏng định dạng, hệ thống sẽ ghi log lại thay vì dừng đột ngột.

### 📌 Kết luận
Việc tự động hóa quy trình sàng lọc CV và xây dựng ma trận kỹ năng bằng n8n và GPT-4o sẽ giúp đội ngũ HR tiết kiệm hàng chục giờ làm việc mỗi tuần, đồng thời đảm bảo tính khách quan và chính xác trong khâu đánh giá năng lực ứng viên. Hãy áp dụng ngay vào doanh nghiệp của các sếp!