---
title: "🚀 Trích xuất báo cáo y tế & Tạo lời khuyên sức khỏe AI với Mistral AI & GPT-4"
description: "Tự động hóa toàn bộ quy trình đọc file PDF/ảnh xét nghiệm y tế từ Google Drive, trích xuất dữ liệu bằng Mistral AI, phân tích chỉ số bất thường và tạo lời khuyên sức khỏe cá nhân hóa bằng GPT-4 lưu thẳng vào Google Sheets."
slug: "trich-xuat-bao-cao-y-te-ai-mistral-gpt4"
tags: [n8n, automation, ai, mistral-ai, openai, google-drive, google-sheets, healthcare]
keywords: [n8n workflow, trích xuất báo cáo y tế, ai health advice, mistral ai ocr, gpt-4 medical data, tự động hóa google drive sheets]
useCase: "Tự động hóa đọc kết quả khám sức khỏe, phân tích chỉ số và đưa ra lời khuyên y tế thông minh."
---

# 🚀 Trích xuất báo cáo y tế & Tạo lời khuyên sức khỏe AI với Mistral AI & GPT-4

Các sếp trong ngành y tế, wellness hay đơn giản là những ai thường xuyên phải xử lý hàng đống kết quả xét nghiệm, phiếu khám bệnh chắc chắn đã ngán ngẩm cảnh gõ tay thủ công từng chỉ số, so sánh khoảng tham chiếu (reference range) xem có bất thường không, rồi lại loay hoay tra cứu cách cải thiện. Công việc này vừa tốn thời gian, dễ sai sót lại chẳng thể scale nổi!

Giải pháp đây rồi! Workflow n8n mạnh mẽ này sẽ tự động hóa **100%** quy trình từ lúc các sếp ném một file PDF hoặc ảnh chụp kết quả xét nghiệm lên Google Drive cho đến khi có ngay một bảng tổng hợp đầy đủ chỉ số, đánh dấu rõ ràng các chỉ số bất thường (Out-of-Range) và tự động "bơm" ra lời khuyên ăn uống, tập luyện cực kỳ cá nhân hóa từ AI. Không cần code, hoạt động mượt mà 24/7!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn OCR & Trích xuất:** Đọc trọn vẹn file PDF hoặc ảnh chụp kết quả xét nghiệm nhờ công nghệ OCR đỉnh cao của Mistral AI.
- **Phân tích thông minh với GPT-4:** Bóc tách dữ liệu thành các trường chuẩn hóa (tên xét nghiệm, kết quả, đơn vị, khoảng tham chiếu) và chuyển hóa thành JSON tinh gọn.
- **Cảnh báo bất thường tự động:** Tự động đối chiếu kết quả với khoảng chuẩn, lọc ra các chỉ số vượt ngưỡng để các sếp có chiến lược can thiệp kịp thời.
- **Lời khuyên sức khỏe cá nhân hóa:** GPT-4 tự động viết lời khuyên về chế độ ăn uống, lối sống dựa trên độ tuổi, giới tính và tình trạng bệnh lý cụ thể của từng kết quả.
- **Lưu trữ gọn gàng:** Tự động đồng bộ toàn bộ kết quả vào tab "All Values" và các chỉ số bất thường vào tab "Out of Range Values" trên Google Sheets để tiện theo dõi.
:::

### 📦 Các thành phần chính trong Workflow
Workflow bao gồm 13 nodes hoạt động nhịp nhàng:
- **Google Drive Trigger:** Theo dõi thư mục chỉ định, phát hiện ngay khi có file PDF/ảnh mới được tải lên.
- **Download file & Check if PDF or Image & If:** Tải file về và phân nhánh xử lý tùy thuộc vào định dạng tài liệu.
- **Extract from PDF & Extract from Image (Mistral AI):** Đọc văn bản và giữ cấu trúc tài liệu bằng OCR của Mistral.
- **Combine page Markdown & Extract Medical Data (AI - OpenAI):** Ghép nối các trang và dùng GPT-4 bóc tách dữ liệu cấu trúc dạng JSON.
- **Parse AI output to one-per-row & Out-of-Range Detection & Advice Fields (Code):** Chuyển đổi mảng JSON thành các item riêng lẻ, so sánh giá trị và phát hiện bất thường.
- **General Health Advice (AI - OpenAI):** Tạo lời khuyên sức khỏe cá nhân hóa cho các chỉ số ngoài khoảng tham chiếu.
- **Merge AI Response Back (Code):** Ghép nối lời khuyên AI với dữ liệu xét nghiệm gốc.
- **Save All Test Results & Save Out-of-Range Results (Google Sheets):** Ghi dữ liệu đồng bộ vào các sheet tương ứng.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã chạy phiên bản n8n (Cloud hoặc Self-hosted).
- **Tài khoản Google Drive & Google Sheets:** Kết nối OAuth2 để theo dõi thư mục và ghi dữ liệu.
- **Mistral AI API Key:** Dành cho các node trích xuất OCR từ PDF và hình ảnh.
- **OpenAI API Key (GPT-4 access):** Bắt buộc để trích xuất dữ liệu thông minh và sinh lời khuyên y tế.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow này.
- Mở n8n Editor, chọn **Add workflow** -> Nhấn tổ hợp `Ctrl + V` (hoặc `Cmd + V`) để dán toàn bộ workflow lên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `Upload pdf/jpeg file to Google drive` (Google Drive Trigger):** Chọn tài khoản Google Drive và trỏ tới thư mục đích (Folder ID) nơi các sếp sẽ upload các file xét nghiệm đầu vào.
- **Node `Extract from PDF` & `Extract from Image` (Mistral AI):** Cấu hình Credential bằng Mistral AI API Key của các sếp.
- **Node `Extract Medical Data (AI)` & `General Health Advice (AI)` (OpenAI):** Thêm OpenAI Credentials và đảm bảo tài khoản có quyền truy cập mô hình GPT-4.
- **Node `Save Out-of-Range Results` & `Save All Test Results` (Google Sheets):** 
  - Kết nối tài khoản Google Sheets.
  - Chuẩn bị một file Google Sheet có sẵn 2 tab (Worksheet): một tab tên **"All Values"** và một tab tên **"Out of Range Values"** với các cột tương ứng để nhận dữ liệu.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** trên từng node hoặc dùng nút **Execute Workflow** để thử nghiệm với một file PDF/ảnh mẫu.
- Sau khi kiểm tra dữ liệu đổ về Google Sheets chính xác, gạt công tắc sang chế độ **Active** để hệ thống tự động hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack Bot:** Thêm một node Telegram hoặc Slack ngay sau node phát hiện bất thường để bắn tin nhắn cảnh báo ngay lập tức cho bác sĩ hoặc bệnh nhân khi có chỉ số "đỏ".
- **Gửi Email tự động:** Kết hợp Gmail node để tự động gửi bản báo cáo sức khỏe kèm lời khuyên của AI trực tiếp cho khách hàng dưới dạng file đẹp mắt.
- **Lưu trữ file processed:** Thêm bước di chuyển file sau khi xử lý xong sang một thư mục "Archived" trên Google Drive để tránh trùng lặp.

### 📌 Kết luận
Workflow này là một cỗ máy tự động hóa đỉnh cao giúp tiết kiệm hàng tá thời gian cho các cơ sở y tế, phòng khám hoặc các cá nhân muốn số hóa dữ liệu sức khỏe. Hãy triển khai ngay hôm nay để trải nghiệm sức mạnh thực sự của AI trong y tế cùng n8n các sếp nhé!