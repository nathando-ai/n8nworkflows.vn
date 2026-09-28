---
title: "🚀 Tự động hóa viết Blog đa tầng WordPress với PerplexityAI và OpenAI trên n8n"
description: "Xây dựng hệ thống content automation toàn diện kết hợp PerplexityAI nghiên cứu chiều sâu, OpenAI viết bài đa chương, tạo hình ảnh minh họa và tự động đăng lên WordPress."
slug: "tu-dong-hoa-viet-blog-wordpress-perplexity-openai"
tags: [n8n, automation, wordpress, openai, perplexity, ai-content]
keywords: [n8n workflow, tự động hóa wordpress, viết blog ai, perplexity ai, openai content generator, content automation]
keywords: [n8n workflow, tự động hóa wordpress, viết blog ai, perplexity ai, openai content generator]
---

# 🚀 Tự động hóa viết Blog đa tầng WordPress với PerplexityAI và OpenAI

Viết blog chất lượng cao để làm SEO chưa bao giờ là công việc nhàn hạ. Các sếp thường phải mất hàng giờ để nghiên cứu từ khóa, tổng hợp tài liệu từ nhiều nguồn, cấu trúc bài viết thành nhiều chương (chapters/subchapters), viết nội dung chi tiết, tạo hình ảnh minh họa và cuối cùng là định dạng, đăng lên WordPress. 

Nếu làm thủ công cho 10 bài blog mỗi tháng, đội ngũ của các sếp sẽ ngốn rất nhiều thời gian và chi phí. 

Giải pháp ư? Workflow n8n siêu cấp "khủng" với 115 nodes này sẽ thay thế toàn bộ quy trình trên. Nó tự động hóa từ việc lên ý tưởng qua Google Sheets/Form, sử dụng **PerplexityAI** để nghiên cứu chuyên sâu, kết hợp **OpenAI** để lập kế hoạch, viết bài đa tầng, tự động tạo ảnh minh họa, đồng bộ Google Docs và publish trực tiếp lên website **WordPress** kèm theo thẻ Tags, Categories chuyên nghiệp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow "khủng" với 115 nodes này chạy mượt mà, ổn định 24/7 mà không sợ timeout, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Biến một quy trình viết bài mất 5-7 tiếng thành một cú click chuột hoặc lịch chạy tự động.
- **Nội dung chiều sâu (Deep Research):** Tận dụng PerplexityAI để quét thông tin thực tế, kết hợp OpenAI để phân rã bài viết thành các chương/tiểu mục cực kỳ chi tiết.
- **Tự động hóa toàn diện Media & SEO:** Tự sinh ảnh minh họa (Featured Image & Chapter Images), tạo Google Docs lưu trữ, tự động gom internal links từ sitemap và đẩy thẳng lên WordPress chuẩn SEO.
- **Vận hành linh hoạt:** Hỗ trợ kích hoạt qua Form submission, Google Sheets, Schedule Trigger hoặc Manual Test.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng bản Self-hosted trên VPS).
- **Tài khoản & API Keys:**
  - **OpenAI API Key** (Dành cho các node AI Agent, Chain LLM, tạo nội dung và hình ảnh).
  - **PerplexityAI API Key** (Dành cho node HTTP Request gọi API nghiên cứu dữ liệu).
  - **WordPress Credentials** (Application Password để n8n có quyền đăng bài, tạo category/tag).
  - **Google Sheets / Google Drive / Google Docs Credentials** (Để quản lý danh sách chủ đề và lưu bản thảo).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ nguồn cấp.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng menu (3 chấm) ở góc trên bên phải -> Chọn **Import from File** và tải file JSON lên.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Vì đây là một workflow phức tạp (115 nodes), các sếp cần chú ý cấu hình kỹ các nhóm node sau:

- **Nhóm Trigger (`Schedule Trigger`, `On form submission`, `When clicking ‘Test workflow’`):** 
  - Chọn cách kích hoạt bài viết phù hợp với quy trình doanh nghiệp (Chạy tự động theo lịch, điền form yêu cầu, hoặc test thủ công).
- **Nhóm Google Sheets (`Google Sheets Create Topics`, `Google Sheets Final Blog`, ...):** 
  - Kết nối tài khoản Google của các sếp, trỏ tới file Google Sheet quản lý nội dung blog để workflow biết lấy chủ đề từ đâu và ghi nhận trạng thái bài viết sau khi hoàn tất.
- **Nhóm AI & Research (`Initial Research`, `Blog Planner`, `Chapter Research`, `PerplexityAI API`):** 
  - Kiểm tra lại các node OpenAI (`OpenAI Chat Model`,...) và điền OpenAI API Key hợp lệ.
  - Cấu hình node `PerplexityAI API` đảm bảo endpoint và API Key của Perplexity được điền chính xác để lấy dữ liệu nghiên cứu thời gian thực.
- **Nhóm WordPress (`Post On Wordpress`, `HTTP Request Get Categories`, `HTTP Request Create Tag`):** 
  - Đảm bảo kết nối tài khoản WordPress bằng **Application Password** (không dùng mật khẩu đăng nhập thông thường). 
  - Kiểm tra lại cấu trúc URL trang WordPress của các sếp.
- **Nhóm Google Drive & Docs (`Create Doc`, `Upload Featured Image To Drive`,...):** 
  - Cấu hình thư mục lưu trữ trên Google Drive để workflow tự động tạo folder và lưu hình ảnh, tài liệu bản thảo cho từng bài viết.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với dữ liệu mẫu (Test run) để kiểm tra từng chặng chạy có bị lỗi xác thực hay thiếu trường dữ liệu nào không.
- Sau khi test thành công, gạt công tắc sang chế độ **Active** để hệ thống tự động vận hành 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống tối ưu hơn nữa, các sếp có thể mở rộng workflow này với các ý tưởng:
1. **Tích hợp Slack/Telegram Notification:** Thêm node gửi thông báo về kênh chat nội bộ ngay khi bài viết được lên lịch hoặc publish thành công lên WordPress.
2. **Kiểm duyệt con người (Human-in-the-loop):** Thay vì publish thẳng lên WordPress, cấu hình dừng ở Google Docs hoặc gửi bản nháp qua email để sếp duyệt trước khi bấm nút xuất bản.
3. **Auto Social Share:** Kết hợp thêm các node đẩy link bài viết mới lên Facebook Page, LinkedIn hoặc Twitter tự động ngay sau khi WordPress trả về thông tin bài đăng thành công.

---

### 📌 Kết luận
Workflow **Multi-Level WordPress Blog Generator** của tác giả Daniel Ng là một "vũ khí tối thượng" cho các đội ngũ Content Marketing và SEO Agency muốn scale-up số lượng bài viết chất lượng cao mà không tốn nhiều nhân lực. Hãy cài đặt ngay lên VPS của các sếp và tận hưởng sức mạnh tự động hóa thời đại AI!