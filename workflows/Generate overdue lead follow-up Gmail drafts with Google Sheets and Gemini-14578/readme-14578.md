---
title: "🚀 Tự động tạo bản nháp email chăm sóc khách hàng tiềm năng quá hạn với Google Sheets và Gemini"
description: "Xây dựng hệ thống n8n tự động quét danh sách lead, phân tích biên bản cuộc họp bằng Google Gemini và tạo Gmail Draft chuẩn hóa, giúp sales tiết kiệm hàng giờ mỗi ngày."
slug: "tu-dong-tao-nhap-email-cham-soc-lead-google-sheets-gemini"
tags: [n8n, automation, google-sheets, google-gemini, gmail, slack, lead-nurturing]
keywords: [n8n workflow, tự động hóa chăm sóc lead, google sheets gemini, tạo email tự động n8n, gmail draft automation]
---

# 🚀 Tự động tạo bản nháp email chăm sóc khách hàng tiềm năng quá hạn với Google Sheets và Gemini

Các sếp làm sales chắc chắn hiểu cảm giác "quên" follow-up lead sau 5-7 ngày vì quá bận rộn với hàng tá công việc thủ công. Việc lục lại lịch sử chat, đọc lại biên bản cuộc họp cũ và ngồi viết từng chiếc email cá nhân hóa ngốn rất nhiều thời gian quý báu.

Đừng lo, workflow n8n cực kỳ thông minh này sẽ thay các sếp làm toàn bộ những việc "nhàm chán" đó: Tự động quét Google Sheets mỗi sáng, lọc ra các lead quá hạn chưa liên hệ, đọc file ghi chú cuộc họp từ Google Drive, nhờ **Google Gemini** viết một email cực kỳ cá nhân hóa và lưu thẳng vào **Gmail Draft** để sales chỉ cần bấm nút gửi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% mỗi sáng:** Chạy định kỳ lúc 9h sáng các ngày trong tuần (Weekday), không bỏ sót bất kỳ lead nào.
- **Cá nhân hóa đỉnh cao bằng AI:** Sử dụng Google Gemini đọc hiểu biên bản cuộc họp (TXT, PDF) để viết nội dung follow-up cực kỳ sát sườn và chuyên nghiệp.
- **An toàn tuyệt đối:** Workflow chỉ lưu vào **Gmail Draft (Bản nháp)**, sales vẫn là người kiểm duyệt cuối cùng trước khi bấm gửi.
- **Cảnh báo lỗi thông minh:** Tích hợp Slack để báo động ngay lập tức nếu thiếu file transcript, lỗi tải file hoặc định dạng file không hỗ trợ.
- **Chống trùng lặp (Deduplication):** Sau khi tạo bản nháp, trạng thái lead tự động cập nhật thành *Draft Created* để không bị lặp lại vào ngày mai.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Cloud hoặc Self-hosted VPS).
- **Google Sheets:** Chứa danh sách lead với các cột chuẩn (xem chi tiết bên dưới).
- **Google Drive / Google Docs:** Nơi lưu trữ file biên bản cuộc họp (Meeting Transcript) định dạng TXT hoặc PDF.
- **Google Gemini API (Google Palm API):** Để AI xử lý văn bản và viết email.
- **Gmail Account:** Kết nối qua OAuth2 để tạo bản nháp email.
- **Slack Workspace & Webhook/OAuth2:** Để nhận thông báo trạng thái và cảnh báo lỗi.
:::

---

## Cấu trúc Google Sheets chuẩn yêu cầu

Các sếp cần chuẩn bị một Google Sheet với các cột sau để workflow nhận diện chính xác:

| Cột | Mô tả chi tiết |
|---|---|
| `Current status` | Trạng thái lead: `New`, `Draft Created`, `Sent`, `Closed` |
| `Last Contact` | Ngày liên hệ cuối cùng với lead |
| `Name` | Tên đầy đủ của khách hàng |
| `Company` | Tên công ty khách hàng |
| `Email` | Địa chỉ email của khách hàng |
| `Meeting Transcript` | Link Google Drive trỏ đến file biên bản cuộc họp |
| `Sales Rep` | Tên nhân viên sales phụ trách lead đó |
| `FollowUp Draft Creation date` | Hệ thống tự điền ngày tạo bản nháp |

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ kho lưu trữ n8n (Link gốc: `https://n8n.io/workflows/14578`) và import trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các node quan trọng sau:
- **Daily 9AM Trigger:** Node `scheduleTrigger` thiết lập lịch chạy tự động mỗi sáng (Thứ 2 - Thứ 6).
- **Read Leads Sheet & Update FollowUp Status with Dates:** Kết nối tài khoản Google Sheets OAuth2, thay `YOUR_SHEET_ID` bằng ID sheet thực tế của các sếp.
- **Filter - Active Leads Only & Filter - 5+ Days No Contact:** Kiểm tra lại tên các cột trong Google Sheet để đảm bảo điều kiện lọc đúng (Status = New, Quá hạn 5+ ngày, có link transcript).
- **HTTP - Download File from Google Drive:** Đảm bảo link Google Drive ở chế độ có thể truy cập công khai (Anyone with the link can view) hoặc cấp quyền cho n8n đọc file.
- **Google Gemini Chat Model:** Cấu hình credentials Google Gemini (`googlePalmApi`) để AI có đủ "công lực" viết email.
- **Gmail - Create Draft:** Kết nối tài khoản Gmail OAuth2 để n8n có quyền tạo bản nháp trong hộp thư.
- **Các node Slack (Alert & Notify):** Cấu hình Slack OAuth2 và trỏ đúng Channel ID của team sales để nhận thông báo khi bản nháp đã sẵn sàng hoặc khi có lỗi xảy ra (thiếu file, lỗi tải file...).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) thủ công từng cụm node hoặc toàn bộ workflow với một dòng dữ liệu mẫu trong Google Sheets.
- Kiểm tra xem bản nháp đã xuất hiện trong Gmail chưa và Slack có bắn tin nhắn báo về không.
- Nếu mọi thứ mượt mà, gạt công tắc **Active** xanh rờn ở góc trên cùng bên phải để workflow tự động chạy ngầm.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng định dạng file:** Các sếp có thể nâng cấp node `Extract Text` hoặc tích hợp thêm tính năng chuyển đổi giọng nói thành văn bản qua Whisper/Gemini để hỗ trợ file ghi âm cuộc gọi (MP3/WAV).
- **Đa dạng hóa use case:** Ngoài chăm sóc lead, workflow này có thể "biến hóa" thành hệ thống nhắc nhở hạn chót hợp đồng, thu thập feedback sau bán hàng, hoặc check-in onboarding khách hàng mới cực kỳ chuyên nghiệp.
- **Tích hợp thêm Chatbot:** Thay vì chỉ thông báo qua Slack, các sếp có thể cấu hình thêm node gửi tin nhắn qua Telegram hoặc Zalo OA cho nhân viên sales.

### 📌 Kết luận
Việc tự động hóa quy trình follow-up lead không chỉ giúp đội ngũ sales tiết kiệm hàng chục giờ mỗi tuần mà còn đảm bảo không một khách hàng tiềm năng nào bị lãng quên. Hãy cài đặt ngay workflow này lên hệ thống n8n của các sếp để tối ưu hóa hiệu suất kinh doanh ngay hôm nay!