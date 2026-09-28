---
title: "🚀 Tự động trích xuất chức danh từ CV ứng viên bằng Google Gemini và n8n"
description: "Hướng dẫn xây dựng sub-workflow n8n tự động đọc file PDF CV ứng viên, sử dụng AI Google Gemini để phân tích và trả về chức danh hiện tại một cách chính xác."
slug: "trich-xuat-chuc-danh-cv-google-gemini-n8n"
tags: [n8n, automation, ai-summarization, google-gemini, hr-automation]
keywords: [n8n workflow, trích xuất cv ai, google gemini n8n, tự động hóa nhân sự, đọc pdf n8n]
---

# 🚀 Tự động trích xuất chức danh từ CV ứng viên bằng Google Gemini

Các sếp làm trong ngành nhân sự (HR) chắc hẳn đã quá quen với cảm giác "ngợp thở" khi phải mở hàng trăm file CV PDF để lọc xem ứng viên đang làm vị trí gì, kinh nghiệm ra sao. Việc đọc thủ công này vừa tốn thời gian, vừa dễ bỏ sót nhân tài. 

Giải pháp là đây! Bài viết này sẽ hướng dẫn các sếp cấu hình một workflow n8n cực kỳ thông minh, đóng vai trò là một sub-workflow chuyên dụng để tự động đọc file CV PDF, "nhờ" AI Google Gemini phân tích và trích xuất chuẩn xác chức danh hiện tại của ứng viên chỉ trong tích tắc.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần mở từng file PDF thủ công để xem thông tin.
- **AI thông minh:** Sử dụng sức mạnh của Google Gemini để đọc hiểu văn bản trong CV một cách ngữ cảnh nhất.
- **Dễ dàng tích hợp:** Được thiết kế tối ưu để gọi như một sub-workflow từ các hệ thống tuyển dụng tự động lớn hơn (Job Search Automation).
- **Linh hoạt mở rộng:** Dễ dàng tùy biến prompt để trích xuất thêm kỹ năng, số năm kinh nghiệm hoặc học vấn nếu muốn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Hệ thống n8n (Self-hosted hoặc Cloud).
- Tài khoản Google AI Studio để lấy API Key của Google Gemini.
- Các file CV định dạng PDF được lưu sẵn trên ổ cứng hoặc đường dẫn mà n8n có thể truy cập.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow này và dán trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 5 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Node `Read/Write Files from Disk`**: Đây là nơi n8n đọc file CV từ ổ cứng. Các sếp cần mở node này và cập nhật lại đường dẫn file PDF (`File(s) Selector`) trỏ đúng đến vị trí lưu CV trên server/máy tính của mình.
- **Node `Extract from File`**: Node này được cấu hình sẵn với thao tác đọc file `pdf`, tự động bóc tách toàn bộ nội dung văn bản thô từ file CV mà không cần chỉnh sửa gì thêm.
- **Node `Message a model` (Google Gemini)**: 
  - Tại phần **Credentials**, các sếp chọn kết nối Google Gemini (PaLM) API. Nếu chưa có, hãy vào Google AI Studio tạo một API Key mới và điền vào.
  - Model mặc định đang dùng là `Gemma-4-31B` (hoặc các dòng model Gemini tương đương). Các sếp có thể đổi sang model Gemini yêu thích khác trong cấu hình node.
- **Node `Return` (Set)**: Xử lý và định dạng lại kết quả trả về từ Gemini để truyền dữ liệu sạch sẽ cho workflow cha (parent workflow).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test step / Execute node) với một file CV mẫu để kiểm tra xem AI đã trả về đúng chức danh hay chưa.
- Sau khi kiểm tra mọi thứ mượt mà, các sếp bật **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng trích xuất thông tin:** Các sếp có thể chỉnh sửa lại Prompt trong node `Message a model` để yêu cầu Gemini trả về thêm định dạng JSON chứa các trường dữ liệu như: *Kỹ năng chính, Số năm kinh nghiệm, Trình độ học vấn*.
- **Kết hợp thông báo Slack/Telegram:** Sau khi nhận kết quả từ sub-workflow này, các sếp có thể nối thêm node gửi thông báo về group chat nội bộ của bộ phận tuyển dụng ngay khi có ứng viên nộp CV mới.
- **Lưu trữ tự động:** Tự động đẩy kết quả trích xuất được vào Google Sheets hoặc Notion để tạo bảng quản lý talent pool chuyên nghiệp.

### 📌 Kết luận
Việc ứng dụng AI và n8n vào quy trình tuyển dụng chưa bao giờ dễ dàng đến thế. Hãy cài đặt ngay workflow này để giải phóng sức lao động thủ công cho đội ngũ HR của các sếp ngay hôm nay!