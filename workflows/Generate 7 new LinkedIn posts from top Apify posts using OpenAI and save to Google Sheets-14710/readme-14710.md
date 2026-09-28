---
title: "🚀 Tự động tạo 7 bài đăng LinkedIn triệu view từ đối thủ bằng Apify & OpenAI"
description: "Hướng dẫn xây dựng Content Engine tự động cào bài viết tốt nhất trên LinkedIn của đối thủ qua Apify, phân tích bằng OpenAI và lưu kết quả vào Google Sheets."
slug: "tu-dong-tao-bai-dang-linkedin-tu-apify-openai-google-sheets"
tags: [n8n, automation, no-code, openai, apify, google-sheets, content-creation]
keywords: [n8n workflow, tự động hóa linkedin, apify scraper, openai content generator, google sheets automation]
---

# 🚀 Tự động tạo 7 bài đăng LinkedIn triệu view từ đối thủ bằng Apify & OpenAI

Các sếp có đang cạn kiệt ý tưởng viết nội dung trên LinkedIn? Việc phải ngồi hàng giờ lướt feed, phân tích bài nào nhiều tương tác của đối thủ, rồi vắt óc biên soạn lại bài mới thực sự là nỗi ám ảnh tốn thời gian. 

Thay vì làm thủ công, workflow n8n cực đỉnh từ chuyên gia Jonas Frewert sẽ giúp các sếp tự động hóa 100% quy trình: **Cào các bài đăng tốt nhất của đối thủ qua Apify ➔ Phân tích mẫu số chung bằng OpenAI ➔ Tự động sản xuất ra 7 bài đăng mới hoàn toàn chất lượng và lưu thẳng vào Google Sheets.** Không cần một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bắt trend chớp nhoáng:** Tự động phân tích các bài post có lượng tương tác/impression khủng nhất từ bất kỳ profile LinkedIn nào.
- **Sản xuất nội dung hàng loạt:** Biến 1 nguồn cảm hứng thành 7 ý tưởng/bài viết hoàn chỉnh với đầy đủ Hook, Cta, Format Type.
- **Lưu trữ khoa học:** Tự động đẩy toàn bộ dữ liệu phân tích và bài viết mới vào Google Sheets để lên lịch đăng bài dễ dàng.
- **Tiết kiệm 90% thời gian:** Giải phóng đội ngũ Marketing khỏi công việc nghiên cứu và viết content lặp đi lặp lại.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Apify:** Cần có API Token và LinkedIn Scraper Actor ID.
- **Tài khoản OpenAI:** Cần có API Key để sử dụng mô hình AI phân tích và viết bài.
- **Google Sheets:** Chuẩn bị sẵn một Google Sheet với các cột yêu cầu (xem chi tiết ở phần cấu hình bên dưới).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy toàn bộ mã nguồn JSON từ n8n, sau đó dán trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 9 nodes được chia thành các khu vực rõ ràng. Các sếp cần chú ý cấu hình các điểm sau:

- **Node `Set Config`:** 
  - Điền Apify Token, LinkedIn Actor ID, và OpenAI API Key vào phần cấu hình của node này.
  - Thay đổi URL profile LinkedIn mẫu thành profile mục tiêu mà các sếp muốn phân tích.
- **Node `Apify Get LinkedIn Posts` & `Validate Config + Build Actor Input`:** 
  - Đảm bảo kết nối tài khoản Apify hoạt động mượt mà để cào dữ liệu bài viết.
- **Node `OpenAI Analyze + Generate`:** 
  - Chọn Credentials OpenAI của các sếp và kiểm tra đoạn prompt phân tích (nếu muốn tùy chỉnh giọng văn thương hiệu).
- **Node `Append Rows to Google Sheet`:** 
  - Kết nối tài khoản Google Sheets thông qua OAuth2.
  - Trỏ đến file Google Sheet và Worksheet cụ thể.
  - **Lưu ý cực kỳ quan trọng:** Trước khi chạy, bảng Google Sheets của các sếp **bắt buộc phải có sẵn các cột tiêu đề sau** (đúng chính tả):
    - `Generated At`
    - `Source Profile`
    - `Top Post Rank`
    - `Top Post Text`
    - `Top Post Impressions`
    - `Insight 1`, `Insight 2`, `Insight 3`, `Insight 4`
    - `New Post Title`, `New Post Hook`, `New Post Text`, `New Post Cta`
    - `Format Type`, `Why It Should Work`
    - `Total Posts Analyzed`, `Top Post Reactions`, `Top Post Comments`, `Top Post Reposts`, `New Post Number`

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** chạy thủ công lần đầu để kiểm tra dữ liệu trả về và đảm bảo các dòng được append chính xác vào Google Sheets.
- Sau khi test thành công, bật công tắc **Active** để hệ thống sẵn sàng hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa định kỳ:** Thay thế node `Manual Trigger` bằng `Schedule Trigger` để workflow tự động cào và tạo content mới vào mỗi thứ Hai hàng tuần.
- **Thông báo qua Slack/Telegram:** Thêm node gửi tin nhắn ngay sau node `Append Rows to Google Sheet` để báo cáo cho team nội dung mỗi khi có 7 bài viết mới xuất hiện trên Google Sheets.
- **Đa dạng hóa nguồn:** Mở rộng danh sách profile đối thủ bằng cách lưu các URL vào một Google Sheet khác và dùng vòng lặp (Loop) để quét lần lượt.

### 📌 Kết luận
Với workflow n8n kết hợp Apify và OpenAI này, các sếp đang sở hữu trong tay một cỗ máy AI chiến lược nội dung tự động thực thụ. Hãy thiết lập ngay hôm nay để tối ưu hóa hiệu suất làm content trên LinkedIn và vượt mặt mọi đối thủ cạnh tranh!