---
title: "🚀 Tự động săn vé máy bay giá rẻ với Bright Data và n8n"
description: "Hướng dẫn sử dụng n8n kết hợp Bright Data Web Unlocker để tự động cào dữ liệu giá vé máy bay từ Skiplagged và lưu trữ vào Google Sheets một cách dễ dàng."
slug: "tu-dong-san-ve-may-bay-gia-re-bright-data-n8n"
tags: [n8n, automation, no-code, web-scraping, bright-data, google-sheets]
keywords: [n8n workflow, săn vé máy bay giá rẻ, cào dữ liệu web, bright data, skiplagged automation]
---

# 🚀 Tự động săn vé máy bay giá rẻ với Bright Data và n8n

Việc săn vé máy bay giá rẻ thủ công thường tốn rất nhiều thời gian và dễ bỏ lỡ các đợt giảm giá chớp nhoáng. Các trang web đặt vé thường có cơ chế chống bot nghiêm ngặt khiến việc cào dữ liệu trở nên khó khăn. 

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách kết hợp **Bright Data Web Unlocker** để vượt qua tường lửa, lấy thông tin giá vé từ **Skiplagged** và tự động đồng bộ toàn bộ dữ liệu vào **Google Sheets** mà không cần viết mã phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Không cần mất công tra cứu thủ công từng chặng bay mỗi ngày.
- **Vượt rào cản chống bot**: Sử dụng Bright Data để dễ dàng lấy dữ liệu HTML từ các trang web khó tính như Skiplagged.
- **Lưu trữ tập trung**: Tự động ghi nhận danh sách giá vé trực tiếp vào Google Sheets để dễ dàng so sánh và theo dõi.
- **Dễ dàng mở rộng**: Dễ dàng tích hợp thêm thông báo qua Telegram/Email hoặc lên lịch chạy tự động hàng ngày.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản [Bright Data](https://get.brightdata.com/1tndi4600b25) để sử dụng dịch vụ Web Unlocker.
- Tài khoản Google có quyền truy cập Google Sheets.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc sao chép mã nguồn JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File / Clipboard** và dán đoạn JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 4 nodes chính hoạt động tuần tự:

1. **Manual Trigger**:
   - Nút khởi động thủ công giúp bạn kiểm tra kết quả ngay lập tức khi cần thiết.
2. **Fetch flight details from skiplegged via bright data (HTTP Request)**:
   - Cấu hình phương thức `POST` gửi đến API của Bright Data (`https://api.brightdata.com/request`).
   - Cung cấp API Key của Bright Data trong phần Header.
   - Thay đổi URL mục tiêu trong body yêu cầu (ví dụ: `https://skiplagged.com/flights/DUB/LON/2024-06-30`) thành chặng bay và ngày bay mong muốn của bạn.
3. **HTML (HTML Extract)**:
   - Sử dụng thao tác `extractHtmlContent`.
   - Cấu hình CSS Selector tương ứng với thẻ chứa giá vé trên trang (ví dụ: `.flights-landing__flight-price`) để trích xuất chính xác danh sách giá vé dưới dạng mảng dữ liệu.
4. **Google Sheets**:
   - Chọn tài khoản Google Sheets thông qua OAuth2 credentials.
   - Chọn file spreadsheet và Sheet Name phù hợp.
   - Map trường dữ liệu giá vé vừa trích xuất từ node HTML vào cột tương ứng (ví dụ: cột `Price`).

#### 3. Kích hoạt ⚡️
- Click vào **Execute Workflow** để chạy thử nghiệm và kiểm tra xem Google Sheet đã nhận được danh sách giá vé chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để hoàn tất.

### ✍️ Mẹo & gợi ý nâng cao
- **Lên lịch tự động**: Thay thế node *Manual Trigger* bằng node *Schedule Trigger* để hệ thống tự động kiểm tra giá vé định kỳ mỗi ngày.
- **Cảnh báo tức thì**: Thêm node *Telegram* hoặc *Gmail* để nhận thông báo ngay lập tức khi phát hiện vé có giá thấp hơn mức kỳ vọng (ví dụ: dưới $100).
- **Mở rộng tuyến đường**: Sử dụng node *Set* hoặc vòng lặp để cấu hình nhiều chặng bay khác nhau trong cùng một lần chạy.

### 📌 Kết luận
Workflow này là một công cụ cực kỳ hữu ích cho những tín đồ du lịch tự túc hoặc những ai muốn theo dõi biến động giá vé máy bay một cách tự động, tiết kiệm tối đa thời gian. Hãy triển khai ngay hôm nay để không bỏ lỡ bất kỳ cơ hội bay giá rẻ nào!