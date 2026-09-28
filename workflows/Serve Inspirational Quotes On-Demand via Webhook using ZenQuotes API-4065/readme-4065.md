---
title: "💡 Tự động lấy câu nói truyền cảm hứng qua Webhook với ZenQuotes API"
description: "Hướng dẫn chi tiết cách tạo workflow n8n để lấy ngẫu nhiên các câu nói truyền cảm hứng từ ZenQuotes API và trả về qua webhook. Giải pháp hoàn hảo cho các ứng dụng nội bộ, chatbot hoặc hệ thống thông báo."
slug: "tu-dong-lay-cau-noi-truyen-cam-hung-qua-webhook-voi-zenquotes-api"
tags: [n8n, automation, no-code, API, webhook]
keywords: [n8n workflow, tự động hóa, ZenQuotes API, webhook, câu nói truyền cảm hứng]
---

# 💡 Tự động lấy câu nói truyền cảm hứng qua Webhook với ZenQuotes API

[Các sếp] có bao giờ cảm thấy mệt mỏi với việc phải tìm kiếm những câu nói truyền cảm hứng mỗi ngày? Với workflow này, các sếp có thể tự động lấy các câu nói ngẫu nhiên từ ZenQuotes API và trả về qua webhook một cách dễ dàng. Đây là giải pháp hoàn hảo cho các ứng dụng nội bộ, chatbot hoặc hệ thống thông báo tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Không cần phải tìm kiếm thủ công các câu nói truyền cảm hứng.
- Tự động hóa hoàn toàn: Workflow tự động lấy và định dạng dữ liệu từ ZenQuotes API.
- Tùy chỉnh dễ dàng: Các sếp có thể thay đổi định dạng dữ liệu theo nhu cầu của mình.
- Tích hợp linh hoạt: Dễ dàng tích hợp với các ứng dụng khác thông qua webhook.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n đã được cài đặt và cấu hình.
- Không cần tài khoản ZenQuotes API vì workflow sử dụng API công khai.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n, các sếp có thể làm theo các bước sau:

1. Truy cập vào n8n Editor.
2. Nhấp vào nút "Import from URL" và dán link sau vào ô nhập liệu: `https://n8n.io/workflows/4065`.
3. Nhấp vào nút "Import" để hoàn tất quá trình import.

Hoặc, các sếp có thể tải xuống file JSON của workflow từ [đây](https://n8n.io/workflows/4065) và import thủ công vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Webhook**: Node này nhận các yêu cầu đến và kích hoạt workflow. Các sếp cần lưu ý rằng đường dẫn webhook có thể thay đổi, vì vậy hãy kiểm tra lại đường dẫn sau khi import.
- **Get Random Quote from ZenQuotes**: Node này gửi yêu cầu đến ZenQuotes API để lấy một câu nói ngẫu nhiên. Không cần cấu hình gì thêm vì workflow đã được thiết lập sẵn.
- **Format data**: Node này định dạng dữ liệu từ ZenQuotes API thành chuỗi 'quote – author'. Các sếp có thể thay đổi định dạng này theo nhu cầu của mình.
- **Send response**: Node này gửi phản hồi lại cho người gửi yêu cầu. Các sếp có thể thay đổi định dạng phản hồi theo nhu cầu của mình.

#### 3. Kích hoạt ⚡️
Sau khi đã cấu hình các node cần thiết, các sếp có thể kích hoạt workflow bằng cách nhấp vào nút "Activate" trên giao diện n8n Editor. Để kiểm tra workflow, các sếp có thể gửi một yêu cầu đến webhook và kiểm tra phản hồi.

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể thêm một node để lưu trữ các câu nói đã lấy vào cơ sở dữ liệu để sử dụng sau này.
- Các sếp có thể tích hợp workflow này với các ứng dụng khác như Slack, Telegram, hoặc Microsoft Teams để tự động gửi các câu nói truyền cảm hứng đến các kênh chat.
- Các sếp có thể thay đổi định dạng dữ liệu để phù hợp với nhu cầu của mình, ví dụ như thêm ngày tháng hoặc tác giả vào câu nói.

### 📌 Kết luận
Workflow này cung cấp một giải pháp tự động hóa hoàn hảo để lấy các câu nói truyền cảm hứng từ ZenQuotes API và trả về qua webhook. Với các bước đơn giản và dễ dàng, các sếp có thể tích hợp workflow này vào các ứng dụng nội bộ hoặc hệ thống thông báo tự động của mình. Hãy thử ngay và trải nghiệm sự tiện lợi mà tự động hóa mang lại!