---
title: "🚀 Tự Động Sao Lưu Email Gmail Vào Google Drive Bằng n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow tự động xuất email từ Gmail và lưu trữ an toàn dưới dạng file trên Google Drive."
slug: "tu-dong-sao-luu-email-gmail-vao-google-drive"
tags: [n8n, automation, no-code, gmail, google-drive, backup]
keywords: [n8n workflow, sao lưu email gmail, google drive automation, export email to drive, n8n gmail google drive]
---

# 🚀 Tự Động Sao Lưu Email Gmail Vào Google Drive Bằng n8n

Việc quản lý và lưu trữ hàng đống email quan trọng (hóa đơn, báo cáo dự án, tài liệu khách hàng) một cách thủ công thực sự là một cơn ác mộng tốn thời gian. Các sếp thường xuyên gặp tình trạng hộp thư quá tải, khó tìm kiếm lại các tài liệu cũ hoặc rủi ro mất mát dữ liệu. 

Giải pháp ở đây là gì? Tự động hóa 100% quy trình này! Với workflow n8n **Gmail to Google Drive Email Export Workflow** do tác giả *Akhil Varma Gadiraju* thiết kế, các hệ thống của các sếp sẽ tự động quét email từ Gmail, chuyển đổi chúng thành định dạng file gọn gàng và lưu trữ ngay ngắn vào thư mục chỉ định trên Google Drive mà không cần động tay chân.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không bao giờ bỏ lỡ việc lưu trữ các email quan trọng từ đối tác hay khách hàng.
- **Tổ chức khoa học**: Toàn bộ email được quy hoạch gọn gàng thành các file lưu trữ trên Google Drive.
- **Tiết kiệm thời gian**: Giải phóng hàng giờ đồng hồ mỗi tuần cho việc tải xuống và phân loại email thủ công.
- **An toàn & Dễ tra cứu**: Tạo ra một hệ thống lưu trữ/sao lưu (backup) minh bạch, phục vụ hoàn hảo cho việc kiểm toán hoặc tra cứu sau này.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản **Google** kết nối với n8n để cấp quyền truy cập Gmail (OAuth2).
- Tài khoản **Google** kết nối với n8n để cấp quyền truy cập Google Drive (OAuth2).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp hãy tải file JSON của workflow (hoặc copy mã nguồn JSON từ trang [n8n Workflow 4236](https://n8n.io/workflows/4236)), sau đó paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, hãy cấu hình các node quan trọng sau đây để workflow chạy đúng ý đồ:

- **Node Gmail**: 
  - Kết nối tài khoản Gmail của các sếp (`gmailOAuth2`).
  - Tại phần cấu hình, hãy cập nhật bộ lọc (ví dụ: thay đổi trường `sender` để lọc email từ một người gửi cụ thể như hóa đơn, báo cáo).
- **Node Convert Time Field (Code node)**: 
  - Chỉnh sửa lại múi giờ (`timeZone`) trong Code node cho phù hợp với thời gian tại Việt Nam (ví dụ: `Asia/Ho_Chi_Minh`).
- **Node Parse Data (Set node)**: 
  - Tùy chỉnh các trường dữ liệu muốn trích xuất từ email (tiêu đề, nội dung, người gửi, thời gian...) bằng cách thêm/bớt các field trong Set node này.
- **Node Convert to File**: 
  - Chọn định dạng file đầu ra mong muốn (JSON, CSV, PDF/HTML tùy thuộc vào cấu hình n8n hỗ trợ).
- **Node Google Drive**: 
  - Kết nối tài khoản Google Drive (`googleDriveOAuth2Api`).
  - Đặt lại tên file đầu ra (`Output File Name`) cho dễ phân biệt.
  - Cập nhật ID thư mục lưu trữ (`folderId`) để các file email được đẩy đúng vào thư mục chỉ định trên Drive của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử (Manual Trigger) với dữ liệu mẫu để kiểm tra xem file đã được tạo và đẩy lên Google Drive thành công chưa.
- Sau khi test ngon lành, hãy bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối thông báo**: Thêm một node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay về máy mỗi khi có một email quan trọng được sao lưu thành công lên Drive.
- **Lọc thông minh**: Kết hợp thêm các điều kiện (If node) để chỉ sao lưu những email có đính kèm file hoặc chứa các từ khóa cụ thể (như "Invoice", "Hóa đơn", "Hợp đồng").
- **Lưu log hệ thống**: Ghi lại lịch sử các email đã xuất vào một Google Sheet để dễ dàng theo dõi dòng tiền hoặc tiến độ công việc.

### 📌 Kết luận
Workflow **Gmail to Google Drive Email Export Workflow** là một trợ thủ đắc lực giúp số hóa và tự động hóa quy trình lưu trữ tài liệu từ email. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa năng suất làm việc từ hôm nay!