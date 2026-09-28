---
title: "🚀 Tự động tạo mã QR từ URL chuyên nghiệp với n8n và QR Server API"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tạo mã QR từ URL đầu vào thông qua biểu mẫu (Form) và QR Server API, giúp người dùng tải xuống ngay lập tức."
slug: "tao-ma-qr-tu-url-tu-dong-voi-n8n"
tags: [n8n, automation, no-code, qr-code, api-integration]
keywords: [n8n workflow, tạo mã QR tự động, qr server api, form trigger n8n, tự động hóa no-code]
---

# 🚀 Tự động tạo mã QR từ URL chuyên nghiệp với n8n và QR Server API

Các sếp có bao giờ cảm thấy mất thời gian mỗi khi cần tạo mã QR cho các chiến dịch marketing, link website hay tài liệu chia sẻ không? Việc phải truy cập các trang web tạo QR thủ công, tải về rồi đổi tên từng file thực sự rất tốn thời gian và nhàm chán.

Giải pháp là đây! Với workflow n8n cực kỳ tinh gọn này, các sếp có thể xây dựng ngay một hệ thống tự động hóa 100%: người dùng chỉ cần điền URL vào biểu mẫu (Form), hệ thống sẽ tự động gọi API sinh mã QR và hiển thị màn hình tải xuống ngay lập tức mà không cần can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và phục vụ khách hàng mọi lúc, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Không cần công cụ trung gian, tích hợp trực tiếp giao diện Form cho người dùng cuối.
- **Tốc độ chớp nhoáng:** Sử dụng QR Server API mạnh mẽ, trả về kết quả và file tải xuống chỉ trong tích tắc.
- **Tiết kiệm thời gian:** Xây dựng một mini-app nội bộ hoặc cổng thông tin tạo QR riêng cho doanh nghiệp cực kỳ đơn giản.
- **Hoạt động liên tục 24/7:** Vận hành ổn định trên nền tảng n8n self-hosted, sẵn sàng phục vụ bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Hệ thống n8n:** Đã cài đặt n8n (Phiên bản Cloud hoặc Self-hosted).
- **Kết nối Internet:** Workflow sử dụng `QR Server API` hoàn toàn miễn phí và không yêu cầu API Key phức tạp, các sếp có thể dùng ngay lập tức!
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ thư viện n8n chính thức (Link gốc: [n.io/workflows/5124](https://n8n.io/workflows/5124)) hoặc tạo mới bằng cách thêm 3 nodes cơ bản sau:
- `On form submission` (Form Trigger)
- `HTTP Request`
- `Form` (Form Completion)

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 3 nodes chính được thiết kế vô cùng tối ưu:

- **Node `On form submission` (Form Trigger):** 
  - Đây là điểm khởi đầu, cung cấp một giao diện web form cho người dùng nhập URL cần chuyển đổi thành mã QR.
  - Các sếp có thể cấu hình thêm tiêu đề form, mô tả hoặc trường dữ liệu (field) nhận URL tùy ý.

- **Node `HTTP Request` (QR code generation):**
  - Node này chịu trách nhiệm gọi API từ dịch vụ `QR Server API` (`https://goqr.me/api/`).
  - Cấu hình phương thức GET kèm theo tham số truyền vào là URL lấy từ trường dữ liệu của form trước đó (`On form submission`). Đảm bảo kiểu dữ liệu trả về được cấu hình dạng file/binary để người dùng dễ dàng tải xuống.

- **Node `Form` (Form ending):**
  - Cấu hình operation là `completion` để hiển thị màn hình kết thúc kèm theo hình ảnh mã QR vừa được tạo, cho phép người dùng cuối bấm tải xuống trực tiếp thiết bị của họ.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng cách điền một URL bất kỳ vào link Form do n8n cung cấp.
- Kiểm tra xem mã QR có hiển thị chính xác và tải về được không.
- Gạt công tắc sang **Active** để đưa workflow vào trạng thái hoạt động chính thức.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống thông minh hơn, các sếp có thể mở rộng workflow này với các ý tưởng sau:
- **Lưu trữ lịch sử:** Thêm một node `Google Sheets` hoặc `Postgres` để lưu lại lịch sử các URL đã được tạo mã QR kèm theo thời gian.
- **Gửi thông báo:** Tích hợp node `Telegram` hoặc `Slack` để thông báo về team mỗi khi có khách hàng/nhân viên tạo một mã QR mới.
- **Tùy chỉnh giao diện:** Tùy biến CSS của trang Form n8n để phù hợp với bộ nhận diện thương hiệu của công ty.

### 📌 Kết luận
Một workflow siêu nhỏ gọn nhưng mang lại giá trị thực tiễn cực cao, giúp tiết kiệm thời gian và tối ưu hóa các thao tác lặp đi lặp lại hàng ngày. Hãy cài đặt ngay lên hệ thống n8n của các sếp để trải nghiệm sự kỳ diệu của tự động hóa!