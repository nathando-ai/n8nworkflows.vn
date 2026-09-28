---
title: "🚀 Tự động trích xuất hóa đơn từ Gmail vào Google Sheets bằng GPT-4o AI"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa toàn bộ quy trình đọc email hóa đơn, dùng AI trích xuất thông tin chi tiết và lưu trữ vào Google Sheets, Google Drive."
slug: "tu-dong-trich-xuat-hoa-don-tu-gmail-vao-google-sheets-gpt-4o"
tags: [n8n, automation, ai, openai, google-sheets, finance]
keywords: [n8n workflow, trích xuất hóa đơn tự động, gpt-4o invoice extraction, google sheets automation, gmail trigger n8n]
---

# 🚀 Tự động trích xuất hóa đơn từ Gmail vào Google Sheets bằng GPT-4o AI

Các sếp có đang mệt mỏi với cảnh cuối tháng phải ngồi mở từng email, tải file PDF hóa đơn về, rồi lúi húi gõ lại từng con số, tên công ty, tiền thuế, hạn thanh toán vào file Excel không? Việc này không chỉ tốn hàng giờ đồng hồ mà còn rất dễ xảy ra sai sót nhập liệu (nhầm số, thiếu hóa đơn). 

Đừng lo, bài viết này sẽ hướng dẫn các sếp setup một siêu workflow **n8n** tự động hóa 100% quy trình này bằng sức mạnh của **GPT-4o (OpenAI AI Agent)**. Workflow sẽ tự động bắt email có chứa hóa đơn từ Gmail, trích xuất dữ liệu, cấu trúc lại thông tin, tạo Google Sheets và sắp xếp gọn gàng trên Google Drive mà không cần một giọt mồ hôi thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh nhập liệu thủ công (Data Entry) cho kế toán và đội ngũ tài chính.
- **Độ chính xác cao:** GPT-4o phân tích thông minh hơn 25+ trường thông tin (Số hóa đơn, ngày tháng, tên công ty, line items, thuế, hạn thanh toán...).
- **Tự động hóa hoàn toàn:** Từ lúc khách hàng/nhà cung cấp gửi email đến khi lưu vào Google Sheets & Google Drive chỉ diễn ra trong vài giây.
- **Hoạt động 24/7:** Chạy ngầm liên tục không mệt mỏi, sẵn sàng bão hòa lượng hóa đơn lớn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** (Self-hosted hoặc n8n Cloud).
- **Gmail Account:** Cần cấp quyền OAuth2 để n8n đọc email và tải tệp đính kèm.
- **OpenAI API Key:** Để sử dụng model `gpt-4o-mini` hoặc `gpt-4o` phân tích văn bản hóa đơn.
- **Google Sheets & Google Drive Accounts:** Cấp quyền OAuth2 để tạo file, ghi dữ liệu và sắp xếp thư mục.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (hoặc tải file JSON từ n8n.io/workflows/4376) và Paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 9 nodes chính hoạt động nhịp nhàng. Các sếp cần chú ý cấu hình kỹ các node sau:

- **Node `Gmail Trigger`**: 
  - Cần tạo một Gmail Label cụ thể (ví dụ: `Invoice Processing`).
  - Gắn nhãn này cho các email chứa hóa đơn đầu vào. Node này sẽ quét email mới liên tục mỗi phút dựa trên nhãn đã chọn.
- **Node `Attachment Verification` (Filter)**: 
  - Đảm bảo logic kiểm tra định dạng tệp đính kèm phải là file PDF (`.pdf`) trước khi chuyển sang bước tiếp theo.
- **Node `Extract Invoice data` (Extract From File)**: 
  - Chọn Operation là `PDF` để chuyển đổi nội dung tệp hóa đơn PDF thành văn bản dạng text thô.
- **Node `OpenAI Chat Model` & `Invoice AI Agent` (@n8n/n8n-nodes-langchain)**: 
  - Kết nối Credentials OpenAI API Key.
  - Chọn model `gpt-4o-mini` (hoặc `gpt-4o`).
  - Đảm bảo system prompt trong Agent yêu cầu AI trả về cấu trúc JSON rõ ràng với các trường: Tên công ty, Mã số thuế, Số hóa đơn, Ngày tháng, Danh sách mặt hàng (Line items), Tổng tiền, Tiền thuế...
- **Node `Create blank spreadsheet` & `Final Spreadsheet with Invoice data` (Google Sheets)**: 
  - Cấu hình tài khoản Google Sheets OAuth2.
  - Đảm bảo node tạo file và node append dữ liệu khớp với cấu trúc JSON mà AI Agent trả về.
- **Node `Move spreadsheet in invoice folder` (Google Drive)**: 
  - Chọn ID của thư mục đích trên Google Drive (Folder chứa hóa đơn) để các file Google Sheets mới tạo tự động nhảy vào đó cho gọn gàng.

#### 3. Kích hoạt ⚡️
- Gửi thử 1 email có file PDF hóa đơn kèm nhãn `Invoice Processing` tới Gmail của các sếp.
- Bấm **Execute Workflow** để test thủ công và kiểm tra kết quả trả về trong Google Sheets.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng thông báo:** Nối thêm node Telegram hoặc Slack vào cuối workflow để gửi thông báo real-time mỗi khi có hóa đơn mới được xử lý thành công.
- **Tích hợp phần mềm kế toán:** Có thể đẩy tiếp dữ liệu từ Google Sheets sang các phần mềm như MISA, QuickBooks hoặc Xero qua API.
- **Xử lý hóa đơn ảnh chụp (Scan):** Nếu nhà cung cấp gửi ảnh chụp thay vì PDF chuẩn, hãy thêm một bước OCR (như Google Cloud Vision hoặc OpenAI Vision) trước khi phân tích.

### 📌 Kết luận
Việc tự động hóa trích xuất hóa đơn với n8n và GPT-4o là bước tiến cực kỳ hiệu quả giúp tối ưu hóa vận hành tài chính cho doanh nghiệp vừa và nhỏ. Hãy triển khai ngay hôm nay để giải phóng thời gian cho đội ngũ kế toán nhé các sếp!