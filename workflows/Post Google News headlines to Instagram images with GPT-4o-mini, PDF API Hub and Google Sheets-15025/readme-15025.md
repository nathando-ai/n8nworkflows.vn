---
title: "🚀 Tự Động Hóa Bài Đăng Tin Tức Google News lên Instagram với AI GPT-4o-mini & Hình Ảnh Branded"
description: "Workflow tự động hóa lấy tin tức từ Google News, viết tiêu đề hấp dẫn bằng AI, tạo hình ảnh branded và đăng lên Instagram hàng giờ một - hoàn toàn không cần code. Giúp các sếp tiết kiệm thời gian và tăng tương tác cho trang Instagram."
slug: "tu-dong-hoa-tin-tuc-google-news-len-instagram"
tags: [n8n, automation, social-media, ai-chatbot, google-sheets, instagram-automation]
keywords: [tự động hóa instagram, n8n workflow google news, ai viết tiêu đề, tạo hình ảnh branded, pdf api hub, gpt-4o-mini]
---

# 🚀 **Tự Động Hóa Tin Tức Google News lên Instagram với AI: Từ Tin Tức → Tiêu Đề Clickbait → Hình Ảnh Branded → Đăng Instagram**

Hiện nay, việc quản lý nội dung cho Instagram của các sếp là một công việc tốn thời gian và dễ bị lặp lại. Thay vì phải thủ công tìm kiếm tin tức, viết tiêu đề hấp dẫn, thiết kế hình ảnh và đăng bài, **workflow này sẽ tự động hóa toàn bộ quy trình trong vòng 1 giờ/lần** - với chất lượng cao và cá nhân hóa theo brand của doanh nghiệp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần**: Không cần tìm kiếm tin tức, viết tiêu đề hoặc thiết kế hình ảnh.
- **Tăng tương tác**: Tiêu đề được viết bằng AI với phong cách clickbait, hình ảnh branded chuyên nghiệp.
- **Tránh lặp tin**: Hệ thống kiểm tra và loại bỏ tin tức đã đăng trước đó.
- **Hoạt động liên tục**: Workflow chạy tự động hàng giờ một, không cần can thiệp.
- **Cá nhân hóa brand**: Hình ảnh và tiêu đề được tối ưu hóa theo phong cách riêng của doanh nghiệp.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Google Sheet** với tab `rss` và các cột sau (đã mô tả chi tiết trong phần hướng dẫn):
   - `guid`, `title`, `pubDate`, `source`, `link`, `topic`, `media_url`, `is_posted`, `created_at`, `updated_at`.
2. **Credentials API**:
   - **Google Sheets OAuth2** (để đọc/giữ dữ liệu tin tức).
   - **OpenAI API Key** (để sử dụng GPT-4o-mini viết tiêu đề).
   - **PDF API Hub API Key** (để tạo hình ảnh từ HTML).
   - **Instagram API Credentials** (để đăng bài tự động).
3. **Mã giảm giá PDF API Hub** (nếu chưa có): [pdfapihub.com](https://pdfapihub.com) (mã giảm giá: **N8N20** - giảm 20%).
4. **N8n Workflow Editor** (cài đặt từ [n8n.io](https://n8n.io/)).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Bước 1**: Tải file JSON của workflow từ [n8n.io/workflows/15025](https://n8n.io/workflows/15025).
- **Bước 2**: Mở **n8n Editor** và chọn **Import Workflow** (icon "Upload").
- **Bước 3**: Chọn file JSON đã tải và nhấn **Import**.

:::note[Lưu ý]
Nếu không muốn tải file, các sếp có thể **copy/paste** JSON từ trang n8n.io vào Editor và nhấn **Create Workflow**.
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Google Sheets**
1. **Tạo Google Sheet mới** với tab `rss` và các cột như mô tả.
2. **Chia sẻ sheet** với n8n bằng cách:
   - Mở Google Sheets → **Chia sẻ** → Thêm email của n8n (n8n@example.com).
   - Chọn quyền **"Sửa"** cho n8n.
3. **Cấu hình node `Fetch Sheet Rows`**:
   - **Google Sheets Credentials**: Chọn OAuth2 đã cấu hình trước.
   - **Sheet Name**: Nhập `rss`.
   - **Range**: Nhập `A1:I` (tất cả cột cần thiết).

#### **B. Cấu hình RSS Feed (Google News)**
1. **Node `Google News RSS`**:
   - **URL**: Sử dụng URL RSS của Google News theo chủ đề (ví dụ: `https://news.google.com/rss/search?q=technology&hl=en-US`).
   - **Topic**: Đặt trong node `Set Topic` (ví dụ: `technology`, `sports`, `business`).

#### **C. Cấu hình AI (GPT-4o-mini)**
1. **Node `Rewrite Headline (AI)`**:
   - **Model**: Chọn `gpt-4o-mini` (đã cấu hình trong node `OpenAI GPT-4o-mini`).
   - **Prompt**: Sử dụng template mặc định (có thể tùy chỉnh trong node `chainLlm`):
     ```
     Rewrite this headline in a catchy, viral-style caption for Instagram.
     Keep it under 150 characters. Make it engaging and click-worthy.
     Original headline: {{$json["title"]}}
     ```
   - **OpenAI API Key**: Điền vào **Credentials** của node `lmChatOpenAi`.

#### **D. Cấu hình PDF API Hub (Tạo Hình Ảnh)**
1. **Node `Generate News Image`**:
   - **API Key**: Điền vào **Credentials** của node `pdfSplitMerge`.
   - **HTML Template**: Sử dụng template mặc định (có thể chỉnh sửa trong node):
     ```html
     <div style="background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%); padding: 20px; color: white; font-family: Arial; text-align: center;">
       <div style="font-size: 12px; margin-bottom: 10px;">🔥 BREAKING NEWS 🔥</div>
       <div style="font-size: 24px; font-weight: bold; margin: 10px 0;">LIVE NOW</div>
       <div style="font-size: 20px; margin: 20px 0;">{{$json["title"]}}</div>
       <div style="font-size: 10px; opacity: 0.8;">Source: {{$json["source"]}}</div>
     </div>
     ```
   - **Chiều rộng/cao**: Đặt thành `375x812` (phù hợp với Instagram).

#### **E. Cấu hình Instagram**
1. **Node `Post to Instagram`**:
   - **Credentials**: Sử dụng OAuth2 của Instagram (cần đăng ký API từ [Meta Developer](https://developers.facebook.com/)).
   - **Caption**: Sử dụng tiêu đề đã viết bởi AI (`{{$json["caption"]}}`).
   - **Image URL**: Sử dụng URL hình ảnh từ node `Generate News Image` (`{{$json["image_url"]}}`).

#### **F. Cấu hình Deduplication (Tránh Lặp Tin)**
1. **Node `Deduplicate Articles`**:
   - **Logic**: Kiểm tra `guid` trong Google Sheet. Nếu `is_posted = TRUE`, bỏ qua tin tức đó.
   - **Mã JavaScript**:
     ```javascript
     const existingRows = $input.all();
     const newArticles = $input.current();

     const postedGuids = existingRows
       .filter(row => row.json.is_posted === true)
       .map(row => row.json.guid);

     const filteredArticles = newArticles.filter(article =>
       !postedGuids.includes(article.json.guid)
     );

     return filteredArticles;
     ```

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chạy workflow với **mode "Test"** để kiểm tra các bước:
     - Tin tức được lấy từ RSS.
     - Tiêu đề được viết bởi AI.
     - Hình ảnh được tạo thành công.
     - Đăng bài lên Instagram (nếu có credentials).
2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển workflow sang **mode "Active"**.
   - Cấu hình **node `Every Hour`** để chạy hàng giờ một (hoặc theo lịch trình mong muốn).

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh Branding**:
   - Chỉnh sửa **HTML template** trong node `Generate News Image` để thêm logo, màu sắc hoặc font chữ riêng của doanh nghiệp.
   - Ví dụ: Thêm logo bằng mã `<img src="https://tên-domain.com/logo.png" style="width: 50px; margin-bottom: 10px;">`.

2. **Lưu Log & Báo Cáo**:
   - Thêm node **Google Sheets** mới để lưu log lỗi hoặc thành công của workflow.
   - Ví dụ: Tạo tab `logs` với cột `timestamp`, `status`, `error` (nếu có).

3. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo khi workflow chạy thành công hoặc lỗi.
   - Ví dụ: Gửi tin nhắn như:
     ```
     🚀 Tin tức mới đã đăng lên Instagram!
     Tiêu đề: {{$json["title"]}}
     Link: {{$json["link"]}}
     ```

4. **Lọc Tin Tức Theo Đặc Trưng**:
   - Sử dụng node **Code** để lọc tin tức theo từ khóa cụ thể (ví dụ: loại bỏ tin tức không liên quan).
   - Ví dụ:
     ```javascript
     const keywords = ["technology", "innovation", "AI"];
     const filteredArticles = $input.current().filter(article =>
       keywords.some(keyword => article.json.title.toLowerCase().includes(keyword))
     );
     return filteredArticles;
     ```

5. **Chỉnh Sửa Lịch Trình**:
   - Thay đổi node `Every Hour` thành `Every 2 Hours` hoặc `Every 3 Hours` để giảm tải cho API.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa hoàn toàn quy trình đăng tin tức lên Instagram, từ lấy tin tức đến viết tiêu đề và tạo hình ảnh branded. Với **AI GPT-4o-mini**, hình ảnh được tạo tự động và tiêu đề hấp dẫn, giúp tăng tương tác cho trang Instagram mà không tốn thời gian.

**Bắt đầu ngay hôm nay!**
1. Chuẩn bị các credentials và Google Sheet.
2. Import workflow và cấu hình theo hướng dẫn.
3. Bật workflow và xem tin tức tự động được đăng lên Instagram hàng giờ một.

👉 **Nếu gặp khó khăn**, các sếp có thể liên hệ cộng đồng n8n trên [Discord](https://n8n.io/community) hoặc comment bên dưới để được hỗ trợ!

---
**#TựĐộngHóaInstagram #N8nAutomation #AIChatbot #GoogleNews #BrandedContent**