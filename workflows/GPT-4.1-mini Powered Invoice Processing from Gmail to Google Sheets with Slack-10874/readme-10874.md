---
title: "🚀 Tự động hóa xử lý hóa đơn từ Gmail, trích xuất AI và duyệt qua Slack với n8n"
description: "Xây dựng quy trình xử lý hóa đơn tự động từ Gmail, sử dụng GPT-4.1-mini bóc tách dữ liệu, lưu Google Sheets và tạo nút Duyệt/Từ chối trực tiếp trên Slack."
slug: "tu-dong-hoa-xu-ly-hoa-don-gmail-ai-slack-n8n"
tags: [n8n, automation, ai, openai, gmail, google-sheets, slack]
keywords: [n8n workflow, tự động hóa hóa đơn, gpt-4 mini, xử lý hóa đơn tự động, n8n gmail google sheets slack]
---

# 🚀 Tự động hóa xử lý hóa đơn từ Gmail, trích xuất AI và duyệt qua Slack

Các sếp có đang mệt mỏi với cảnh cuối tháng phải ngồi mở từng email, tải file PDF hóa đơn về, căng mắt đọc từng con số rồi thủ công nhập vào Google Sheets để làm báo cáo không? Việc này không chỉ tốn hàng giờ đồng hồ mà còn rất dễ xảy ra sai sót lệch số liệu.

Chưa kể, quy trình xin phê duyệt thanh toán đôi khi rườm rà qua lại giữa email và các phòng ban. Giải pháp cho các sếp đây: một workflow n8n tự động hóa 100% toàn bộ quy trình từ lúc hóa đơn chui vào Gmail cho đến khi bóc tách dữ liệu bằng AI và gửi yêu cầu sếp duyệt ngay trên Slack chỉ với 1 cú click!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần thủ công tải PDF hay gõ tay dữ liệu vào bảng tính.
- **Độ chính xác cao:** Ứng dụng sức mạnh của OpenAI GPT-4.1-mini để bóc tách chính xác các thông tin quan trọng như số hóa đơn, tên công ty, số tiền, ngày tháng.
- **Quy trình phê duyệt mượt mà:** Sếp nhận thông báo kèm nút **Approve / Reject** trực tiếp trên Slack, bấm là cập nhật trạng thái ngay lập tức.
- **Hoạt động tự động 24/7:** Chạy ngầm liên tục, cứ có hóa đơn mới là xử lý trong tích tắc.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Gmail Account / Credentials** để bắt email hóa đơn đến.
- **OpenAI API Key** (Sử dụng model `gpt-4.1-mini` để trích xuất dữ liệu cấu trúc).
- **Google Sheets** (Đã tạo sẵn bảng tính lưu hóa đơn).
- **Slack Workspace** & Bot Token (Để gửi tin nhắn thông báo và nhận phản hồi duyệt).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã nguồn JSON của workflow hoặc tải file JSON gốc từ nguồn, sau đó dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình chính xác các node sau:
- **Node `1. New Invoice Email Received` (Gmail Trigger):** Thêm credentials Gmail và tùy chỉnh lại câu lệnh tìm kiếm `q` (ví dụ: `subject:invoice` hoặc từ khóa tìm kiếm hóa đơn phù hợp với doanh nghiệp các sếp).
- **Node `OpenAI Chat Model`:** Cấu hình OpenAI API key và đảm bảo model đang chọn là `gpt-4.1-mini`.
- **Node `6. Log Invoice to Google Sheet` & các node update (`9a`, `9b`):** Kết nối tài khoản Google Sheets, chọn đúng file Google Sheet và Sheet Name. Cấu trúc các cột trong Sheet bắt buộc phải có: `invoice_number`, `company`, `amount`, `date`, `due_date`, `status`, `rawText`.
- **Node `7. Send Approval Request to Slack`:** Kết nối Slack credentials và điền Channel ID nơi sếp muốn nhận thông báo.
- **❗️ LƯU Ý QUAN TRỌNG VỀ WEBHOOK:** 
  1. Các sếp phải **Active workflow** (bật công tắc ở góc trên bên phải) trước.
  2. Sau đó, copy **Production URLs** từ hai node `Webhook (Approve)` và `Webhook (Reject)`.
  3. Dán các URL này vào node `7. Send Approval Request to Slack` để thay thế cho đoạn placeholder `https://YOUR_WEBHOOK_BASE_URL`. Có như vậy khi click nút trên Slack, hệ thống mới nhận diện và cập nhật trạng thái được.

#### 3. Kích hoạt ⚡️
- Chạy thử một email mẫu (Test step/Execute workflow) để kiểm tra luồng dữ liệu từ Gmail $\rightarrow$ AI $\rightarrow$ Google Sheets $\rightarrow$ Slack.
- Khi mọi thứ đã xanh mướt, bật **Active workflow** để hệ thống tự động chạy thật.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo Telegram:** Ngoài Slack, các sếp có thể nhân bản nhánh thông báo sang Telegram nếu đội ngũ quen dùng app này hơn.
- **Tự động chuyển tiền / hạch toán:** Kết nối thêm node chuyển tiền tự động (như Stripe, PayPal hoặc API ngân hàng) ngay sau khi trạng thái chuyển sang `approved`.
- **Lưu trữ file PDF:** Thêm node Google Drive để tự động lưu bản PDF hóa đơn vào thư mục tương ứng của công ty.

### 📌 Kết luận
Workflow này là một mảnh ghép hoàn hảo để tự động hóa hoàn toàn phòng kế toán/vận hành, giúp doanh nghiệp tiết kiệm nhân lực và kiểm soát chi phí cực kỳ chặt chẽ. Chúc các sếp cài đặt thành công và "lên đời" tự động hóa cho doanh nghiệp của mình!