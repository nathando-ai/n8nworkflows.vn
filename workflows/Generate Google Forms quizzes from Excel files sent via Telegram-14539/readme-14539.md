---
title: "🚀 Tự động tạo Quiz Google Forms từ file Excel gửi qua Telegram với n8n"
description: "Biến file Excel chứa câu hỏi thành Google Forms trắc nghiệm tự động 100% chỉ bằng thao tác kéo thả file qua Telegram bot."
slug: "tao-google-forms-quiz-tu-excel-qua-telegram-n8n"
tags: [n8n, automation, telegram, google-forms, excel, no-code, document-extraction]
keywords: [n8n workflow, tạo google form tự động, excel sang google forms, telegram bot n8n, trắc nghiệm google forms]
---

# 🚀 Tự động tạo Quiz Google Forms từ file Excel gửi qua Telegram

Các sếp làm trong ngành giáo dục, đào tạo nội bộ hay tổ chức sự kiện chắc chắn đã quen thuộc với nỗi khổ: mỗi khi cần tạo một bài kiểm tra (Quiz) hay khảo sát lớn, việc ngồi copy-paste từng câu hỏi, từng đáp án từ file Excel lên Google Forms tốn hàng giờ đồng hồ, cực kỳ nhàm chán và dễ sai sót. 

Đừng lo, workflow n8n cực đỉnh được phát triển bởi tác giả **Ramdoni** sẽ giải quyết triệt để vấn đề này. Các sếp chỉ cần gửi file Excel chứa câu hỏi vào Telegram Bot, hệ thống sẽ tự động đọc dữ liệu, khởi tạo Google Form, chuyển đổi sang chế độ Quiz (chấm điểm tự động) và gửi lại link hoàn chỉnh chỉ trong vòng vài phút!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh thủ công nhập liệu từng câu hỏi trắc nghiệm.
- **Tự động hóa hoàn toàn:** Chỉ cần tương tác trực tiếp qua Telegram, cực kỳ tiện lợi trên cả điện thoại và máy tính.
- **Chuẩn hóa dữ liệu thông minh:** Tự động lọc định dạng file, xử lý hàng loạt qua cơ chế batching (chia nhỏ lô) để tránh lỗi API.
- **Tạo Quiz chuyên nghiệp:** Tự động bật chế độ chấm điểm (Quiz Mode) và thêm các câu hỏi kèm đáp án đúng chuẩn xác lên Google Forms.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** Đã chạy ổn định (Self-hosted hoặc Cloud).
- **Telegram Bot Token:** Tạo qua `@BotFather` trên Telegram.
- **Google Cloud Console Credentials:** Cần cấu hình OAuth2 hoặc API Key có quyền truy cập Google Forms API và Google Drive API.
- **Mẫu file Excel (XLSX):** Chứa danh sách câu hỏi, các đáp án và đáp án đúng theo định dạng chuẩn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy đoạn mã JSON của workflow này, sau đó vào giao diện n8n, chọn **Add workflow** -> **Import from JSON** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không lỗi, các sếp cần chú ý cấu hình kỹ các node trọng điểm sau:

- **Telegram Trigger – Receive File**: Kết nối với Telegram Bot Credentials của sếp để lắng nghe sự kiện người dùng gửi file.
- **Validate File Type (Excel Only)** và **Normalize Question Data**: Các node `code` (Javascript) giúp lọc định dạng file chỉ nhận `.xlsx` và chuẩn hóa cấu trúc dữ liệu câu hỏi từ Excel thành định dạng mà Google Forms API yêu cầu.
- **Create Google Form** & **Add Question to Form** (HTTP Request nodes): 
  - Cần cấu hình OAuth2 với tài khoản Google của sếp.
  - Đảm bảo Google Forms API đã được bật trên Google Cloud Console.
- **Enable Quiz Mode** (HTTP Request): Node này gửi request cấu hình để chuyển Google Form vừa tạo sang chế độ Quiz (có tính điểm).
- **Rate Limit Delay (2.5s)** (Wait node): Giúp giãn cách thời gian giữa các request thêm câu hỏi, tránh việc vượt quá giới hạn (Rate Limit) của Google API.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử gửi một file Excel mẫu qua Telegram Bot của sếp để test xem form đã được tạo thành công chưa.
- Sau khi test ngon lành, hãy gạt công tắc sang **Active** để bot hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình hơn nữa, các sếp có thể mở rộng workflow này bằng cách:
1. **Thông báo qua Slack/Microsoft Teams:** Gửi thêm cảnh báo hoặc link bài test vào kênh chung của phòng ban khi có người tạo quiz thành công.
2. **Lưu lịch sử vào Google Sheets:** Ghi lại thông tin người tạo, tên file Excel và link Google Form vừa tạo để dễ quản lý.
3. **Xử lý lỗi thông minh:** Kết nối nhánh lỗi (`If Not Excel` hoặc lỗi API) để gửi chi tiết lỗi bằng tiếng Việt về Telegram cho người dùng biết cách khắc phục.

### 📌 Kết luận
Workflow tích hợp Telegram và Google Forms này là một "vũ khí" cực mạnh mẽ giúp tự động hóa khâu khảo sát và tạo đề thi trắc nghiệm. Hãy cài đặt ngay hôm nay để giải phóng sức lao động khỏi những công việc lặp đi lặp lại nhé các sếp!