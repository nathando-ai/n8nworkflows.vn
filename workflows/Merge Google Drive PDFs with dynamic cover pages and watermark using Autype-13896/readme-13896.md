---
title: "🚀 Tự động hóa gộp file PDF từ Google Drive với trang bìa động và Watermark bằng n8n & Autype"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n để gom toàn bộ file PDF từ Google Drive, tự động tạo trang bìa, gộp tài liệu xen kẽ, đóng dấu watermark và lưu lại."
slug: "gop-pdf-google-drive-trang-bia-dong-watermark-autype"
tags: [n8n, automation, google-drive, autype, pdf-processing, no-code]
keywords: [n8n workflow, gộp file pdf google drive, tạo trang bìa pdf tự động, chèn watermark pdf, autype n8n]
---

# 🚀 Tự động hóa gộp file PDF từ Google Drive với trang bìa động và Watermark

Các sếp có bao giờ cảm thấy đau đầu khi phải tổng hợp hàng chục file PDF báo cáo, tài liệu rời rạc từ Google Drive thành một cuốn báo cáo tổng hợp hoàn chỉnh? Việc làm thủ công như tải từng file về, thiết kế trang bìa riêng cho từng phần, chèn watermark rồi gộp lại không chỉ tốn hàng giờ đồng hồ mà còn dễ xảy ra sai sót.

Giải pháp đây rồi! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ thông minh, tự động hóa 100% quy trình: **Đọc file PDF từ Google Drive -> Tự động sinh trang bìa động (tên, ngày tháng, chủ sở hữu) -> Ghép xen kẽ trang bìa và tài liệu -> Đóng dấu bản quyền (Watermark) -> Lưu ngược lại Google Drive**. Toàn bộ quy trình diễn ra trơn tru nhờ sự kết hợp giữa n8n và Autype.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow xử lý tài liệu nặng chạy ổn định 24/7 mà không sợ sập giữa chừng, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 99% thời gian:** Không còn cảnh copy-paste hay chỉnh sửa thủ công từng trang bìa file PDF.
- **Tính chuyên nghiệp cao:** Mỗi tài liệu đều được gắn một trang bìa chuẩn chỉnh, hiển thị đầy đủ thông tin metadata (tên file, ngày tạo, người sở hữu).
- **Bảo mật và đồng bộ:** Tự động đóng dấu Watermark công ty với độ trong suốt tùy chỉnh trên mọi trang.
- **Tự động hóa hoàn toàn:** Gom nhóm, xử lý hàng loạt và lưu trữ trực tiếp về đúng thư mục Google Drive gốc chỉ bằng 1 cú click hoặc chạy định kỳ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Do workflow này sử dụng Community Node, các sếp **bắt buộc phải dùng bản n8n Self-hosted** (không chạy được trên n8n Cloud).
- **Tài khoản Autype:** Đăng ký tài khoản miễn phí tại [app.autype.com](https://app.autype.com) và vào mục **Settings → API Keys** để lấy API Key.
- **Cài đặt Community Node:** Cài đặt gói `n8n-nodes-autype` vào instance n8n của các sếp qua menu **Settings → Community Nodes**.
- **Google Drive Credentials:** Kết nối tài khoản Google của các sếp qua OAuth2 trong phần credentials của n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn gốc (hoặc copy mã JSON) và chọn **Import from File / Paste JSON** trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, hãy chú ý cấu hình chính xác các node quan trọng sau đây:
- **List PDFs in Folder (`googleDrive`):** Chọn tài khoản Google Drive OAuth2 đã kết nối, sau đó trỏ đến ID thư mục chứa các file PDF nguồn cần xử lý.
- **Build Title Pages JSON (`code`):** Node này chứa đoạn mã xử lý dữ liệu để cấu hình nội dung trang bìa dựa trên thông tin metadata của file (tên, ngày tạo, ngày sửa, chủ sở hữu). Các sếp có thể tùy chỉnh lại giao diện hoặc trường hiển thị nếu muốn.
- **Render Title Pages PDF, Upload Title Pages PDF, Extract Title Page, Merge All PDFs, Add Company Watermark (`n8n-nodes-autype`):** Tất cả các node này đều yêu cầu cấu hình **Autype API Key** thông qua Credentials đã tạo. Đảm bảo các sếp đã điền chính xác khóa API từ Autype.
- **Save Final PDF to Drive (`googleDrive`):** Cấu hình thư mục đích để lưu file PDF hoàn thiện (đặt tên mặc định theo định dạng `merged-documents-YYYY-MM-DD.pdf`).

#### 3. Kích hoạt ⚡️
- Nhấn **"Test Workflow"** ở node **Run Workflow** (`manualTrigger`) để chạy thử nghiệm với một thư mục mẫu trên Google Drive và kiểm tra kết quả trả về.
- Sau khi test thành công, bật trạng thái **Active** cho workflow để sẵn sàng đưa vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa hơn nữa quy trình làm việc, các sếp có thể mở rộng workflow này bằng cách:
1. **Thêm thông báo Telegram/Slack:** Gửi tin nhắn tự động kèm đường dẫn file PDF hoàn thiện ngay khi workflow chạy xong.
2. **Kích hoạt tự động (Webhook / Schedule):** Thay vì dùng nút bấm thủ công (`manualTrigger`), có thể thay bằng `Schedule Trigger` để gom file tự động vào cuối tuần hoặc cuối tháng, hoặc dùng Webhook nhận yêu cầu từ hệ thống CRM/ERP.
3. **Lưu lịch sử chạy (Google Sheets):** Thêm một node Google Sheets để ghi lại log tên file, thời gian gộp và trạng thái xử lý nhằm dễ dàng đối soát khi cần thiết.

### 📌 Kết luận
Workflow gộp PDF kết hợp trang bìa động và Watermark với n8n & Autype là một "vũ khí" cực kỳ lợi hại cho các phòng ban Nhân sự, Kế toán, hay Sales – những nơi thường xuyên phải xử lý và đóng gói tài liệu gửi đối tác, khách hàng. Hãy triển khai ngay hôm nay để tối ưu hóa năng suất làm việc cho đội ngũ của mình nhé các sếp!