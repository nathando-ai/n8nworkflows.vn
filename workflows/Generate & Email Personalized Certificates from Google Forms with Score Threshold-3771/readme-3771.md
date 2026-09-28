---
title: "🚀 Tự động tạo và gửi chứng chỉ cá nhân hóa từ Google Forms qua n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động chấm điểm, tạo Google Slide chứng chỉ, chuyển thành PDF và gửi email cho học viên dựa trên ngưỡng điểm đạt được."
slug: "tu-dong-tao-va-gui-chung-chi-tu-google-forms-n8n"
tags: [n8n, automation, google-forms, google-slides, gmail, e-learning]
keywords: [n8n workflow, tạo chứng chỉ tự động, google forms n8n, google slides sang pdf, gửi email tự động n8n]
---

# 🚀 Tự động tạo và gửi chứng chỉ cá nhân hóa từ Google Forms với n8n

Việc tổ chức các bài kiểm tra, khóa học trực tuyến và cấp chứng chỉ thủ công cho học viên thực sự là một cơn ác mộng tốn thời gian. Bạn phải kiểm tra điểm số từng người, tạo mẫu chứng chỉ, điền tên, xuất file PDF và gửi email hàng loạt. Một quy trình lặp đi lặp lại dễ xảy ra sai sót.

Giải pháp? Workflow n8n này sẽ tự động hóa **100%** quy trình từ lúc học viên nộp bài Google Form, kiểm tra điều kiện điểm số (Score Threshold), tự động thiết kế chứng chỉ cá nhân hóa bằng Google Slides, chuyển đổi sang PDF và gửi thẳng vào Gmail của học viên. Không cần biết lập trình!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Không còn phải làm thủ công từng chứng chỉ một.
- **Phản hồi tức thì:** Học viên vừa nộp bài đạt điểm là nhận ngay chứng chỉ trong hòm thư chỉ sau vài giây.
- **Cá nhân hóa chuyên nghiệp:** Tự động điền tên học viên và điểm số chính xác lên mẫu chứng chỉ thiết kế sẵn.
- **Hoạt động 24/7:** Chạy ngầm mượt mà, không bỏ sót bất kỳ học viên nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Self-hosted hoặc Cloud).
- Tài khoản Google (Google Forms, Google Sheets, Google Drive, Google Slides).
- Tài khoản Gmail để gửi email tự động.
- Mẫu Google Slide chứng chỉ (với thẻ placeholder như `[ name ]`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc copy trực tiếp mã nguồn workflow, sau đó paste vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình lần lượt các node quan trọng sau trên canvas:

- **Google Sheets Trigger:** Kết nối tài khoản Google của bạn. Dán ID của Google Sheet được tạo tự động từ Google Form (bật chế độ Quiz Mode).
- **Extract essential data (Set):** Lọc và chọn các trường dữ liệu cần thiết từ form gửi về (thường gồm: *Name*, *Email*, *Score*).
- **Score Checker (If):** Đặt điều kiện điểm số tối thiểu để vượt qua bài kiểm tra. Nếu đạt, workflow sẽ đi theo nhánh tiếp theo.
- **Copy from your template (Google Drive):** Tạo bản sao từ mẫu Google Slide chứng chỉ của bạn. Điền ID của template Google Slide vào node này.
- **Replace text (Google Slides):** Cấu hình để node tự động tìm thẻ `[ name ]` trong slide và thay thế bằng tên của học viên.
- **Convert to PDF (Google Drive):** Tải file Google Slide đã thay tên về dưới dạng file PDF, chuẩn bị đính kèm email.
- **Send to user's email (Gmail):** Soạn nội dung email chúc mừng, đính kèm file PDF chứng chỉ và gửi trực tiếp tới email của học viên.

#### 3. Kích hoạt ⚡️
- Thực hiện submit thử 1 dữ liệu mẫu trên Google Form để Test Run trên n8n.
- Kiểm tra kết quả ở hòm thư xem chứng chỉ đã được gửi đúng chuẩn chưa.
- Bật công tắc **Active** để workflow chính thức chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Telegram/Slack:** Thêm một node thông báo về nhóm nội bộ mỗi khi có học viên xuất sắc đạt chứng chỉ.
- **Lưu trữ backup:** Tự động lưu bản PDF chứng chỉ vào một thư mục riêng biệt trên Google Drive để ban quản lý dễ dàng kiểm tra sau này.
- **Tùy biến email:** Sử dụng HTML để thiết kế email chào mừng chuyên nghiệp và bắt mắt hơn thay vì dùng văn bản thuần túy.

### 📌 Kết luận
Với workflow n8n này, việc cấp chứng chỉ cho hàng trăm, hàng ngàn học viên không còn là nỗi ám ảnh. Triển khai ngay hôm nay để tối ưu hóa vận hành và mang lại trải nghiệm chuyên nghiệp nhất cho học viên của các sếp!