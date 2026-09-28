---
title: "🚀 Tự động hóa xử lý hóa đơn Outlook bằng GPT-4.1-mini và lưu trữ OneDrive Excel"
description: "Hướng dẫn chi tiết workflow n8n tự động đọc email hóa đơn từ Outlook, trích xuất dữ liệu bằng AI, lưu file PDF vào OneDrive và ghi log vào Excel."
slug: "tu-dong-hoa-xu-ly-hoa-don-outlook-gpt-4-mini-onedrive-excel"
tags: [n8n, automation, no-code, outlook, openai, onedrive, excel]
keywords: [n8n workflow, xử lý hóa đơn tự động, outlook to excel, ai extract invoice, gpt-4-mini n8n]
---

# 🚀 Tự động hóa xử lý hóa đơn Outlook bằng GPT-4.1-mini và lưu trữ OneDrive Excel

Các sếp có đang cảm thấy mệt mỏi mỗi khi cuối tháng hoặc cuối tuần phải ngồi "bới tung" hòm thư Outlook, tải từng file PDF hóa đơn về máy, đọc thủ công từng con số rồi hì hục copy-paste vào file Excel quản lý? Công việc thủ công này không chỉ ngốn hàng giờ đồng hồ quý giá mà còn cực kỳ dễ xảy ra sai sót (như nhầm tiền thuế, sót hóa đơn, sai tên nhà cung cấp).

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ mạnh mẽ: tự động hóa 100% quy trình từ lúc email hóa đơn đến, bóc tách dữ liệu thông minh bằng AI, lưu trữ tệp đính kèm khoa học trên OneDrive và cập nhật thẳng vào bảng Excel của doanh nghiệp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần nhập liệu thủ công, mọi hóa đơn đều được xử lý ngay khi vừa xuất hiện trong hộp thư.
- **Độ chính xác cao:** Sử dụng mô hình **GPT-4.1-mini** thông minh để bóc tách chính xác 14 trường dữ liệu quan trọng từ nội dung email và file PDF đính kèm.
- **Lưu trữ khoa học:** File PDF hóa đơn được tự động đổi tên chuẩn chỉnh và lưu vào các thư mục theo ngày trên OneDrive.
- **Báo cáo tổng kết tiện lợi:** Tự động gửi email tổng hợp (Daily Digest) hàng ngày giúp các sếp nắm bắt tình hình tài chính nhanh chóng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** Đã cài đặt sẵn (phiên bản Cloud hoặc Self-hosted).
- **Microsoft Outlook Account & Credentials:** Tài khoản Microsoft 365 có cấu hình OAuth2 để đọc và gửi email.
- **Microsoft Graph API Credentials:** Dùng để tương tác với OneDrive và Excel thông qua `microsoftExcel` và `httpRequest`.
- **OpenAI API Key:** Để kết nối với node AI sử dụng model `gpt-4.1-mini`.
- **File Excel trên OneDrive:** Đã tạo sẵn một bảng (Table) quản lý hóa đơn (ví dụ: `tblInvoices`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy mã JSON của workflow này, vào giao diện n8n chọn **Add workflow** -> Nhấp vào biểu tượng menu (3 chấm) ở góc trên bên phải -> Chọn **Import from Clipboard** và dán đoạn JSON vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công, các sếp cần cấu hình lại các node sau cho khớp với hệ thống của mình:

- **Schedule — Daily Trigger:** Mặc định lịch chạy là 7 giờ sáng mỗi ngày. Các sếp có thể thay đổi thời gian này nếu muốn.
- **Outlook — Get Unread Emails:** Chọn đúng credentials tài khoản Outlook của các sếp, sau đó cập nhật thông số `foldersToInclude` trỏ đúng vào thư mục Inbox cần quét.
- **OpenAI — GPT-4.1-mini Model:** Thêm OpenAI API credentials và đảm bảo model được chọn là `gpt-4.1-mini`. Node AI kế tiếp (**AI — Extract Invoice Fields**) sẽ tự động bóc tách 14 trường dữ liệu từ email.
- **Excel — Append Invoice Row:** Cấu hình credentials Microsoft Graph, sau đó cập nhật đúng thông tin Workbook, Worksheet và Table ID tương ứng với bảng `tblInvoices` của các sếp trên OneDrive.
- **Code — Build Digest Email:** Cập nhật đường dẫn `oneDriveFolderUrl` trỏ về thư mục chứa hóa đơn trên OneDrive của doanh nghiệp.
- **Outlook — Send Daily Digest:** Điền địa chỉ email người nhận báo cáo tổng kết hàng ngày.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử với dữ liệu mẫu (Test run) và kiểm tra xem dữ liệu đã được đẩy vào Excel hay chưa.
- Sau khi test thành công, gạt công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình quản lý hóa đơn hơn nữa, các sếp có thể mở rộng workflow với các ý tưởng sau:
- **Tích hợp Slack/Telegram:** Thêm node gửi thông báo ngay lập tức vào nhóm chat công ty mỗi khi có hóa đơn giá trị lớn được ghi nhận.
- **Lưu log lỗi:** Kết hợp nhánh Error Trigger để gửi email cảnh báo về bộ phận kỹ thuật nếu quá trình bóc tách AI hoặc kết nối Excel gặp sự cố.
- **Phân loại theo nhà cung cấp:** Tự động tạo thư mục con trên OneDrive dựa trên tên nhà cung cấp được AI bóc tách thay vì chỉ gom nhóm theo ngày.

### 📌 Kết luận
Tự động hóa quy trình xử lý hóa đơn với n8n, OpenAI và Microsoft 365 là bước tiến lớn giúp doanh nghiệp tối ưu hóa vận hành, loại bỏ sai sót thủ công và tiết kiệm chi phí nhân sự đáng kể. Chúc các sếp cài đặt thành công! Nếu gặp khó khăn gì, hãy để lại bình luận hoặc trao đổi trực tiếp nhé.