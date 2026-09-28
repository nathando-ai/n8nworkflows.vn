---
title: "🚀 Tự Động Lấy Hình Ảnh Từ DummyJSON API Bằng HTTP Request Trong n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động gọi API để lấy hình ảnh mẫu từ DummyJSON nhanh chóng và dễ dàng cho các nhà phát triển và marketer."
slug: "tao-hinh-anh-tu-dummyjson-api-n8n-http-request"
tags: [n8n, automation, no-code, http-request, dummyjson, marketing]
keywords: [n8n workflow, dummyjson api, http request node, tu dong hoa n8n, api integration]
---

# 🚀 Tự Động Lấy Hình Ảnh Từ DummyJSON API Bằng HTTP Request Trong n8n

Trong quá trình phát triển ứng dụng hoặc làm marketing, các sếp thường xuyên cần hình ảnh mẫu (placeholder images) để thiết kế giao diện, thử nghiệm hệ thống hoặc làm báo cáo. Thay vì đi tìm kiếm thủ công từng tấm hình, chúng ta có thể tự động hóa hoàn toàn quy trình này bằng một workflow n8n cực kỳ tinh gọn sử dụng **HTTP Request Node**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Không cần thao tác thủ công, gọi API và nhận dữ liệu hình ảnh ngay lập tức.
- **Tiết kiệm thời gian**: Cung cấp nguồn hình ảnh mẫu nhanh chóng cho các chiến dịch marketing hoặc test hệ thống.
- **Dễ dàng mở rộng**: Làm nền tảng để kết nối với các dịch vụ lưu trữ hoặc xử lý ảnh tiếp theo trong chuỗi workflow.
- **Hoạt động linh hoạt**: Dễ dàng kích hoạt thủ công để kiểm tra hoặc tích hợp vào các kịch bản tự động phức tạp hơn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n (Cloud hoặc Self-hosted).
- Không cần tài khoản hay API Key phức tạp vì workflow sử dụng **DummyJSON API** hoàn toàn miễn phí và công khai.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó thêm thủ công 3 nodes cơ bản hoặc sử dụng JSON từ template gốc để import vào hệ thống của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 3 nodes chính rất cơ bản:
- **When clicking ‘Test workflow’ (`manualTrigger`)**: Node khởi chạy thủ công. Các sếp có thể thay thế bằng *Webhook*, *Schedule Trigger* hoặc bất kỳ trigger nào khác tùy theo nhu cầu thực tế.
- **Fetch Image from API (`httpRequest`)**: Node cốt lõi thực hiện gọi GET request tới DummyJSON API để lấy dữ liệu hình ảnh. Các sếp cần kiểm tra lại endpoint URL trong phần cài đặt của node này để đảm bảo trả về đúng định dạng mong muốn.
- **Set Image Properties (`set`)**: Node dùng để định dạng và lọc lại các thuộc tính của hình ảnh (như URL, kích thước, tên file) trước khi chuyển sang bước tiếp theo trong hệ thống.

#### 3. Kích hoạt ⚡️
- Nhấn nút **‘Test workflow’** để kiểm tra xem dữ liệu trả về từ API có chính xác hay không.
- Sau khi kiểm tra thành công, các sếp có thể lưu lại và chuyển sang các bước tích hợp nâng cao.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Telegram/Slack**: Gửi trực tiếp hình ảnh lấy được từ API lên nhóm chat của team marketing để làm hình minh họa ngẫu nhiên mỗi ngày.
- **Lưu trữ tự động**: Kết hợp thêm node Google Drive hoặc AWS S3 để tải và lưu trữ vĩnh viễn những hình ảnh này về kho của doanh nghiệp.
- **Tạo lịch trình tự động**: Thay thế Trigger thủ công bằng *Schedule Trigger* để hệ thống tự động cào dữ liệu hình ảnh theo khung giờ cố định.

### 📌 Kết luận
Chỉ với 3 nodes đơn giản trong n8n, các sếp đã có thể tự động hóa việc lấy dữ liệu hình ảnh mẫu từ nguồn API bên thứ ba một cách mượt mà. Hãy áp dụng ngay vào hệ thống của mình để tối ưu hóa các thao tác kỹ thuật hàng ngày!