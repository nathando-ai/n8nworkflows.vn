---
title: "🚀 Tự động tạo caption Instagram chuẩn xu hướng từ Hashtag bằng Apify và GPT-4o-mini"
description: "Hướng dẫn xây dựng workflow n8n tự động quét hashtag Instagram qua Apify, phân tích nội dung bài viết bằng AI GPT-4o-mini và trả về danh sách ý tưởng caption chuyên nghiệp."
slug: "tao-caption-instagram-tu-dong-apify-gpt-4o-mini-n8n"
tags: [n8n, automation, instagram, apify, openai, ai-agent]
keywords: [n8n workflow, tự động hóa instagram, apify instagram scraper, gpt-4o-mini, tạo caption ai]
---

# 🚀 Tự động tạo caption Instagram chuẩn xu hướng từ Hashtag bằng Apify và GPT-4o-mini

Các sếp làm sáng tạo nội dung hoặc quản lý mạng xã hội chắc chắn đã từng đau đầu mỗi khi phải ngồi "soi" hàng loạt bài viết trên Instagram để tìm ý tưởng viết caption, bắt trend hay phân tích đối thủ. Việc này vừa tốn thời gian, vừa dễ gây cạn kiệt ý tưởng sáng tạo.

Giải pháp là gì? Workflow n8n này sẽ tự động hóa 100% quy trình: Quét các bài viết mới nhất theo hashtag bất kỳ thông qua **Apify**, gom nhóm dữ liệu, phân tích bằng **AI Agent (GPT-4o-mini)** và trả về các ý tưởng caption chuẩn cấu trúc, giúp các sếp "sản xuất" content đều đặn mỗi ngày mà không tốn một giọt mồ hôi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần thủ công tìm kiếm và đọc từng bài post trên Instagram nữa.
- **Bắt trend cực nhanh:** AI tự động phân tích các nội dung phổ biến nhất dựa trên hashtag thực tế.
- **Cấu trúc rõ ràng:** Kết quả trả về dưới dạng JSON có cấu trúc (Post Idea & Most Common Post) dễ dàng tích hợp vào các hệ thống khác như Google Sheets hoặc Notion.
- **Tùy biến linh hoạt:** Dễ dàng thay đổi từ khóa hashtag bất kỳ chỉ bằng một cú click.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
1. **Tài khoản n8n** (Cloud hoặc Self-hosted).
2. **Tài khoản Apify**: Lấy API Token để kết nối với Actor quét Instagram Hashtag.
3. **OpenAI API Key**: Để sử dụng mô hình GPT-4o-mini phân tích nội dung.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor của mình, hoặc import file JSON tải từ thư viện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 12 nodes được thiết kế mạch lạc. Các sếp cần chú ý cấu hình các điểm sau:

- **Node `Create Search Term` (Set):** 
  - Đây là nơi định nghĩa từ khóa hashtag các sếp muốn quét. Mặc định là `n8n`, hãy sửa lại thành hashtag mục tiêu của sếp (ví dụ: `AI`, `Marketing`, `Automation`...).
  ```json
  {
    "Search_Term": "yourCustomHashtag"
  }
  ```

- **Node `Find Recent Posts` (HTTP Request):**
  - Cần cấu hình Credentials loại **HTTP Query Auth**.
  - Lấy API Token từ Apify Console và truyền vào query string dạng: `?token=yourTokenHere`.
  - Body JSON gửi đi sẽ tự động nhận giá trị hashtag từ node `Create Search Term`.

- **Node `OpenAI Chat Model` & `AI Agent`:**
  - Chọn model `gpt-4o-mini` tiết kiệm chi phí và tốc độ cao.
  - Cấu hình Credentials **OpenAI API Key** của các sếp.
  - Prompt hệ thống trong AI Agent sẽ dựa vào các bài post quét được để sinh ra cấu trúc JSON:
  ```text
  {
    "Post Idea": ["Idea1", "Idea2"],
    "Most Common Post": ["common post 1", "common post 2"]
  }
  ```

- **Node `Structured Output Parser`:** Giúp ép kết quả trả về từ OpenAI đúng định dạng JSON chuẩn để các node phía sau (`Split Out`, `Split Out1`, `Merge`) xử lý mượt mà.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** (thông qua node `When clicking ‘Execute workflow’`) để test thử với dữ liệu mẫu.
- Sau khi kiểm tra luồng dữ liệu chạy trơn tru, các sếp có thể đổi Trigger sang Webhook hoặc Schedule (Cron) nếu muốn chạy định kỳ hàng tuần.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa workflow này cho công việc thực tế, các sếp có thể mở rộng thêm:
1. **Lưu tự động vào Google Sheets / Airtable:** Thêm một node Google Sheets ở cuối để lưu lại các "Post Idea" và "Most Common Post" phục vụ cho việc lên lịch content.
2. **Gửi thông báo qua Telegram/Slack:** Bắn kết quả gợi ý caption trực tiếp vào group chat của team MKT mỗi sáng thứ Hai hàng tuần.
3. **Tích hợp Buffer / Hootsuite:** Tự động hóa khâu lên lịch đăng bài từ các ý tưởng do AI gợi ý.

### 📌 Kết luận
Workflow quét hashtag Instagram và tạo caption bằng AI này là một "vũ khí" lợi hại giúp tối ưu hóa năng suất cho các nhà sáng tạo nội dung và Digital Marketer. Hãy triển khai ngay hôm nay để tiết kiệm hàng giờ làm việc thủ công!