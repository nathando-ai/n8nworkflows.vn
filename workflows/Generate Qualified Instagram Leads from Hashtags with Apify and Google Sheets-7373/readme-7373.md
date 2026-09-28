---
title: "🚀 Tự động quét và lọc khách hàng tiềm năng chất lượng trên Instagram từ Hashtag với Apify và n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy hashtag từ Google Sheets, cào bài viết Instagram qua Apify, lọc ngôn ngữ và kiểm tra follower để tìm khách hàng tiềm năng."
slug: "tu-dong-quet-loc-lead-instagram-apify-google-sheets"
tags: [n8n, automation, instagram, lead-generation, apify, google-sheets]
keywords: [n8n workflow, tự động hóa instagram, quét lead instagram, apify instagram scraper, lọc khách hàng tiềm năng n8n]
---

# 🚀 Tự động quét và lọc khách hàng tiềm năng chất lượng trên Instagram từ Hashtag

Các sếp có đang tốn hàng giờ mỗi ngày để lướt Instagram, tìm kiếm các hashtag liên quan đến ngách kinh doanh của mình, lọc bài viết thủ công và "đột nhập" từng profile xem họ có phải là khách hàng tiềm năng (có lượng follower vừa đủ, đúng ngôn ngữ) hay không? Việc này không chỉ cực kỳ tốn thời gian mà còn rất dễ bỏ sót khách hàng.

Đừng lo, bài toán này sẽ được giải quyết triệt để 100% tự động bằng workflow n8n kết hợp với Apify và Google Sheets. Các sếp chỉ cần ngồi nhâm nhi ly cà phê, hệ thống sẽ tự động làm thay toàn bộ quy trình nặng nhọc đó!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần tìm kiếm và lọc thủ công từng tài khoản Instagram nữa.
- **Lọc thông minh đa tầng:** Tự động loại bỏ các bài rác chỉ có hashtag, chỉ giữ lại bài viết đúng ngôn ngữ (ví dụ: tiếng Anh) và đúng tiệp khách hàng.
- **Target chuẩn xác:** Lọc trực tiếp danh sách người dùng theo khoảng follower mong muốn (tránh tài khoản ảo hoặc siêu Influencer quá đắt đỏ).
- **Đồng bộ hóa dữ liệu:** Toàn bộ danh sách hashtag đầu vào và kết quả lead chất lượng được quản lý mượt mà.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Self-hosted hoặc n8n Cloud).
- **Tài khoản Apify:** Cần có tài khoản và API Token để sử dụng các Actor cào dữ liệu Instagram.
- **Google Sheets:** Chuẩn bị sẵn một file Google Sheet chứa danh sách các hashtag cần cào dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, sau đó dán trực tiếp vào giao diện n8n Editor (hoặc import file JSON qua menu *Add workflow -> Import from File*).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 12 nodes được thiết kế tỉ mỉ, các sếp cần chú ý cấu hình các điểm mấu chốt sau:

- **Node `Get list of Hashtags` (Google Sheets):** 
  - Kết nối tài khoản Google thông qua `googleSheetsOAuth2Api`.
  - Chỉ định đúng file Google Sheet và Sheet Name chứa danh sách hashtag đầu vào của các sếp.
- **Nodes `Scrape instagram hashtag posts` & `Scrape instagram Profiles` (HTTP Request / Apify):**
  - Cần điền Apify API Token vào phần Header Authentication để n8n có thể gọi các Actor cào dữ liệu từ Instagram.
- **Nodes `IF — Hashtags Only`, `IF — English Only` & `If followers are in a certain range continue` (IF Nodes):**
  - Tùy chỉnh logic điều kiện bên trong các node này cho phù hợp với tiêu chí của doanh nghiệp (ví dụ: thay đổi ngôn ngữ cần lọc, định mức số lượng follower tối thiểu và tối đa).
- **Nodes `make hashtag links` & `Format captions, usernames and data` (Code Nodes):**
  - Các đoạn mã JavaScript đã được viết sẵn để chuyển đổi định dạng URL và làm sạch dữ liệu text, các sếp chỉ cần giữ nguyên hoặc tinh chỉnh nếu muốn thay đổi cách bóc tách từ khóa.

#### 3. Kích hoạt ⚡️
- Bấm nút **‘Execute workflow’** ở node `When clicking ‘Execute workflow’` để chạy thử nghiệm và kiểm tra dữ liệu trả về ở từng bước.
- Sau khi kiểm tra dữ liệu đã chuẩn chỉnh, hãy gạt công tắc sang **Active** để workflow sẵn sàng vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack vào cuối chuỗi để nhận thông báo ngay lập tức khi hệ thống quét được một loạt Lead mới tiềm năng trong ngày.
- **Lưu tự động vào CRM:** Thay vì dừng ở việc lọc dữ liệu, các sếp có thể đẩy thẳng danh sách Username chất lượng này vào HubSpot, Notion hoặc một Google Sheet lưu danh sách Lead chuyên biệt để đội Sales tiến hành outreach.
- **Chạy tự động định kỳ:** Thay thế node `Manual Trigger` bằng `Schedule Trigger` để n8n tự động quét hashtag mỗi ngày hoặc mỗi tuần một lần mà không cần can thiệp thủ công.

### 📌 Kết luận
Việc tự động hóa quy trình tìm kiếm khách hàng trên Instagram chưa bao giờ dễ dàng đến thế với sức mạnh của n8n và Apify. Hãy triển khai ngay workflow này để tối ưu hóa phễu bán hàng và vượt mặt đối thủ trong cuộc đua tiếp cận khách hàng trên mạng xã hội nhé các sếp!