---
title: "🚀 Tự động hóa tạo bảng điểm học tập (Report Card) và gửi email cho phụ huynh với n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động tính toán điểm số, tạo file PDF bảng điểm chuyên nghiệp và gửi email cho phụ huynh qua Gmail."
slug: "tu-dong-hoa-tao-bang-diem-va-gui-email-cho-phu-huynh"
tags: [n8n, automation, no-code, gmail, pdf-generation, education]
keywords: [n8n workflow, tự động hóa giáo dục, tạo bảng điểm PDF tự động, gửi email học sinh n8n, html to pdf]
---

# 🚀 Tự động hóa tạo bảng điểm học tập và gửi email cho phụ huynh

Việc tổng hợp điểm số, thiết kế bảng điểm, xuất ra file PDF và gửi email thủ công cho từng phụ huynh mỗi dịp cuối kỳ là một cơn ác mộng tốn hàng giờ đồng hồ của giáo viên và bộ phận hành chính trường học. Nguy cơ tính nhầm điểm hoặc gửi nhầm bảng điểm của học sinh này cho phụ huynh học sinh khác là rất cao.

Workflow n8n này sinh ra để giải quyết triệt để nỗi đau đó! Hệ thống sẽ tự động hóa 100% quy trình: lấy dữ liệu từ bảng dữ liệu, tính toán điểm số/xếp loại, tạo giao diện bảng điểm HTML, chuyển đổi thành file PDF chuyên nghiệp, gửi email tự động qua Gmail kèm file đính kèm, đồng thời cập nhật trạng thái để tránh gửi lặp lại.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Xử lý hàng loạt bảng điểm của toàn bộ học sinh chỉ trong vài phút thay vì làm thủ công.
- **Độ chính xác tuyệt đối:** Tự động tính tổng điểm, phần trăm, xếp loại (A+, A, B...) và đưa ra nhận xét dựa trên thuật toán chuẩn hóa.
- **Chuyên nghiệp hóa:** Tạo ra các bảng điểm định dạng PDF đẹp mắt, đồng bộ layout trường học.
- **Hoạt động thông minh:** Cơ chế kiểm tra trạng thái giúp chống gửi trùng lặp, an toàn và bảo mật dữ liệu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc n8n Cloud).
- **n8n Data Table:** Nơi lưu trữ thông tin và điểm số của học sinh.
- **Gmail Account:** Tài khoản Google để cấu hình node `Send a message to Parents` (OAuth2 credentials).
- **HTML to PDF API/Service:** Credentials cho node `Convert HTML to PDF` (HTMLCSSToPDF hoặc dịch vụ tương đương).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và dán trực tiếp vào n8n Editor, hoặc import file JSON thông qua menu tuỳ chọn trong n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình các node cốt lõi sau:
- **Get row(s) (`dataTable`):** Trỏ tới Data Table chứa danh sách học sinh. Cấu hình điều kiện chỉ lấy các bản ghi có `Status` còn trống (để tránh xử lý lại những học sinh đã được gửi bảng điểm).
- **Calculate Grade and Remarks (`code`):** Kiểm tra đoạn code JavaScript tính toán điểm trung bình, phần trăm, xếp loại (A+, A, B, C, D) và các nhận xét tự động cho phù hợp với tiêu chí của trường.
- **Build HTML Report Card (`code`):** Nơi chứa mã HTML/CSS thiết kế giao diện bảng điểm. Các sếp có thể thay đổi logo trường, màu sắc hoặc bố cục tại đây.
- **Convert HTML to PDF (`n8n-nodes-htmlcsstopdf.htmlcsstopdf`):** Kết nối tài khoản API của dịch vụ chuyển đổi HTML sang PDF để tạo file tải về.
- **Send a message to Parents (`gmail`):** Chọn credentials Gmail OAuth2 đã kết nối và cấu hình nội dung email (tiêu đề, cú pháp gọi tên học sinh, điểm số và gắn link PDF).
- **Wait 3 Seconds (`wait`):** Giúp trì hoãn 3 giây giữa các lần gửi để tránh bị Google giới hạn tốc độ API (rate limit) hoặc bị đánh dấu spam.
- **Update row(s) (`dataTable`):** Cập nhật lại `Status` thành `"Sent"`, ghi nhận thời gian `Sent_At` và đường dẫn file PDF (`Report_URL`) để đánh dấu học sinh đã hoàn tất.

#### 3. Kích hoạt ⚡️
- Nhấn **Run Workflow Manually** để test thử với 1-2 dòng dữ liệu mẫu trong Data Table xem email có gửi về đúng hay không.
- Sau khi kiểm tra mọi thứ hoàn hảo, gạt công tắc sang **Active** để hệ thống sẵn sàng vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Thêm một node thông báo vào nhóm chat của giáo viên mỗi khi hệ thống hoàn tất việc gửi toàn bộ bảng điểm.
- **Lưu trữ Cloud:** Thay vì chỉ lưu link tạm thời, có thể kết hợp thêm node Google Drive hoặc OneDrive để lưu trữ file PDF vĩnh viễn phục vụ công tác tra cứu sau này.
- **Lên lịch chạy định kỳ (Schedule Trigger):** Thay thế `Manual Trigger` bằng `Schedule Trigger` để tự động hóa hoàn toàn vào cuối mỗi học kỳ mà không cần bấm nút thủ công.

### 📌 Kết luận
Workflow tự động hóa tạo bảng điểm học tập và gửi email này là trợ thủ đắc lực giúp số hóa quy trình quản lý học sinh của các cơ sở giáo dục. Hãy triển khai ngay hôm nay để tối ưu hóa thời gian và mang lại sự chuyên nghiệp tuyệt đối trong mắt phụ huynh!