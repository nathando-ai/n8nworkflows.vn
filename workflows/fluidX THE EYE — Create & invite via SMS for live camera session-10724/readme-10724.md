---
title: "🚀 Tự động hóa phiên hỗ trợ trực tuyến với fluidX THE EYE và AI tích hợp n8n"
description: "Hướng dẫn xây dựng workflow n8n tích hợp fluidX THE EYE, OpenAI Vision và Google Drive để tự động tạo phiên gọi video trực tiếp, phân tích hình ảnh và lưu trữ dữ liệu."
slug: "tu-dong-hoa-phien-ho-tro-truc-tuyen-fluidx-the-eye"
tags: [n8n, automation, no-code, fluidX, OpenAI, Google Drive]
keywords: [n8n workflow, fluidX THE EYE, tự động hóa hỗ trợ khách hàng, AI phân tích hình ảnh, WebRTC video session]
---

# 🚀 Tự động hóa phiên hỗ trợ trực tuyến với fluidX THE EYE và AI

Các doanh nghiệp cung cấp dịch vụ hỗ trợ kỹ thuật từ xa thường gặp khó khăn trong việc thiết lập nhanh chóng các phiên video trực tuyến, mời khách hàng qua SMS, thông báo cho nhân viên qua email, cũng như lưu trữ và phân tích hình ảnh/video thu thập được một cách thủ công. Việc này tốn rất nhiều thời gian và dễ xảy ra sai sót.

Workflow n8n chuyên nghiệp này (được thiết kế bởi chuyên gia Olaf Titel) sẽ giải quyết triệt để vấn đề trên bằng cách tự động hóa 100% quy trình: từ việc tiếp nhận yêu cầu qua form, tạo phiên gọi video thời gian thực **fluidX THE EYE**, gửi tin nhắn SMS mời khách hàng, gửi email cho tổng đài viên, cho đến sử dụng AI (`OpenAI`) để phân tích hình ảnh và lưu trữ toàn bộ tài liệu lên Google Drive.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Khách hàng nhận được SMS chứa link tham gia phiên live camera ngay sau khi điền form.
- **Tích hợp AI thông minh:** Tự động phân tích hình ảnh chụp từ phiên hỗ trợ bằng OpenAI Vision và tổng hợp báo cáo.
- **Lưu trữ khoa học:** Tự động tạo thư mục trên Google Drive và lưu toàn bộ file hình ảnh, báo cáo tóm tắt theo từng phiên làm việc.
- **Thông báo đa kênh:** Gửi email chi tiết cho Agent và SMS trực tiếp cho User một cách mượt mà.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API credentials sau:
1. **fluidX Account:** Đăng ký tài khoản tại [live.fluidx.digital](https://live.fluidx.digital) (gói TEST ABO, €0) và lấy API Key (HTTP Header Auth với header `x-api-key`).
2. **SMTP Account:** Tài khoản gửi email cho outbound email (Agent).
3. **OpenAI API Key:** Dành cho node `Analyze image` (GPT-4 Vision).
4. **Google Drive API:** Tài khoản Google kết nối OAuth2 để lưu trữ file.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp tiến hành copy mã JSON của workflow hoặc import file trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `On form submission`**: Form thu thập thông tin số điện thoại của khách hàng và email của nhân viên. Các sếp có thể tùy chỉnh các trường trường dữ liệu hiển thị trên form tại đây.
- **Node `Set Config`**: Điền các cấu hình mặc định ban đầu cho hệ thống fluidX, kiểm tra lại thông số API endpoint nếu cần.
- **Node `Create Session Folder` & `Upload file` & `Upload Session Summary`**: Chọn đúng credential Google Drive và tạo sẵn một thư mục tên là `THEEYE` trong thư mục gốc Google Drive của các sếp để workflow có nơi lưu trữ tài liệu.
- **Node `Analyze image`**: Kết nối OpenAI credentials, cấu hình mô hình Vision để phân tích hình ảnh thu được từ thiết bị của khách hàng.
- **Các node `fluidX API - ...`**: Toàn bộ các HTTP Request gọi đến API của fluidX đều yêu cầu gắn `HTTP Header Auth` với API key lấy từ trang quản trị fluidX (`x-api-key`).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng cách submit form mẫu để kiểm tra toàn bộ chuỗi luồng từ SMS, email đến Google Drive.
- Sau khi test thành công, bật công tắc **Active** để đưa workflow vào vận hành thực tế 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram**: Thêm node thông báo qua Telegram hoặc Slack mỗi khi có một phiên hỗ trợ mới được tạo hoặc kết thúc.
- **Lưu log chi tiết**: Kết nối thêm một Database (như Supabase hoặc PostgreSQL) để lưu lịch sử các phiên hỗ trợ phục vụ việc thống kê, chăm sóc khách hàng về sau.
- **Tùy biến prompt AI**: Tối ưu prompt trong node `Analyze image` để AI trích xuất đúng các thông tin kỹ thuật đặc thù theo ngành nghề kinh doanh của các sếp.

### 📌 Kết luận
Workflow **fluidX THE EYE** kết hợp cùng n8n là giải pháp tối ưu giúp tự động hóa hoàn toàn quy trình hỗ trợ khách hàng qua video trực tuyến tích hợp AI. Hãy triển khai ngay hôm nay để nâng tầm trải nghiệm dịch vụ và tiết kiệm hàng giờ làm việc thủ công cho đội ngũ vận hành!