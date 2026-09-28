---
title: "🚀 Tự động tạo Podcast đa giọng đọc AI cực kỳ tự nhiên từ Google Sheets với n8n"
description: "Hướng dẫn cấu hình workflow n8n tự động hóa quy trình tạo podcast đa giọng đọc (multispeaker) sử dụng AI, kết hợp Google Sheets và Google Drive."
slug: "tu-dong-tao-podcast-da-giong-doc-ai-tu-nhien-google-sheets-n8n"
tags: [n8n, automation, no-code, AI, Google Sheets, Google Drive, Podcast]
keywords: [n8n workflow, tạo podcast bằng AI, multispeaker podcast, tự động hóa Google Sheets, AI voice generator]
---

# 🚀 Tạo Podcast Đa Giọng Đọc AI Tự Nhiên Từ Google Sheets với n8n

Việc sản xuất nội dung âm thanh hoặc podcast thủ công thường ngốn rất nhiều thời gian từ khâu viết kịch bản, phân chia giọng đọc cho đến thu âm và dựng file. Nếu các sếp đang muốn tự động hóa hoàn toàn quy trình này để tạo ra các chương trình audio, bản tin hoặc nội dung Marketing bằng giọng đọc AI tự nhiên như người thật thì đây chính là workflow hoàn hảo!

Workflow này sẽ tự động đọc kịch bản từ **Google Sheets**, gọi API tạo giọng đọc AI đa nhân vật (multispeaker), kiểm tra trạng thái xử lý, tải file audio hoàn chỉnh và lưu trữ gọn gàng lên **Google Drive** mà không cần đụng đến một dòng code phức tạp nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Biến văn bản kịch bản thô thành file audio hoàn chỉnh chỉ với vài cú click hoặc chạy tự động theo lịch.
- **Giọng đọc AI chân thực:** Hỗ trợ đa giọng đọc (multispeaker), tạo ngữ điệu tự nhiên, sống động như một cuộc trò chuyện thật.
- **Quản lý tập trung:** Kịch bản lưu ở Google Sheets, file audio thành phẩm tự động đồng bộ thẳng vào Google Drive.
- **Hoạt động tự động thông minh:** Có cơ chế chờ (Wait) và kiểm tra trạng thái (Status check) để đảm bảo file audio được render thành công trước khi tải về.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản **Google Sheets** (chứa file kịch bản podcast).
- Tài khoản **Google Drive** (nơi lưu trữ file audio xuất ra).
- API Key/Credentials của dịch vụ tạo giọng đọc AI (tích hợp qua node `HTTP Request`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON tải từ nguồn gốc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình kỹ các node trọng điểm sau:
- **Node `Get Podcast text` (Google Sheets):** Kết nối tài khoản Google của các sếp, chọn đúng file Google Sheets chứa kịch bản podcast và chọn đúng sheet/range dữ liệu.
- **Node `Full Podcast Text` (Code) & `Get all rows` (Aggregate):** Kiểm tra cấu trúc dữ liệu đầu ra để đảm bảo kịch bản được gom nhóm chính xác trước khi gửi sang dịch vụ AI.
- **Node `Create Audio` & `Get status` (HTTP Request):** Cấu hình Endpoint API, Headers và Authentication Key của dịch vụ chuyển văn bản thành giọng nói AI mà các sếp đang sử dụng.
- **Node `Wait 60 sec.` (Wait):** Điều chỉnh thời gian chờ phù hợp nếu file audio của các sếp có độ dài lớn, giúp hệ thống kịp render xong trước khi gọi lệnh lấy file.
- **Node `Upload Audio` (Google Drive):** Chọn thư mục đích trên Google Drive để lưu trữ các file audio hoàn thành.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** tại node `When clicking ‘Test workflow’` để kiểm tra toàn bộ luồng chạy với dữ liệu mẫu.
- Sau khi test thành công, bật nút **Active** để workflow sẵn sàng phục vụ các sếp bất cứ lúc nào.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối thông báo:** Thêm node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay về máy cho các sếp kèm link file audio trên Google Drive mỗi khi render xong.
- **Lên lịch tự động (Cron):** Thay thế node `Manual Trigger` bằng `Schedule Trigger` để tự động tạo podcast hàng ngày hoặc hàng tuần từ các kịch bản mới được cập nhật trên Google Sheets.
- **Quản lý trạng thái:** Thêm một bước cập nhật ngược lại Google Sheets (Cập nhật cột "Trạng thái" thành "Đã xong" và gắn link Audio) để dễ dàng theo dõi tiến độ sản xuất.

### 📌 Kết luận
Workflow tạo podcast đa giọng đọc AI này là vũ khí cực kỳ lợi hại cho các nhà sáng tạo nội dung, marketer và doanh nghiệp muốn tối ưu hóa sản xuất content audio. Hãy cài đặt ngay hôm nay để đưa quy trình làm việc của các sếp lên một tầm cao mới!