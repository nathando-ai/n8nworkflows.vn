---
title: "📊 Tự Động Hoàn Thành Báo Cáo Forum Disqus & Gửi Email HTML Chi Tiết (Không Cần Code)"
description: "Workflow này tự động thu thập dữ liệu từ Forum Disqus (bài viết, chủ đề, danh mục) và chuyển đổi thành bảng HTML, sau đó gửi báo cáo định kỳ qua Gmail. Giúp các sếp tiết kiệm 10+ giờ/tháng và theo dõi hoạt động diễn đàn một cách chuyên nghiệp."
slug: "tieu-dong-hoan-thanh-bao-cao-disqus-voi-gmail-html"
tags: [n8n, automation, marketing, disqus, gmail, html-table, no-code]
keywords: [tự động hóa disqus, báo cáo diễn đàn, gửi email html, n8n workflow marketing, thu thập dữ liệu forum]
---

# 🚀 **Tự Động Hoàn Thành Báo Cáo Forum Disqus & Gửi Email HTML Chi Tiết (Không Cần Code)**

### **Nỗi Đau Của Các Sếp**
Các sếp quản lý diễn đàn Disqus thường phải:
- **Làm thủ công** thu thập dữ liệu từ các bài viết, chủ đề và danh mục.
- **Tốn thời gian** để tổng hợp và chuyển đổi thành bảng dữ liệu dễ đọc.
- **Không có báo cáo định kỳ**, dẫn đến mất thông tin quan trọng về tương tác của người dùng.
- **Không thể cá nhân hóa** báo cáo theo nhu cầu riêng của doanh nghiệp.

Workflow này **giải quyết tất cả** bằng cách tự động hóa toàn bộ quy trình, từ thu thập dữ liệu đến gửi báo cáo qua email với định dạng HTML chuyên nghiệp.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10+ giờ/tháng** – Không cần làm thủ công thu thập và tổng hợp dữ liệu.
✅ **Báo cáo định kỳ tự động** – Gửi email hàng tuần/tháng với dữ liệu mới nhất.
✅ **Định dạng HTML chuyên nghiệp** – Bảng dữ liệu dễ đọc, có thể chia sẻ với khách hàng hoặc đội ngũ.
✅ **Tương tác với Disqus** – Theo dõi bài viết, chủ đề và danh mục một cách chi tiết.
✅ **Không cần kỹ năng code** – Cài đặt và chạy workflow chỉ với vài bước đơn giản.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Disqus** – Đăng ký và lấy **API Key** từ [Trang quản lý Disqus](https://disqus.com/admin/).
2. **Tài khoản Gmail** – Để nhận và gửi báo cáo (cần **OAuth 2.0** hoặc **SMTP**).
3. **Tên Forum Disqus** – Địa chỉ URL của diễn đàn bạn muốn thu thập dữ liệu.
4. **Thời gian chạy tự động** – Cài đặt **n8n Self-hosted** để workflow hoạt động 24/7.
:::

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập vào tài khoản.
2. Nhấn **"Create new workflow"** → **"Import from JSON"**.
3. Dán JSON từ [link gốc](https://n8n.io/workflows/4531) hoặc tải file JSON từ đây.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **11 node** quan trọng, các sếp cần cấu hình như sau:

##### **A. Node `manualTrigger` (Kích hoạt thủ công)**
- **Lưu ý**: Node này chỉ dùng để **test workflow** trước khi chạy tự động. Sau khi cấu hình xong, các sếp nên **bật `Active`** và cài đặt **Trigger Schedule** (nếu dùng n8n Self-hosted).

##### **B. Node `Get Forum`, `Get Posts Forum`, `Get Threads Forum`, `Get Categories Forum` (Thu thập dữ liệu Disqus)**
- **Cấu hình Disqus API**:
  - **API Key**: Điền từ trang quản lý Disqus.
  - **Forum Name**: Điền tên hoặc URL của diễn đàn (ví dụ: `https://tên-diễn-dàn.disqus.com`).
  - **Limit**: Đặt số lượng bài viết/chủ đề lấy (ví dụ: `100`).
  - **Fields**: Chọn các trường cần thu thập (ví dụ: `title`, `url`, `created_at`, `author`).

##### **C. Node `Merge Threads + Forum` & `Merge Categories + Posts` (Gộp dữ liệu)**
- **Lưu ý**: Các node này **không cần chỉnh sửa**, chỉ đảm bảo dữ liệu từ Disqus được gộp đúng cấu trúc.

##### **D. Node `Merge All` (Gộp tất cả dữ liệu)**
- **Kiểm tra**: Đảm bảo tất cả dữ liệu từ các node Disqus được gộp thành một mảng duy nhất.

##### **E. Node `Combine Data` (Code)**
- **Lưu ý**: Node này **không cần chỉnh sửa** vì đã được tối ưu hóa để kết hợp dữ liệu từ các node trước.
- **Nội dung code**:
  ```javascript
  // Dữ liệu đầu vào từ node Merge All
  const mergedData = $input.all();

  // Kết hợp dữ liệu thành một mảng duy nhất
  const combinedData = mergedData.flatMap(item => item.json);
  ```
  - **Nếu cần thay đổi**: Các sếp có thể mở node này và chỉnh sửa logic nếu muốn thêm/bỏ trường dữ liệu.

##### **F. Node `Format Table` (Code)**
- **Lưu ý**: Node này **chuyển đổi dữ liệu thành định dạng HTML** để gửi qua email.
- **Nội dung code**:
  ```javascript
  // Tạo bảng HTML từ dữ liệu
  const tableRows = $input.all().map(item => {
    return `
      <tr>
        <td>${item.title || 'N/A'}</td>
        <td>${item.url || 'N/A'}</td>
        <td>${item.created_at || 'N/A'}</td>
        <td>${item.author || 'N/A'}</td>
      </tr>
    `;
  }).join('');

  const tableHTML = `
    <table border="1" cellpadding="5" cellspacing="0" style="border-collapse: collapse;">
      <thead>
        <tr>
          <th>Tiêu đề</th>
          <th>Link</th>
          <th>Thời gian tạo</th>
          <th>Tác giả</th>
        </tr>
      </thead>
      <tbody>
        ${tableRows}
      </tbody>
    </table>
  `;

  return { html: tableHTML };
  ```
  - **Nếu cần thay đổi**: Các sếp có thể chỉnh sửa các trường (`title`, `url`,...) để phù hợp với dữ liệu của mình.

##### **G. Node `Gmail Report Notifications` (Gửi email)**
- **Cấu hình Gmail**:
  - **Authentication**: Chọn **OAuth 2.0** (khuyến nghị) hoặc **SMTP**.
  - **From Email**: Điền địa chỉ email muốn gửi (ví dụ: `báo cáo@tên-doanh-nghiệp.com`).
  - **To Email**: Điền email nhận báo cáo (ví dụ: `quanly@tên-doanh-nghiệp.com`).
  - **Subject**: Đặt tiêu đề email (ví dụ: **"Báo cáo hoạt động diễn đàn Disqus - Tuần ${new Date().toLocaleString('vi-VN', { week: 'long' })}"**).
  - **HTML Body**: Chọn **HTML** và điền nội dung từ node `Format Table`.
  - **Attachments**: Nếu cần, thêm file đính kèm (ví dụ: file CSV từ dữ liệu).

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Execute"** để chạy workflow với dữ liệu mẫu.
   - Kiểm tra email đã nhận được báo cáo HTML chưa.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, nhấn **"Active"** để workflow chạy tự động.
   - **Nếu dùng n8n Self-hosted**, cài đặt **Trigger Schedule** (ví dụ: chạy hàng tuần vào thứ 7 sáng 8h).

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi báo cáo định kỳ**:
   - Cài đặt **Trigger Schedule** trong n8n Self-hosted để workflow chạy hàng tuần/tháng.
   - Ví dụ: `0 0 * * 0` (chạy vào thứ bảy hàng tuần).

2. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo báo cáo mới qua chat.

3. **Lưu log dữ liệu**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu dữ liệu dài hạn và theo dõi lịch sử.

4. **Tự động phân tích dữ liệu**:
   - Sử dụng node **Code** để tính toán thống kê (ví dụ: số bài viết mới, chủ đề nóng nhất) và thêm vào email.

5. **Cá nhân hóa báo cáo**:
   - Thêm node **Template Engine** (ví dụ: **Handlebars**) để tự động thay đổi tiêu đề hoặc nội dung email dựa trên dữ liệu.
:::

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc thu thập và tổng hợp dữ liệu từ Disqus một cách thủ công. Với **báo cáo HTML chuyên nghiệp** và **gửi tự động qua email**, các sếp có thể tập trung vào việc phân tích và cải thiện trải nghiệm người dùng trên diễn đàn.

**Hành động ngay**:
1. **Cài đặt n8n Self-hosted** trên VPS để workflow chạy 24/7.
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Bật Active** và bắt đầu tự động hóa báo cáo của mình!

---
:::note[LƯU Ý CUỐI CUNG]
- **N8n Self-hosted** là lựa chọn tối ưu để workflow chạy liên tục. Các sếp có thể đăng ký **VPS TinoHost** với mã giảm giá **VPSN8N** (giảm tới 39%) hoặc **VPS Xeon 4GB chỉ 50k/tháng** để tiết kiệm chi phí.
- **Nếu gặp vấn đề**, các sếp có thể liên hệ với tác giả [Ghufran Ridhawi](https://n8n.io/workflows/4531) qua email hoặc [n8n Community](https://community.n8n.io/) để hỗ trợ.
:::

---
**Chúc các sếp thành công với việc tự động hóa báo cáo Disqus!** 🚀