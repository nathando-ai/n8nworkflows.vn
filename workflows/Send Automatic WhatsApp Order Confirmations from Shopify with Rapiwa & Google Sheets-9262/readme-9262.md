---
title: "🚀 Tự Động Gửi Xác Nhận Đơn Hàng WhatsApp Từ Shopify Với Rapiwa & Google Sheets"
description: "Workflow n8n tự động nhận đơn từ Shopify, kiểm tra số WhatsApp hợp lệ qua Rapiwa, gửi tin nhắn xác nhận cá nhân hóa và ghi log chi tiết vào Google Sheets."
slug: "tu-dong-gui-xac-nhan-don-hang-whatsapp-shopify-rapiwa"
tags: [n8n, automation, no-code, whatsapp-marketing, shopify-integration, rapidwa]
keywords: [n8n workflow, tự động hóa whatsapp, shopify webhook, rapiwa api, google sheets log]
---

# 🚀 Tự Động Gửi Xác Nhận Đơn Hàng WhatsApp Từ Shopify Với Rapiwa & Google Sheets

Các sếp kinh doanh online (eCommerce) chắc hẳn đều hiểu nỗi đau khi khách hàng đặt hàng xong mà không nhận được thông báo xác nhận ngay lập tức. Việc này không chỉ gây trải nghiệm khách hàng kém mà còn tăng tỷ lệ hủy đơn hoặc hỏi lại nhân viên qua chat. Làm thủ công thì tốn thời gian, dễ sai sót, còn thuê nhân viên thì chi phí cao.

Workflow n8n này chính là giải pháp "chốt hạ" cho bài toán đó. Nó hoạt động hoàn toàn tự động 100%, không cần code: Nhận webhook từ Shopify -> Làm sạch dữ liệu -> Kiểm tra số WhatsApp có tồn tại không (tránh gửi nhầm) -> Gửi tin nhắn xác nhận chi tiết -> Ghi log vào Google Sheets để đối soát.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian thủ công:** Tin nhắn được gửi ngay lập tức sau khi khách đặt hàng, không cần nhân viên can thiệp.
- **Tăng độ tin cậy & Chuyên nghiệp:** Khách nhận được thông tin đơn hàng chi tiết (sản phẩm, địa chỉ, tổng tiền) ngay trên WhatsApp - kênh chat phổ biến nhất.
- **Tránh lãng phí chi phí API:** Workflow kiểm tra số WhatsApp hợp lệ trước khi gửi, giúp không tốn credit cho các số rác hoặc không tồn tại.
- **Dữ liệu minh bạch:** Mọi đơn hàng (gửi thành công hay thất bại) đều được ghi log chi tiết vào Google Sheets để dễ dàng đối soát và phân tích.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để triển khai workflow này, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Chạy local hoặc trên VPS.
2. **Tài khoản Rapiwa:** Nền tảng gửi tin nhắn WhatsApp. Cần lấy **API Key (Bearer Token)** từ dashboard Rapiwa.
3. **Shopify Store:** Đã cấu hình Webhook cho sự kiện `orders/create` (hoặc tương tự) trỏ về URL webhook của n8n.
4. **Tài khoản Google:** Để tạo Google Sheet lưu log và cấu hình OAuth2 credentials trong n8n.
5. **Google Sheet mẫu:** Tạo sheet với các cột: `name`, `number`, `order id`, `item name`, `total price`, `validity`, `status`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON workflow từ link gốc hoặc copy toàn bộ code JSON.
2. Mở n8n Editor, chọn **Import from URL** hoặc **Import from File**.
3. Sau khi import, workflow sẽ hiện ra với các node đã được kết nối sẵn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần click vào từng node và cấu hình lại cho đúng thông tin của mình:

*   **Node: Webhook**
    *   Mặc định là `POST`.
    *   Copy **Webhook URL** (Production) để cấu hình trong Shopify Admin -> Settings -> Notifications -> Webhooks. Chọn sự kiện `orders/create`.

*   **Node: Clean Webhooks Response Data (Code)**
    *   Node này dùng JavaScript để bóc tách dữ liệu thô từ Shopify.
    *   *Lưu ý:* Nếu cấu trúc dữ liệu Shopify của các sếp khác (ví dụ dùng app trung gian), có thể cần chỉnh lại các field mapping trong code này (ví dụ: `customer.phone`, `line_items[0].title`).

*   **Node: Check valid whatsapp number Using Rapiwa1 (HTTP Request)**
    *   **Authentication:** Chọn credentials `httpBearerAuth` đã tạo cho Rapiwa.
    *   **URL:** `https://app.rapiwa.com/api/verify-whatsapp`
    *   **Body:** Đảm bảo field `number` nhận giá trị từ node trước đó (số điện thoại đã làm sạch).

*   **Node: If**
    *   Logic: Kiểm tra xem `data.exists` có bằng `true` không.
    *   *Lưu ý kỹ thuật:* Nếu Rapiwa trả về boolean `true/false` thay vì string `"true"`, các sếp nên chỉnh điều kiện trong node này cho khớp để tránh lỗi logic.

*   **Node: Send Message Using Rapiwa (HTTP Request)**
    *   **Authentication:** Chọn credentials `httpHeaderAuth` hoặc `httpBearerAuth` tùy theo cách Rapiwa yêu cầu (thường là Bearer Token).
    *   **URL:** `https://app.rapiwa.com/api/send-message`
    *   **Body:** Chỉnh sửa phần `message` để phù hợp với thương hiệu của các sếp. Workflow mẫu đã có template chi tiết gồm: Tên khách, Sản phẩm, SKU, Địa chỉ giao hàng, Tổng tiền. Các sếp chỉ cần thay tên shop và điều chỉnh nội dung nếu cần.

*   **Node: Change State of Rows in Verified & Sent (Google Sheets)**
    *   **Authentication:** Chọn credentials `googleSheetsOAuth2Api`.
    *   **Document ID & Sheet Name:** Điền ID và tên sheet của các sếp.
    *   **Operation:** `Update`.
    *   **Mapping:** Đảm bảo các cột `validity` = `verified` và `status` = `sent` được map đúng.

*   **Node: Change State of Rows in Unverified & Not Sent (Google Sheets)**
    *   Tương tự node trên, nhưng map `validity` = `unverified` và `status` = `not sent`.

*   **Node: Wait**
    *   Mặc định có thể là vài giây. Các sếp nên giữ khoảng 3-5 giây để tránh bị Rapiwa hoặc WhatsApp đánh dấu là spam (rate limit).

#### 3. Kích hoạt ⚡️
1. **Test Run:**
    *   Tạo một đơn hàng test trên Shopify (hoặc dùng Postman để gửi POST request mẫu vào Webhook URL).
    *   Chạy workflow và kiểm tra:
        *   Số điện thoại có được làm sạch không?
        *   Rapiwa có trả về kết quả verify không?
        *   Tin nhắn có đến điện thoại test không?
        *   Google Sheet có cập nhật dòng mới không?
2. **Bật Active:**
    *   Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải n8n.
    *   Workflow sẽ bắt đầu lắng nghe webhook từ Shopify và tự động xử lý mọi đơn hàng mới.

### ✍️ Mẹo & gợi ý nâng cao
- **Cá nhân hóa tin nhắn hơn:** Thêm tên sản phẩm cụ thể, mã giảm giá đã dùng, hoặc link theo dõi đơn hàng vào template tin nhắn WhatsApp.
- **Tích hợp thêm kênh dự phòng:** Nếu số WhatsApp không hợp lệ (branch False), các sếp có thể thêm node gửi Email hoặc SMS để đảm bảo khách hàng vẫn nhận được thông báo.
- **Báo cáo định kỳ:** Thêm một workflow n8n khác chạy hàng ngày vào 9h sáng, đọc dữ liệu từ Google Sheet và gửi báo cáo tổng hợp (số đơn gửi thành công, thất bại) qua Telegram hoặc Slack cho team quản lý.
- **Tối ưu chi phí:** Nếu lưu lượng đơn hàng lớn, cân nhắc nâng cấp gói Rapiwa hoặc sử dụng API WhatsApp Business chính thức (Meta) nếu ngân sách cho phép, tuy nhiên Rapiwa vẫn là lựa chọn linh hoạt và dễ triển khai hơn cho giai đoạn đầu.

### 📌 Kết luận
Việc tự động hóa xác nhận đơn hàng qua WhatsApp không chỉ giúp các sếp tiết kiệm nhân sự mà còn nâng tầm trải nghiệm khách hàng lên một đẳng cấp mới. Với workflow n8n kết hợp Rapiwa và Google Sheets này, các sếp có thể dễ dàng triển khai trong 15 phút, không cần biết code. Hãy thử ngay hôm nay để thấy sự khác biệt trong tỷ lệ chuyển đổi và sự hài lòng của khách hàng!