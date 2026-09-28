---
title: "🚀 Tự động tạo Social Ads đa nền tảng (FB, IG, Pinterest) bằng Website Scraping, Gemini & Ideogram AI"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu website, dùng Google Gemini viết content và Ideogram AI vẽ hình ảnh quảng cáo chuẩn kích thước cho Facebook, Instagram và Pinterest."
slug: "tu-dong-tao-social-ads-voi-gemini-va-ideogram"
tags: [n8n, automation, no-code, ai, content-creation, gemini, ideogram]
keywords: [n8n workflow, tạo quảng cáo tự động, google gemini, ideogram ai, website scraping, facebook ads, instagram ads, pinterest ads]
---

# 🚀 Tự động tạo Social Ads đa nền tảng (FB, IG, Pinterest) bằng AI

Các sếp có thấy mệt mỏi mỗi khi cần lên chiến dịch quảng cáo mới? Nào là phải ngồi đọc lại website sản phẩm, chắt lọc nội dung, viết copy cho từng kênh (Facebook, Instagram, Pinterest), rồi lại loay hoay thiết kế hình ảnh với đủ loại kích thước khác nhau từ Feed, Story cho đến Reels hay Pins? Công việc này tốn hàng giờ đồng hồ, thậm chí cả ngày trời cho mỗi sản phẩm.

Đừng lo, workflow n8n đỉnh cao được phát triển bởi **Malik Hashir** này sẽ giải quyết trọn gói bài toán trên chỉ trong một cú click. Hệ thống sẽ tự động đọc nội dung website của các sếp, dùng sức mạnh của **Google Gemini** để phân tích và sáng tạo nội dung, kết hợp cùng **Ideogram AI** để tạo hình ảnh đúng chuẩn kích thước, sau đó trả kết quả thẳng về **Slack** cho các sếp kiểm duyệt!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chỉ cần nhập URL website và chọn loại quảng cáo qua Form, mọi thứ còn lại AI lo.
- **Đa dạng nền tảng & kích thước:** Tự động tối ưu hình ảnh và nội dung cho Facebook (Feed, Story), Instagram (Feed, Story, Reel) và Pinterest (Pin, Story).
- **AI thông minh:** Kết hợp Firecrawl để cào web, Google Gemini viết prompt/nội dung cực bén, và Ideogram AI tạo ảnh cực nghệ.
- **Quy trình duyệt mượt mà:** Gửi trực tiếp hình ảnh và nội dung hoàn thiện về kênh Slack để đội ngũ review ngay lập tức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Firecrawl API Key:** Dùng cho node cào dữ liệu website.
- **Google Gemini API Key (Google AI Studio):** Cho node AI phân tích và tạo prompt.
- **Ideogram API Key:** Dùng để sinh ảnh quảng cáo thông qua HTTP Request.
- **Slack Account & Bot Token:** Để nhận thông báo kết quả (hoặc các sếp có thể đổi sang Telegram/Discord tùy ý).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn hoặc copy trực tiếp mã JSON.
- Trong giao diện n8n Editor, bấm vào menu **Add workflow** -> Chọn **Import from File** hoặc dán trực tiếp JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình chính xác các node cốt lõi sau:

- **📝 Form Trigger:** Nơi bắt đầu quy trình. Các sếp có thể tùy biến các trường nhập liệu trên form (ví dụ: Link website, Mô tả sản phẩm, Tên thương hiệu, Định dạng mong muốn...).
- **Scrape One Page via Firecrawl - user /scrape endpoint:** Cần điền Firecrawl API Key trong phần Credentials để node này có thể truy cập và cào sạch nội dung trang web mục tiêu.
- **Prompt Generation With AI (Google Gemini):** Kết nối với tài khoản Google Gemini của các sếp. Node này chịu trách nhiệm đóng vai Marketer chuyên nghiệp để đọc nội dung web và viết ra các prompt sinh ảnh siêu chi tiết.
- **🎨 Các node HTTP Request (FB Feed, IG Story, Pinterest Pin...):** Đây là các node gọi API tới Ideogram AI để tạo ảnh theo các kích thước chuẩn:
  - FB Feed: `1200x630`
  - FB Story / IG Story / IG Reel / Pinterest Story: `1080x1920`
  - IG Feed: `1080x1080`
  - Pinterest Pin: `1000x1500`
  *Hãy đảm bảo các sếp đã điền đúng Ideogram API Key trong header của các HTTP Request này.*
- **📤 Các node Slack (Send FB Feed, Send IG Story...):** Cấu hình Slack Credentials và chọn Channel (kênh) mà các sếp muốn bot đẩy hình ảnh cùng nội dung quảng cáo về.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng cách điền thông tin vào form giao diện.
- Kiểm tra xem dữ liệu có chảy qua các nhánh `🔀 Route by Dimensions` (Switch node) chính xác không.
- Sau khi test thành công, gạt công tắc sang **Active** để đưa workflow vào trạng thái vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Đổi kênh nhận tin:** Nếu team của các sếp không dùng Slack, hoàn toàn có thể thay thế các node Slack bằng node Telegram Bot để nhận ảnh và content ngay trên điện thoại cực kỳ tiện lợi.
- **Lưu trữ tự động:** Thêm một node Google Sheets hoặc Airtable ngay sau bước AI Prompt để lưu lại lịch sử các chiến dịch quảng cáo đã tạo, phục vụ việc phân tích về sau.
- **Mở rộng nền tảng:** Có thể bổ sung thêm các nhánh Switch cho TikTok Ads hoặc LinkedIn Ads nếu doanh nghiệp có nhu cầu chạy đa kênh rộng hơn.

### 📌 Kết luận
Với workflow tích hợp AI đa phương thức này, việc sản xuất tài nguyên quảng cáo hàng ngày không còn là gánh nặng cho đội ngũ Marketing nữa. Hãy "lên đồ" ngay cho hệ thống n8n của các sếp và tận hưởng sức mạnh tự động hóa!