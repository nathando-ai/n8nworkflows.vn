---
title: "🚀 Phân tích và Tóm tắt tài liệu PDF phân cấp tự động với Mistral AI & OneDrive"
description: "Hướng dẫn xây dựng workflow n8n tự động quét thư mục và thư mục con trên Microsoft OneDrive, trích xuất văn bản PDF và sử dụng Mistral AI để tóm tắt, trích xuất thông tin."
slug: "phan-tich-tom-tat-pdf-mistral-ai-onedrive"
tags: [n8n, automation, no-code, Mistral AI, OneDrive, AI Summarization]
keywords: [n8n workflow, tóm tắt pdf tự động, mistral ai onedrive, trích xuất văn bản pdf, ai document extraction]
---

# 🚀 Phân tích và Tóm tắt tài liệu PDF phân cấp tự động với Mistral AI & OneDrive

Các sếp có đang gặp khó khăn trong việc quản lý hàng ngàn tài liệu PDF nằm rải rác trong các thư mục và thư mục con (nested folders) trên Microsoft OneDrive? Việc phải mở từng file, đọc hiểu, tổng hợp thông tin và phân loại thủ công tiêu tốn rất nhiều thời gian và dễ xảy ra sai sót. 

Giải pháp gì cho bài toán này? Workflow n8n siêu việt mang tên **"Nested PDF Analysis with Mistral AI & OneDrive for Document Summarization"** (với 41 nodes được tối ưu hóa) sẽ tự động hóa toàn bộ quy trình: Từ việc quét thư mục, lọc file PDF, tải xuống, trích xuất nội dung cho đến việc sử dụng sức mạnh của **Mistral AI** để phân tích, tạo bản tóm tắt, tìm kiếm các phát hiện quan trọng và lưu trữ dữ liệu một cách gọn gàng!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Quét các cấu trúc thư mục phức tạp lên đến 8 cấp độ trên OneDrive mà không cần can thiệp thủ công.
- **Trích xuất thông minh:** Tự động nhận diện file PDF, bóc tách văn bản và giao cho Mistral AI (`mistral-small-latest`) xử lý.
- **Structured Data Chuẩn Xác:** Nhận kết quả trả về theo định dạng cấu trúc rõ ràng (Summary, Key_Findings, Scope, Date, Location, File_Name, Path).
- **Lưu trữ tập trung:** Tự động đồng bộ và lưu trữ kết quả phân tích vào n8n Data Table (hoặc dễ dàng mở rộng ra Google Sheets/Excel).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (phiên bản hỗ trợ LangChain nodes).
- **Microsoft OneDrive Account:** Tài khoản kết nối với n8n để truy cập các thư mục chứa tài liệu.
- **Mistral AI API Key:** Tài khoản và API key từ Mistral AI để vận hành các mô hình ngôn ngữ lớn (LLM Chat Model & Agents).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cấp hoặc copy toàn bộ mã JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp (Ctrl+V) vào màn hình canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần lưu ý cấu hình kỹ các node sau:

- **Node `Search for Main Folder` (Microsoft OneDrive):** 
  - Nhập chính xác tên thư mục chính (Main Folder) chứa các thư mục con và tài liệu PDF của các sếp. 
  - *Mẹo:* Đảm bảo tên thư mục là **duy nhất** để OneDrive không bị nhầm lẫn với các thư mục có tên tương tự.
- **Cấu trúc thư mục (8 layers deep):** 
  - Workflow được thiết kế sẵn với các chuỗi `Get items in a folder` và `If PDF` để duyệt sâu tối đa 8 lớp thư mục. Nếu cấu trúc của các sếp sâu hơn, hãy bổ sung thêm các node tương ứng.
- **Node `Mistral Cloud Chat Model`:** 
  - Chọn credentials của Mistral AI và đảm bảo model đang trỏ tới `mistral-small-latest` (hoặc model phù hợp khác).
- **Node `Insert row` (Data Table):** 
  - Hãy tạo trước một n8n Data Table với các cột tiêu chuẩn: `Summary`, `Key_Findings`, `Scope`, `Date`, `Location`, `File_Name`, và `Path`.
  - Kiểm tra lại phần mapping dữ liệu tại node này để chắc chắn các thông tin từ AI trả về được đẩy đúng cột.
- **Các node AI Agent (`Overview`, `Document Information`) và Output Parser:** 
  - Xem xét lại cấu trúc prompt và `Structured Output Parser` nếu các sếp muốn trích xuất thêm các trường thông tin đặc thù khác (ví dụ: chi phí, tên đối tác, trạng thái hợp đồng...).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (`Execute Workflow`) với một vài file mẫu để kiểm tra log và dữ liệu trả về trong Data Table.
- Sau khi kiểm tra mọi thứ hoạt động hoàn hảo, hãy bật công tắc **Active** để workflow chạy tự động theo lịch trình của `Schedule Trigger1`.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng lưu trữ:** Ngoài n8n Data Table, các sếp có thể thêm node Google Sheets hoặc Microsoft Excel để xuất bản báo cáo ra file trực quan cho sếp lớn xem.
- **Thông báo tự động:** Kết hợp thêm node Slack hoặc Telegram để gửi thông báo ngay lập tức về kênh chat mỗi khi có một tài liệu mới được phân tích xong.
- **Xử lý tài liệu khác:** Tại khu vực tài liệu non-PDF (được lưu ý trên canvas), các sếp có thể nhân bản quy trình để xử lý thêm các định dạng như Word (.docx) hay Excel (.xlsx).

### 📌 Kết luận
Workflow "Nested PDF Analysis with Mistral AI & OneDrive" là một trợ lý ảo cực kỳ mạnh mẽ giúp tự động hóa toàn bộ khâu đọc hiểu và tổng hợp tài liệu doanh nghiệp. Hãy áp dụng ngay hôm nay để giải phóng sức lao động và tối ưu hóa năng suất làm việc của đội ngũ các sếp nhé!