---
title: "🚀 Tự Động Tạo Khách Hàng Shopify Từ Google Sheet (Không Code)"
description: "Hướng dẫn chi tiết cách import danh sách khách hàng từ Google Sheet vào Shopify chỉ với 1 click, giúp tiết kiệm hàng giờ nhập liệu thủ công và đảm bảo dữ liệu chính xác 100%."
slug: "tao-khach-hang-shopify-tu-google-sheet"
tags: [n8n, shopify, google-sheets, e-commerce, automation, no-code]
keywords: [n8n workflow shopify, import customer shopify, tự động hóa bán hàng, google sheet to shopify, n8n graphql]
---

# 🚀 Tự Động Tạo Khách Hàng Shopify Từ Google Sheet (Không Code)

Các sếp làm e-commerce chắc hẳn đều từng trải qua cảm giác "đau đầu" khi phải nhập liệu hàng trăm, hàng nghìn khách hàng từ file Excel hoặc Google Sheet vào Shopify. Làm thủ công không chỉ tốn thời gian mà còn dễ xảy ra lỗi chính tả, sai định dạng số điện thoại, hoặc bỏ sót thông tin quan trọng. Đặc biệt, Shopify rất khắt khe về định dạng số điện thoại quốc tế, việc nhập tay dễ dẫn đến lỗi "Invalid phone number".

Workflow này chính là giải pháp "cứu tinh" giúp các sếp tự động hóa 100% quy trình này. Chỉ cần có một Google Sheet chứa danh sách khách hàng, n8n sẽ tự động đọc dữ liệu và gọi API GraphQL của Shopify để tạo mới khách hàng trong vài giây. Không cần viết một dòng code nào, không cần lo lắng về lỗi định dạng nếu tuân thủ đúng cấu trúc cột.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi cần đồng bộ dữ liệu thường xuyên, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tối đa:** Chuyển đổi hàng trăm dòng dữ liệu từ Sheet sang Shopify chỉ trong vài giây thay vì hàng giờ nhập tay.
- **Độ chính xác 100%:** Loại bỏ hoàn toàn lỗi con người (sai chính tả email, sai định dạng số điện thoại) nhờ kiểm soát chặt chẽ qua cấu trúc cột.
- **Quy trình chuẩn hóa:** Dữ liệu khách hàng luôn nhất quán, sẵn sàng cho các chiến dịch marketing email hoặc SMS ngay sau khi import.
- **Dễ dàng mở rộng:** Có thể kết hợp thêm các bước xác thực email hoặc gán tag khách hàng ngay trong cùng một workflow.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Bản miễn phí hoặc Self-hosted.
2. **Tài khoản Google:** Đã kết nối với n8n thông qua OAuth2 (để đọc Google Sheets).
3. **Tài khoản Shopify Admin:** Quyền truy cập vào phần Settings > Apps.
4. **Shopify Admin API Token:** Token bắt đầu bằng `shpat_` (hướng dẫn tạo bên dưới).
5. **Google Sheet:** Chứa danh sách khách hàng với các cột đúng chuẩn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n của các sếp.
2. Chọn **Import from URL** hoặc **Import from File**.
3. Dán link workflow gốc: `https://n8n.io/workflows/4866` hoặc tải file JSON về và import.
4. Workflow sẽ hiển thị 3 node chính: `Start Workflow`, `Google Sheet, Fetch Customers`, và `Shopify, CustomerCreate`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**A. Cấu hình Google Sheet (Node: `Google Sheet, Fetch Customers`)**
1. **Chọn Credentials:** Chọn tài khoản Google đã kết nối (OAuth2).
2. **Chọn Sheet:** Chọn đúng Google Sheet chứa danh sách khách hàng.
3. **Định dạng dữ liệu (RẤT QUAN TRỌNG):**
   - Dòng 1 của Sheet phải là tên cột (Header).
   - Các cột bắt buộc phải có tên chính xác sau (thứ tự cột không quan trọng, nhưng tên cột phải khớp):
     - `first_name`: Họ tên (String).
     - `last_name`: Tên (String).
     - `email`: Email hợp lệ.
     - `mobile_phone`: Số điện thoại quốc tế, **không có khoảng trắng**, ví dụ: `+84912345678`. (Shopify sẽ từ chối nếu sai định dạng này).

**B. Cấu hình Shopify (Node: `Shopify, CustomerCreate`)**
1. **Chọn Credentials:** Chọn hoặc tạo mới credential loại **Header Auth**.
   - **Key:** `X-Shopify-Access-Token`
   - **Value:** Dán token Shopify của các sếp (bắt đầu bằng `shpat_...`).
2. **Cấu hình GraphQL Query:**
   - Node này sử dụng API GraphQL. Các sếp cần đảm bảo query trong node đã được cấu hình sẵn để map các trường `first_name`, `last_name`, `email`, `phone` từ input của n8n vào biến `customerCreate`.
   - *Lưu ý:* Nếu import từ file JSON chuẩn, query thường đã được viết sẵn. Các sếp chỉ cần kiểm tra lại phần `input` của query có khớp với tên cột trong Google Sheet không.

**C. Hướng dẫn tạo Shopify Access Token (Nếu chưa có)**
1. Vào **Settings** > **Apps and sales channels**.
2. Chọn **Develop apps**.
3. Bấm **Create app**, đặt tên (ví dụ: "N8N Import Tool").
4. Bấm **Configure Admin API scopes**.
5. Cấp quyền tối thiểu: `read_customers` và `write_customers`.
6. Bấm **Save**.
7. Quay lại trang app, bấm **Install app** > **Install**.
8. Bấm **Reveal token once** và copy token. Lưu lại ở nơi an toàn (Password Manager).

#### 3. Kích hoạt ⚡️
1. **Test Run:** Bấm nút **Execute Workflow** (hoặc bấm vào từng node để test riêng).
   - Kiểm tra node Google Sheet: Dữ liệu có được đọc đúng không?
   - Kiểm tra node Shopify: Có thông báo "Customer created" không?
2. **Kiểm tra trên Shopify:** Vào **Customers** trong Shopify Admin để xác nhận khách hàng đã được tạo mới.
3. **Bật Active:** Khi đã test thành công, bật công tắc **Active** ở góc trên bên phải.
   - *Gợi ý:* Nếu muốn chạy tự động định kỳ (ví dụ: mỗi 15 phút), các sếp có thể thay node `Start Workflow` (Manual Trigger) bằng `Schedule Trigger`.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước xác thực Email:** Trước khi tạo khách hàng, các sếp có thể thêm node `IF` để kiểm tra xem email đã tồn tại trong Shopify chưa (dùng query `customerSearch`), tránh lỗi trùng lặp.
- **Gán Tag tự động:** Trong query GraphQL `customerCreate`, các sếp có thể thêm trường `tags` để tự động gán tag "Imported-from-Sheet" hoặc "VIP" cho khách hàng mới.
- **Gửi thông báo qua Telegram/Slack:** Thêm node `Telegram` hoặc `Slack` ở cuối workflow để gửi thông báo "Đã import thành công X khách hàng" khi workflow chạy xong.
- **Xử lý lỗi:** Thêm node `Error Trigger` hoặc cấu hình `On Error` cho node Shopify để log lại các dòng dữ liệu bị lỗi (ví dụ: số điện thoại sai định dạng) vào một Sheet khác để các sếp dễ dàng sửa chữa.

### 📌 Kết luận
Việc nhập liệu khách hàng thủ công là một trong những "nỗi đau" lớn nhất của các chủ shop mới. Với workflow n8n này, các sếp có thể biến quy trình tẻ nhạt đó thành một tác vụ tự động, nhanh chóng và chính xác. Hãy thử ngay hôm nay để giải phóng thời gian tập trung vào việc bán hàng và phát triển chiến lược marketing!