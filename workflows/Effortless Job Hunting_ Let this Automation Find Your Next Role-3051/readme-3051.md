---
title: "🚀 Tự động hóa tìm việc làm với AI: Quét CV và gom Job xịn siêu tốc"
description: "Hướng dẫn sử dụng n8n workflow để tự động đọc CV từ Google Drive, phân tích bằng AI OpenAI và tìm kiếm việc làm phù hợp đẩy thẳng vào Google Sheets."
slug: "tu-dong-hoa-tim-viec-lam-voi-ai-n8n"
tags: [n8n, automation, ai, openai, hr, google-drive, google-sheets]
keywords: [n8n workflow, tự động tìm việc, AI job hunting, phân tích CV tự động, google sheets automation]
use strict: true
---

# 🚀 Tự động hóa tìm việc làm với AI: Quét CV và gom Job xịn siêu tốc

Các sếp có đang mệt mỏi mỗi khi phải lướt hàng trăm trang tuyển dụng, lọc từng job phù hợp với kỹ năng của mình, rồi lại hì hục copy-paste vào Excel? Việc tìm kiếm công việc mơ ước đôi khi lại tốn thời gian y như một công việc chính thức vậy!

Đừng lo, bài toán đó sẽ được giải quyết triệt để với workflow n8n cực đỉnh mang tên **"Effortless Job Hunting"** do tác giả *Mateo Fiorito Rocha* xây dựng. Giải pháp này giúp các sếp tự động hóa 100% quy trình: Đọc CV từ Google Drive $\rightarrow$ Dùng AI phân tích năng lực $\rightarrow$ Truy vấn các cơ hội việc làm phù hợp $\rightarrow$ Tổng hợp và phân loại gọn gàng vào Google Sheets. Không cần code, chỉ cần setup một lần và để hệ thống tự chạy!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải thủ công tìm việc trên LinkedIn, VietnamWorks hay TopCV.
- **Cá nhân hóa thông minh:** AI (OpenAI) trực tiếp phân tích CV của các sếp để tìm ra "tọa độ" kỹ năng chuẩn xác nhất, từ đó đề xuất đúng việc, đúng tầm.
- **Quản lý khoa học:** Toàn bộ tin tuyển dụng được gom sạch sẽ, phân loại bài bản vào một file Google Sheets duy nhất.
- **Chủ động hoàn toàn:** Kích hoạt thủ công bất cứ lúc nào các sếp muốn cập nhật các cơ hội việc làm mới nhất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Drive Credentials:** Để lưu trữ và tải xuống file CV định dạng PDF của các sếp.
- **OpenAI API Key:** Dùng cho node AI phân tích nội dung CV.
- **HTTP API / Job Board API (nếu có):** Để node `Find Suitable Job Offers` truy vấn dữ liệu việc làm.
- **Google Sheets Credentials:** Để lưu danh sách các công việc được tìm thấy.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này, vào giao diện n8n chọn **Add workflow** -> Nhấn tổ hợp `Ctrl + V` (hoặc `Cmd + V`) để dán trực tiếp vào màn hình Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình kỹ các node trọng điểm sau:
- **On clicking 'execute' (`manualTrigger`):** Điểm khởi đầu để kích hoạt quy trình quét việc làm bất cứ khi nào các sếp muốn.
- **Download Resume (PDF File) (`googleDrive`):** Kết nối tài khoản Google Drive của các sếp và trỏ tới file CV (PDF) chính chủ.
- **Read PDF (`readPDF`):** Đọc toàn bộ nội dung văn bản bên trong file CV vừa tải về.
- **Analyse Resume (`openAi`):** Chọn credentials OpenAI. Tại đây, cấu hình prompt để AI trỏ đúng vào các kỹ năng cốt lõi, kinh nghiệm và vị trí mong muốn của các sếp từ nội dung CV.
- **Find Suitable Job Offers (`httpRequest`):** Cấu hình Endpoint API tuyển dụng (hoặc trang web tích hợp) để gửi yêu cầu tìm kiếm dựa trên từ khóa mà AI vừa trích xuất từ CV.
- **Filter Relevant Information & Organise the Job Posts (`splitOut`):** Các node này giúp tách nhỏ danh sách dữ liệu thô thành từng dòng công việc riêng biệt để dễ dàng xử lý.
- **Upload Job Posts Organised in a Spreadsheet (`googleSheets`):** Kết nối tài khoản Google, chọn file Spreadsheet và Mapping chính xác các trường dữ liệu (Tên công ty, Vị trí, Link ứng tuyển, Mức lương...) vào các cột tương ứng.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để test thử nghiệm với dữ liệu CV thực tế của các sếp.
- Kiểm tra lại kết quả trên Google Sheets xem dữ liệu đã đổ về chuẩn chỉnh chưa.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa định kỳ:** Thay vì dùng `Manual Trigger`, các sếp có thể đổi sang node `Schedule Trigger` để n8n tự động quét việc làm mới mỗi sáng lúc 8:00 AM.
- **Nhận thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để mỗi khi có job mới xịn sò, hệ thống sẽ bắn tin nhắn trực tiếp vào điện thoại cho các sếp ngay lập tức.
- **Lưu log lỗi:** Thiết lập thêm nhánh xử lý lỗi (Error Trigger) để đề phòng trường hợp API tuyển dụng phản hồi chậm hoặc lỗi mạng.

### 📌 Kết luận
Việc tìm việc chưa bao giờ "nhàn" và thông minh đến thế! Hãy áp dụng ngay workflow này để tối ưu hóa hành trình sự nghiệp của mình, để AI làm việc nặng nhọc thay cho các sếp nhé! Chúc các sếp sớm tìm được công việc như ý!