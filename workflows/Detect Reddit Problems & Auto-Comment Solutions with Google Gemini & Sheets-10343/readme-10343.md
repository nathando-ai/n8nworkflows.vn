---
title: "🚀 Tự động quét vấn đề trên Reddit và phản hồi bằng Google Gemini & Google Sheets"
description: "Xây dựng hệ thống AI tự động tìm kiếm bài đăng phàn nàn trên Reddit, phân tích vấn đề, tạo giải pháp bằng Google Gemini, lưu vào Google Sheets và tự động bình luận."
slug: "tu-dong-quet-reddit-va-phai-hoi-bang-gemini-va-google-sheets"
tags: [n8n, automation, no-code, reddit, google-gemini, google-sheets, ai-agent]
keywords: [n8n workflow, tự động hóa reddit, google gemini ai, quản lý mạng xã hội, auto comment reddit]
---

# 🚀 Tự động quét vấn đề trên Reddit và phản hồi bằng Google Gemini & Google Sheets

Các sếp có đang tốn hàng giờ mỗi ngày để lướt các cộng đồng như Reddit nhằm tìm kiếm khách hàng tiềm năng, điểm đau (pain points) của người dùng hoặc các chủ đề thảo luận liên quan đến sản phẩm của mình không? Việc làm thủ công này vừa mất thời gian, vừa dễ bỏ sót thông tin quan trọng.

Giải pháp đây rồi! Workflow n8n này sẽ tự động hóa 100% quy trình: Quét bài viết trên Reddit $\rightarrow$ Lọc lọc nhiễu $\rightarrow$ Dùng AI (Google Gemini) phân tích xem đó có phải là vấn đề thực sự hay không $\rightarrow$ Tạo giải pháp chi tiết $\rightarrow$ Lưu kết quả vào Google Sheets để theo dõi và optionally (tùy chọn) tự động bình luận trực tiếp lên bài viết đó.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần thủ công lướt sub-reddit tìm khách hàng hay ý tưởng content nữa.
- **Phân loại thông minh bằng AI:** Google Gemini tự động lọc bỏ các bài viết rác, chỉ giữ lại những bài thực sự có vấn đề/nỗi đau cần giải quyết.
- **Giải pháp tức thì:** AI tự động soạn thảo câu trả lời/giải pháp chi tiết, chuyên nghiệp dựa trên nội dung bài đăng.
- **Lưu trữ & Quản lý dễ dàng:** Mọi dữ liệu và giải pháp đều được đồng bộ tự động vào Google Sheets để đội ngũ dễ dàng kiểm duyệt.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
1. **Tài khoản Reddit & API (OAuth):** Cho các node *Post Searching* và *Create a comment in a post*.
2. **Tài khoản Google & API Key:** 
   - Google Gemini API Key (cho 2 node AI Agent).
   - Google Sheets Credentials (cho node *Append row in sheet*).
3. **Google Sheets Template:** Một bảng tính Google Sheets chuẩn bị sẵn các cột để lưu trữ dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy đoạn mã JSON của workflow từ nguồn cung cấp.
- Vào giao diện n8n Editor, chọn **Add workflow** $\rightarrow$ **Import from File/Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các node cốt lõi sau trước khi cho chạy thật:

- **Post Searching (Reddit):** 
  - Chọn Credentials Reddit của các sếp.
  - Thay đổi Subreddit (mặc định là `r/n8n`) và từ khóa tìm kiếm (mặc định là *“Why i stopped using”*) thành ngách sản phẩm của các sếp.
- **If Condition & If Condition 2:** 
  - Node 1 lọc các bài có `ups >= 2` và `selftext` không trống. Các sếp có thể tăng độ chặt (ví dụ `ups >= 5`) để lấy bài chất lượng hơn.
  - Node 2 kiểm tra kết quả phân loại từ AI (`$json.output` chứa chữ "Yes").
- **AI Agent & AI Agent1 (Google Gemini):**
  - Cấu hình Credentials cho **Google Gemini Chat Model** và **Google Gemini Chat Model1** (sử dụng model `gemini-2.0-flash` cho tốc độ phản hồi nhanh).
  - Tinh chỉnh Prompt của AI Agent phân loại và AI Agent tạo giải pháp sao cho phù hợp với giọng điệu thương hiệu của các sếp.
- **Append row in sheet (Google Sheets):**
  - Chọn Google Sheets Credentials.
  - Trỏ tới Spreadsheet ID và tên Sheet cụ thể của các sếp. Map các trường dữ liệu như Tiêu đề, Nội dung, Giải pháp của AI vào các cột tương ứng.
- **Create a comment in a post (Reddit):**
  - ⚠️ **LƯU Ý QUAN TRỌNG:** Node này mặc định nên để **Disabled** (tắt) trong quá trình test.
  - Khi đã kiểm tra kỹ chất lượng giải pháp của AI và muốn tự động đăng bình luận, các sếp hãy map `postId` với ID bài viết trên Reddit và `commentText` với nội dung giải pháp do AI tạo ra, sau đó mới bật node này lên.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute workflow** (vì workflow dùng *Manual Trigger* ở bản demo) để test thử nghiệm.
- Kiểm tra kết quả trả về ở Google Sheets và log của n8n.
- Nếu mọi thứ hoạt động trơn tru, hãy chuyển sang dùng *Schedule Trigger* (ví dụ chạy 1 lần/ngày) và bật **Active** workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack sau bước tạo giải pháp để nhận thông báo ngay lập tức trên điện thoại mỗi khi có bài viết mới cần chăm sóc.
- **Lưu lịch sử chạy:** Kết hợp thêm các bước kiểm tra trùng lặp (Duplicate Check) qua Google Sheets hoặc cơ sở dữ liệu để tránh việc AI phân tích hoặc bình luận trùng một bài viết nhiều lần.
- **Mở rộng nguồn quét:** Không chỉ giới hạn ở Reddit, các sếp có thể mở rộng sang Twitter (X), Facebook Groups hoặc các diễn đàn ngành khác.

### 📌 Kết luận
Workflow **Detect Reddit Problems & Auto-Comment Solutions** là một trợ lý ảo cực kỳ đắc lực giúp các sếp khai thác triệt để nguồn traffic chất lượng cao từ mạng xã hội, tìm kiếm insight khách hàng và tiếp cận họ một cách tự động, thông minh. Hãy triển khai ngay lên VPS của mình và tối ưu hóa quy trình marketing ngay hôm nay các sếp nhé!