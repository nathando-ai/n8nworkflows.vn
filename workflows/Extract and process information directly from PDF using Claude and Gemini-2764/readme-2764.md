---
title: "🚀 Tự động trích xuất thông tin PDF thông minh với Claude 3.5 Sonnet và Gemini 2.0 Flash qua n8n"
description: "Hướng dẫn xây dựng workflow n8n so sánh trực tiếp khả năng xử lý PDF một chạm giữa Claude 3.5 Sonnet và Gemini 2.0 Flash không cần qua bước OCR trung gian."
slug: "trich-xuat-thong-tin-pdf-claude-gemini-n8n"
tags: [n8n, automation, ai, claude, gemini, pdf-extraction]
keywords: [n8n workflow, trích xuất pdf ai, claude 3.5 sonnet pdf, gemini 2.0 flash pdf, tự động hóa n8n]
---

# 🚀 Tự động trích xuất thông tin PDF thông minh với Claude 3.5 Sonnet và Gemini 2.0 Flash

Các sếp có bao giờ cảm thấy mệt mỏi khi phải copy dữ liệu thủ công từ hàng loạt file hóa đơn, hợp đồng, hay báo cáo PDF dài dằng dặc? Hay việc dùng các công cụ OCR truyền thống vừa chậm, vừa sai sót, lại phải tốn thêm một bước gọi LLM để xử lý? 

Workflow n8n này từ **Agent Studio** chính là "vũ khí tối thượng" giúp giải quyết bài toán đó. Nó cho phép các sếp **trích xuất và xử lý dữ liệu trực tiếp từ file PDF chỉ trong một bước duy nhất**, đồng thời cho phép so sánh "nặng ký" về kết quả, tốc độ phản hồi (latency) và chi phí giữa hai mô hình AI hàng đầu hiện nay: **Claude 3.5 Sonnet** và **Gemini 2.0 Flash**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tối ưu quy trình 1 bước:** Bỏ qua hoàn toàn bước OCR phức tạp, gửi thẳng file PDF gốc vào AI.
- **So sánh trực quan:** Đánh giá chính xác mô hình nào (Claude hay Gemini) phù hợp hơn với nhu cầu trích xuất dữ liệu đặc thù của doanh nghiệp.
- **Tùy biến linh hoạt:** Dễ dàng định nghĩa prompt theo ý muốn để lấy ra đúng các trường dữ liệu cần thiết (JSON, text thuần...).
- **Tiết kiệm thời gian:** Xử lý hàng loạt tài liệu tự động, loại bỏ hoàn toàn thao tác nhập liệu bằng tay.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để vận hành trơn tru workflow này, các sếp cần chuẩn bị:
- Một tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản và kết nối **Google Drive** (để lấy file PDF mẫu).
- **Anthropic API Key** (để gọi Claude 3.5 Sonnet - lấy tại [Anthropic Console](https://console.anthropic.com/settings/keys)).
- **Google Gemini API Key** (để gọi Gemini 2.0 Flash - lấy tại [Google AI Studio](https://aistudio.google.com/app/apikey)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow, dán trực tiếp vào n8n Editor hoặc sử dụng tính năng import file JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 6 nodes chính, các sếp cần chú ý cấu hình các điểm sau:
- **Google Drive Node:** Kết nối tài khoản Google Drive của các sếp và trỏ tới file PDF mẫu cần trích xuất dữ liệu.
- **Extract from File Node:** Node này thực hiện việc đọc file PDF từ Google Drive và chuyển đổi sang định dạng Base64 (định dạng bắt buộc để cả 2 API của Claude và Gemini xử lý trực tiếp tệp tài liệu).
- **Define Prompt Node (`set`):** Nơi các sếp viết câu lệnh (prompt) yêu cầu AI trích xuất thông tin gì từ PDF (ví dụ: *"Hãy trích xuất tên khách hàng, tổng tiền, ngày hóa đơn thành định dạng JSON"*).
  - *Mẹo với Gemini:* Có thể thêm cấu hình `responseMimeType: application/json` để ép kết quả trả về dạng JSON chuẩn.
  - *Mẹo với Claude:* Sử dụng kỹ thuật "Prefill response format" để định hình trước cấu trúc JSON đầu ra.
- **Call Gemini 2.0 Flash & Call Claude 3.5 Sonnet Nodes (`httpRequest`):** Điền các API Key tương ứng đã chuẩn bị vào phần Credentials của từng node. *(Lưu ý: Các sếp hoàn toàn có thể tắt 1 trong 2 node này nếu chỉ muốn test một mô hình duy nhất).*

#### 3. Kích hoạt ⚡️
- Nhấn nút **"Test workflow"** để chạy thử nghiệm với file PDF trên Google Drive.
- Kiểm tra kết quả trả về ở tab Output của hai node gọi AI để so sánh chất lượng.
- Sau khi kiểm tra mọi thứ mượt mà, gạt công tắc sang **Active** để đưa workflow vào hoạt động chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Lưu trữ:** Nối tiếp kết quả JSON trả về từ AI vào Google Sheets, Airtable hoặc cơ sở dữ liệu nội bộ để tự động lưu trữ thông tin.
- **Gửi thông báo:** Kết hợp thêm node Telegram hoặc Slack để gửi bản tóm tắt trích xuất PDF ngay vào group chat của team ngay khi xử lý xong.
- **Xử lý hàng loạt (Batch Processing):** Thay vì chọn một file cố định trên Google Drive, các sếp có thể mở rộng bằng trigger quét thư mục Google Drive định kỳ để tự động hóa toàn bộ kho tài liệu đầu vào.

### 📌 Kết luận
Việc tích hợp AI đa mô hình trực tiếp vào quy trình xử lý tài liệu PDF chưa bao giờ dễ dàng đến thế. Hãy áp dụng ngay workflow này vào hệ thống của các sếp để tối ưu hóa năng suất và trải nghiệm sức mạnh của AI thế hệ mới!