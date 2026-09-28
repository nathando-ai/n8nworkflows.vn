---
title: "🚀 Tự động giám sát tin nhắn LinkedIn Sales Navigator với Gmail và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động quét email thông báo từ LinkedIn Sales Navigator, đối soát với danh sách khách hàng trên Google Sheets và gửi cảnh báo thông minh qua Gmail."
slug: "giam-sat-tin-nhan-linkedin-sales-navigator-voi-gmail-google-sheets"
tags: [n8n, automation, linkedin, gmail, google-sheets, sales-automation]
keywords: [n8n workflow, tự động hóa linkedin, sales navigator, quản lý lead google sheets, gmail automation]
---

# 🚀 Tự động giám sát tin nhắn LinkedIn Sales Navigator với Gmail & Google Sheets

Các sếp làm sales hay b2b chắc hẳn đều đau đầu mỗi khi phải liên tục kiểm tra hộp thư LinkedIn Sales Navigator để xem có khách hàng tiềm năng nào nhắn tin hay không. Việc check thủ công vừa tốn thời gian, lại rất dễ bỏ sót các cơ hội vàng từ những "khách nóng". 

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n tự động hóa 100%. Workflow này sẽ thay các sếp "canh gác" hộp thư LinkedIn thông qua Gmail, tự động đối soát với cơ sở dữ liệu trên Google Sheets và gửi cảnh báo ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Không bỏ lỡ khách hàng:** Tự động phát hiện và cảnh báo ngay khi có tin nhắn mới trên LinkedIn Sales Navigator.
- **Tiết kiệm thời gian:** Loại bỏ hoàn toàn việc phải mở LinkedIn kiểm tra thủ công nhiều lần mỗi ngày.
- **Phân loại thông minh:** Tự động đối chiếu thông tin người gửi với database trên Google Sheets để biết rõ lead nào đang quan tâm.
- **Hoạt động 24/7:** Chạy ngầm liên tục, đảm bảo các sếp luôn nắm bắt thông tin nhanh như chớp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản **Gmail** (đã cấp quyền kết nối với n8n để đọc và gửi email thông báo).
- Tài khoản **Google Sheets** chứa sẵn danh sách database khách hàng tiềm năng (leads) của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này (hoặc tải file từ nguồn gốc) và dán trực tiếp vào n8n Editor của mình. Workflow gồm 8 nodes được thiết kế mạch lạc, sẵn sàng sử dụng.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Manual Trigger - Click to Execute**: Node kích hoạt thủ công để các sếp test thử workflow. (Sau này có thể đổi sang Schedule Trigger để chạy tự động theo giờ).
- **Fetch LinkedIn Notification Emails (Gmail)**: Kết nối tài khoản Gmail của các sếp. Cấu hình bộ lọc tìm kiếm (Query) để chỉ quét các email thông báo đến từ LinkedIn Sales Navigator (ví dụ: `from:linkedin sales navigator`).
- **Extract Sender Name from Email (Code)**: Node chạy mã JavaScript để bóc tách tên người gửi từ nội dung email thông báo của LinkedIn.
- **Fetch Lead Database from Sheets (Google Sheets)**: Kết nối tài khoản Google, trỏ tới file **Google Sheets** chứa danh sách lead của các sếp. Đọc đúng tên Sheet/Tab cần lấy dữ liệu.
- **Clean and Extract Lead Name (Code)**: Làm sạch định dạng tên lead để chuẩn bị cho bước so khớp.
- **Merge Senders and Leads Data (Merge)**: Gộp dữ liệu từ email LinkedIn và dữ liệu từ Google Sheets lại với nhau.
- **Match LinkedIn Senders with Lead Database (Code)**: Thuật toán so khớp xem người gửi tin nhắn có khớp với lead nào trong database hay không.
- **Send Categorized Alert Email (Gmail)**: Cấu hình gửi email cảnh báo về hộp thư chính của các sếp với đầy đủ thông tin chi tiết về lead và nội dung tin nhắn.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** ở node *Manual Trigger* để chạy thử với dữ liệu cũ và kiểm tra kết quả trả về.
- Sau khi test thành công, các sếp bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Chat:** Thay vì chỉ gửi email cảnh báo, các sếp có thể thay thế hoặc bổ sung node **Telegram** hoặc **Slack** để nhận thông báo tức thì trên điện thoại.
- **Lưu log tự động:** Thêm một bước ghi nhận lịch sử tương tác ngược lại vào Google Sheets để đội ngũ Sales dễ dàng theo dõi trạng thái chăm sóc.
- **Chạy tự động định kỳ:** Thay thế node Trigger thủ công bằng *Schedule Trigger* (ví dụ: chạy mỗi 30 phút/lần) để hệ thống tự động hóa hoàn toàn.

### 📌 Kết luận
Với workflow n8n này, việc quản lý tin nhắn và chăm sóc khách hàng tiềm năng trên LinkedIn Sales Navigator chưa bao giờ dễ dàng đến thế. Hãy cài đặt ngay để tối ưu hóa quy trình sales của doanh nghiệp các sếp nhé!