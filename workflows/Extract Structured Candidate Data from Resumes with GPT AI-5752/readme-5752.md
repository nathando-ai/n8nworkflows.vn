---
title: "🚀 Trích xuất thông tin CV ứng viên tự động với AI Agent và OpenAI trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động đọc CV dưới mọi định dạng (PDF, DOCX, TXT...), dùng GPT-4o-mini trích xuất dữ liệu có cấu trúc và lưu thẳng vào Google Sheets."
slug: "trich-xuat-thong-tin-cv-ung-vien-ai-n8n"
tags: [n8n, automation, no-code, hr-automation, openai, google-sheets]
keywords: [n8n workflow, trích xuất CV tự động, AI Agent n8n, OpenAI GPT-4o-mini, quản lý hồ sơ ứng viên, Google Sheets automation]
---

# 🚀 Trích xuất thông tin CV ứng viên tự động với AI Agent và OpenAI trong n8n

Các sếp làm nhân sự (HR) chắc chắn hiểu được cảm giác "ngợp thở" mỗi mùa tuyển dụng khi phải nhận hàng trăm CV đủ các định dạng: PDF, HTML, TXT, Excel... Việc phải đọc thủ công từng hồ sơ, copy thông tin như họ tên, kinh nghiệm, kỹ năng vào file Excel hay Google Sheets vừa tốn thời gian, vừa dễ xảy ra sai sót.

Được thiết kế bởi **Angel Menendez** (Staff Developer Advocate tại n8n), workflow này sẽ giải quyết triệt để bài toán trên. Bằng cách kết hợp sức mạnh của **AI Agent**, **OpenAI (GPT-4o-mini)** và các node trích xuất dữ liệu tệp, workflow giúp tự động hóa 100% quy trình đọc CV, bóc tách dữ liệu theo cấu trúc chuẩn và lưu trữ gọn gàng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa đa định dạng:** Hỗ trợ trích xuất văn bản từ hàng loạt định dạng tệp phổ biến như PDF, HTML, CSV, TXT, XML, ODS, XLS, RTF.
- **Cấu trúc hóa dữ liệu thông minh:** Sử dụng AI Agent kết hợp `Structured Output Parser` và mô hình `OpenAI Chat Model1` (GPT-4o-mini) để trả về các trường thông tin đồng nhất (Họ tên, email, kỹ năng, kinh nghiệm...).
- **Đồng bộ thời gian thực:** Tự động ghi nhận hoặc cập nhật dữ liệu ứng viên trực tiếp vào `Google Sheets` thông qua thao tác `appendOrUpdate`.
- **Tiết kiệm 90% thời gian:** Giải phóng đội ngũ tuyển dụng khỏi các tác vụ thủ công lặp đi lặp lại để tập trung vào việc phỏng vấn và đánh giá con người.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** Đã cài đặt n8n (phiên bản cloud hoặc self-hosted).
- **OpenAI API Key:** Tài khoản OpenAI có sẵn số dư để gọi API mô hình `gpt-4o-mini`.
- **Google Sheets:** Một file Google Sheet được thiết kế sẵn các cột tiêu đề để lưu thông tin ứng viên.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ kho lưu trữ n8n (Link gốc: [n8n.io/workflows/5752](https://n8n.io/workflows/5752)) và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình kỹ lưỡng các node sau:

- **When chat message received (`chatTrigger`) & Switch (`switch`):** Điểm khởi đầu nhận yêu cầu hoặc file CV tải lên từ người dùng. Node `Switch` sẽ phân loại định dạng tệp để chuyển đến nhánh trích xuất phù hợp.
- **Bộ các node trích xuất file (`Extract from PDF`, `Extract from HTML`, `Extract from TXT`, v.v.):** Đảm bảo các node này nhận đúng tệp đầu vào từ người dùng để bóc tách văn bản thô (raw text) chính xác nhất.
- **OpenAI Chat Model1 (`lmChatOpenAi`):** Cần kết nối `openAiApi` credentials của các sếp và kiểm tra tham số model đang chọn là `gpt-4o-mini` để tối ưu chi phí và tốc độ.
- **AI Agent1 (`agent`) & Structured Output Parser (`outputParserStructured`):** Cấu hình prompt cho AI Agent biết rõ cần trích xuất những trường dữ liệu nào từ nội dung CV (ví dụ: Full Name, Email, Phone, Skills, Years of Experience). Output Parser sẽ ép AI trả về đúng định dạng JSON yêu cầu.
- **Google Sheets (`googleSheets`):** 
  - Chọn tài khoản Google Sheets thông qua `googleSheetsOAuth2Api`.
  - Chọn file Google Sheet và Sheet Name cụ thể của các sếp.
  - Thiết lập operation là `appendOrUpdate` và ánh xạ (map) các trường dữ liệu từ output của AI vào đúng các cột trong bảng tính.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** với một file CV mẫu (PDF hoặc TXT) để kiểm tra luồng chạy từ đầu đến cuối.
- Kiểm tra lại Google Sheets xem dữ liệu đã được điền chính xác hay chưa.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để chính thức đưa workflow vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Thêm node Slack hoặc Telegram ở cuối workflow để bắn thông báo ngay về nhóm tuyển dụng mỗi khi có một ứng viên mới nộp CV thành công.
- **Lọc ứng viên tự động:** Thêm một bước điều kiện (If node) dựa trên kết quả trả về của AI để tự động gắn nhãn "Đạt" hoặc "Cần xem xét" dựa trên tiêu chí kinh nghiệm tối thiểu.
- **Gửi email phản hồi tự động:** Kết hợp node Gmail để tự động gửi email cảm ơn ứng viên đã nộp hồ sơ kèm theo thông tin tiếp theo trong quy trình.

### 📌 Kết luận
Workflow **Extract Structured Candidate Data from Resumes with GPT AI** là một "vũ khí tối tân" giúp các doanh nghiệp tối ưu hóa quy trình tuyển dụng thời đại số. Chỉ với vài bước cài đặt đơn giản trên n8n, các sếp đã có thể tự động hóa hoàn toàn khâu xử lý hồ sơ rườm rà. Chúc các sếp cài đặt thành công và xây dựng được đội ngũ nhân sự xuất sắc!