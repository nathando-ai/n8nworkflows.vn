---
title: "🚀 Giám sát người cao tuổi qua LINE và AI Gemini với n8n và Google Sheets"
description: "Tự động hóa chăm sóc người cao tuổi bằng cách theo dõi tin nhắn LINE, phân tích cảm xúc bằng AI Gemini, ghi log Google Sheets và cảnh báo khẩn cấp tự động."
slug: "giam-sat-nguoi-cao-tuoi-line-gemini-google-sheets"
tags: [n8n, automation, line, gemini, google-sheets, ai]
keywords: [n8n workflow, chăm sóc người cao tuổi, line bot ai, gemini sentiment analysis, tự động hóa n8n]
---

# 🚀 Tự Động Hóa Chăm Sóc Người Cao Tuổi: Giám Sát LINE & Phân Tích Cảm Xúc AI Gemini

Các sếp có bao giờ lo lắng về việc ở xa không thể nắm bắt tình hình sức khỏe hay tinh thần của ông bà, cha mẹ lớn tuổi ở nhà không? Việc gọi điện hỏi thăm mỗi ngày đôi khi không khả thi, và những thay đổi nhỏ trong tâm trạng hay sự im lặng bất thường rất dễ bị bỏ quên.

Workflow n8n này chính là giải pháp "người gác cửa" thông minh 100% không cần code. Hệ thống sẽ tự động kết nối ứng dụng **LINE** quen thuộc của người cao tuổi với trí tuệ nhân tạo **Google Gemini** để phân tích cảm xúc tin nhắn, ghi nhận vào **Google Sheets**, và tự động gửi cảnh báo khẩn cấp cho con cháu khi phát hiện dấu hiệu bất thường hoặc sự im lặng kéo dài.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **An tâm từ xa:** Tự động theo dõi các hoạt động hằng ngày qua tin nhắn LINE mà không làm phiền sự riêng tư của người lớn tuổi.
- **Phát hiện rủi ro sớm nhờ AI:** Sử dụng Google Gemini để phân tích cảm xúc (sentiment), kịp thời phát hiện các dấu hiệu tiêu cực, lo âu hoặc đau buồn để cảnh báo gia đình.
- **Kiểm tra sự vắng mặt (Inactivity Check):** Tự động gửi nhắc nhở nhẹ nhàng lúc 11:00 trưa nếu chưa thấy tương tác và escalate (leo thang) cảnh báo khẩn cấp sau 3 tiếng nếu vẫn im lặng.
- **Hoạt động tự động 24/7:** Vận hành bền bỉ trên n8n, ghi log đầy đủ minh bạch vào Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **LINE Developers** (để tạo LINE Bot và lấy Webhook).
- Tài khoản **Google Cloud / Google Drive** (để tạo Google Sheets và Google Gemini API Key).
- Google Gemini API Key.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy toàn bộ mã nguồn JSON, sau đó paste trực tiếp vào màn hình n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số sau trong các node quan trọng:

- **LINE Webhook (Node `LINE Webhook`):** Cấu hình đường dẫn Webhook path và phương thức `POST`. Sau đó, lấy URL Production của webhook này dán vào phần cài đặt Webhook trong LINE Developers Console.
- **Cấu hình người dùng (Node `Config` và `Config for Daily`):** Mở node này để điền các thông tin quan trọng như `PARENT_LINE_ID` (LINE ID của ông bà/cha mẹ), `CHILD_LINE_ID` (LINE ID của con cháu nhận tin nhắn), và `SHEET_ID`.
- **Google Sheets (Nodes `Log to Sheets` và `Read Logs`):** Chuẩn bị sẵn một Google Sheet với các tiêu đề cột: `Date`, `Time`, `Message`, `Sentiment`, `Alert`. Kết nối tài khoản Google Sheets credentials và trỏ tới file sheet này.
- **AI Phân tích (Node `Gemini: Analyze`):** Nhập Google Gemini API Key để cho phép AI đọc nội dung tin nhắn LINE và đánh giá mức độ rủi ro (sentiment/risk).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng cách gửi một tin nhắn mẫu qua LINE Bot để kiểm tra luồng nhận Webhook, Gemini phân tích và ghi dữ liệu vào Google Sheets.
- Sau khi mọi thứ chạy mượt mà, gạt công tắc **Active workflow** sang màu xanh để hệ thống bắt đầu giám sát tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm kênh cảnh báo:** Ngoài LINE, các sếp có thể nối thêm node Telegram hoặc Slack vào nhánh cảnh báo (`Alert Child`, `Emergency Alert`) để đa dạng hóa kênh nhận thông tin.
- **Báo cáo tuần:** Kết hợp thêm một Schedule Trigger chạy vào Chủ Nhật hàng tuần để tổng hợp tâm trạng, tần suất nhắn tin gửi vào email cho con cháu theo dõi sức khỏe tinh thần dài hạn của người thân.
- **Lưu lịch sử lỗi:** Thêm node Error Trigger để bắt các sự cố kết nối API và gửi thông báo về Zalo/Telegram cá nhân của lập trình viên.

### 📌 Kết luận
Ứng dụng AI và tự động hóa vào việc chăm sóc gia đình chưa bao giờ dễ dàng đến thế. Với workflow n8n này, các sếp vừa tiết kiệm được thời gian kiểm tra, vừa đảm bảo sự an toàn tối đa cho người thân yêu mỗi ngày. Hãy triển khai ngay hôm nay nhé!