---
title: "🚀 Tự Động Hóa Tạo Bài Blog SEO Từ Tin Tức Google News Với AI Claude, Gemini & RankMath – Không Cần Code"
description: "Workflow tự động hóa 24/7 lấy tin tức Google News, lọc chọn bài viết chất lượng, tạo nội dung blog SEO hoàn chỉnh, sinh ảnh featured bằng AI và đăng tải tự động lên WordPress. Giúp các sếp tiết kiệm 10+ giờ/ngày và tăng traffic từ SEO."
slug: "tieu-dong-hoa-tao-bai-blog-seo-tu-google-news-voi-ai-claude-gemini-rankmath"
tags: [n8n, automation, content-creation, ai-seo, wordpress, google-news, no-code]
keywords: [tự động hóa blog SEO, n8n workflow google news, tạo bài blog tự động, AI Claude Gemini cho SEO, đăng bài WordPress tự động]
---

# 🚀 **Tự Động Hóa Tạo Bài Blog SEO Từ Tin Tức Google News Với AI Claude, Gemini & RankMath**

### **Giải pháp hoàn hảo cho các sếp muốn:**
- **Tiết kiệm 10+ giờ/ngày** viết blog thủ công.
- **Tăng traffic SEO** với nội dung tự động hóa chất lượng cao.
- **Cập nhật liên tục** bài viết mới từ Google News mà không cần can thiệp.
- **Sử dụng AI Claude và Gemini** để tạo nội dung và hình ảnh featured chuyên nghiệp.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** – Workflow chạy tự động mỗi 12 giờ, không cần theo dõi thủ công.
✅ **Nội dung SEO ưu việt** – AI Claude và Gemini phân tích tin tức, tạo bài viết với từ khóa phù hợp và cấu trúc chuyên nghiệp.
✅ **Hình ảnh featured tự động** – Gemini sinh ảnh 16:9 ratio phù hợp với tiêu chuẩn SEO.
✅ **Lưu trữ và theo dõi** – Tất cả bài viết được ghi log vào Google Sheets, giúp quản lý dễ dàng.
✅ **Tích hợp RankMath** – Bài viết được tối ưu SEO ngay từ khi đăng tải.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
- **Tài khoản WordPress** với API Key (để đăng bài tự động).
- **Google Sheets** (để lưu log bài viết đã xử lý).
- **API Key SerpAPI** (để lấy tin tức từ Google News).
- **API Key OpenRouter** (để kết nối với AI Claude).
- **API Key Google Gemini** (để sinh ảnh featured).
- **Thiết lập RankMath** trên WordPress (để tối ưu SEO).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/14576](https://n8n.io/workflows/14576) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/14576) và paste vào **Import Workflow** trong n8n.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **23 node** phức tạp, các sếp cần chú ý cấu hình sau:

#### **🔹 Node "Google_news search" (SerpAPI)**
- **Tham số quan trọng:**
  - `operation: "google_news"` (đã mặc định).
  - **Query:** Thay đổi từ khóa tìm kiếm (ví dụ: `"tin tức công nghệ Việt Nam"`).
  - **Limit:** Đặt số lượng bài viết lấy (ví dụ: `10`).

#### **🔹 Node "OpenRouter Chat Model" (Claude AI)**
- **Tham số cần thiết:**
  - **Model:** `anthropic/claude-sonnet-4.5` (đã mặc định).
  - **Prompt:** Cần chỉnh sửa để phù hợp với chiến lược SEO của bạn (ví dụ:
    ```json
    "prompt": "Tóm tắt bài viết này thành một bài blog SEO với tiêu đề hấp dẫn, từ khóa 'tin tức công nghệ', và cấu trúc 3 phần: Giới thiệu, Nội dung chi tiết, Kết luận. Đảm bảo nội dung độc lập và không sao chép."
    ```

#### **🔹 Node "GoogleGemini" (Sinh ảnh featured)**
- **Tham số cần thiết:**
  - **Prompt:** Đặt cài đặt như:
    ```json
    "prompt": "{{ $json.output.prompt }} image should be 16:9 ratio, professional style, SEO-friendly"
    ```
  - **Kích thước:** Đảm bảo ảnh sinh ra phù hợp với tiêu chuẩn WordPress (1200x675px).

#### **🔹 Node "WordPress" (Đăng bài)**
- **Tham số cần thiết:**
  - **Credentials:** Chọn `wordpressApi` (đã cấu hình trước).
  - **Meta Title/Description:** Nếu muốn tự động hóa, chỉnh node `Add Image, Meta Title, Description to Post` với:
    ```json
    "meta_title": "{{ $json.output.meta_title }}",
    "meta_description": "{{ $json.output.meta_description }}"
    ```

#### **🔹 Node "Google Sheets" (Lưu log)**
- **Tham số cần thiết:**
  - **Sheet Name:** Đặt tên bảng (ví dụ: `Blog_Logs`).
  - **Columns:** Cần thêm cột `Status`, `Date`, `URL` để theo dõi.

---
### **3. Kích hoạt ⚡️**
1. **Test Run:** Chạy thử với dữ liệu mẫu để kiểm tra các node như:
   - `Google_news search` → `Split into Items` → `Slect one worthy article`.
2. **Bật Active:** Sau khi kiểm tra thành công, bật **Active** cho workflow.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC TỐI ƯU NÂNG CAO]
- **Tích hợp Slack/Telegram:** Thêm node `n8n-nodes-base.slack` để thông báo khi bài viết đăng thành công.
- **Lưu log chi tiết:** Sử dụng node `n8n-nodes-base.stickyNote` để ghi chú lỗi hoặc cập nhật.
- **Điều chỉnh lịch chạy:** Thay đổi `Run Every 12 Hours` thành `Run Every 6 Hours` nếu cần cập nhật tin tức thường xuyên hơn.
- **Tối ưu RankMath:** Sử dụng node `httpRequest` để tự động thêm schema markup cho bài viết.
- **Duy trì danh sách từ khóa:** Sử dụng Google Sheets để quản lý danh sách từ khóa SEO và cập nhật cho AI.
:::

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa tạo nội dung blog SEO từ tin tức Google News mà không cần viết một dòng code. Với sự hỗ trợ của **AI Claude, Gemini và RankMath**, bài viết sẽ được tối ưu hóa hoàn toàn, giúp tăng **traffic và thứ hạng SEO** một cách tự động.

👉 **Hãy import ngay và bắt đầu tự động hóa blog của mình!** Nếu gặp vấn đề, các sếp có thể liên hệ với tác giả [Salman Mehboob](https://n8n.io/workflows/14576) để hỗ trợ.

---
:::note[CHÚ Ý CUỐI CÙNG]
- **Để workflow chạy ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::