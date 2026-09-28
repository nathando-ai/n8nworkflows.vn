---
title: "🚀 Tự động tạo phụ đề AI cho video với ZapCap và Google Drive trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa hoàn toàn quy trình tạo phụ đề (caption) chuyên nghiệp cho video bằng ZapCap AI thông qua Google Drive."
slug: "tu-dong-tao-phu-de-ai-video-zapcap-google-drive-n8n"
tags: [n8n, automation, zapcap, google-drive, ai-video, content-creation]
keywords: [n8n workflow, tự động hóa tạo phụ đề video, zapcap ai, google drive trigger, làm phụ đề video tự động]
---

# 🚀 Tự động tạo phụ đề AI cho video với ZapCap và Google Drive

Các sếp làm nội dung video có thấy mệt mỏi khi cứ phải ngồi hàng giờ liền để nghe lại video, gõ từng dòng phụ đề (subtitle) rồi chỉnh sửa thời gian hiển thị không? Việc này không chỉ tốn thời gian mà còn làm chậm tiến độ xuất bản nội dung lên TikTok, Reels hay YouTube Shorts.

Giải pháp ở đây là gì? Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình: Chỉ cầnném video gốc vào một thư mục Google Drive, hệ thống sẽ tự động gửi qua **ZapCap AI** để tạo phụ đề chuyên nghiệp, sau đó tải về và lưu ngược lại vào Google Drive. Mọi thứ diễn ra tự động mà không cần tốn một phút thao tác thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- 🚀 **Tiết kiệm thời gian tuyệt đối**: Không còn cảnh ngồi gõ caption thủ công, giải phóng hàng giờ đồng hồ làm việc.
- ⚡ **Tăng tốc sản xuất nội dung**: Video có phụ đề chuẩn chỉnh sẵn sàng lên sóng chỉ sau vài phút.
- 🎯 **Kết quả chuyên nghiệp**: Phụ đề sinh bởi AI chính xác, định dạng bắt mắt, thu hút người xem.
- ☁️ **Vận hành đám mây 100%**: Không cần phần mềm nặng nhọc cài trên máy tính, chạy ngầm mượt mà 24/7.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google Drive** (để cấu hình OAuth2 credentials và các Trigger).
- **Tài khoản ZapCap & API Key**: Đăng ký và lấy API Key miễn phí tại [ZapCap Dashboard](https://platform.zapcap.ai/dashboard/api-key).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ n8n template (ID: 8938) hoặc copy đoạn JSON và paste trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Google Drive Trigger**: Kết nối tài khoản Google Drive của các sếp. Chọn một thư mục nguồn (Source Folder) chuyên để chứa các video mới cần làm phụ đề.
- **Upload video to ZapCap (HTTP Request)**: 
  - Đảm bảo video trong thư mục Google Drive được cấp quyền chia sẻ *"Anyone with the link"* (Bất kỳ ai có đường liên kết đều có thể xem) để ZapCap có thể truy cập và lấy file video.
- **Trigger video processing & Get processing task & Download completed video (HTTP Request)**:
  - Cấu hình Header Authentication cho các request gọi tới API của ZapCap. Header Name bắt buộc phải đặt là `x-api-key` và điền chuỗi API Key lấy từ tài khoản ZapCap của các sếp.
- **Wait (Node)**: Node này có nhiệm vụ chờ đợi quá trình render video của AI (thường mất từ 30 giây đến 2 phút tùy độ dài video).
- **Upload file (Google Drive)**:
  - Chọn thư mục đích (Destination Folder) trên Google Drive để lưu video hoàn chỉnh sau khi đã có phụ đề. 
  - **Lưu ý quan trọng**: Nên để thư mục chứa video đầu ra khác với thư mục nguồn (Source Folder) để tránh việc workflow bị kích hoạt lặp vô hạn (infinite loop).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử tải một video ngắn lên thư mục nguồn trên Google Drive để test xem toàn bộ chuỗi hoạt động có trơn tru không.
- Sau khi test thành công, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Gắn thêm node Telegram hoặc Slack vào cuối workflow để nhận thông báo ngay khi video chạy phụ đề xong và sẵn sàng đăng tải.
- **Tự động đăng mạng xã hội**: Nối tiếp node Google Drive cuối cùng với các node đăng bài tự động lên TikTok, YouTube hoặc Facebook Reels.
- **Quản lý log**: Thêm bước ghi lại lịch sử các video đã xử lý vào Google Sheets để dễ dàng theo dõi hiệu suất sản xuất content.

### 📌 Kết luận
Workflow tạo phụ đề AI với ZapCap và Google Drive thực sự là "vũ khí bí mật" cho các nhà sáng tạo nội dung và Digital Marketer. Thiết lập một lần, tự động hóa dài lâu. Chúc các sếp cài đặt thành công và sản xuất ngàn triệu view!