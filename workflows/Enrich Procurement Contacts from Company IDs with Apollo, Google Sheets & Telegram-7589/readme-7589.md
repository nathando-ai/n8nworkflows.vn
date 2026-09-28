---
title: "🚀 Tự động hóa tìm kiếm và làm giàu thông tin liên hệ phòng mua hàng với Apollo, Google Sheets và Telegram"
description: "Hướng dẫn chi tiết cách xây dựng hệ thống tự động quét Company ID, khai thác thông tin người liên hệ procurement qua Apollo.io, lưu vào Google Sheets và thông báo qua Telegram."
slug: "tu-dong-hoa-enrich-procurement-contacts-apollo-google-sheets-telegram"
tags: [n8n, automation, no-code, apollo, lead-generation, google-sheets]
keywords: [n8n workflow, apollo.io enrichment, tự động hóa tìm kiếm khách hàng, procurement contacts, n8n google sheets telegram]
---

# 🚀 Tự động hóa tìm kiếm và làm giàu thông tin liên hệ phòng mua hàng (Procurement)

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thủ công tra cứu từng Company ID, mò mẫm tìm kiếm thông tin của các trưởng phòng mua hàng (Procurement Manager), nhân sự phụ trách thu mua trên Apollo.io rồi copy-paste vào Google Sheets? Quá trình này không chỉ ngốn hàng giờ đồng hồ mà còn dễ xảy ra sai sót, bỏ lỡ cơ hội tiếp cận khách hàng tiềm năng.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n tự động hóa 100% do **Khaisa Studio** thiết kế. Hệ thống sẽ tự động quét danh sách công ty, khai thác thông tin liên hệ chất lượng từ Apollo, lưu trữ gọn gàng vào Google Sheets và gửi thông báo trạng thái tức thì qua Telegram.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Quét và làm giàu dữ liệu (Data Enrichment) liên tục mà không cần can thiệp thủ công.
- **Tiết kiệm thời gian cực lớn:** Thay vì tốn hàng ngày để tìm kiếm thông tin, hệ thống xử lý hàng loạt các công ty chỉ trong vài phút.
- **Quản lý dữ liệu tập trung:** Toàn bộ thông tin liên hệ chi tiết của bộ phận mua hàng được đồng bộ thẳng vào Google Sheets.
- **Cảnh báo và theo dõi thời gian thực:** Nhận thông báo kết quả thành công hoặc lỗi qua Telegram ngay lập tức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Apollo.io** kèm API Key để truy xuất dữ liệu công ty và con người.
- **Google Sheets** chứa sẵn file data mẫu (gồm danh sách Company ID).
- **Telegram Bot Token và Chat ID** để nhận tin nhắn thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow trống trên n8n Editor, sau đó copy toàn bộ mã JSON của workflow (hoặc import file JSON tương ứng từ link gốc) và dán trực tiếp vào giao diện.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Get Apollo Company ID & Save Person to Google Sheet & Mark Company as Processed:** 
  Kết nối tài khoản Google Sheets của các sếp. Trỏ đúng đến file Google Sheet và tên Sheet (Tab) chứa danh sách Company ID và nơi lưu kết quả trả về.
- **Run Every X Minutes & Pause Before Next Run:** 
  Cấu hình tần suất chạy tự động (Schedule Trigger) và thời gian chờ (Wait) giữa các lần gọi API để tránh vượt quá giới hạn (Rate Limit) của Apollo.io.
- **Define Search Settings & Build Search Filters:** 
  Thiết lập các bộ lọc tìm kiếm (ví dụ: chức danh "Procurement", "Purchasing Manager", quốc gia, quy mô công ty...) để nhắm đúng đối tượng mục tiêu.
- **Search People in Apollo & Get Person Contact Details:** 
  Cấu hình **HTTP Request** nodes bằng cách điền Apollo API Key vào phần Header để xác thực.
- **Send Alert to Telegram & Notify: Success:** 
  Kết nối Telegram Bot Credentials, điền Chat ID của cá nhân hoặc group làm việc để nhận thông báo trạng thái.
- **Catch Workflow Error & Format Error Message:** 
  Giúp bắt các ngoại lệ không mong muốn, tự động định dạng lỗi và bắn cảnh báo về Telegram qua node **Send Alert to Telegram**.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với một vài dòng dữ liệu mẫu để kiểm tra xem quá trình gọi API Apollo và ghi nhận Google Sheets có hoạt động chính xác không.
- Sau khi test xanh mượt, các sếp bật công tắc **Active** để workflow tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp CRM:** Có thể bổ sung node HubSpot hoặc Salesforce ngay sau bước tìm kiếm contact để đồng bộ lead trực tiếp vào hệ thống Sales.
- **Xử lý trùng lặp (Deduplication):** Thêm một bước kiểm tra email trước khi lưu vào Google Sheets để tránh lưu trùng dữ liệu cũ.
- **Bổ sung AI sàng lọc:** Kết hợp OpenAI/Claude node để đánh giá độ phù hợp của chức danh nhân sự trước khi gọi API chi tiết liên hệ, giúp tối ưu số lượng credit Apollo sử dụng.

### 📌 Kết luận
Workflow "Enrich Procurement Contacts" là trợ thủ đắc lực giúp đội ngũ Sales và Marketing tự động hóa hoàn toàn khâu tìm kiếm data chất lượng cao. Hãy triển khai ngay hôm nay để tối ưu hóa hiệu suất đội ngũ kinh doanh các sếp nhé!