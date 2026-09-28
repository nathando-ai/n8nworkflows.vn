---
title: "🚀 Tự Động Hóa Tạo Bài Viết & Ảnh Facebook Chuyên Nghiệp Với AI Gemini & Graph API - Không Cần Code"
description: "Workflow này tự động viết bài viết Facebook chuyên nghiệp, tạo hình ảnh đẹp mắt từ văn bản thô và đăng lên Fanpage chỉ với một cú nhấp chuột. Giúp tiết kiệm thời gian lên đến 80% cho việc tạo nội dung, đồng thời nâng cao chất lượng hình ảnh và văn bản với AI Gemini."
slug: "tieu-dong-hoa-tao-bai-viet-va-anh-facebook-voi-gemini"
tags: [n8n, automation, no-code, ai-gemini, facebook-graph-api, content-creation, multimodal-ai]
keywords: [tự động hóa facebook, tạo bài viết facebook tự động, gemini ai facebook, tự động hóa nội dung social media, workflow n8n facebook, tạo ảnh facebook tự động]
---

# 🚀 **Tự Động Hóa Tạo Bài Viết & Ảnh Facebook Chuyên Nghiệp Với AI Gemini & Graph API**

## **💡 Giải Pháp Cho Những Người Quản Lý Fanpage Bận Rộn**
Bạn đã bao giờ cảm thấy **mệt mỏi** khi phải viết bài viết Facebook từ đầu, chọn hình ảnh phù hợp, chỉnh sửa và đăng tải? Hoặc **chán ngấy** với những hình ảnh cũ kĩ, không thu hút người dùng? Workflow này sẽ **giải phóng bạn khỏi công việc thủ công** bằng cách tự động:
- **Viết bài viết Facebook chuyên nghiệp** với emoji, hashtag và phong cách phù hợp với brand.
- **Tạo hoặc chỉnh sửa hình ảnh** đẹp mắt, chuyên nghiệp, phù hợp với nội dung bài viết.
- **Đăng bài tự động** lên Fanpage chỉ với một cú nhấp chuột.

**Kết quả?** Bạn sẽ **tiết kiệm 80% thời gian** so với cách làm thủ công, đồng thời **nâng cao chất lượng nội dung** với hình ảnh và văn bản AI sinh.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm thời gian** lên đến 80% cho việc tạo nội dung Facebook.
✅ **Hình ảnh chuyên nghiệp** được AI chỉnh sửa hoặc tạo mới từ đầu, phù hợp với phong cách brand.
✅ **Bài viết tự động** với emoji, hashtag và cấu trúc thu hút người đọc.
✅ **Hoạt động 24/7** – Không cần can thiệp thủ công sau khi cấu hình.
✅ **Cá nhân hóa** – Đáp ứng được nhiều phong cách viết và yêu cầu hình ảnh khác nhau.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Cloud** (để sử dụng **Google Gemini API**):
   - API Key của **Google Palm API** (đăng ký tại [Google AI Studio](https://makersuite.google.com/)).
   - Credential trong n8n với tên: **`googlePalmApi`**.

2. **Tài khoản Facebook Business Manager**:
   - **Page Access Token** của Fanpage cần đăng bài (có quyền `publish_pages`).
   - Credential trong n8n với tên: **`facebookGraphApi`**.

3. **Dữ liệu đầu vào** (có thể từ:
   - **Manual Trigger** (nhấn nút thủ công).
   - **Webhook** (từ Google Sheets, Notion, hoặc ứng dụng khác).
   - **Schedule Trigger** (đăng bài định kỳ).

4. **Máy chủ n8n ổn định** (Self-hosted trên VPS để hoạt động 24/7).
   :::info[Gợi ý hạ tầng cho n8n]
   Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
   :::
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [n8n Workflow](https://n8n.io/workflows/15794).
2. Trong n8n Editor, nhấn **Import** và chọn file JSON.
3. Hoặc copy toàn bộ JSON và dán vào **Import Workflow** trong menu.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **11 node** quan trọng, các sếp cần cấu hình kỹ như sau:

#### **🔹 Node 1: Manual Trigger (Hoặc Webhook/Schedule)**
- **Lưu ý**: Nếu muốn tự động hóa hoàn toàn, thay thế **Manual Trigger** bằng:
  - **Webhook Trigger** (để nhận dữ liệu từ Google Sheets, Notion, hoặc API khác).
  - **Schedule Trigger** (để đăng bài định kỳ).

#### **🔹 Node 2: Set Context (Cấu hình dữ liệu đầu vào)**
- **Cần chỉnh sửa**:
  - `raw_content`: Nội dung thô cần viết bài (ví dụ: "Mở bán sản phẩm mới").
  - `fanpage_name`: Tên Fanpage cần đăng bài.
  - `content_style`: Phong cách viết (ví dụ: "Chuyên nghiệp", "Thân thiện", "Humor").
  - `page_access_token`: Token của Facebook Page (có quyền `publish_pages`).
  - `original_image_url` (nếu có): Link hình ảnh gốc muốn chỉnh sửa (nếu không, AI sẽ tạo mới).

#### **🔹 Node 3: AI Agent (Viết Bài & Tạo Prompt Hình Ảnh)**
- **Không cần chỉnh sửa**, nhưng các sếp có thể **cải thiện prompt** bằng cách:
  - Thêm yêu cầu cụ thể về phong cách bài viết (ví dụ: "Sử dụng nhiều emoji", "Thêm hashtag #MuaSắmViệtNam").
  - Đặt yêu cầu về hình ảnh (ví dụ: "Hình ảnh phải có màu sắc tươi sáng, phù hợp với brand").

#### **🔹 Node 4 & 5: Google Gemini Chat Model (Tạo Bài Viết & Prompt)**
- **Không cần chỉnh sửa**, nhưng các sếp nên kiểm tra:
  - Credential **`googlePalmApi`** đã được kết nối đúng.
  - Output của node này sẽ là:
    - `post_caption`: Nội dung bài viết Facebook hoàn chỉnh.
    - `image_prompt`: Prompt chi tiết cho AI tạo hình ảnh.

#### **🔹 Node 6: JSON Output Parser (Xử lý Output AI)**
- **Không cần chỉnh sửa**, nhưng các sếp nên kiểm tra:
  - Output có chứa `post_caption` và `image_prompt` không.

#### **🔹 Node 7: Select Image Mode (Lựa Chọn Chế Độ Hình Ảnh)**
- **Lưu ý**:
  - Nếu có `original_image_url`, workflow sẽ **chỉnh sửa hình ảnh cũ**.
  - Nếu không có, workflow sẽ **tạo hình ảnh mới**.

#### **🔹 Node 8 & 9: Edit Original Image / Generate New Image**
- **Không cần chỉnh sửa**, nhưng các sếp nên kiểm tra:
  - **Node Edit Original Image**:
    - AI sẽ giữ **cấu trúc và chủ đề** của hình gốc, nhưng **tăng cường màu sắc và phong cách chuyên nghiệp**.
  - **Node Generate New Image**:
    - AI sẽ tạo **hình ảnh hoàn toàn mới**, phù hợp với prompt từ AI Agent.

#### **🔹 Node 10: Post to Facebook (Đăng Bài)**
- **Cần chỉnh sửa**:
  - **Credential**: Đảm bảo đã kết nối `facebookGraphApi` với token đúng.
  - **Output**: Kiểm tra bài viết đã đăng thành công trên Fanpage.

#### **🔹 Node 11: Post Result (Lưu Kết Quả)**
- **Không cần chỉnh sửa**, nhưng các sếp có thể **lưu log** vào Google Sheets hoặc Slack để theo dõi.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và kiểm tra output.
   - Đảm bảo bài viết và hình ảnh được tạo đúng yêu cầu.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển workflow sang **Active**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**CÁCH LÀM TIẾP THEO**]
1. **Kết hợp với Slack/Telegram**:
   - Sau khi đăng bài, gửi thông báo kết quả lên Slack/Telegram bằng node **`httpRequest`** hoặc **`slack`**.

2. **Lưu Log vào Google Sheets**:
   - Sử dụng node **`googleSheets`** để ghi lại lịch sử đăng bài (ngày, nội dung, link bài).

3. **Đăng Bài Định Kỳ**:
   - Thay thế **Manual Trigger** bằng **`scheduleTrigger`** để đăng bài tự động vào giờ cố định.

4. **Chỉnh Sửa Phong Cách AI**:
   - Nếu muốn bài viết hoặc hình ảnh khác biệt, chỉnh sửa **prompt** trong node **`Set Context`** hoặc **`AI Agent`**.

5. **Sử Dụng AI Model Khác**:
   - Nếu muốn thay thế **Google Gemini**, các sếp có thể sử dụng **Mistral AI** hoặc **Claude** (nhưng cần cập nhật node tương ứng).

6. **Tạo Nhiều Bài Viết Từ Một Nội Dung**:
   - Sử dụng **Loop** để tạo nhiều biến thể bài viết và hình ảnh từ cùng một nội dung gốc.
:::

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho những ai muốn **tự động hóa toàn bộ quy trình tạo và đăng bài Facebook** mà không cần viết code. Với **AI Gemini**, bài viết và hình ảnh sẽ **luôn chuyên nghiệp, thu hút và phù hợp với brand**.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với dữ liệu mẫu** trước khi kích hoạt.
3. **Bật Active** và bắt đầu **tiết kiệm thời gian**!

---
**💡 Cảm ơn các sếp đã tham khảo!**
Nếu workflow này giúp ích, hãy **đánh giá** và **chia sẻ** để nhiều người biết đến. Nếu có thắc mắc, hãy để lại comment bên dưới! 🚀

---
**📌 Ghi chú từ tác giả (Nguyễn Thiệu Toàn - Jay Nguyen):**
*"Nếu workflow này mang lại giá trị cho công việc của các sếp, hãy ủng hộ tôi một ly cà phê qua [đây](https://nguyenthieutoan.com/payment/).* 😊
- **Website**: [nguyenthieutoan.com](https://nguyenthieutoan.com)
- **Email**: me@nguyenthieutoan.com
- **GenStaff**: [genstaff.net](https://genstaff.net)
- **Xem thêm workflow của tôi**: [n8n Creators](https://n8n.io/creators/nguyenthieutoan/)"*