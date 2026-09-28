---
title: "🚀 Tổng Hợp Đánh Giá Tự Động: Trustpilot, Google & Facebook vào Google Sheets"
description: "Workflow n8n tự động gom mọi đánh giá từ Trustpilot, Google và Facebook về một Google Sheets duy nhất. Tiết kiệm hàng giờ mỗi tuần, chuẩn hóa dữ liệu và theo dõi uy tín thương hiệu thời gian thực."
slug: "tong-hop-danh-gia-trustpilot-google-facebook"
tags: [n8n, automation, no-code, reputation-management, google-sheets, shopify]
keywords: [n8n workflow, tự động hóa đánh giá, gom review, quản lý uy tín, google sheets automation]
---

# 🚀 Tổng Hợp Đánh Giá Tự Động: Trustpilot, Google & Facebook vào Google Sheets

Trong kinh doanh hiện đại, đánh giá (review) là "tiền mặt" của uy tín. Tuy nhiên, việc phải mở 3-4 tab trình duyệt khác nhau để kiểm tra Trustpilot, Google Maps và Facebook mỗi ngày là một gánh nặng vô hình. Bạn mất thời gian, dễ bỏ sót phản hồi tiêu cực, và dữ liệu rời rạc khiến việc phân tích xu hướng khách hàng trở nên cực kỳ khó khăn.

Workflow này giải quyết triệt để vấn đề đó. Nó hoạt động như một "trợ lý ảo" không ngủ, tự động quét các nền tảng lớn nhất, chuẩn hóa dữ liệu (điểm số, nội dung, ngày giờ) và lưu chúng vào một bảng Google Sheets duy nhất. Các sếp chỉ cần mở một file duy nhất để nắm bắt toàn bộ bức tranh phản hồi từ khách hàng, không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/tuần:** Không còn việc copy-paste thủ công từ các nền tảng khác nhau.
- **Dữ liệu tập trung & Chuẩn hóa:** Mọi review được đưa về một định dạng thống nhất trong Google Sheets, dễ dàng lọc và phân tích.
- **Phát hiện vấn đề tức thì:** Dễ dàng tạo bộ lọc (Filter) trong Sheets để tìm các review 1-2 sao và phản hồi nhanh chóng.
- **Tích hợp hệ sinh thái:** Dữ liệu review được gắn với sản phẩm (nếu dùng Shopify), giúp liên kết phản hồi với hiệu suất bán hàng cụ thể.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã cài đặt và chạy (Cloud hoặc Self-hosted).
- **Google Sheets:** Một file Google Sheet trống hoặc có sẵn các cột: `Product Name`, `Platform`, `Rating`, `Review Text`, `Date`, `Source URL`.
- **API Keys / Credentials:**
    - **Shopify Admin API Key:** (Tùy chọn) Nếu muốn gắn review với sản phẩm cụ thể.
    - **Google Cloud API Key:** Để gọi API Google Places (lấy review Google Maps).
    - **Facebook Graph API Token:** Để lấy review từ trang Facebook Business.
    - **Trustpilot API Key:** (Nếu có) Hoặc cấu hình HTTP Request để scrape/call API công khai nếu được phép.
- **Business ID:** ID của doanh nghiệp trên Google Places và Facebook.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow từ link gốc hoặc copy toàn bộ code JSON.
2. Mở n8n Editor của bạn.
3. Chọn **Import from URL** (nếu có link) hoặc **Import from Clipboard** (nếu đã copy JSON).
4. Workflow sẽ hiện ra với 8 nodes chính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Workflow mặc định là khung sườn, các sếp cần điền thông tin thực tế của mình vào các node sau:

*   **Node: `Daily Review Sync` (Schedule Trigger)**
    *   Mặc định chạy mỗi ngày. Các sếp có thể chỉnh tần suất (ví dụ: mỗi 4 giờ) nếu muốn dữ liệu mới hơn.

*   **Node: `Get Products` (Shopify)**
    *   *Lưu ý:* Node này dùng để lấy danh sách sản phẩm làm "chìa khóa" gắn với review.
    *   **Cấu hình:** Chọn Credentials Shopify.
    *   **Tham số:** Chọn `Limit` (số lượng sản phẩm muốn quét, ví dụ: 50) và `Fields` (chỉ lấy `id`, `title` để nhẹ dữ liệu).
    *   *Nếu không dùng Shopify:* Các sếp có thể xóa node này và chuyển sang dùng một danh sách tĩnh (Static Data) hoặc bỏ qua bước gắn sản phẩm, chỉ tập trung vào review chung của thương hiệu.

*   **Node: `Fetch Trustpilot Reviews` (HTTP Request)**
    *   **Method:** GET
    *   **URL:** Thay thế bằng endpoint API của Trustpilot hoặc URL scrape (nếu dùng kỹ thuật khác).
    *   **Headers:** Thêm `Authorization` hoặc `X-API-KEY` nếu cần.
    *   *Mẹo:* Nếu Trustpilot không cho phép API miễn phí, các sếp có thể cân nhắc dùng một node `Code` để parse HTML hoặc dùng dịch vụ bên thứ 3.

*   **Node: `Fetch Google Reviews` (HTTP Request)**
    *   **URL:** `https://places.googleapis.com/v1/places/{YOUR_PLACE_ID}/reviews`
    *   **Headers:**
        *   `Content-Type`: `application/json`
        *   `X-Goog-Api-Key`: `[Điền API Key Google Cloud của bạn]`
        *   `X-Goog-FieldMask`: `reviews.rating, reviews.text, reviews.authorDisplayName, reviews.creationTime`
    *   **Body:** Có thể thêm filter `minRating` hoặc `maxRating` nếu muốn.

*   **Node: `Fetch Facebook Reviews` (HTTP Request)**
    *   **URL:** `https://graph.facebook.com/v18.0/{YOUR_PAGE_ID}/reviews`
    *   **Query Parameters:**
        *   `fields`: `rating, message, created_time, from`
        *   `limit`: `50`
        *   `access_token`: `[Điền Page Access Token của bạn]`

*   **Node: `Normalize Review Data` (Code)**
    *   Node này dùng JavaScript để gộp dữ liệu từ 3 nguồn (Trustpilot, Google, FB) vào một cấu trúc chung.
    *   **Kiểm tra:** Đảm bảo logic trong code khớp với cấu trúc JSON trả về từ các API ở trên. Nếu API thay đổi, các sếp cần chỉnh lại phần `json.rating`, `json.text`... trong node Code này.

*   **Node: `Check if Reviews Found` (IF)**
    *   Node này kiểm tra xem có dữ liệu mới không để tránh ghi đè hoặc ghi rỗng vào Sheets.
    *   **Điều kiện:** `length` của mảng review > 0.

*   **Node: `Store Reviews Database` (Google Sheets)**
    *   **Credentials:** Chọn tài khoản Google của bạn.
    *   **Document ID:** ID của file Google Sheet (lấy từ URL: `docs.google.com/spreadsheets/d/[ID_NÀY]/edit`).
    *   **Sheet Name:** Tên tab trong file (ví dụ: `Reviews`).
    *   **Operation:** `Append` (Thêm dòng mới).
    *   **Mapping:** Ánh xạ các trường dữ liệu từ node `Normalize Review Data` vào các cột tương ứng trong Sheet.

#### 3. Kích hoạt ⚡️
1. Nhấn **Test Workflow** (hoặc nút Play) để chạy thử với dữ liệu mẫu.
2. Kiểm tra kết quả:
    *   Mở Google Sheet xem có dòng dữ liệu mới xuất hiện không.
    *   Kiểm tra xem dữ liệu có bị lỗi format (ví dụ: ngày giờ, ký tự đặc biệt) không.
3. Nếu ổn, nhấn **Active** để workflow tự động chạy theo lịch đã đặt.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp AI để phân tích cảm xúc:** Thêm một node `OpenAI` hoặc `Anthropic` sau bước `Normalize Review Data`. Yêu cầu AI phân loại review là "Tích cực", "Trung tính" hoặc "Tiêu cực" và thêm cột `Sentiment` vào Sheets.
- **Cảnh báo qua Slack/Telegram:** Thêm node `Slack` hoặc `Telegram` sau node `IF`. Nếu phát hiện review dưới 3 sao, tự động gửi thông báo cho đội ngũ CSKH để phản hồi ngay lập tức.
- **Tạo Dashboard PowerBI/Looker Studio:** Vì dữ liệu đã nằm gọn trong Google Sheets, các sếp có thể kết nối trực tiếp với Looker Studio (miễn phí) để tạo dashboard trực quan hóa xu hướng đánh giá theo tháng, theo sản phẩm.
- **Lọc theo sản phẩm cụ thể:** Nếu dùng Shopify, các sếp có thể tạo thêm logic để chỉ lấy review của các sản phẩm "Best Seller" hoặc sản phẩm mới ra mắt để tập trung nguồn lực chăm sóc.

### 📌 Kết luận
Việc quản lý danh tiếng (Reputation Management) không nên là một công việc thủ công, lặp đi lặp lại. Với workflow này, các sếp đã biến dữ liệu phân tán từ 3 nền tảng lớn nhất thành một kho dữ liệu tập trung, sạch sẽ và sẵn sàng để phân tích. Hãy dành thời gian tiết kiệm được để tập trung vào việc cải thiện sản phẩm và dịch vụ, thay vì loay hoay với việc copy-paste review.

Chúc các sếp triển khai thành công và xây dựng thương hiệu vững mạnh! 🚀