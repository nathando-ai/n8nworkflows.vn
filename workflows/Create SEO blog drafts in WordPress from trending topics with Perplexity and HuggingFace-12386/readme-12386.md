---
title: "🚀 Tự Động Hóa Viết Bài Blog SEO Từ Chủ Đề Nóng Trên WordPress Với Perplexity & HuggingFace"
description: "Workflow tự động hóa hoàn toàn không cần code giúp các sếp Marketing và SEO tự động tạo nháp bài blog từ chủ đề trending, tối ưu SEO, và tự động sinh ảnh bìa bằng AI. Tiết kiệm thời gian lên đến 80% cho quá trình content creation."
slug: "tieu-dong-hoa-viet-bai-blog-seo-tu-chu-de-nong-tren-wordpress"
tags: [n8n, automation, seo, content-marketing, ai-generate, wordpress, perplexity, huggingface]
keywords: [n8n workflow seo, tự động hóa viết bài blog, content marketing tự động, ai tạo bài blog, wordpress automation, perplexity ai, huggingface flux]
---

# 🚀 **Tự Động Hóa Viết Bài Blog SEO Từ Chủ Đề Nóng Trên WordPress Với Perplexity & HuggingFace**

### **Giải pháp cho các sếp Marketing & SEO:**
Bạn đã bao giờ phải mất **giờ đồng hồ** để tìm kiếm chủ đề trending, viết bài blog, tối ưu SEO, và thiết kế ảnh bìa? Hay phải **đợi đợi** các nhà thiết kế tạo hình ảnh cho bài viết? **Workflow này sẽ tự động hóa toàn bộ quá trình chỉ với một cú nhấp chuột!**

Với **Perplexity AI** (tìm kiếm chủ đề hot), **HuggingFace FLUX** (sinh ảnh AI), và **Google Sheets** (quản lý chủ đề), workflow này sẽ:
✅ **Tự động phát hiện** chủ đề trending trong 24-48 giờ qua.
✅ **Tạo nháp bài blog** hoàn chỉnh với tiêu đề, nội dung, từ khóa, và mô tả meta (SEO-optimized).
✅ **Sinh ảnh bìa** từ AI và tự động gắn vào bài viết.
✅ **Tạo draft trên WordPress** sẵn sàng cho việc review và xuất bản.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao, phù hợp với AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ **80% công việc viết bài thủ công** sang tự động hóa.
- **Nội dung SEO tối ưu**: Perplexity tự động sinh tiêu đề, nội dung, từ khóa và mô tả meta.
- **Ảnh bìa chuyên nghiệp**: HuggingFace FLUX tạo hình ảnh AI chất lượng cao chỉ trong vài giây.
- **Quản lý chủ đề hiệu quả**: Google Sheets lưu trữ và theo dõi chủ đề đã xử lý.
- **Hoạt động liên tục**: Workflow chạy tự động mỗi khi có chủ đề mới (không cần can thiệp thủ công).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản & API Keys**:
- **Perplexity AI** (đăng ký tại [perplexity.ai](https://www.perplexity.ai/))
- **Google Sheets** (tạo một bảng mới với cấu trúc cụ thể)
- **WordPress** (trang blog cần tự động hóa)
- **HuggingFace** (API token cho FLUX, đăng ký tại [huggingface.co](https://huggingface.co/))

✔ **Google Sheet cấu trúc**:
| Column Name       | Type    | Mô tả                                  |
|-------------------|---------|----------------------------------------|
| `Topic`           | Text    | Chủ đề trending được chọn             |
| `is_generated`    | Boolean | Dấu hiệu đã sinh nội dung chưa        |
| `title`           | Text    | Tiêu đề bài blog (sẽ được sinh tự động) |
| `content`         | Text    | Nội dung bài blog                     |
| `keywords`        | Text    | Từ khóa SEO                            |
| `meta_description`| Text    | Mô tả meta cho SEO                     |

✔ **WordPress**:
- **Trang blog** cần quyền chỉnh sửa (nhớ lấy `authorId` từ trang cá nhân).
- **URL WordPress** (điền vào node `Create a post`).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow:
- **Tải file JSON** từ [n8n.io/workflows/12386](https://n8n.io/workflows/12386) và import vào **n8n Editor**.
- **Copy/paste JSON** từ file vào **Create Workflow** trong n8n.

:::note[Lưu ý]
- **Không sao chép toàn bộ JSON** từ trang n8n.io (do có phần metadata không cần thiết).
- **Chỉ copy phần `nodes` và `connections`** trong file JSON.
:::

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp **phải cấu hình** các node sau:

##### **A. Cấu hình Perplexity AI**
- **Node**: `Find top trending topics` và `Generate content and image prompt using Perplexity AI`
  - **API Key**: Điền vào `Perplexity API Key` (tìm trong tài khoản Perplexity).
  - **Model**: Để mặc định (`sonar-pro`).
  - **Prompt**: Các sếp có thể **tùy chỉnh** prompt để phù hợp với phong cách viết của mình (ví dụ: yêu cầu thêm từ khóa cụ thể).

##### **B. Cấu hình Google Sheets**
- **Node**: `Add topic to Google Sheets` và `Get most recent topics from Google Sheet`
  - **Google Sheets Credential**: Chọn credential đã tạo (nếu chưa có, tạo tại `Credentials` trong n8n).
  - **Sheet ID**: Thay thế `YOUR_GOOGLE_SHEET_ID` bằng **ID của Google Sheet** (tìm trong URL của sheet: `https://docs.google.com/spreadsheets/d/[ID]/edit`).
  - **Sheet Name**: Điền tên sheet (ví dụ: `SEO_Content_Tracker`).

##### **C. Cấu hình WordPress**
- **Node**: `Create a post`
  - **WordPress Credential**: Chọn credential đã tạo (nếu chưa có, tạo tại `Credentials` trong n8n).
  - **Site URL**: Thay thế `your-site.com` bằng **URL của trang WordPress**.
  - **Author ID**: Điền **ID của tác giả** (tìm trong `Users` của WordPress).
  - **Status**: Đặt thành `draft` (để bài viết chưa xuất bản).

##### **D. Cấu hình HuggingFace FLUX**
- **Node**: `Generate featured image using HuggingFace FLUX`
  - **API Token**: Thay thế `YOUR_TOKEN_HERE` bằng **API token** từ HuggingFace.
  - **Endpoint**: Để mặc định (`https://api-inference.huggingface.co/models/runwayml/stable-diffusion-v1-5`).
  - **Prompt**: Workflow sẽ tự động sinh **prompt từ nội dung bài viết** (không cần chỉnh sửa).

##### **E. Cấu hình Code Nodes**
- **Node**: `Parse Content from string to JSON` và `Select a clean trending topic`
  - **Không cần chỉnh sửa** (n8n tự động xử lý JSON).
- **Node**: `Update name and extension of image`
  - **Không cần chỉnh sửa** (n8n tự động đổi tên file ảnh).

##### **F. Cấu hình HTTP Request Nodes**
- **Node**: `Upload image to WP media Library` và `Assign image to an article as a Featured image`
  - **URL**: Điền vào `https://your-site.com/wp-json/wp/v2/media` (thay `your-site.com` bằng URL WordPress).
  - **Headers**:
    - `Authorization`: `Bearer YOUR_WORDPRESS_TOKEN` (tạo token tại `Settings > General > API` trong WordPress).
    - `Content-Type`: `multipart/form-data`.

---

#### **3. Kích hoạt ⚡️**
Sau khi cấu hình xong:
1. **Test Run** với dữ liệu mẫu:
   - Nhấn `Execute Workflow` và kiểm tra từng node có hoạt động không.
   - Kiểm tra **Google Sheet** có thêm chủ đề mới không.
   - Kiểm tra **WordPress** có tạo draft bài viết không.
2. **Bật Active**:
   - Đặt `Active` thành `true` để workflow chạy tự động khi có chủ đề mới.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CẬP NHẬT & TỰ ĐỘNG HÓA HƠN]
1. **Kết hợp với Slack/Telegram**:
   - Thêm node `Slack` hoặc `Telegram Bot` để thông báo khi có bài viết mới được tạo.
   - Ví dụ: `When a new draft is created → Send notification to Slack`.

2. **Lưu log hoạt động**:
   - Thêm node `Sticky Note` để ghi lại lịch sử chủ đề đã xử lý (giúp theo dõi và tránh trùng lặp).

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node `Google Sheets` để **tính toán thống kê** số lượng bài viết sinh ra trong tháng.
   - Kết hợp với node `Email` để gửi báo cáo tự động cho team.

4. **Tùy chỉnh prompt Perplexity**:
   - Nếu muốn **phân tích sâu hơn**, cập nhật prompt để yêu cầu Perplexity sinh:
     - **Câu hỏi thường gặp (FAQ)**.
     - **Danh sách từ khóa cạnh tranh**.
     - **Gợi ý liên kết nội bộ (internal links)**.

5. **Sử dụng AI khác cho nội dung**:
   - Thay vì Perplexity, các sếp có thể thử **LLM khác** như Mistral, Grok, hoặc Gemini để sinh nội dung.
   - Cập nhật node `Generate content and image prompt` với API mới.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp Marketing & SEO để tập trung vào **strategy** thay vì công việc thủ công. Với **Perplexity AI** tìm chủ đề, **HuggingFace FLUX** sinh ảnh, và **WordPress automation**, các sếp sẽ:
✔ **Tiết kiệm 80% thời gian viết bài**.
✔ **Nội dung SEO tối ưu** từ đầu đến cuối.
✔ **Ảnh bìa chuyên nghiệp** chỉ trong vài giây.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**Hãy thử ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Bật Active** và để nó làm việc cho bạn.
3. **Xem kết quả** trong Google Sheet và WordPress.

**Nếu cần hỗ trợ thêm**, các sếp có thể liên hệ với tác giả **Nayankumar Thakor** qua [link tư vấn custom](https://nayankumar-thakor.notion.site/Book-a-consultation-for-custom-n8n-work-6f4d3e5d3b4a4b4c4d4e4f5a) để tối ưu workflow phù hợp với nhu cầu cụ thể!

---
**🚀 Chúc các sếp thành công với chiến dịch content marketing tự động hóa!**