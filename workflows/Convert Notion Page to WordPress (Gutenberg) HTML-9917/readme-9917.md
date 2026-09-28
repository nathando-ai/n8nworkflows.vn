---
title: "🚀 Chuyển Notion Page Sang HTML Gutenberg WordPress Tự Động (Không Cần Code)"
description: "Workflow n8n chuyên nghiệp chuyển đổi nội dung từ Notion sang HTML Gutenberg cho WordPress chỉ trong vài giây, tiết kiệm thời gian viết lại thủ công và đảm bảo tính nhất quán cao. Phù hợp cho blogger, marketer và quản trị viên nội dung."
slug: "chuyen-notion-sang-html-gutenberg-wordpress"
tags: [n8n, automation, content-creation, wordpress, notion, html-gutenberg]
keywords: [n8n workflow chuyển Notion sang WordPress, tự động hóa nội dung, chuyển đổi Notion thành HTML, Gutenberg WordPress, lưu trữ nội dung hiệu quả]
---

# 🚀 **Chuyển Notion Page Sang HTML Gutenberg WordPress Tự Động (Không Cần Code)**

## **📌 Nỗi Đau Của Các Sếp Khi Viết Nội Dung WordPress**
Các sếp thường phải:
- **Chép nội dung từ Notion sang WordPress** một cách thủ công, mất thời gian và dễ bị lỗi.
- **Không thể giữ được định dạng** như bold, italic, danh sách, hình ảnh, hoặc các block phức tạp từ Notion.
- **Phải viết lại từ đầu** khi cập nhật nội dung, làm mất đi tính nhất quán và hiệu quả.

**Workflow này giải quyết tất cả vấn đề trên bằng cách tự động hóa toàn bộ quá trình chuyển đổi nội dung từ Notion sang HTML Gutenberg WordPress chỉ trong vài giây!**

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần chép nội dung thủ công, giảm thiểu lỗi sai.
- **Định dạng hoàn hảo**: Bất kỳ block Notion (heading, image, video, toggle, column) đều được chuyển thành HTML Gutenberg chính xác.
- **Hoạt động liên tục**: Chỉ cần cập nhật Notion, workflow tự động đồng bộ nội dung sang WordPress.
- **Tích hợp hoàn hảo**: Hoạt động như một sub-workflow, có thể gọi từ bất kỳ workflow n8n khác.
- **Dễ dàng mở rộng**: Thêm các bước xử lý như gửi email thông báo, lưu log, hoặc chia sẻ kết quả trên Slack.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
- **Tài khoản Notion** và **API Key Notion** (tạo tại [Notion API](https://www.notion.so/help/integrate-api)).
- **WordPress** với plugin **REST API** (nếu muốn tự động đẩy nội dung).
- **n8n Self-hosted** (không dùng phiên bản cloud để đảm bảo tính ổn định 24/7).
- **URL của trang Notion** cần chuyển đổi (được truyền vào workflow).
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [link gốc](https://n8n.io/workflows/9917).
2. Mở **n8n Editor** và chọn **"Import"** → Chọn file JSON.
3. **Hoặc** copy toàn bộ JSON và dán vào **"Import from JSON"** trong Editor.

:::note[LƯU Ý]
- Workflow này được thiết kế làm **sub-workflow**, nên các sếp cần gọi nó từ một workflow cha khác.
- Nếu muốn chạy thử, có thể kích hoạt **Manual Trigger** và nhập URL Notion vào node **"Edit Fields2"**.
:::

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node "Get a database page" (Lấy trang Notion)**
- **Credentials**: Chọn `notionApi` (đã cấu hình trước).
- **URL Notion**: Điền vào node **"Edit Fields2"** (hoặc truyền từ workflow cha).

#### **🔹 Node "Get many child blocks" (Lấy tất cả block con)**
- **Credentials**: Chọn `notionApi`.
- **fetchNestedBlocks: true**: Đã được thiết lập sẵn để lấy tất cả block, bao gồm block trong column, toggle, etc.

#### **🔹 Node "decode paragraphs" (Chuyển đổi đoạn văn bản)**
- **Logic**: Chuyển Notion's annotations (bold, italic, link) thành HTML (`<strong>`, `<em>`, `<a>`).
- **Không cần chỉnh sửa**, chỉ cần đảm bảo node **"choose content field"** lấy dữ liệu từ `$json.content`.

#### **🔹 Node "decode blocks" (Chuyển đổi tất cả loại block)**
- **Switch statement**: Chuyển đổi từng loại block Notion (heading, image, video, divider) thành HTML Gutenberg.
- **Ví dụ**:
  - `heading_1` → `<h1 class="wp-block-heading">`
  - `image` → `<figure class="wp-block-image">`
- **Không cần chỉnh sửa**, nhưng nếu muốn thêm loại block mới, cần mở node này và bổ sung vào switch case.

#### **🔹 Node "drop unnecessary fields" (Loại bỏ trường không cần thiết)**
- **Giảm tải dữ liệu**: Chỉ giữ lại `id`, `parent_id`, `type`, và `content` (HTML đã chuyển đổi).
- **Không cần chỉnh sửa**, nhưng nếu muốn thêm trường khác, mở node và sửa lại.

#### **🔹 Node "nested blocks" (Xử lý block lồng nhau)**
- **Quá trình quan trọng**: Tìm tất cả block con của column và inject HTML vào trong block cha.
- **Ví dụ**: Nếu có một block `column_list` chứa nhiều block con, node này sẽ wrap chúng vào `<div class="wp-block-columns">`.
- **Không cần chỉnh sửa**, nhưng nếu gặp lỗi với block cụ thể, có thể mở node và debug.

#### **🔹 Node "only top level blocks" (Lọc block cấp cao nhất)**
- **Lọc block cha**: Chỉ giữ lại block là con trực tiếp của trang Notion (loại bỏ block con lồng nhau).
- **Điều kiện**: `parent_id` phải trùng với `page_id` từ node **"Get a database page"**.

#### **🔹 Node "choose content field" (Chọn trường nội dung)**
- **Tạo trường `wp`**: Giữ nội dung HTML trong trường `wp` để dễ dàng xử lý sau.
- **Logic**: `$json.children || $json.content` → Nếu block có children (như column), lấy từ `children`; nếu không, lấy từ `content`.

#### **🔹 Node "Aggregate" (Kết hợp tất cả block)**
- **Gộp thành mảng**: Tất cả block HTML được gộp thành một mảng để dễ dàng join sau.

#### **🔹 Node "join lines" (Nối các dòng HTML)**
- **Kết quả cuối cùng**: Tất cả block HTML được nối thành một chuỗi duy nhất, sẵn sàng để đẩy vào WordPress.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn **"Execute workflow"** và nhập URL Notion vào node **"Edit Fields2"**.
   - Kiểm tra kết quả trong node **"join lines"** để đảm bảo HTML được chuyển đổi chính xác.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, bật **Active** để workflow hoạt động liên tục.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **🔹 Kết Hợp Với WordPress REST API**
- Sau khi có HTML từ workflow, các sếp có thể gọi **WordPress REST API** để tự động đẩy bài viết:
  ```json
  {
    "title": "Tên bài viết",
    "content": "HTML từ workflow",
    "status": "publish"
  }
  ```
- **Node cần thêm**: `n8n-nodes-base.httpRequest` để gọi API WordPress.

### **🔹 Gửi Thông Báo Khi Cập Nhật**
- Thêm node **Slack** hoặc **Email** để thông báo khi workflow hoàn thành:
  ```json
  {
    "text": "Bài viết đã được chuyển từ Notion sang WordPress thành công!"
  }
  ```

### **🔹 Lưu Log Lịch Sử Cập Nhật**
- Sử dụng **Google Sheets** hoặc **Notion Database** để lưu lịch sử chuyển đổi:
  ```json
  {
    "notion_url": "URL Notion",
    "wordpress_url": "URL WordPress",
    "timestamp": "2024-05-20T12:00:00Z"
  }
  ```

### **🔹 Tự Động Chạy Khi Cập Nhật Notion**
- Sử dụng **Webhook Notion** để kích hoạt workflow khi có thay đổi:
  - Cài đặt **Notion Webhook** và kết nối với node **"When Executed by Another Workflow"**.

---

## **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quá trình chuyển đổi nội dung từ Notion sang WordPress **không cần viết code**. Bằng cách kết hợp với **n8n Self-hosted**, các sếp có thể đảm bảo tính ổn định và hoạt động liên tục 24/7.

**🚀 Hãy áp dụng ngay và tiết kiệm thời gian cho công việc nội dung của mình!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::