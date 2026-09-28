---
title: "🚀 Tự động phát hiện nội dung website lỗi thời bằng AI, Google Sheets và Gmail"
description: "Hướng dẫn cài đặt workflow n8n tự động quét sitemap hàng tuần, dùng AI (OpenAI) đánh giá độ tươi mới của bài viết, lưu Google Sheets và gửi báo cáo qua Gmail."
slug: "tu-dong-phat-hien-noi-dung-website-loi-thoi-n8n-openai"
tags: [n8n, automation, no-code, openai, google-sheets, gmail, ai-agent]
keywords: [n8n workflow, tự động hóa n8n, phát hiện nội dung lỗi thời, AI content audit, quản lý SEO website, openai gpt-4o-mini]
---

# 🚀 Tự động phát hiện nội dung website lỗi thời bằng AI, Google Sheets và Gmail

Các sếp làm SEO hay quản trị website chắc chắn hiểu cảm giác "đau đầu" khi website ngày càng phình to, nhưng những bài viết cũ từ nhiều năm trước đã lỗi thời, sai thông tin mà nhân sự không có thời gian kiểm tra thủ công. Việc để nội dung cũ kỹ không chỉ làm giảm trải nghiệm người dùng mà còn kéo tụt thứ hạng SEO trên Google.

Workflow n8n này do chuyên gia **Alejandro Alfonso** xây dựng sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa 100%: định kỳ quét sitemap, lọc ra các trang lâu ngày chưa cập nhật, nhờ AI (OpenAI) chấm điểm độ mới và đưa ra gợi ý sửa đổi, sau đó lưu vào Google Sheets và gửi báo cáo trực quan qua Gmail. Các sếp không cần tốn một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Định kỳ thứ Hai hàng tuần, hệ thống tự động chạy ngầm mà không cần con người nhúng tay.
- **Đánh giá thông minh bằng AI:** OpenAI (GPT-4o-mini) phân tích nội dung thực tế, xếp hạng mức độ tươi mới (`LOW`, `MEDIUM`, `HIGH`, `CRITICAL`) kèm theo gợi ý cải thiện cụ thể.
- **Lưu trữ bài bản:** Tự động ghi nhận toàn bộ dữ liệu kiểm toán (audit) vào Google Sheets để dễ dàng theo dõi tiến độ cập nhật.
- **Báo cáo trực quan:** Gửi email qua Gmail với định dạng HTML đầy màu sắc, giúp các sếp nắm bắt ngay lập tức các trang nào cần ưu tiên xử lý gấp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **OpenAI API Key** (Sử dụng model `gpt-4o-mini`).
- **Google Account** (Để kết nối Google Sheets và Gmail OAuth2).
- **Sitemap URL** của website cần quét (`https://domain.com/sitemap.xml`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã nguồn JSON của workflow (hoặc tải file từ nguồn gốc) và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 14 nodes, các sếp cần chú ý cấu hình kỹ các điểm sau để hệ thống chạy mượt mà:

- **Node `Site Configuration` (Loại: Set):** 
  - Mở node này và cấu hình lại các thông số: `sitemapUrl` (đường dẫn sitemap của sếp), `staleDays` (số ngày tối đa cho phép trước khi bị coi là cũ, mặc định là 180 ngày), và `alertEmail` (email nhận báo cáo).
- **Node `OpenAI Chat Model` (Loại: lmChatOpenAi):** 
  - Chọn model `gpt-4o-mini` và kết nối thông tin `OpenAI API credentials` của các sếp.
- **Node `Save to Content Audit Sheet` (Loại: googleSheets):** 
  - Chuẩn bị một Google Sheet có một Tab tên là **ContentAudit** với các cột: `scan_date`, `page_url`, `last_modified`, `days_since_update`, `ai_review`.
  - Dán URL của Google Sheet vào tham số của node này và kết nối tài khoản Google Sheets OAuth2.
- **Node `Email Content Audit Report` (Loại: gmail):** 
  - Kết nối tài khoản Gmail OAuth2 để hệ thống có quyền gửi email báo cáo về hộp thư của sếp.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để test thử nghiệm với dữ liệu mẫu xem hệ thống chạy có trơn tru hay không.
- Nếu mọi thứ xanh mướt, hãy bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy vào 7 giờ sáng thứ Hai hàng tuần.

### ✍️ Mẹo & gợi ý nâng cao
- **Đổi kênh nhận thông báo:** Thay vì Gmail, các sếp có thể thay thế bằng node Telegram hoặc Slack để team nội dung nhận được cảnh báo ngay lập tức trên nhóm chat công ty.
- **Lọc chuyên mục:** Chỉnh sửa ở phần **Parse Sitemap URLs** (Node Code) để chỉ quét các URL thuộc chuyên mục `/blog/` hoặc `/docs/`, bỏ qua các trang tĩnh như Giới thiệu, Liên hệ.
- **Tùy chỉnh ngưỡng thời gian:** Nếu website ra mắt bài viết liên tục, có thể giảm `staleDays` xuống 90 ngày để siết chặt chất lượng nội dung.

### 📌 Kết luận
Một website có nội dung cũ kỹ, lỗi thời sẽ làm giảm uy tín thương hiệu và lãng phí nguồn lực SEO. Với workflow n8n tự động hóa kết hợp OpenAI này, các sếp vừa tiết kiệm hàng tá giờ rà soát thủ công, vừa luôn giữ cho website của mình luôn mới mẻ trong mắt Google và người dùng. Lên đồ và áp dụng ngay thôi nào các sếp!