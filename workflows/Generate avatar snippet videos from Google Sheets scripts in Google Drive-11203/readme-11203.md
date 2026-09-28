---
title: "🚀 Tự động tạo video snippet avatar từ Google Sheets và AI Veo trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động đọc kịch bản từ Google Sheets, tạo video snippet bằng Google Gemini Veo và lưu trữ trực tiếp lên Google Drive."
slug: "tu-dong-tao-video-avatar-tu-google-sheets-va-ai-veo"
tags: [n8n, automation, google-sheets, google-drive, google-gemini, ai-video]
keywords: [n8n workflow, tạo video tự động, google sheets n8n, google gemini veo, ai video generator, automation content]
---

# 🚀 Tự động tạo video snippet avatar từ Google Sheets và Google Drive với n8n

Việc sản xuất hàng loạt các đoạn video snippet ngắn (video ngắn, video quảng cáo, video avatar) theo kịch bản có sẵn thường ngốn rất nhiều thời gian của các nhà sáng tạo nội dung và đội ngũ marketing. Việc copy từng đoạn kịch bản, dựng hình, render rồi lưu trữ thủ công dễ dẫn đến sai sót và mệt mỏi.

Được phát triển bởi **Angel Menendez** (Staff Developer Advocate tại n8n), workflow này giải quyết triệt để bài toán trên bằng cách tự động hóa 100%: đọc kịch bản từ Google Sheets, kết hợp mô hình AI tạo video tiên tiến (Google Gemini / Veo) để tạo video, sau đó tự động lưu vào Google Drive và cập nhật ngược lại link video vào bảng tính.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Chuyển đổi hàng loạt kịch bản văn bản thành video snippet chỉ với 1 cú click (hoặc lên lịch chạy tự động).
- **Đồng bộ thông minh:** Tự động đẩy file video lên Google Drive và điền link chia sẻ ngược lại vào Google Sheets tương ứng với từng dòng kịch bản.
- **Tận dụng sức mạnh AI:** Ứng dụng mô hình tạo video hiện đại của Google Gemini/Veo để tạo hình ảnh và chuyển động mượt mà.
- **Quy trình lặp (Looping) tối ưu:** Xử lý từng dòng dữ liệu tuần tự, tránh bị quá tải API hoặc lỗi hệ thống.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google** đã kết nối với n8n (OAuth2 cho Google Sheets và Google Drive).
- **Google Gemini API Key** (Google Palm/Gemini API credentials) hỗ trợ tạo video bằng Veo.
- **1 Google Sheet mẫu** chứa nội dung kịch bản (Script) và mô tả Avatar (Avatar Description).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ nguồn gốc (n8n.io/workflows/11203) hoặc copy đoạn JSON và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 10 nodes chính hoạt động nhịp nhàng với nhau. Các sếp cần chú ý cấu hình kỹ các node sau:

- **`Global Variables` & `Set Loop Inputs`**: Nơi khai báo các biến toàn cục và tham số đầu vào cho vòng lặp. Hãy kiểm tra lại tên các cột trong Google Sheets của các sếp có khớp với tên biến trong n8n hay không.
- **`Get Script` & `Get Avatar Description` (Google Sheets Nodes)**: 
  - Chọn tài khoản Google Sheets Credentials đã liên kết.
  - Trỏ đến đúng File ID và Sheet Name (Tên trang tính) chứa kịch bản video của các sếp.
- **`Generate a video with Veo` (Google Gemini Node)**:
  - Cấu hình Credentials sử dụng `Google Palm/Gemini API`.
  - Tinh chỉnh Prompt theo ý muốn (mặc định node này lấy dữ liệu mô tả avatar `{{ $json.Description }}` và khung hình `{{ $json.framing }}` từ Google Sheets để tạo video).
- **`Upload video file` (Google Drive Node)**:
  - Chọn Google Drive Credentials.
  - Chọn thư mục đích (Folder ID) trên Google Drive nơi lưu trữ các video được tạo ra.
- **`Update row in sheet with link to video` (Google Sheets Node)**:
  - Cấu hình operation là `update`.
  - Đảm bảo ánh xạ đúng dòng dữ liệu và ghi link file Google Drive (`webViewLink` hoặc `webContentLink`) vào cột tương ứng trên Sheet.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm (Test run) với 1-2 dòng dữ liệu đầu tiên.
- Kiểm tra kết quả trên Google Drive và Google Sheets xem video đã được sinh ra và cập nhật link thành công chưa.
- Sau khi mọi thứ chạy mượt mà, hãy gạt công tắc sang chế độ **Active** để chính thức vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Trigger theo thời gian (Schedule Trigger):** Thay vì dùng nút `Manual Trigger`, các sếp có thể thay thế bằng Schedule Trigger để n8n tự động quét Google Sheets và tạo video vào mỗi khung giờ cố định trong ngày.
- **Tích hợp thông báo Telegram/Slack:** Thêm một node thông báo gửi về Telegram hoặc Slack cá nhân/nhóm ngay sau khi workflow chạy xong toàn bộ danh sách kịch bản.
- **Lưu trữ Log lỗi:** Sử dụng Error Trigger để bắt lỗi nếu có dòng nào đó quá hạn mức API hoặc lỗi tạo video từ Gemini, giúp các sếp dễ dàng kiểm tra và xử lý lại.

### 📌 Kết luận
Workflow tạo video snippet avatar từ Google Sheets này là một "vũ khí" cực mạnh mẽ giúp tiết kiệm hàng tá giờ làm việc thủ công cho các nhà sáng tạo nội dung. Hãy thiết lập ngay hôm nay để tối ưu hóa quy trình sản xuất video của các sếp!