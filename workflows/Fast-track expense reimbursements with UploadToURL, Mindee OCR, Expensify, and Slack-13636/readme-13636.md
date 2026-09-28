---
title: "🚀 Tự động hóa hoàn toàn quy trình hoàn thuế/chi phí với UploadToURL, Mindee OCR và Slack"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình hoàn phí: nhận hóa đơn qua Form, đọc dữ liệu bằng Mindee OCR, xét duyệt thông minh qua Slack và đồng bộ vào Expensify, Google Sheets."
slug: "tu-dong-hoa-quy-trinh-hoan-chi-phi-n8n-mindee-expensify"
tags: [n8n, automation, ai-ocr, expensify, slack, productivity]
keywords: [n8n workflow, tự động hóa hoàn phí, Mindee OCR, Expensify automation, xử lý hóa đơn tự động, Slack approval]
---

# 🚀 Tự động hóa hoàn toàn quy trình hoàn phí (Expense Reimbursements) với AI & n8n

Các sếp có thấy mệt mỏi khi nhân viên liên tục phàn nàn về việc điền form hoàn chi phí (expense reimbursement) thủ công, trong khi đội ngũ tài chính lại mất hàng giờ để đối chiếu hóa đơn mờ nhạt, thiếu thông tin? 

Giải pháp cho các sếp đây: Một đường ống xử lý "chụp-và-gửi" (snap-and-submit) hoàn toàn tự động 100%. Workflow này sẽ lưu trữ ảnh hóa đơn qua UploadToURL, trích xuất dữ liệu thông minh bằng Mindee OCR, tự động phê duyệt các khoản nhỏ hoặc đẩy qua Slack cho quản lý xét duyệt đối với các khoản lớn, sau đó đồng bộ thẳng vào Expensify và Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Nhân viên chỉ cần upload ảnh hóa đơn qua form, mọi việc còn lại hệ thống lo.
- **Chính xác tuyệt đối:** Mindee OCR đọc chuẩn xác tên nhà cung cấp, tổng tiền, ngày tháng và thuế.
- **Phê duyệt thông minh:** Các khoản chi phí nhỏ được duyệt tự động (Auto-approve), khoản lớn tự động gửi thông báo 1-click duyệt nhanh qua Slack cho quản lý.
- **Đồng bộ đa nền tảng:** Tự động tạo bản ghi trong Expensify, lưu log kiểm toán vào Google Sheets và gửi email thông báo cho nhân viên qua Gmail.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị các tài khoản và API keys sau:
- **n8n Instance** (Đã cài sẵn Community Nodes `n8n-nodes-uploadtourl`).
- **Mindee API Account** (Dùng cho OCR hóa đơn).
- **Expensify Account & API** (Tạo bản ghi chi phí).
- **Slack Bot/Workspace** (Gửi yêu cầu phê duyệt tương tác).
- **Google Sheets & Gmail** (Lưu log và gửi thông báo xác nhận).
- **Biến môi trường (Environment Variables):** `AUTO_APPROVE_THRESHOLD`, `EXPENSIFY_POLICY_ID`, và `MANAGER_SLACK_USER_ID`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ n8n template hoặc copy toàn bộ JSON.
- Mở n8n Editor, chọn **Add workflow** -> Nhấn tổ hợp `Ctrl + V` (hoặc `Cmd + V`) để dán toàn bộ các nodes lên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 17 nodes được chia thành 4 giai đoạn chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Form Trigger - Submit Receipt**: Form thân thiện với thiết bị di động, nhận các trường: Tên nhân viên, Email, Email quản lý, Danh mục chi phí và File hóa đơn (hỗ trợ `jpg`, `jpeg`, `png`, `pdf`, `heic`).
- **Upload to URL (Remote & Binary)**: Yêu cầu cài đặt Community Node `n8n-nodes-uploadtourl`. Node này giúp host ảnh hóa đơn và trả về link CDN vĩnh viễn phục vụ cho việc kiểm toán (`audit trail`). File được đổi tên chuẩn dạng: `EXP-{timestamp}-{employeeSlug}.ext`.
- **Mindee - Extract Receipt Data**: Sử dụng `httpRequest` gọi đến endpoint `/expense_receipts/v5/predict` của Mindee để trích xuất dữ liệu và điểm độ tin cậy (`confidence score`).
- **Parse OCR & Score Confidence (Code Node)**: Tính điểm tin cậy tổng hợp. Logic đánh giá tự động: `confidence ≥ 0.85 AND total ≤ AUTO_APPROVE_THRESHOLD`. 
- **Confidence Gate — Auto or Manager? (If Node)**: 
  - *Nhánh Auto-approved*: Tạo ngay bản ghi trên Expensify (trạng thái `approved`) và gửi email thông báo ETA cho nhân viên qua **Gmail - Employee Confirmation**.
  - *Nhánh Manager Review*: Gửi thông tin kèm nút bấm Accept/Reject trực tiếp qua **Slack - Manager Approval Request** tới `MANAGER_SLACK_USER_ID`.
- **Sheets - Append Audit Row**: Mọi yêu cầu (dù duyệt tự động hay qua quản lý) đều được ghi nhận đầy đủ vào Google Sheets làm bằng chứng kiểm toán.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách gửi 1 form mẫu với hóa đơn thực tế.
- Kiểm tra kết quả trả về trên Google Sheets, Gmail và Slack xem đã thông suốt chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để đưa workflow vào vận hành thực tế 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Thay vì chỉ dùng Slack, các sếp có thể tích hợp thêm Telegram Bot hoặc Microsoft Teams để quản lý duyệt chi phí linh hoạt hơn.
- **Cảnh báo gian lận**: Thêm một bước kiểm tra trùng lặp (Duplicate Check) dựa trên số tiền, ngày tháng và tên nhà cung cấp trong Google Sheets để tránh nhân viên nộp trùng hóa đơn.
- **Báo cáo định kỳ**: Tạo thêm một workflow nhỏ chạy hàng tuần tổng hợp tổng chi phí hoàn lại gửi vào kênh Slack của phòng Kế toán.

### 📌 Kết luận
Quy trình hoàn chi phí thủ công giờ đây đã trở thành dĩ vãng. Với sự kết hợp của n8n, Mindee AI OCR và Slack, doanh nghiệp của các sếp có thể tiết kiệm hàng chục giờ làm việc mỗi tháng, loại bỏ sai sót và tăng tốc độ thanh toán cho nhân viên. Triển khai ngay thôi các sếp ơi!