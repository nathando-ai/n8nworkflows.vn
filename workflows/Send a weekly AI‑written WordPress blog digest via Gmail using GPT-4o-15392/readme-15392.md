---
title: "🚀 Tự Động Hóa Báo Cáo Blog WordPress Tuần Kể Từ AI GPT-4o Với Gmail - Giảm 90% Thời Gian Làm Thủ Công"
description: "Workflow tự động hóa lấy bài viết mới từ WordPress, sử dụng AI GPT-4o viết tóm tắt chuyên nghiệp, và gửi newsletter tuần cho khách hàng qua Gmail. Giúp tiết kiệm 90% thời gian viết báo cáo, đồng thời nâng cao chất lượng nội dung với sự hỗ trợ của trí tuệ nhân tạo."
slug: "tieu-dong-hoa-bao-cao-blog-wordpress-tu-gpt-4o"
tags: [n8n, automation, ai-summarization, wordpress, gmail, no-code, ai-content-generation]
keywords: [tự động hóa blog wordpress, ai viết tóm tắt bài viết, newsletter tự động, gpt-4o n8n, gửi email tự động từ wordpress, tự động hóa nội dung marketing]
---

# 🚀 **Tự Động Hóa Báo Cáo Blog WordPress Tuần Kể Từ AI GPT-4o Với Gmail**

### **Giải Pháp Cho Người Sở Hữu Blog WordPress Muốn Tiết Kiệm Thời Gian Viết Báo Cáo Tuần**
Làm thủ công việc tổng hợp bài viết mới từ WordPress, viết tóm tắt và gửi newsletter cho khách hàng là một công việc **mệt mỏi và tốn thời gian**. Mỗi tuần, bạn phải:
- Lấy dữ liệu từ WordPress (thường là API REST).
- Chọn bài viết mới nhất trong 7 ngày.
- Viết tóm tắt ngắn gọn (3-5 câu) cho mỗi bài.
- Thiết kế email đẹp mắt và gửi cho danh sách khách hàng.
- Loại bỏ email không hợp lệ.

**Workflow này tự động hóa toàn bộ quá trình chỉ trong 10 phút cài đặt!** Sử dụng **GPT-4o** để viết tóm tắt chuyên nghiệp, **Google Sheets** để quản lý danh sách khách hàng, và **Gmail** để gửi newsletter tự động hàng tuần.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 90% thời gian** viết báo cáo tuần: Không cần viết tóm tắt thủ công.
✅ **Nội dung chuyên nghiệp** nhờ AI GPT-4o: Tóm tắt ngắn gọn, chính xác và thu hút.
✅ **Gửi email tự động** hàng tuần: Không lo quên hoặc gửi sai thời gian.
✅ **Danh sách khách hàng quản lý dễ dàng** trên Google Sheets: Cập nhật và loại bỏ email không hợp lệ tự động.
✅ **Email đẹp mắt** với thiết kế responsive: Khách hàng dễ dàng đọc trên mọi thiết bị.
✅ **Hoạt động liên tục** 24/7: Không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản WordPress** (API REST API phải được kích hoạt).
2. **Tài khoản Gmail** (để gửi email newsletter).
3. **Tài khoản OpenAI** (để sử dụng GPT-4o).
4. **Google Sheets** (để lưu danh sách khách hàng).
5. **n8n Self-hosted** (do workflow sử dụng node `@n8n/n8n-nodes-langchain`).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/15392](https://n8n.io/workflows/15392) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/15392) và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **8 node chính**, các sếp cần chú ý cấu hình sau:

##### **🔹 Node 1: Weekly Schedule (Lịch Trình Tự Động)**
- **Thiết lập:** Chọn **Mỗi tuần** và thời gian gửi (ví dụ: **10h sáng thứ Hai**).
- **Lưu ý:** Đảm bảo n8n đang chạy 24/7 trên VPS.

##### **🔹 Node 2: Fetch WP Posts (Lấy Bài Viết Từ WordPress)**
- **Tham số cần điền:**
  - **URL WordPress REST API:** `https://tên-blog-của-bạn.com/wp-json/wp/v2/posts`
  - **Query Parameters:**
    - `per_page=20` (lấy tối đa 20 bài viết mới nhất).
    - `days=7` (chỉ lấy bài viết trong 7 ngày gần nhất).
    - `include=featured_media` (để lấy ảnh bìa bài viết).
- **Lưu ý:** Nếu API không trả về dữ liệu, kiểm tra **CORS** và **quyền truy cập** của WordPress.

##### **🔹 Node 3: Process Posts (Xử Lý Dữ Liệu)**
- **Mã JavaScript:** Node này tự động chuyển đổi dữ liệu từ API thành định dạng dễ đọc cho AI.
- **Không cần chỉnh sửa** (nếu không biết code, để nguyên).

##### **🔹 Node 4 & 5: LLM — GPT-4o & AI — Generate Summaries (AI Viết Tóm Tắt)**
- **Tham số cần điền:**
  - **OpenAI API Key:** Điền vào **Credentials** của node `lmChatOpenAi`.
  - **Prompt mẫu (có thể chỉnh sửa):**
    ```plaintext
    Tóm tắt bài viết {title} (được đăng ngày {date}) trong 3-5 câu ngắn gọn, chuyên nghiệp và thu hút. Đảm bảo bao gồm:
    - Điểm chính của bài viết.
    - Lợi ích cho độc giả.
    - Kết thúc bằng một câu gọi hành động (CTA) mời đọc bài đầy đủ.
    ```
- **Lưu ý:**
  - Đảm bảo **OpenAI API Key** có đủ credit để chạy.
  - Nếu muốn cải thiện chất lượng tóm tắt, thử thay đổi prompt.

##### **🔹 Node 6: Format HTML Email (Thiết Kế Email)**
- **Mã HTML mẫu:** Node này render email với cấu trúc:
  ```html
  <div>
    <h1>Tên Blog - Báo Cáo Tuần {Ngày}</h1>
    <p>Xin chào {Tên Khách Hàng},</p>
    <p>Dưới đây là tóm tắt những bài viết mới nhất tuần qua:</p>
    <!-- Dữ liệu từ AI được chèn vào đây -->
    <p>Trân trọng,</p>
    <p>Đội ngũ {Tên Blog}</p>
  </div>
  ```
- **Lưu ý:**
  - Thay thế **logo, màu sắc, và footer** bằng nội dung của blog.
  - Nếu không biết code HTML, có thể **copy mã từ node này** và chỉnh sửa trên [CodePen](https://codepen.io/) trước.

##### **🔹 Node 7: Get Subscribers (Lấy Danh Sách Khách Hàng)**
- **Tham số cần điền:**
  - **Google Sheets URL:** `https://docs.google.com/spreadsheets/d/{ID_SHEET}/edit`
  - **Sheet Name:** Tên tab chứa danh sách email (ví dụ: `Khách Hàng`).
  - **Columns:** Chọn cột chứa **email** (ví dụ: `Email`).
- **Lưu ý:**
  - Đảm bảo **Google Sheets OAuth2** được cấu hình trong n8n.
  - Mỗi hàng trong Sheet phải có **cột Email** để workflow biết gửi cho ai.

##### **🔹 Node 8: Send Newsletter (Gửi Email)**
- **Tham số cần điền:**
  - **Gmail OAuth2 Credentials:** Đăng nhập và cấp quyền cho n8n.
  - **From Email:** Địa chỉ email bạn muốn gửi từ (ví dụ: `no-reply@ten-blog.com`).
- **Lưu ý:**
  - Nếu email bị đánh dấu là spam, kiểm tra **SPF/DKIM** của Gmail.
  - Nếu muốn gửi từ nhiều địa chỉ, thêm **credentials mới** trong n8n.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run:** Chạy workflow với **dữ liệu mẫu** để kiểm tra:
   - AI có viết tóm tắt không?
   - Email có format đúng không?
   - Danh sách khách hàng có được lấy không?
2. **Bật Active:** Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động hàng tuần.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Logo & Branding:**
   - Trong node **Format HTML Email**, thêm mã `<img src="https://tên-blog.com/logo.png">` để hiển thị logo.
   - Thay đổi màu nền và font theo branding của blog.

2. **Lưu Log & Theo Dõi:**
   - Thêm node **StickyNote** sau **Send Newsletter** để ghi lại:
     - Số email đã gửi thành công.
     - Số email bị lỗi (ví dụ: không hợp lệ).
   - Ví dụ:
     ```json
     {
       "text": `📧 Newsletter sent on ${new Date().toLocaleDateString()}:
       - Success: ${successCount} emails
       - Failed: ${failedCount} emails (invalid emails)`
     }
     ```

3. **Gửi Email qua Slack/Telegram:**
   - Thêm node **Slack Webhook** sau **Send Newsletter** để thông báo khi gửi thành công:
     ```json
     {
       "text": `🚀 Newsletter sent! Check: ${emailLink}`
     }
     ```

4. **Tăng Cường Tóm Tắt AI:**
   - Thử prompt mới như:
     ```plaintext
     Viết tóm tắt bài viết {title} như một bài viết trên Medium, bao gồm:
     1. Mở đầu hấp dẫn.
     2. 3 điểm chính với ví dụ thực tế.
     3. Kết luận với câu hỏi thách thức độc giả.
     ```

5. **Tự Động Cập Nhật Danh Sách Khách Hàng:**
   - Nếu danh sách khách hàng thay đổi thường xuyên, thêm node **Google Sheets Update** để tự động cập nhật.

---

### 📌 **Kết Luận**
Workflow này **giải phóng bạn khỏi công việc viết báo cáo tuần** và thay vào đó, **AI GPT-4o tự động viết tóm tắt chuyên nghiệp**, trong khi **n8n tự động gửi email** cho khách hàng. **Chỉ cần cài đặt 1 lần**, workflow sẽ hoạt động **mỗi tuần tự động** mà không cần can thiệp.

**Hành động ngay:**
1. **Cài đặt n8n trên VPS** (nếu chưa có).
2. **Import workflow** và cấu hình các node theo hướng dẫn.
3. **Test run** và bật **Active** để bắt đầu tự động hóa!

**Nếu có vấn đề, hãy để lại comment bên dưới** hoặc liên hệ với **AI Solutions** để hỗ trợ! 🚀