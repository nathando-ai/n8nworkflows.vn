---
title: "🚀 Tự động giám sát thi công công trình từ Google Drive bằng GPT-4o-mini, Gmail và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động phân tích hình ảnh công trình từ Google Drive bằng AI, gửi báo cáo qua Gmail và lưu log vào Google Sheets."
slug: "tu-dong-giam-sat-thi-co-cong-trinh-google-drive-ai-gmail-sheets"
tags: [n8n, automation, ai, google-drive, google-sheets, gmail, openai]
keywords: [n8n workflow, tự động hóa thi công, AI phân tích hình ảnh, google drive ai, giám sát công trình tự động]
---

# 🚀 Tự động giám sát thi công công trình từ Google Drive bằng AI

Việc giám sát tiến độ và chất lượng thi công tại các công trường xây dựng thường tốn rất nhiều thời gian. Các kỹ sư hoặc quản lý dự án phải liên tục kiểm tra hàng trăm bức ảnh gửi từ hiện trường, đánh giá lỗi kỹ thuật, an toàn lao động và làm báo cáo thủ công. Việc này dễ dẫn đến quá tải, bỏ sót lỗi hoặc chậm trễ trong việc cập nhật tiến độ.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách **tự động hóa 100% quy trình kiểm tra hình ảnh thi công từ Google Drive**, ứng dụng sức mạnh của AI (GPT-4o-mini) để phân tích chi tiết, tự động gửi báo cáo qua Gmail và lưu vết toàn bộ vào Google Sheets mà không cần con người nhúng tay vào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Nhận diện ảnh mới trên Google Drive theo lịch trình định sẵn (Schedule Trigger) và xử lý ngay lập tức.
- **AI chuyên gia kỹ thuật:** Sử dụng OpenAI Chat Model để đánh giá giai đoạn thi công, chất lượng thực hiện, các điểm chưa phù hợp (non-conformities), vấn đề an toàn và đưa ra khuyến nghị.
- **Báo cáo chuyên nghiệp:** Tự động gửi email qua Gmail kèm theo báo cáo chi tiết và hình ảnh trực quan đến các bên liên quan.
- **Lưu trữ minh bạch:** Tự động lưu log vào Google Sheets và dọn dẹp file (di chuyển sang thư mục "Processed") để tránh xử lý trùng lặp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và dịch vụ sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- Tài khoản **Google Drive** (với 2 thư mục: Thư mục chứa ảnh đầu vào và Thư mục chứa ảnh đã xử lý).
- Tài khoản **Google Sheets** (tạo sẵn file log với các cột tương ứng).
- Tài khoản **Gmail** để gửi báo cáo.
- **OpenAI API Key** (để cấu hình cho model GPT-4o-mini).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ n8n hoặc import trực tiếp file template vào giao diện n8n Editor của mình. Workflow bao gồm 15 nodes được thiết kế mạch lạc từ khâu quét ảnh, xử lý AI, cho đến phân phối kết quả.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node quan trọng sau:

- **`Schedule Trigger (Configurable Interval)`**: Đặt lịch chạy định kỳ (ví dụ: mỗi giờ hoặc hàng ngày) tùy theo nhu cầu thực tế của dự án.
- **`Config`**: Cập nhật các thông tin cấu hình cơ bản như: Địa chỉ email nhận báo cáo, tiêu đề email hoặc các biến số chung.
- **`Drive: List files (Input folder)`** & **`Drive: Download image`**: Kết nối tài khoản Google Drive OAuth2 và điền **Folder ID** của thư mục chứa ảnh hiện trường công trình gửi lên.
- **`AI: Analyze image`** & **`OpenAI Chat Model`**: Kết nối OpenAI Credentials, chọn model `gpt-4.1-mini` và thiết lập Prompt hướng dẫn AI tập trung vào các tiêu chí xây dựng (giai đoạn thi công, chất lượng, lỗi kỹ thuật, an toàn lao động).
- **`Gmail: Send report`**: Kết nối tài khoản Gmail OAuth2 để cho phép gửi email tự động từ workflow.
- **`Sheets: Append log row`**: Kết nối Google Sheets OAuth2, chọn file Google Sheet quản lý log và mapping các trường dữ liệu kết quả từ AI vào các cột tương ứng.
- **`Drive: Move image (Processed folder)`**: Cấu hình **Folder ID** của thư mục "Processed" để di chuyển các hình ảnh đã được phân tích xong, giúp tránh việc xử lý lại ảnh cũ ở lần chạy sau.

#### 3. Kích hoạt ⚡️
- Bấm nút **Test workflow** để chạy thử với một vài bức ảnh mẫu trong Google Drive.
- Kiểm tra kết quả trên Gmail, Google Sheets và thư mục Drive xem file đã được di chuyển đúng chưa.
- Khi mọi thứ đã chạy trơn tru, bật công tắc **Active** góc trên cùng bên phải để workflow tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo tức thời:** Kết nối thêm node Telegram hoặc Slack để gửi cảnh báo khẩn cấp ngay lập tức nếu AI phát hiện ra các lỗi nghiêm trọng về an toàn lao động (`safety issues`).
- **Dashboard quản lý trực quan:** Kết nối Google Sheets vừa log dữ liệu với Google Looker Studio để vẽ biểu đồ tiến độ và tần suất lỗi thi công theo thời gian thực cho sếp lớn xem.
- **Phân loại theo dự án:** Mở rộng workflow bằng cách sử dụng nhiều thư mục Drive khác nhau cho các công trình khác nhau và phân luồng xử lý tương ứng.

### 📌 Kết luận
Với workflow n8n này, việc giám sát công trình xây dựng bằng hình ảnh trở nên thông minh, tự động và tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần. Chúc các sếp cài đặt thành công và tối ưu hóa hiệu suất quản lý dự án của mình!