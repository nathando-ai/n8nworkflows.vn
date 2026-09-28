---
title: "🚀 Tự Động Hoàn Thành Báo Cáo Cập Nhật Việc Làm LinkedIn Hàng Ngày Với Google Sheets & Email"
description: "Workflow tự động hóa 100% không code giúp các sếp lấy dữ liệu việc làm LinkedIn theo keyword, lưu vào Google Sheets, và gửi báo cáo email hàng ngày với thiết kế HTML đẹp mắt. Tiết kiệm thời gian lên đến 5 giờ/tuần cho việc tra cứu thủ công."
slug: "tieu-dong-hoan-thanh-bao-cao-viec-lam-linkedin"
tags: [n8n, automation, no-code, content-creation, apify, google-sheets, gmail, linkedin-jobs]
keywords: [tự động hóa việc làm LinkedIn, n8n workflow, báo cáo hàng ngày, google sheets api, gmail automation, apify scraper]
---

# 🚀 **Tự Động Hoàn Thành Báo Cáo Việc Làm LinkedIn Hàng Ngày Với Google Sheets & Email**

### **Nỗi Đau Của Các Sếp**
Mỗi ngày, các sếp phải mất **từ 30 phút đến 1 giờ** để:
- Tra cứu việc làm trên LinkedIn theo keyword, vị trí, hoặc ngành nghề.
- Lọc và ghi chép thông tin (tên công ty, mức lương, địa điểm làm việc, ngày đăng).
- So sánh và lưu trữ dữ liệu để theo dõi xu hướng thị trường.
- Gửi báo cáo cho đồng nghiệp hoặc bản thân để theo dõi.

**Kết quả?** Thời gian quý giá bị "chôn vùi" trong công việc thủ công, trong khi cơ hội việc làm mới liên tục xuất hiện mà không được cập nhật kịp thời.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5 giờ/tuần** (tương đương 200 giờ/năm) cho việc tra cứu thủ công.
- **Dữ liệu chính xác và cập nhật** hàng ngày, không phụ thuộc vào sự nhớ của con người.
- **Báo cáo email tự động** với thiết kế HTML đẹp mắt, dễ đọc trên mọi thiết bị.
- **Lưu trữ dài hạn** trên Google Sheets, có thể phân tích sau này.
- **Tùy chỉnh linh hoạt** theo keyword, vị trí, và mức lương mong muốn.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Apify** (miễn phí) và [API Key](https://apify.com/).
2. **Google Sheets** với các cột cần thiết (tên công ty, vị trí, mức lương, ngày đăng, liên kết).
3. **Tài khoản Gmail** (để nhận email báo cáo hàng ngày).
4. **N8n Self-hosted** (để chạy workflow 24/7).
5. **Các API Key sau** đã được cấu hình trong n8n:
   - `apifyApi` (từ Apify).
   - `googleSheetsOAuth2Api` (từ Google Cloud Console).
   - `gmailOAuth2` (từ Google Cloud Console).

👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%) để tự động hóa workflow 24/7.
:::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/9240](https://n8n.io/workflows/9240) (chọn "Download JSON").
2. Trong n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. Nhấn **Import Workflow**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở n8n Editor → Nhấn **Import** → Chọn **Paste JSON**.
2. Copy toàn bộ JSON từ [n8n.io/workflows/9240](https://n8n.io/workflows/9240) (chọn "Copy JSON").
3. Dán vào ô và nhấn **Import**.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 Node "Get LinkedIn jobs" (Apify)**
- **Cấu hình Apify Actor**:
  - **Actor**: Chọn [`LinkedIn Jobs Scraper - No Cookies`](https://apify.com/apimaestro/linkedin-jobs-scraper-api).
  - **Key Parameters**:
    - `keywords`: Điền từ khóa tìm kiếm (ví dụ: `"Phân tích dữ liệu AND Python"`).
    - `location`: Địa điểm (ví dụ: `"Hà Nội, Việt Nam"`).
    - `limit`: Số lượng việc làm (ví dụ: `20`).
    - `sort`: Giữ nguyên `"date_posted"` để lấy việc làm mới nhất.
    - `date_posted`: Giữ nguyên `"last_7_days"` (có thể thay đổi thành `"last_30_days"`).

- **Credentials**:
  - Chọn `apifyApi` (đã cấu hình trước trong n8n).

#### **🔹 Node "Add jobs to Google Sheet" (Google Sheets)**
- **Chọn Sheet và Tab**:
  - Đảm bảo Google Sheet đã được tạo và chia sẻ với tài khoản n8n.
  - Chọn **Sheet Name** và **Tab Name** trong node.
- **Operation**: Giữ nguyên `"append"` để thêm dữ liệu mới vào cuối sheet.

#### **🔹 Node "Send a message" (Gmail)**
- **Điền địa chỉ email**:
  - Điền email của bạn (hoặc email nhóm) vào trường `to`.
- **Subject & Body**:
  - Subject: Giữ nguyên hoặc thay đổi thành `"Báo cáo việc làm LinkedIn - [Ngày]`".
  - Body: Dữ liệu sẽ tự động được format từ node **Code** (xem phần sau).

#### **🔹 Node "Set job data & HTML" (Code)**
- **Mở node Code** và chỉnh sửa logic HTML:
  ```javascript
  // Dữ liệu mẫu (có thể thay đổi theo yêu cầu)
  const formattedJobs = $input.all().map(job => {
    return `
      <div style="border: 1px solid #ddd; padding: 10px; margin-bottom: 10px; border-radius: 5px;">
        <h3>${job.title}</h3>
        <p><strong>Công ty:</strong> ${job.company}</p>
        <p><strong>Mức lương:</strong> ${job.salary || "Không xác định"}</p>
        <p><strong>Địa điểm:</strong> ${job.location || "Không xác định"}</p>
        <p><strong>Ngày đăng:</strong> ${job.date_posted}</p>
        <a href="${job.url}" target="_blank">Xem chi tiết</a>
      </div>
    `;
  }).join('');
  $output.all = {
    html: formattedJobs,
    date: new Date().toLocaleDateString('vi-VN', { day: '2-digit', month: '2-digit', year: 'numeric' })
  };
  ```
  - **Lưu ý**:
    - Thay đổi `job.title`, `job.company`, `job.salary`, `job.location`, `job.url` theo cấu trúc dữ liệu từ Apify.
    - Thêm/loại các thông tin tùy ý (ví dụ: thêm `job.description` nếu muốn).

#### **🔹 Node "Every day at noon..." (Schedule Trigger)**
- **Chỉnh thời gian**:
  - Giữ nguyên `"Every day at noon"` (12:00 GMT+7) hoặc thay đổi thành giờ phù hợp.
  - **Lưu ý**: Nếu chạy trên VPS ở Việt Nam, hãy chọn **timezone: `Asia/Ho_Chi_Minh`**.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run**:
   - Nhấn **Run Workflow** để kiểm tra dữ liệu đầu ra.
   - Kiểm tra email và Google Sheets xem có dữ liệu không.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động hàng ngày.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Tùy Chỉnh Keyword & Lọc Việc Làm**
- Sử dụng **Boolean operators** trong `keywords` để lọc chính xác:
  - `"Phân tích dữ liệu AND Python NOT intern"` (tìm việc làm Python cho phân tích dữ liệu, loại bỏ intern).
  - `"Chief Technology Officer OR CTO"` (tìm cả CTO và CEO).

### **2. Thêm Thông Tin Chi Tiết Vào Email**
- Mở node **Code** và thêm `job.description` vào HTML:
  ```javascript
  <p><strong>Mô tả công việc:</strong> ${job.description || "Không có mô tả"}</p>
  ```

### **3. Lưu Log & Theo Dõi Lịch Sử**
- Thêm node **StickyNote** để ghi chú:
  ```javascript
  $output.all = {
    ...$input.all,
    note: `Workflow chạy thành công vào ${new Date().toLocaleString()}`
  };
  ```
- Hoặc kết nối với **Slack/Telegram** để thông báo khi workflow chạy.

### **4. Gửi Báo Cáo Định Kỳ (Tuần/Tháng)**
- Thay đổi node **Schedule Trigger** thành:
  - `"Every Monday at 9 AM"` (báo cáo tuần).
  - `"First day of the month at 8 AM"` (báo cáo tháng).

### **5. Tích Hợp AI Đọc Mô Tả Việc Làm**
- Sử dụng node **LLM** (ví dụ: Mistral, Llama) để tóm tắt mô tả công việc:
  ```javascript
  const summary = await $node["LLM"].execute({
    prompt: `Tóm tắt mô tả công việc sau trong 3 dòng: ${job.description}`
  });
  ```

---

## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào việc **phân tích cơ hội việc làm** thay vì mất công tra cứu thủ công. Với **Google Sheets** làm kho lưu trữ và **email tự động** với thiết kế đẹp mắt, bạn sẽ **không bao giờ bỏ lỡ cơ hội việc làm mới**!

🚀 **Hành động ngay**:
1. Cài đặt n8n trên VPS (đăng ký [TinoHost](https://tino.vn/vps-n8n?affid=388) với mã **VPSN8N**).
2. Import workflow và cấu hình theo hướng dẫn.
3. **Bật Active** và bắt đầu nhận báo cáo hàng ngày!

**Cần hỗ trợ?** Liên hệ với tác giả Robin Geuens trên [LinkedIn](https://www.linkedin.com/in/rgeuens/) hoặc comment bên dưới! 👇