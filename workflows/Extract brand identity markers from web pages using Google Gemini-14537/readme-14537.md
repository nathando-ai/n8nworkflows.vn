---
title: "🚀 Trích xuất dấu ấn nhận diện thương hiệu tự động từ website với Google Gemini và n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu website, sử dụng Google Gemini AI để phân tích tông giọng, phong cách giao tiếp và trả về cấu trúc JSON chuẩn."
slug: "trich-xuat-dau-an-nhan-dien-thuong-hieu-google-gemini-n8n"
tags: [n8n, automation, google-gemini, ai-summarization, market-research, no-code]
keywords: [n8n workflow, trich xuất nhận diện thương hiệu, google gemini ai, cào dữ liệu website tự động, marketing automation]
---

# 🚀 Trích xuất dấu ấn nhận diện thương hiệu tự động từ website với Google Gemini và n8n

Các agency marketing hoặc đội ngũ làm nội dung thường gặp khó khăn lớn khi phải phân tích tông giọng (tone of voice) và phong cách giao tiếp của khách hàng từ website của họ để chuẩn hóa cho các chiến dịch mới. Việc làm thủ công này vừa tốn thời gian, vừa dễ bỏ sót các thông điệp cốt lõi.

Workflow n8n này ra đời như một giải pháp tự động hóa 100% không cần code, giúp các sếp lấy nội dung website, đưa qua **Google Gemini AI** phân tích cấu trúc nhận diện thương hiệu bằng lời (verbal brand identity markers) và trả kết quả hiển thị ngay trực quan trên một trang web hoàn chỉnh.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Thay vì đọc thủ công cả website, AI sẽ tóm tắt và phân tích chỉ trong vài giây.
- **Đồng bộ phong cách:** Giúp các agency nắm bắt chính xác văn phong, thông điệp cốt lõi của khách hàng để tạo nội dung mới chuẩn xác.
- **Đầu ra trực quan:** Dữ liệu trả về được phân tích thành định dạng JSON chuẩn và render trực tiếp thành giao diện web dễ đọc.
- **Vận hành linh hoạt:** Tích hợp sẵn form nhập URL, cho phép chạy on-demand bất cứ lúc nào cần nghiên cứu đối thủ hoặc khách hàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- **Google Gemini API Key** (Google Palm/Gemini Credentials) để AI xử lý ngôn ngữ tự nhiên.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ template gốc của tác giả Blake Wise hoặc copy trực tiếp mã nguồn JSON dán vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 9 nodes chính vận hành theo luồng từ Form đến AI và trả về kết quả HTML:

- **URL Form (`URL Form` - Form Trigger):** Node khởi chạy bằng giao diện form. Các sếp có thể thay đổi câu hỏi hoặc giao diện form thu thập URL nếu muốn.
- **Check URL (`Check URL` - Switch) & Add Missing Protocol (`Add Missing Protocol` - Set):** Các node này kiểm tra xem người dùng đã nhập tiền tố `http://` hay `https://` chưa. Nếu thiếu, hệ thống sẽ tự động thêm `https://` vào trước URL.
- **HTTP Request (`HTTP Request`):** Thực hiện tải mã nguồn HTML của trang web được nhập.
- **HTML (`HTML`):** Trích xuất và làm sạch nội dung văn bản thô từ mã nguồn trang web.
- **Extract Vault A (`Extract Vault A` - Google Gemini):** Node cốt lõi sử dụng LLM của Google. Các sếp cần cấu hình **Credentials** cho Google Gemini API và kiểm tra prompt yêu cầu AI trả về cấu trúc dữ liệu JSON định sẵn (thông điệp, tông giọng, phong cách...).
- **Extract AI Response (`Extract AI Response` - Set) & Extract Nested Data (`Extract Nested Data` - Set):** Xử lý và bóc tách dữ liệu JSON mà Gemini trả về để chuyển hóa thành các biến sử dụng được.
- **Form (`Form` - Completion):** Hiển thị kết quả trực quan trên giao diện form hoàn thành cho người dùng xem.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách nhập một URL bất kỳ vào Form.
- Kiểm tra kết quả hiển thị trên màn hình hoàn thành.
- Sau khi test thành công, bật công tắc **Active** để đưa workflow vào trạng thái chạy chính thức.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa workflow này cho các nghiệp vụ chuyên sâu hơn, các sếp có thể:
- **Gửi kết quả về Slack/Telegram:** Thay vì chỉ hiển thị trên form, hãy cấu hình để bắn báo cáo phân tích thương hiệu về nhóm chat nội bộ ngay khi hoàn tất.
- **Lưu vào Google Sheets / Airtable:** Lưu lại lịch sử các URL đã phân tích kèm kết quả JSON của AI để xây dựng thư viện nghiên cứu thị trường (Market Research).
- **Mở rộng prompt AI:** Tùy chỉnh prompt trong node Gemini để trích xuất thêm các yếu tố khác như bảng màu, đối tượng mục tiêu, hoặc điểm đau của khách hàng.

### 📌 Kết luận
Workflow "Extract Brand Identity Markers from Web Pages using Google Gemini" là một công cụ cực kỳ mạnh mẽ giúp tự động hóa quá trình nghiên cứu đối thủ và khách hàng bằng AI. Hãy cài đặt ngay để tối ưu hóa hiệu suất công việc của đội ngũ marketing nhà các sếp!