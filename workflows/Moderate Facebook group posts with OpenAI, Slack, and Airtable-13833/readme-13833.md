---
title: "🚀 Kiểm duyệt tự động bài đăng nhóm Facebook bằng OpenAI, Slack và Airtable"
description: "Tự động kiểm duyệt, phân loại nội dung bài đăng trên nhóm Facebook bằng AI OpenAI, thông báo qua Slack và lưu trữ dữ liệu vào Airtable một cách chuyên nghiệp."
slug: "kiem-duyet-tu-dong-bai-dang-facebook-openai-slack-airtable"
tags: [n8n, automation, no-code, facebook, openai, slack, airtable]
keywords: [n8n workflow, tự động hóa facebook, kiểm duyệt bài viết openai, slack notification, airtable automation]
---

# 🚀 Kiểm duyệt tự động bài đăng nhóm Facebook bằng OpenAI, Slack và Airtable

Quản lý một cộng đồng hoặc nhóm Facebook lớn luôn là cơn ác mộng đối với các quản trị viên (Admin). Việc phải đọc từng bài đăng, lọc bỏ các nội dung spam, ngôn từ độc hại (toxic) hay nội dung vi phạm quy tắc nhóm chiếm rất nhiều thời gian và dễ bỏ sót. 

Giải pháp gì cho các sếp? Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n tự động hóa 100% quy trình kiểm duyệt bài đăng nhóm Facebook. Sử dụng sức mạnh AI từ **OpenAI** để phân tích nội dung, gửi cảnh báo tức thì qua **Slack** khi có bài viết vi phạm, đồng thời lưu trữ toàn bộ lịch sử kiểm duyệt vào **Airtable** để dễ dàng quản lý.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** AI thay thế con người đọc và phân tích nội dung bài đăng ngay khi được gửi lên nhóm.
- **Bảo vệ cộng đồng 24/7:** Phát hiện và cảnh báo sớm các nội dung spam, xúc phạm hoặc vi phạm quy tắc nhóm.
- **Đồng bộ dữ liệu mượt mà:** Mọi bài đăng và kết quả kiểm duyệt đều được lưu trữ có hệ thống trên Airtable.
- **Cảnh báo thông minh:** Admin nhận thông báo chi tiết kèm ngữ cảnh ngay trên kênh Slack của đội ngũ.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản OpenAI:** API Key có hạn mức sử dụng để gọi mô hình GPT.
- **Tài khoản Slack:** Bot Token hoặc Webhook để gửi tin nhắn thông báo.
- **Tài khoản Airtable:** Base và Table đã được thiết lập sẵn các cột để lưu trữ thông tin bài viết.
- **Facebook App / Webhook:** Nguồn cấp dữ liệu bài đăng từ nhóm Facebook (thông qua Webhook hoặc Meta Graph API).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn hoặc copy đoạn mã JSON của workflow.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow vận hành trơn tru, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Webhook Node (`n8n-nodes-base.webhook`):** 
  - Đóng vai trò là điểm tiếp nhận dữ liệu bài đăng mới từ nhóm Facebook. Các sếp cần cấu hình URL Webhook này vào ứng dụng Facebook (Facebook App) của mình.
- **OpenAI Node (`@n8n/n8n-nodes-langchain.openAi`):** 
  - Kết nối thông tin API Key của OpenAI.
  - Cấu hình Prompt phù hợp để yêu cầu AI đọc nội dung bài viết, phân loại (Hợp lệ / Vi phạm) và đưa ra lý do ngắn gọn.
- **If Node (`n8n-nodes-base.if`):** 
  - Dùng để tách luồng dựa trên kết quả trả về từ OpenAI (Nếu bài viết an toàn -> Chuyển sang luồng lưu trữ; Nếu bài viết vi phạm -> Chuyển sang luồng cảnh báo).
- **Slack Node (`n8n-nodes-base.slack`):** 
  - Thiết lập Credential xác thực với workspace Slack.
  - Chọn kênh (Channel) nhận thông báo và soạn nội dung cảnh báo kèm theo link bài viết gốc.
- **Airtable Node (`n8n-nodes-base.airtable`):** 
  - Kết nối tài khoản Airtable.
  - Chọn Base và Table tương ứng, sau đó map các trường dữ liệu (Tiêu đề, Nội dung, Tác giả, Kết quả kiểm duyệt từ AI) vào các cột trong bảng.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng một vài dữ liệu bài đăng mẫu (cả bài sạch và bài vi phạm) để kiểm tra luồng chạy của các node `Code`, `Set`, `Merge`, `SplitOut`, `SplitInBatches`.
- Sau khi kiểm tra mọi thứ hoạt động chính xác, bật công tắc **Active** để workflow tự động hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Zalo:** Ngoài Slack, các sếp có thể nhân bản node thông báo để gửi tin nhắn về nhóm Telegram riêng của đội ngũ quản trị viên.
- **Tự động hóa hành động:** Mở rộng workflow bằng cách gọi Facebook API để tự động ẩn hoặc xóa bài viết nếu OpenAI đánh giá mức độ vi phạm ở mức độ nghiêm trọng (Critical).
- **Lưu log định kỳ:** Sử dụng thêm Google Sheets hoặc một bảng Airtable phụ để tổng hợp báo cáo số lượng bài đăng vi phạm mỗi tuần/tháng gửi cho quản lý.

### 📌 Kết luận
Việc kiểm duyệt nội dung cộng đồng thủ công nay đã trở nên lỗi thời và tốn kém nhân lực. Với workflow n8n kết hợp OpenAI, Slack và Airtable này, các sếp hoàn toàn có thể tự động hóa toàn bộ quy trình, giúp nhóm Facebook luôn sạch sẽ, chuyên nghiệp và tiết kiệm tối đa thời gian quản lý. Chúc các sếp "lên đồ" thành công!