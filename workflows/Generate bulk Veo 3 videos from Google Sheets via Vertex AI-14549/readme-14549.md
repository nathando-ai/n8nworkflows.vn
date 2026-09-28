---
title: "🚀 Tự động tạo hàng loạt video Veo 3 từ Google Sheets qua Vertex AI bằng n8n"
description: "Hướng dẫn xây dựng pipeline tự động hóa tạo video hàng loạt với Vertex AI từ Google Sheets, tự động kiểm tra trạng thái, lưu trữ Google Drive và cập nhật kết quả."
slug: "tu-dong-tao-video-veo-3-tu-google-sheets-vertex-ai"
tags: [n8n, automation, vertex-ai, google-sheets, google-drive, video-generation]
keywords: [n8n workflow, tạo video tự động, vertex ai veo 3, google sheets automation, n8n google drive]
---

# 🚀 Tự động tạo hàng loạt video Veo 3 từ Google Sheets qua Vertex AI

Việc tạo video bằng AI hàng loạt (bulk video generation) thường ngốn rất nhiều thời gian thủ công: từ việc nhập prompt, gọi API, chờ đợi render, tải xuống cho đến việc lưu trữ và cập nhật link vào bảng tính quản lý. 

Giải pháp? Workflow n8n này sẽ tự động hóa toàn bộ quy trình từ A-Z: nhận dữ liệu từ Google Sheets, gửi yêu cầu tới Vertex AI, lặp lại tiến trình kiểm tra trạng thái render, tự động tải video lên Google Drive và trả kết quả ngược lại Google Sheets hoàn toàn không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chỉ cần điền prompt vào Google Sheets, hệ thống sẽ tự sinh video chạy ngầm.
- **Vòng lặp thông minh (Loop & Wait):** Tự động kiểm tra trạng thái video từ Vertex AI cho đến khi hoàn thành mà không sợ lỗi timeout.
- **Đồng bộ đa nền tảng:** Tự động convert file video, lưu trữ an toàn trên Google Drive và ghi nhận link truy cập trực tiếp vào Sheet.
- **Xử lý lỗi chuyên nghiệp:** Tự động bắt lỗi phát sinh và cập nhật trạng thái lỗi vào Google Sheet để dễ dàng theo dõi, xử lý lại.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Self-hosted hoặc Cloud).
- Tài khoản Google Cloud Platform (GCP) đã kích hoạt Vertex AI API.
- Tài khoản Google Drive & Google Sheets (có quyền truy cập API/OAuth2).
- File Google Sheet mẫu chứa danh sách prompt tạo video.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc copy trực tiếp mã JSON từ n8n Hub, sau đó dán vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Google Sheet Trigger (Webhook):** Cấu hình webhook để nhận sự kiện kích hoạt từ Google Sheet mỗi khi có dòng dữ liệu mới hoặc yêu cầu tạo video được thêm vào.
- **Data collection (Set):** Gom nhóm dữ liệu đầu vào từ Google Sheets (Prompt, cài đặt tỷ lệ khung hình, độ dài...) trước khi đẩy qua AI.
- **Vertex AI Send for Generation (HTTP Request):** Cấu hình API Endpoint và thông tin xác thực OAuth2/Service Account của Google Cloud Vertex AI để gửi yêu cầu khởi tạo video Veo 3.
- **Fetch/Check Video & Wait before next video check:** Cấu hình node HTTP Request kết hợp node **Wait** để tạo cơ chế polling (lặp kiểm tra trạng thái) định kỳ cho đến khi video render xong.
- **Upload Video to Drive (Google Drive):** Kết nối tài khoản Google Drive OAuth2 để lưu trữ các file video thành phẩm vào thư mục định sẵn.
- **Update video Link in sheet & Update Eror in Sheet (Google Sheets):** Cấu hình tài khoản Google Sheets OAuth2 để cập nhật link video thành công hoặc ghi chú lỗi (nếu có) vào các cột tương ứng trên bảng tính.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một dòng dữ liệu mẫu để kiểm tra toàn bộ luồng từ Vertex AI đến Google Drive.
- Bật công tắc **Active** để đưa workflow vào trạng thái vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack vào nhánh thành công/thất bại để nhận thông báo tức thì ngay khi video được render xong hoặc gặp sự cố.
- **Quản lý phân loại thư mục:** Tự động tạo thư mục con trên Google Drive theo ngày tháng hoặc tên chiến dịch để quản lý video khoa học hơn.
- **Báo cáo định kỳ:** Kết hợp thêm node cron/schedule để tổng hợp số lượng video đã tạo thành công gửi báo cáo qua Email vào cuối ngày.

### 📌 Kết luận
Workflow tạo video tự động hàng loạt với Vertex AI và Google Sheets là một "vũ khí" cực mạnh cho các Agency, nhà sáng tạo nội dung và đội ngũ marketing. Hãy triển khai ngay hôm nay để tiết kiệm hàng chục giờ làm việc thủ công!