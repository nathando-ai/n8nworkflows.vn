---
title: "🚀 Tự động hóa xử lý hóa đơn điện tử Colombia với Gmail, GPT-4o và Google Workspace"
description: "Hướng dẫn chi tiết workflow n8n tự động trích xuất, phân loại hóa đơn điện tử từ Gmail, xử lý bằng AI GPT-4o-mini và lưu trữ lên Google Drive, Google Sheets."
slug: "tu-dong-hoa-xu-ly-hoa-don-dien-tu-colombia-n8n"
tags: [n8n, automation, ai, gpt-4o, gmail, google-drive, google-sheets]
keywords: [n8n workflow, hóa đơn điện tử, tự động hóa kế toán, gpt-4o mini n8n, trích xuất hóa đơn pdf xml]
---

# 🚀 Tự động hóa xử lý hóa đơn điện tử Colombia với Gmail, GPT-4o & Google Workspace

Các sếp làm trong lĩnh vực tài chính, kế toán hoặc quản lý doanh nghiệp có mệt mỏi với việc hàng tháng phải tải từng file hóa đơn từ email, giải nén file `.zip`, đọc thủ công từng file PDF/XML để nhập số liệu vào Excel và lưu trữ vào Drive không? Việc này vừa tốn thời gian, dễ sai sót lại cực kỳ nhàm chán.

Giải pháp đây rồi! Workflow n8n này sẽ tự động hóa **100% quy trình xử lý hóa đơn điện tử** (đặc biệt tối ưu theo chuẩn DIAN tại Colombia). Từ lúc email chứa file `.zip` hóa đơn nhảy vào Gmail cho đến khi dữ liệu được bóc tách bằng AI thông minh, chuẩn hóa, lưu file gọn gàng trên Google Drive và cập nhật thẳng vào Google Sheets. Tất cả diễn ra tự động mà không cần một giọt mồ hôi thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và không bị gián đoạn khi xử lý file nặng, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh download thủ công, đổi tên file hay gõ Excel mỏi tay.
- **AI thông minh bóc tách chuẩn xác:** Sử dụng LangChain Agent kết hợp GPT-4o-mini để đọc hiểu hóa đơn (PDF/XML) cực kỳ chính xác các trường như: Số hóa đơn, NIT, Ngày phát hành, Subtotal, VAT, Tổng tiền, CUFE...
- **Tự động đối soát tài chính:** Tích hợp công cụ Calculator để kiểm tra `Tổng tiền = Subtotal + VAT`, đảm bảo không lệch một xu.
- **Lưu trữ chuyên nghiệp:** File PDF tự động đổi tên theo chuẩn `YYYY-MM-DD-NUMERO_FACTURA.pdf` và lưu gọn gàng lên Google Drive, đồng thời chống trùng lặp dữ liệu trên Google Sheets nhờ khóa duy nhất (`NIT + Số hóa đơn`).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- **Tài khoản Gmail** (để cấu hình `Gmail Trigger`).
- **OpenAI API Key** (dành cho node OpenAI Chat Model chạy mô hình `gpt-4o-mini`).
- **Google Drive Account** (cấp quyền OAuth2 cho các node Google Drive).
- **Google Sheets Account** (cấp quyền OAuth2 và chuẩn bị sẵn một file Google Sheets chứa các cột thông tin hóa đơn).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã nguồn JSON của workflow (từ trang nguồn n8n) và dán trực tiếp vào n8n Editor của mình, hoặc sử dụng tính năng import từ file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình các node cốt lõi sau:
- **On Email receipt (`gmailTrigger`):** Kết nối tài khoản Gmail của các sếp. Cấu hình bộ lọc tìm kiếm email (ví dụ: quét các email có file đính kèm dạng `.zip` chứa hóa đơn).
- **OpenAI Chat Model (`lmChatOpenAi`):** Chọn credentials OpenAI và đảm bảo model đang trỏ về `gpt-4o-mini` (hoặc model phù hợp) để tiết kiệm chi phí mà vẫn đảm bảo độ thông minh.
- **Extract Data from PDF and XML (`agent`):** Kiểm tra lại phần Prompt hệ thống trong Agent để đảm bảo AI trích xuất đúng các trường dữ liệu mong muốn (Loại hóa đơn, số hóa đơn, ngày, NIT, tổng tiền, CUFE...).
- **Create initial PDF & Update PDF with actual name (`googleDrive`):** Trỏ đến thư mục (Folder ID) trên Google Drive nơi các sếp muốn lưu trữ các file hóa đơn gốc.
- **Create or update row (`googleSheets`):** Kết nối tới file Google Sheets quản lý tài chính của các sếp, trỏ đúng Sheet Name và cấu hình chế độ `Append or Update` dựa trên trường khóa duy nhất (`Key = NIT_Emisor + Numero_Factura`) để tránh tạo dòng trùng lặp khi email gửi lại hoặc xử lý lại.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử với một email mẫu thực tế để kiểm tra dữ liệu bóc tách qua từng node (`Split XML and PDF`, `Extract PDF Data`, `Calculator`,...).
- Sau khi test thành công, bật nút **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack ở cuối luồng để gửi tin nhắn thông báo ngay lập tức về điện thoại mỗi khi có hóa đơn mới được xử lý và lưu thành công.
- **Quản lý lỗi (Error Handling):** Thêm Error Trigger để bắt các trường hợp email lỗi file `.zip`, file hỏng hoặc AI đọc lỗi, giúp hệ thống không bị khựng giữa chừng.
- **Báo cáo định kỳ:** Kết hợp thêm Google Sheets / Cron node để tổng hợp chi phí mua hàng theo tuần/tháng và gửi báo cáo tóm tắt qua email cho sếp lớn.

### 📌 Kết luận
Workflow này là một cỗ máy tự động hóa hoàn hảo cho bài toán xử lý hóa đơn, giúp tối ưu hóa quy trình kế toán cá nhân hoặc doanh nghiệp nhỏ. Hãy triển khai ngay hôm nay để giải phóng bản thân khỏi những tác vụ thủ công nhàm chán!