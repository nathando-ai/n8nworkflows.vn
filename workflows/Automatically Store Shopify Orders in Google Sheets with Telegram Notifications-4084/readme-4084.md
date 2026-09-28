---
title: "🚀 Tự Động Lưu Đơn Hàng Shopify Vào Google Sheets Với Thông Báo Telegram - Không Cần Code!"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp Shopify lưu tất cả đơn hàng mới vào Google Sheets ngay lập tức, đồng thời nhận thông báo Telegram tức thời. Giúp theo dõi đơn hàng hiệu quả, giảm thiểu sai sót và tiết kiệm thời gian lên đến 80% cho bộ phận bán hàng."
slug: "tieu-dong-luu-don-hang-shopify-vao-google-sheets-voi-telegram"
tags: [n8n, automation, shopify, google-sheets, telegram, no-code, ecommerce]
keywords: [tự động hóa shopify, lưu đơn hàng shopify vào google sheets, thông báo telegram shopify, workflow n8n shopify, tự động hóa bán hàng online]
---

# 🚀 **Tự Động Lưu Đơn Hàng Shopify Vào Google Sheets Với Thông Báo Telegram - Không Cần Code!**

### **Giải pháp cho các sếp Shopify:**
Hàng ngày, các sếp phải thủ công ghi chép đơn hàng từ Shopify vào Google Sheets để theo dõi, phân tích và báo cáo. Đây là công việc **lặp đi lặp lại, tốn thời gian và dễ sai sót**. Với **workflow này**, các sếp sẽ:
✅ **Tự động lưu tất cả đơn hàng mới** vào Google Sheets **ngay khi khách hàng đặt hàng**.
✅ **Nhận thông báo Telegram tức thời** khi có đơn hàng mới, giúp phản hồi khách hàng nhanh chóng.
✅ **Giảm thiểu sai sót** do ghi chép thủ công.
✅ **Tiết kiệm thời gian lên đến 80%** cho bộ phận bán hàng và quản lý.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần ghi chép thủ công, đơn hàng được lưu tự động vào Google Sheets.
- **Theo dõi đơn hàng hiệu quả**: Dữ liệu được cập nhật tức thời, giúp phân tích doanh số và hành vi mua hàng dễ dàng.
- **Phản hồi khách hàng nhanh chóng**: Nhận thông báo Telegram ngay khi có đơn hàng mới, giúp hỗ trợ khách hàng kịp thời.
- **Báo cáo tự động**: Dữ liệu trong Google Sheets có thể được sử dụng để tạo báo cáo hàng ngày, tuần hoặc tháng.
- **Hoạt động 24/7**: Workflow chạy liên tục, không phụ thuộc vào giờ làm việc của nhân viên.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Shopify** với **webhook** được cấu hình để gửi dữ liệu đến n8n.
2. **Google Sheets** đã chuẩn bị sẵn với **bảng dữ liệu** để lưu đơn hàng (cột cần thiết: `Order ID`, `Customer Name`, `Email`, `Order Date`, `Total Price`, `Products`, `Status`).
3. **Bot Telegram** và **Chat ID** để nhận thông báo.
4. **API Key** của n8n (nếu tự host) hoặc tài khoản n8n.io miễn phí.
5. **Credentials** cho Google Sheets (OAuth 2.0) và Telegram Bot Token.
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/4084) hoặc sao chép mã JSON từ trang này.
- Mở **n8n Editor** và chọn **Import Workflow** → Dán hoặc tải file JSON.
- **Kích hoạt workflow** bằng cách bật nút **Active** ở góc trên bên phải.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này bao gồm **7 node** quan trọng, các sếp cần cấu hình như sau:

##### **🔹 Node 1: Receive New Shopify Order (Webhook)**
- **Cấu hình Webhook**:
  - **Path**: `shopify-webhook` (không thay đổi).
  - **HTTP Method**: `POST`.
  - **URL Webhook**: Các sếp cần **cấu hình trên Shopify Admin**:
    1. Truy cập **Shopify Admin** → **Settings** → **Notifications** → **Webhooks**.
    2. Thêm **New Webhook**:
       - **Topic**: `orders/create` (hoặc `orders/updated` nếu muốn cập nhật đơn hàng đã tồn tại).
       - **Webhook URL**: `https://[your-n8n-domain]/webhook/shopify-webhook` (địa chỉ webhook của n8n).
       - **Format**: `JSON`.
       - **Secret** (không bắt buộc, nhưng khuyến nghị để tăng an toàn).
    3. **Lưu** và kiểm tra lại trên n8n để đảm bảo webhook hoạt động.

##### **🔹 Node 2: Transform Order Data to Standard Format (Function)**
- **Mã JavaScript** đã được viết sẵn trong node này để **chuyển đổi dữ liệu Shopify** thành định dạng chuẩn.
- **Không cần chỉnh sửa** trừ khi các sếp muốn thêm hoặc loại bỏ trường dữ liệu cụ thể.
- **Output**: Dữ liệu được chuẩn hóa để lưu vào Google Sheets.

##### **🔹 Node 3: Save Order to Google Sheets (Google Sheets)**
- **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước khi import).
- **Operation**: `append` (lưu dữ liệu mới vào cuối bảng).
- **Sheet Name**: Điền tên **bảng Google Sheets** muốn lưu đơn hàng (ví dụ: `Đơn Hàng Shopify`).
- **Range**: Điền **địa chỉ ô** bắt đầu lưu dữ liệu (ví dụ: `A1`).
- **Headers**: Bật **`Use headers`** để đảm bảo cột dữ liệu được định danh chính xác.
- **Lưu ý**:
  - Các sếp cần **chia sẻ bảng Google Sheets** với tài khoản n8n (nếu tự host) hoặc tài khoản n8n.io.
  - **Kiểm tra cấu trúc bảng**: Đảm bảo bảng có các cột phù hợp với dữ liệu từ Shopify (ví dụ: `Order ID`, `Customer Name`, `Total Price`, `Products`).

##### **🔹 Node 4: Success? (If)**
- **Điều kiện kiểm tra**: Nếu lưu vào Google Sheets thành công (`$json["success"] === true`), workflow sẽ chuyển sang **Send Success Notification**.
- Nếu thất bại, workflow sẽ chuyển sang **Send Error Notification**.

##### **🔹 Node 5 & 6: Send Error Notification / Send Success Notification (Telegram)**
- **Credentials**: Chọn `telegramApi` (đã cấu hình trước khi import).
- **Chat ID**: Điền **Chat ID** của Telegram Bot (có thể tìm bằng cách gửi tin nhắn cho bot và copy ID từ URL).
- **Message**: Tùy chỉnh nội dung thông báo:
  - **Thành công**:
    ```plaintext
    🚀 Đơn hàng mới được lưu thành công!
    ID: {{ $node["Transform Order Data to Standard Format"].json["order"]["id"] }}
    Khách hàng: {{ $node["Transform Order Data to Standard Format"].json["order"]["customer"]["first_name"] }}
    Tổng tiền: {{ $node["Transform Order Data to Standard Format"].json["order"]["total_price"] }}
    ```
  - **Lỗi**:
    ```plaintext
    ❌ Lỗi khi lưu đơn hàng vào Google Sheets!
    Lỗi: {{ $json["error"] }}
    ```
- **Lưu ý**:
  - Các sếp cần **tạo Bot Telegram** và lấy **Token API**:
    1. Mở **Telegram** → Tìm bot `@BotFather`.
    2. Gửi `/newbot` và theo hướng dẫn để tạo bot.
    3. Copy **Token API** của bot.
    4. Cấu hình **credentials Telegram** trong n8n:
       - **Token**: Điền Token API từ bước trên.
       - **Chat ID**: Tìm bằng cách gửi tin nhắn cho bot và copy từ URL (ví dụ: `https://t.me/[botname]?start=[chat_id]`).

##### **🔹 Node 7: Variables (Set)**
- **Chỉnh sửa biến toàn cầu** (nếu cần):
  - Các sếp có thể thêm hoặc chỉnh sửa biến như `GOOGLE_SHEETS_RANGE` hoặc `TELEGRAM_CHAT_ID` trong node này để **tối ưu hóa workflow**.

---
#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một **đơn hàng mẫu** từ Shopify đến webhook để kiểm tra workflow.
   - Kiểm tra **Google Sheets** và **Telegram** để đảm bảo dữ liệu được lưu và thông báo được gửi.
2. **Bật Active workflow**:
   - Sau khi kiểm tra thành công, bật nút **Active** để workflow chạy liên tục.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Lưu log hoạt động**:
   - Thêm node **Google Drive** hoặc **Slack** để lưu log của workflow (ví dụ: thời gian đơn hàng được xử lý, trạng thái thành công/thất bại).

2. **Gửi báo cáo định kỳ**:
   - Sử dụng **node `n8n-nodes-base.dateTime`** kết hợp với **Google Sheets API** để tạo báo cáo doanh số hàng ngày/tuần/tháng.

3. **Kết hợp với Slack**:
   - Thay vì Telegram, các sếp có thể cấu hình **Slack Webhook** để nhận thông báo trong kênh Slack.

4. **Tự động cập nhật trạng thái đơn hàng**:
   - Sử dụng **node `n8n-nodes-base.httpRequest`** để gọi API Shopify để cập nhật trạng thái đơn hàng (ví dụ: `fulfilled`, `cancelled`).

5. **Duy trì dữ liệu lâu dài**:
   - Sử dụng **node `n8n-nodes-base.googleDrive`** để sao lưu dữ liệu Google Sheets vào Google Drive định kỳ.

6. **Tích hợp với CRM**:
   - Kết nối với **HubSpot**, **Zoho CRM** hoặc **Salesforce** để tự động cập nhật thông tin khách hàng từ Shopify.
:::

---
### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công ghi chép đơn hàng, đồng thời **tăng cường hiệu quả quản lý** với thông báo tức thời và dữ liệu tự động hóa. **Chỉ cần 10 phút để cấu hình**, sau đó workflow sẽ hoạt động **một cách tự động 24/7**.

👉 **Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất bán hàng!**
👉 **Nếu cần hỗ trợ**, liên hệ với **RedOne** (Automation Expert) để tối ưu hóa workflow cho doanh nghiệp của các sếp.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::