---
title: "🚀 Tự Động Gửi Bản Tin Tỷ Giá Ngoại Tệ Hàng Ngày Qua CurrencyFreaks API và Gmail"
description: "Hướng dẫn xây dựng workflow n8n tự động cập nhật và gửi bảng tỷ giá ngoại tệ (USD, EUR, GBP,...) qua email mỗi ngày bằng CurrencyFreaks API và Gmail."
slug: "tu-dong-gui-ty-gia-ngoai-te-hang-ngay-currency-freaks-gmail"
tags: [n8n, automation, no-code, currency-exchange, gmail-api, finance]
keywords: [n8n workflow, tỷ giá ngoại tệ, currencyfreaks api, tự động gửi email, n8n gmail, finance automation]
---

# 🚀 Tự Động Gửi Bản Tin Tỷ Giá Ngoại Tệ Hàng Ngày Qua CurrencyFreaks API và Gmail

Các sếp làm trong lĩnh vực tài chính, đầu tư, thương mại quốc tế hay đơn giản là cần theo dõi tỷ giá ngoại tệ mỗi ngày chắc chắn đã ngán ngẩm cảnh phải tra cứu thủ công trên các website, sau đó copy paste vào email gửi cho sếp lớn hoặc đối tác. Việc này vừa mất thời gian, vừa dễ nhầm lẫn khi thị trường biến động liên tục.

Giải pháp là gì? Hãy để n8n lo toàn bộ quy trình này! Với workflow tự động hóa này, các sếp có thể nhận bản tin tỷ giá ngoại tệ cập nhật từng ngày một cách chính xác, chuyên nghiệp ngay trong hộp thư Gmail mà không tốn một giọt mồ hôi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Lịch trình chạy tự động mỗi ngày (hoặc theo khung giờ tùy chỉnh), không cần thao tác tay.
- **Dữ liệu chính xác thời gian thực**: Kết nối trực tiếp với CurrencyFreaks API để lấy tỷ giá mới nhất.
- **Trình bày chuyên nghiệp**: Email định dạng HTML đẹp mắt, hiển thị rõ ngày tháng, đồng tiền cơ sở và danh sách tỷ giá các ngoại tệ quan trọng (PKR, GBP, EUR, USD, BDT, INR,...).
- **Tiết kiệm thời gian**: Loại bỏ hoàn toàn công việc tra cứu và tổng hợp thủ công nhàm chán.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
1. **Tài khoản n8n** (Cloud hoặc Self-hosted).
2. **Tài khoản CurrencyFreaks**: Đăng ký tài khoản miễn phí để lấy API Key gọi dữ liệu tỷ giá.
3. **Tài khoản Google (Gmail)**: Để cấu hình OAuth2 kết nối gửi email tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (hoặc tải file JSON từ nguồn) và dán trực tiếp vào n8n Editor của mình. Workflow gồm 6 nodes chính được sắp xếp gọn gàng theo luồng: 
`Schedule Trigger` → `Set API Key & Preferred Currencies` → `Get Latest Rate` → `Set Recipient Email` → `Set E-mail Subject` → `Send a message (Gmail)`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:
- **Schedule Trigger**: Thiết lập khoảng thời gian chạy mong muốn (ví dụ: chạy vào 8:00 sáng mỗi ngày).
- **Set API Key & Preferred Currencies**: Điền `API Key` của CurrencyFreaks và danh sách các đồng tiền các sếp muốn theo dõi (ví dụ: `PKR, GBP, EUR, USD, BDT, INR`).
- **Get Latest Rate (HTTP Request)**: Kiểm tra lại Endpoint API của CurrencyFreaks để đảm bảo truyền đúng biến API Key và danh sách tiền tệ từ node trước.
- **Set Recipient Email & Set E-mail Subject**: Điền địa chỉ email nhận báo cáo và tiêu đề email theo ý muốn.
- **Send a message (Gmail)**: Chọn Credentials loại `gmailOAuth2` đã được xác thực với tài khoản Gmail của các sếp để cho phép n8n gửi email thay mặt.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm (Test run) xem email có được gửi đi thành công hay không.
- Kiểm tra hộp thư đến, nếu email hiển thị đầy đủ bảng tỷ giá định dạng HTML đẹp mắt thì các sếp chỉ cần bật nút **Active** xanh bên góc phải là xong!

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Thay vì chỉ gửi Gmail, các sếp có thể nối thêm node Telegram hoặc Slack để bắn tin nhắn tỷ giá thẳng lên nhóm chat công ty.
- **Lưu trữ lịch sử**: Thêm node Google Sheets để lưu lại lịch sử biến động tỷ giá mỗi ngày phục vụ việc vẽ biểu đồ phân tích sau này.
- **Cảnh báo biến động**: Thêm các điều kiện (If Node) để nếu một ngoại tệ nào đó biến động vượt ngưỡng cho phép, hệ thống sẽ tự động gửi cảnh báo khẩn cấp.

### 📌 Kết luận
Một workflow cực kỳ gọn nhẹ nhưng mang lại giá trị thực tiễn cao cho bất kỳ ai cần theo dõi tài chính, ngoại hối thường xuyên. Hãy cài đặt ngay hôm nay để tối ưu hóa công việc của các sếp nhé!