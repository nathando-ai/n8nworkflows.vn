---
title: "🚀 Tự động trích xuất hóa đơn từ Gmail vào Google Sheets, Airtable bằng n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình xử lý hóa đơn từ Gmail, phân tích PDF thông minh và đồng bộ dữ liệu vào Google Sheets, Airtable không cần code."
slug: "tu-dong-trich-xuat-hoa-don-tu-gmail-vao-sheets-airtable-n8n"
tags: [n8n, automation, no-code, invoice-processing, google-sheets, airtable, gmail]
keywords: [n8n workflow, trích xuất hóa đơn tự động, invoice parsing n8n, tự động hóa kế toán, google sheets airtable n8n]
---

# 🚀 Tự động trích xuất hóa đơn từ Gmail vào Google Sheets, Airtable

Các sếp có đang mệt mỏi mỗi cuối tháng khi phải mở từng email, tải file PDF hóa đơn về máy, gõ thủ công từng con số (nhà cung cấp, tổng tiền, thuế, hạn thanh toán) vào Google Sheets hay phần mềm kế toán không? Việc này không chỉ tốn hàng giờ đồng hồ mà còn dễ xảy ra sai sót chết người.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một pipeline tự động hóa chuẩn công nghiệp (Industrial-grade pipeline) với **n8n**, giúp tự động bắt hóa đơn từ Gmail, bóc tách dữ liệu bằng AI/JSON, phân loại tự động và đồng bộ thẳng vào **Google Sheets**, **Airtable**, cùng cơ chế kiểm duyệt thông minh!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn nhập liệu thủ công, hệ thống tự động xử lý ngay khi hóa đơn vừa đến trong hộp thư.
- **Độ chính xác cao:** Trích xuất tự động các trường dữ liệu quan trọng (Vendor, Total, Tax, Due Date) kèm điểm số tin cậy (Confidence Score).
- **Phân luồng thông minh (Auto-Approval):** Hóa đơn chuẩn sẽ được tự động lưu kho; hóa đơn giá trị cao hoặc độ tin cậy thấp sẽ được đẩy vào hàng đợi duyệt thủ công (Review Queue) và gửi cảnh báo qua Slack/Gmail.
- **Lưu trữ khoa học:** Tự động backup file PDF gốc lên Google Drive với metadata đầy đủ.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Gmail** (để cấu hình Trigger nhận email và gửi cảnh báo).
- **Google Drive & Google Sheets** (để lưu trữ file PDF và bảng dữ liệu Ledger/Review Queue).
- **Airtable Base** (để tạo bản ghi quản lý hóa đơn).
- **Slack Workspace** (tùy chọn: để nhận thông báo trạng thái hóa đơn).
- **API Credential cho node HTML to PDF (Parse)**.
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này, vào giao diện n8n, chọn **Add workflow** -> **Import from JSON** và dán vào là xong!

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Pipeline này gồm 13 nodes được chia thành 4 giai đoạn chính. Các sếp cần cấu hình kỹ các điểm sau:

- **Node `Gmail: Watch Invoices`**: Kết nối tài khoản Gmail của các sếp, thiết lập bộ lọc (query) chỉ bắt các email có đính kèm file PDF hóa đơn để tránh quét nhầm email rác.
- **Node `HTML to PDF: Parse to JSON`**: Cần điền chính xác API credentials của dịch vụ parse PDF để chuyển đổi dữ liệu thô từ file PDF sang cấu trúc JSON chuẩn.
- **Node `Code: AI Ledger Mapper`**: Node này dùng custom code để trích xuất các trường như Vendor, Total, Tax, Due Date và tính toán điểm số tin cậy (`Extraction_Confidence`).
- **Node `IF: Auto-Approve`**: Thiết lập điều kiện tự động duyệt. Ví dụ: 
  - *Green Path (Đường xanh):* Điểm tin cậy `> 0.7` VÀ Tổng tiền `< $5000` $\rightarrow$ Chạy tiếp sang Google Sheets, Airtable và Google Drive.
  - *Amber Path (Đường vàng):* Điểm tin cậy thấp hoặc hóa đơn giá trị lớn $\rightarrow$ Chuyển hướng sang hàng đợi kiểm duyệt.
- **Các node đích (`Google Sheets: Add Row`, `Airtable: Create Record`, `Google Drive: Archive Invoice`)**: Chọn đúng bảng (Sheet/Base) và map lại các trường dữ liệu tương ứng khớp với cấu trúc bảng của các sếp.
- **Node `Slack: Review Required` & `Gmail: Review Alert`**: Cấu hình kênh Slack hoặc email nhận thông báo khi có hóa đơn cần sếp duyệt thủ công.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách gửi một email chứa file PDF hóa đơn mẫu vào Gmail đã kết nối.
- Kiểm tra xem dữ liệu đã đổ về Google Sheets/Airtable chưa.
- Nếu mọi thứ chạy mượt mà, hãy gạt công tắc sang chế độ **Active** để hệ thống tự động cày 24/7 cho các sếp!

---

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình tài chính của doanh nghiệp, các sếp có thể mở rộng workflow này thêm các tính năng:
1. **Tích hợp Zalo/Telegram Bot:** Thay vì dùng Slack, có thể đẩy thông báo cần duyệt hóa đơn thẳng vào nhóm Telegram/Zalo của bộ phận kế toán để phản hồi nhanh hơn.
2. **Auto-Reply Email:** Tự động gửi email phản hồi lại nhà cung cấp rằng "Đã nhận được hóa đơn và đang trong quá trình xử lý" sau khi hệ thống quét thành công.
3. **Báo cáo định kỳ:** Tạo thêm một nhánh chạy vào cuối tuần để tổng hợp tổng chi phí trong tuần từ Google Sheets và gửi báo cáo tóm tắt qua email cho Giám đốc tài chính (CFO).

### 📌 Kết luận
Việc tự động hóa quy trình xử lý hóa đơn với n8n không chỉ giúp tiết kiệm hàng chục giờ nhập liệu mỗi tháng mà còn loại bỏ hoàn toàn sai sót do con người. Hãy triển khai ngay hôm nay để tối ưu hóa vận hành cho doanh nghiệp của các sếp!