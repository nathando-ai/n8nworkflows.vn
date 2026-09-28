---
title: "🚀 Tự động giám sát thư mục Dropbox và lọc file mới thông qua NocoDB với n8n"
description: "Hướng dẫn cài đặt và sử dụng workflow n8n giúp tự động theo dõi thay đổi trong Dropbox, so sánh với cơ sở dữ liệu NocoDB để chỉ lọc ra các file mới và xử lý tự động."
slug: "tu-dong-giam-sat-dropbox-va-loc-file-moi-nocoDB-n8n"
tags: [n8n, automation, no-code, dropbox, nocodb, webhook]
keywords: [n8n workflow, tự động hóa dropbox, giám sát thư mục dropbox, lọc file mới nocoDB, n8n webhook]
---

# 🚀 Tự động giám sát thư mục Dropbox và lọc file mới thông qua NocoDB

Các sếp có bao giờ gặp khó khăn khi phải liên tục kiểm tra xem có tài liệu, hình ảnh hay báo cáo nào mới được tải lên các thư mục Dropbox của công ty hay không? Việc kiểm tra thủ công vừa tốn thời gian, dễ bỏ sót, lại vừa nhàm chán. 

Giải pháp tuyệt vời cho các sếp đây! Bài viết này sẽ hướng dẫn chi tiết cách thiết lập một workflow n8n cực kỳ thông minh, tự động nhận thông báo từ Dropbox khi có thay đổi, đối chiếu với cơ sở dữ liệu NocoDB để lọc ra **đúng các file hoàn toàn mới**, và kích hoạt các quy trình xử lý tiếp theo mà không cần chạm tay vào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Nhận webhook realtime từ Dropbox ngay khi có file hoặc thư mục mới xuất hiện.
- **Loại bỏ trùng lặp thông minh:** Sử dụng NocoDB để lưu trữ lịch sử và so sánh, đảm bảo chỉ xử lý các file chưa từng được ghi nhận trước đó.
- **Phân loại linh hoạt:** Hỗ trợ nhiều cách tiếp cận (xử lý toàn bộ file trong thư mục hoặc chỉ lọc file mới) thông qua các Sub-workflow.
- **Phản hồi nhanh chóng:** Đáp ứng các yêu cầu xác thực từ Dropbox trong vòng chưa đầy 10 giây.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance **n8n** đang hoạt động.
- Tài khoản **Dropbox** (đã cấu hình App/Webhook để kết nối với n8n).
- Tài khoản **NocoDB** kèm bảng dữ liệu (Table) để lưu trữ danh sách các file đã được quét.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp hãy tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow (từ nguồn cung cấp) và dán trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 14 nodes phối hợp nhịp nhàng với nhau để giải quyết bài toán theo dõi file. Các sếp cần chú ý cấu hình các node cốt lõi sau:

- **Node `Webhook`**: Node này đóng vai trò điểm chạm nhận tín hiệu từ Dropbox. Các sếp cần copy Webhook URL được cung cấp và cấu hình nó vào phần Webhooks của Dropbox App để nhận sự kiện `folder.changed` hoặc tương tự.
- **Node `Dropbox - List watched folder` & `Dropbox get files`**: Cần kết nối tài khoản thông qua **Dropbox OAuth2 API**. Tham số đường dẫn `path` được trỏ động từ biến cấu hình (`={{ $json.folder_to_watch }}`).
- **Node `NocoDB - Get know files to exclude` & `NocoDB - Add this file in the table`**: Kết nối bằng **NocoDB API Token**. Sếp cần trỏ đúng đến Base và Table trong NocoDB chuyên dùng để lưu vết các file đã xử lý.
- **Node `Merge - Keep only new items`**: Node này chịu trách nhiệm so sánh danh sách file hiện có trên Dropbox với danh sách trong NocoDB để lọc ra những file chưa tồn tại.
- **Node `Execute Workflow...`**: Đây là các node gọi Sub-workflow. Các sếp cần chuẩn bị sẵn các sub-workflow con để định nghĩa rõ hành động tiếp theo (ví dụ: gửi thông báo Telegram, lưu file về server riêng, tạo bản ghi trong Notion...).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Node** ở node Webhook hoặc gửi một request thử nghiệm từ Dropbox để kiểm tra luồng dữ liệu chạy qua các nhánh `Switch File vs Folder`.
- Sau khi kiểm tra mọi thứ chạy mượt mà, các sếp hãy bật công tắc **Active** ở góc trên cùng bên phải để workflow chính thức trực chiến 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Kết hợp thêm node Telegram hoặc Slack ngay sau bước phát hiện file mới để đội ngũ nhận được thông báo ngay lập tức.
- **Quản lý lỗi (Error Handling):** Thêm Error Trigger vào n8n để nếu kết nối Dropbox hoặc NocoDB gặp sự cố mạng, hệ thống sẽ tự động gửi email cảnh báo cho quản trị viên.
- **Lưu trữ file đính kèm:** Có thể kết hợp thêm bước tự động tải file từ Dropbox về Google Drive hoặc lưu trữ nội bộ bằng các node chuyên dụng.

### 📌 Kết luận
Với workflow giám sát Dropbox kết hợp NocoDB này, các sếp sẽ tiết kiệm được rất nhiều thời gian quản lý tài liệu, tránh việc bỏ sót file và tự động hóa toàn bộ quy trình vận hành dữ liệu của doanh nghiệp. Hãy áp dụng ngay vào hệ thống của mình nhé!