---
title: "🔍 **Tự Động Hóa Theo Dõi Giá Thương Hiệu Cạnh Tranh: Web Scraping + Google Sheets + Cảnh Báo Discord (Không Cần Code!)**"
description: "Workflow tự động hóa theo dõi giá sản phẩm của đối thủ cạnh tranh, so sánh với giá của bạn, và gửi cảnh báo Discord khi giá đối thủ thấp hơn. Giúp các sếp tiết kiệm thời gian, tối ưu chiến lược giá và phản ứng nhanh chóng trên thị trường."
slug: "tieu-dong-ho-gia-thuong-hieu-canh-tranh"
tags: [n8n, automation, market-research, web-scraping, google-sheets, discord-alerts]
keywords: [tự động hóa theo dõi giá cạnh tranh, n8n workflow, so sánh giá sản phẩm, cảnh báo Discord, tự động hóa marketing, web scraping không code]
---

# 🚀 **Tự Động Hóa Theo Dõi Giá Thương Hiệu Cạnh Tranh: Giải Pháp Không Cần Code Cho Chiến Lược Giá Hiệu Quả**

---

### **💡 Nỗi Đau Của Các Sếp: Theo Dõi Giá Thương Hiệu Cạnh Tranh Thủ Công Làm Giảm Hiệu Quả**
Bạn có bao giờ phải:
- **Tốn thời gian** để tra cứu giá sản phẩm của đối thủ hàng ngày?
- **Mất cơ hội** khi giá đối thủ hạ xuống nhưng bạn không biết kịp thời?
- **Không có báo cáo tự động** để so sánh và điều chỉnh chiến lược giá?
- **Phải làm thủ công** trên nhiều trang web khác nhau, dễ bị lỗi hoặc quên?

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Web scraping** giá sản phẩm của đối thủ từ trang web.
✅ **So sánh** với giá của bạn trong Google Sheets.
✅ **Gửi cảnh báo Discord** khi giá đối thủ thấp hơn.
✅ **Tự động hóa** quy trình hàng ngày, không cần can thiệp thủ công.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tra cứu giá thủ công hàng ngày.
- **Cảnh báo tức thời**: Nhận thông báo Discord khi giá đối thủ thấp hơn.
- **Chiến lược giá thông minh**: So sánh và điều chỉnh giá dựa trên dữ liệu tự động.
- **Dữ liệu chính xác**: Tránh sai sót do con người gây ra.
- **Hoạt động 24/7**: Theo dõi liên tục, không phụ thuộc vào giờ làm việc.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Discord**:
   - **Webhook URL** từ Discord (để gửi cảnh báo).
   - [Hướng dẫn tạo Webhook Discord](https://support.discord.com/hc/en-us/articles/228383668-Intro-to-Webhooks).
2. **Tài khoản Google**:
   - **Google Sheets** với cấu trúc bảng như sau:
     | Name          | Page URL          | Our Price | Competitor Price | Status (0/1) |
     |---------------|-------------------|-----------|-------------------|--------------|
     | Sản phẩm A   | `https://...`     | 1.500.000 |                   | 0            |
     | Sản phẩm B   | `https://...`     | 2.000.000 |                   | 0            |
   - **API Key Google Sheets** (cấu hình trong n8n).
3. **Trang web của đối thủ**:
   - Các sếp cần **URL sản phẩm** của đối thủ để workflow scraping.
4. **n8n Self-hosted**:
   - Cài đặt n8n trên VPS (không dùng phiên bản miễn phí trên cloud).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải workflow từ [đây](https://n8n.io/workflows/6179) (nếu cần).
2. Trong n8n Editor, nhấn **Import** và chọn file JSON.
   *Hoặc* copy toàn bộ JSON và paste vào **Import Workflow** trong menu.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **13 node**, các sếp cần chú ý cấu hình sau:

##### **A. Cấu Hình Schedule Trigger (Điều Khiển Lịch Trình)**
- Node này **khởi động workflow hàng ngày** (hoặc theo lịch bạn thiết lập).
- **Lưu ý**:
  - Thay đổi `cron` trong **Schedule Trigger** để điều chỉnh thời gian chạy (ví dụ: `0 0 * * *` để chạy hàng ngày lúc 00:00).
  - **Không** để mặc định `* * * * *` (chạy liên tục).

##### **B. Cấu Hình Google Sheets**
Workflow sử dụng **Google Sheets** để:
1. **Lấy dữ liệu sản phẩm chưa kiểm tra** (`get unchecked row`).
2. **Cập nhật trạng thái** (`Update status to 1` hoặc `Update status back to 0`).

**Cấu trúc bảng phải đúng**:
- Cột `Status` phải là số (0 hoặc 1).
- Các cột khác (`Name`, `Page URL`, `Our Price`) phải có dữ liệu mẫu.

**Lưu ý**:
- Trong node `get unchecked row`, chọn **Sheet Name** và **Range** (ví dụ: `Sheet1!A:E`).
- Trong node `Update status to 1` và `Update status back to 0`, chọn **Row ID** từ dữ liệu input.

##### **C. Cấu Hình Web Scraping (HTTP Request + HTML Extraction)**
Workflow **scraping giá** từ trang web đối thủ qua 2 node:
1. **HTTP Request to product page**:
   - Điền **URL sản phẩm** của đối thủ vào `Url`.
   - Chọn **Method**: `GET`.
   - **Headers**: Thêm `User-Agent` (ví dụ: `Mozilla/5.0`).
2. **Price extract from page**:
   - Node này **trích xuất giá** từ HTML.
   - **Lưu ý**: Các sếp cần **chỉnh XPath/CSS Selector** phù hợp với trang web của đối thủ.
     - Ví dụ: Nếu giá ở trong `<span class="price">`, điền `css selector` là `.price`.
     - **Gợi ý**: Sử dụng [DevTools](https://developer.chrome.com/docs/devtools/) để tìm selector chính xác.

##### **D. Cấu Hình Logic So Sánh Giá (`price greater than ours?`)**
Node `if` này **so sánh giá đối thủ vs giá của bạn**:
- **Điều kiện**: `json["competitorPrice"] < json["ourPrice"]` (giá đối thủ < giá bạn).
- **Nếu đúng**: Gửi cảnh báo Discord.
- **Nếu sai**: Bỏ qua.

##### **E. Cấu Hình Cảnh Báo Discord**
Node `Discord price alert` gửi thông báo khi giá đối thủ thấp hơn:
- **Lưu ý**:
  - Điền **Webhook URL** từ Discord vào `Webhook URL`.
  - **Thể loại tin nhắn**: Sử dụng `json["name"]`, `json["competitorPrice"]`, `json["ourPrice"]` để hiển thị thông tin chi tiết.
    Ví dụ:
    ```json
    {
      "content": `🚨 Giá của ${json["name"]} đã thấp hơn giá của bạn!
      - Giá đối thủ: ${json["competitorPrice"]}
      - Giá bạn: ${json["ourPrice"]}
      - Link: ${json["pageUrl"]}`
    }
    ```

##### **F. Cấu Hình Trạng Thái (`Update status`)**
Workflow **cập nhật trạng thái** trong Google Sheets để tránh lặp lại:
- **Node `Update status to 1`**: Đặt `Status = 1` khi đã kiểm tra.
- **Node `Update status back to 0`**: Đặt `Status = 0` vào ngày hôm sau (quan trọng để chạy lại cho tất cả sản phẩm).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn **Test Tab** trong n8n Editor.
   - Nhấn **Execute Workflow** với dữ liệu mẫu (ví dụ: 1 hàng trong Google Sheets).
   - Kiểm tra:
     - Cảnh báo Discord có xuất hiện không?
     - Giá được trích xuất chính xác không?
     - Trạng thái trong Sheets có cập nhật không?
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Active** sang `ON`.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Email**:
   - Thay vì chỉ Discord, các sếp có thể thêm node **Slack** hoặc **Email** để cảnh báo.
   - Ví dụ: Sử dụng node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.email`.

2. **Lưu Log Dữ Liệu**:
   - Thêm node **Google Sheets** hoặc **Database** (ví dụ: PostgreSQL) để lưu lịch sử giá.
   - Có thể sử dụng node `n8n-nodes-base.database` để lưu dữ liệu dài hạn.

3. **Báo Cáo Định Kỳ**:
   - Sử dụng node **Google Sheets** hoặc **PDF Generator** để tạo báo cáo hàng tuần/month.
   - Ví dụ: Tính trung bình giá đối thủ, so sánh với giá của bạn.

4. **Tự Động Hạ Giá**:
   - Nếu muốn **hạ giá tự động** khi đối thủ hạ giá, các sếp có thể kết hợp với node **API của hệ thống ERP** (ví dụ: Shopify, WooCommerce) để điều chỉnh giá.

5. **Xử Lý Lỗi**:
   - Thêm node **Error Handling** (ví dụ: `n8n-nodes-base.set`) để xử lý trường hợp trang web đối thủ bị down.
   - Ví dụ: Gửi cảnh báo Discord khi scraping thất bại.

---

### 📌 **Kết Luận: Áp Dụng Ngay Để Thắng Trên Thị Trường!**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào chiến lược kinh doanh chứ không phải theo dõi giá thủ công. Với **cảnh báo tức thời** và **dữ liệu chính xác**, bạn có thể:
✔ **Hạ giá kịp thời** khi đối thủ hạ giá.
✔ **Tăng giá** khi thị trường ổn định.
✔ **Cập nhật chiến lược** dựa trên dữ liệu thực tế.

**Hành động ngay hôm nay**:
1. **Cài đặt n8n trên VPS** (dùng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và theo dõi kết quả!

---
**💬 Có thắc mắc? Hãy để lại comment bên dưới hoặc liên hệ với tôi để được hỗ trợ chi tiết!** 🚀