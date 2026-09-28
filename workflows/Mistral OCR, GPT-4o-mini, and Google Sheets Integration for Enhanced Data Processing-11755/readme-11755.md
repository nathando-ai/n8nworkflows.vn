---
title: "🚀 Tự động hóa xử lý hóa đơn thông minh với Mistral OCR, GPT-4o-mini và Google Sheets"
description: "Hướng dẫn chi tiết xây dựng workflow n8n tự động trích xuất dữ liệu hóa đơn PDF, PNG, JPG bằng Mistral OCR và GPT-4o-mini, sau đó lưu vào Google Sheets."
slug: "tu-dong-hoa-xu-ly-hoa-don-mistral-ocr-gpt-4o-mini-google-sheets"
tags: [n8n, automation, no-code, invoice-processing, ai, google-sheets, mistral-ocr]
keywords: [n8n workflow, xử lý hóa đơn tự động, mistral ocr, gpt-4o-mini, google sheets automation]
---

# 🚀 Tự động hóa xử lý hóa đơn thông minh với Mistral OCR, GPT-4o-mini và Google Sheets

Các sếp có đang mệt mỏi vì mỗi cuối tháng phải ngồi nhập thủ công hàng trăm tờ hóa đơn (PDF, ảnh chụp) vào Excel hay phần mềm kế toán? Việc này không chỉ tốn hàng giờ đồng hồ mà còn dễ dẫn đến sai sót số liệu, nhầm lẫn tiền thuế hay tên nhà cung cấp.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một **Workflow n8n hoàn toàn tự động** (tác giả Antonio Gasso) kết hợp sức mạnh của **Mistral OCR** (chuyên gia đọc chữ trên tài liệu) và **GPT-4o-mini** (trích xuất thông tin cấu trúc), giúp tự động hóa 100% quy trình đọc hóa đơn và lưu thẳng vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh gõ tay từng con số từ hóa đơn vào file quản lý.
- **Độ chính xác cao:** Kết hợp OCR chuyên dụng của Mistral và khả năng hiểu ngữ cảnh siêu việt của GPT-4o-mini.
- **Quản lý tập trung:** Mọi dữ liệu như Số hóa đơn, Ngày, Nhà cung cấp, Tiền thuế, Tổng tiền... được đồng bộ trực tiếp vào Google Sheets kèm điểm tin cậy (Confidence Score).
- **Vận hành trơn tru:** Hỗ trợ xử lý hàng loạt nhiều file cùng lúc với cơ chế kiểm soát tốc độ (Rate Limit) thông minh.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Mistral API Key** (Lấy tại [console.mistral.ai](https://console.mistral.ai)).
- **OpenAI API Key** (Lấy tại [platform.openai.com](https://platform.openai.com) để dùng model `gpt-4o-mini`).
- **Google Account** để kết nối Google Sheets.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow này hoặc copy toàn bộ mã nguồn JSON, sau đó dán (Paste) trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 11 nodes liên kết chặt chẽ với nhau. Các sếp cần chú ý cấu hình các điểm sau:

- **Invoice Upload Form (`formTrigger`):** Giao diện web form đơn giản để người dùng tải lên nhiều file hóa đơn (PDF, PNG, JPG) cùng lúc.
- **Mistral OCR (`httpRequest`):** 
  - Tạo credential loại **HTTP Header Auth**.
  - Cài đặt Header Name: `Authorization`
  - Cài đặt Header Value: `Bearer <MISTRAL_API_KEY_CUA_BAN>`
- **OpenAI Model (`lmChatOpenAi`):** Chọn model `gpt-4o-mini` và kết nối với OpenAI API Key. Node này sẽ làm việc cùng **Extract Invoice Fields** (`informationExtractor`) để bóc tách các trường dữ liệu chuẩn xác.
- **Save to Sheets (`googleSheets`):** 
  - Kết nối tài khoản Google thông qua OAuth2.
  - Chuẩn bị sẵn một Google Sheet với các cột tiêu đề bắt buộc sau:
    `Invoice Number | Invoice Date | Vendor Name | Vendor Tax ID | Subtotal | Tax Rate (%) | Tax Amount | Total Amount | Currency | Filename | Confidence | Status | Issues | Processed At | Pages`
  - Điền đúng **Sheet ID** và tên Sheet vào node này.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử tải lên một vài hóa đơn mẫu qua Form để kiểm tra dữ liệu trả về.
- Nếu mọi thứ hiển thị mượt mà trên Google Sheets, các sếp hãy bật **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống xịn sò hơn nữa, các sếp có thể mở rộng workflow này bằng cách:
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack để bắn tin nhắn thông báo mỗi khi có hóa đơn mới được xử lý thành công hoặc cảnh báo nếu điểm tin cậy (Confidence) quá thấp.
- **Lọc hóa đơn trùng lặp:** Thêm một bước kiểm tra số hóa đơn trong Google Sheets trước khi lưu để tránh việc một hóa đơn bị upload 2 lần.
- **Tự động lưu trữ file:** Đẩy file hóa đơn gốc từ Form lên Google Drive hoặc OneDrive và lưu kèm đường dẫn vào Google Sheets.

### 📌 Kết luận
Việc tự động hóa quy trình xử lý hóa đơn chưa bao giờ dễ dàng đến thế với sự trợ giúp của AI và n8n. Hãy thiết lập ngay hôm nay để giải phóng thời gian cho đội ngũ kế toán và tối ưu hóa vận hành doanh nghiệp các sếp nhé!