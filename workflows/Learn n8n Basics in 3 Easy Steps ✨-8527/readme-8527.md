---
title: "🚀 Hướng dẫn học n8n cơ bản trong 3 bước đơn giản cho người mới bắt đầu"
description: "Làm chủ n8n nhanh chóng với workflow mẫu giúp tự động lấy dữ liệu từ internet, xử lý dữ liệu và gửi email thông báo hoàn toàn tự động."
slug: "hoc-n8n-co-ban-trong-3-buoc"
tags: [n8n, automation, no-code, beginner, tutorial, gmail]
keywords: [n8n workflow, học n8n cơ bản, tự động hóa no-code, n8n tutorial tiếng việt, schedule trigger n8n]
---

# 🚀 Hướng dẫn học n8n cơ bản trong 3 bước đơn giản

Việc bắt đầu làm quen với một nền tảng tự động hóa mới đôi khi khiến các sếp cảm thấy bối rối trước quá nhiều tính năng và khái niệm phức tạp. Thay vì đọc tài liệu dài dòng, cách tốt nhất để học n8n là thực hành ngay trên một workflow mẫu hoàn chỉnh. Bài viết này sẽ hướng dẫn các sếp từng bước làm chủ n8n thông qua template chính thức từ đội ngũ n8n, giúp các sếp hiểu cách lấy dữ liệu từ internet, xử lý chúng và gửi email tự động chỉ trong vài phút.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Nắm vững nền tảng:** Hiểu rõ cách hoạt động của Triggers (Kích hoạt), Actions (Hành động) và Data Mapping (Ánh xạ dữ liệu) trong n8n.
- **Tự động hóa thông minh:** Biết cách gọi API bên ngoài (HTTP Request) để lấy thông tin ngẫu nhiên như câu nói hay hoặc trò đùa lập trình.
- **Gửi email tự động:** Tích hợp Gmail để gửi kết quả đã xử lý đến hộp thư cá nhân theo lịch trình hoặc khi bấm thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản Gmail cá nhân hoặc doanh nghiệp để kết nối qua OAuth2.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tìm và import template này trực tiếp từ thư viện workflow của n8n (Template ID: `8527`) hoặc sao chép mã JSON của workflow để dán vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này được chia thành các bước rõ ràng trên canvas giúp các sếp dễ dàng thao tác:

- **Node `1. Click 'Execute workflow'` (Manual Trigger) & Node `2. Get inspirational quote from the internet` (HTTP Request):** 
  Đây là bước đầu tiên để làm quen. Các sếp chỉ cần nhấn nút "Execute workflow" để kích hoạt node này. Nó sẽ gửi một HTTP Request gọi API ngẫu nhiên để lấy về một câu nói truyền cảm hứng từ internet.
- **Node `3. Set` (Results / Map the fields):** 
  Sau khi nhận dữ liệu thô, node này đóng vai trò trích xuất và ánh xạ (map) các trường dữ liệu cần thiết. Các sếp nhấp đúp vào node để xem cấu trúc dữ liệu đã được định dạng lại như thế nào.
- **Node `Connect your Gmail` (Gmail):** 
  Để gửi email kết quả (câu nói hay hoặc trò đùa lập trình), các sếp cần cấu hình tài khoản Gmail. Chọn **Credentials** kiểu `gmailOAuth2` và thực hiện cấp quyền theo hướng dẫn trên màn hình n8n. Sau đó, điền địa chỉ email người nhận (Recipient) và nội dung muốn gửi.
- **Node `Schedule me here` / `Schedule Trigger`:** 
  Sau khi đã chạy thử thủ công thành công, các sếp cấu hình node này để tự động chạy workflow theo lịch trình định sẵn (ví dụ: gửi câu nói hay vào mỗi buổi sáng).

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute workflow** ở từng node để kiểm tra luồng dữ liệu chạy mượt mà không báo lỗi.
- Sau khi kiểm tra hoàn tất, gạt công tắc **Active** ở góc trên bên phải để bật workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa nội dung:** Kết hợp thêm node `Programming joke` để gửi kèm các câu đùa vui vẻ bên cạnh câu nói truyền cảm hứng.
- **Mở rộng kênh thông báo:** Thay vì chỉ gửi qua Gmail, các sếp có thể nối thêm node Telegram hoặc Slack để bắn tin nhắn trực tiếp lên nhóm chat công ty.
- **Lưu lịch sử:** Thêm một node Google Sheets ở cuối luồng để lưu lại tất cả những câu nói đã gửi theo từng ngày.

### 📌 Kết luận
Workflow "Learn n8n Basics" là bước đệm hoàn hảo để các sếp làm quen với tư duy tự động hóa no-code mà không sợ bị ngợp. Hãy import ngay vào hệ thống của mình, thực hành từng bước và bắt đầu tạo ra những con bot tự động hóa đầu tiên nhé các sếp!