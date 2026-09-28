---
title: "🚀 Tự động giám sát bài viết LinkedIn và tạo bản tóm tắt nội dung bằng OpenAI & Airtable"
description: "Hướng dẫn xây dựng workflow n8n tự động quét bài viết LinkedIn của cộng đồng, tóm tắt thông minh bằng AI và lưu trữ vào Airtable."
slug: "tu-dong-giam-sat-linkedin-va-tom-tat-ai-airtable"
tags: [n8n, automation, openai, airtable, linkedin, ai-content]
keywords: [n8n workflow, tự động hóa linkedin, tóm tắt bài viết ai, openai n8n, quản lý nội dung airtable]
---

# 🚀 Tự động giám sát bài viết LinkedIn và tạo bản tóm tắt nội dung bằng OpenAI & Airtable

Các sếp làm cộng đồng (Community Manager), sáng tạo nội dung hay quản lý mạng xã hội chắc chắn hiểu cảm giác mệt mỏi thế nào khi phải thủ công lướt từng profile LinkedIn mỗi ngày để xem các thành viên đang thảo luận gì, đăng bài gì. Việc này vừa tốn thời gian, dễ bỏ sót thông tin quan trọng lại cực kỳ nhàm chán.

Hiểu được nỗi đau đó, workflow n8n tuyệt vời được thiết kế bởi **Anna Bui** sẽ giúp các sếp tự động hóa 100% quy trình này: Tự động quét bài đăng, nhờ OpenAI (GPT-4o-mini) phân tích/tóm tắt và lưu trữ ngăn nắp vào Airtable mà không tốn một giọt mồ hôi thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Deploy VPS tốc độ cao chỉ từ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần thủ công kiểm tra hàng chục/hàng trăm profile LinkedIn mỗi ngày.
- **Tóm tắt thông minh bằng AI:** Nhận ngay các bản tóm tắt súc tích, dễ quét nội dung (scan) nhờ OpenAI LangChain tích hợp sẵn.
- **Chống trùng lặp thông minh:** Hệ thống tự động kiểm tra bài viết đã tồn tại trong database trước khi lưu mới.
- **Hoạt động tự động 24/7:** Chạy ngầm theo lịch trình định sẵn (Schedule Trigger) với cơ chế chống Rate Limit an toàn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Airtable Account:** Tạo sẵn Base gồm 2 bảng (Table 1: Quản lý danh sách Profile LinkedIn; Table 2: Lưu trữ bài viết và bản tóm tắt).
- **LinkedIn API Access:** Sử dụng Professional Network Data API từ RapidAPI.
- **OpenAI API Key:** Dùng cho các node phân tích và tóm tắt nội dung.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ nguồn gốc hoặc file mẫu, sau đó vào giao diện n8n Editor chọn **Add workflow** -> **Import from File / Paste JSON** để đưa toàn bộ 23 nodes lên màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm các cụm chức năng chính cần cấu hình cẩn thận:

- **Schedule Trigger:** Node khởi chạy lịch trình. Các sếp có thể chỉnh thời gian chạy mỗi ngày 1 lần hoặc tùy chỉnh theo nhu cầu.
- **Get Daily LinkedIn Post (HTTP Request):** Node gọi API lấy bài đăng. Cần điền đúng Endpoint của RapidAPI LinkedIn và gắn Header chứa API Key của các sếp.
- **Lookup CB Community & Daily Check & Lookup Post & Create Digestion (Airtable):** 
  - Các node này yêu cầu kết nối `airtableTokenApi`.
  - Các sếp cần trỏ đúng **Base** và **Table** tương ứng trong tài khoản Airtable của mình cho từng node.
- **OpenAI Chat Model & LinkedIn Digestion (LangChain nodes):**
  - Node **OpenAI Chat Model** yêu cầu kết nối `openAiApi` (dùng model `gpt-4o-mini` tối ưu chi phí và tốc độ).
  - Kiểm tra lại Prompt bên trong chuỗi LangChain để đảm bảo văn phong tóm tắt tiếng Việt hoặc tiếng Anh theo ý muốn.
- **Random Delay & Wait:** Các node này có sẵn để chống việc gọi API quá nhanh gây lỗi Rate Limit từ LinkedIn. Các sếp giữ nguyên hoặc điều chỉnh thời gian chờ cho phù hợp.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử với dữ liệu từ 2-3 profile mẫu trước để kiểm tra dữ liệu trả về ở các node Code và Airtable.
- Sau khi test thành công không báo lỗi, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack ngay sau node `Create Digestion` để bắn thông báo ngay lập tức về nhóm khi có bài viết chất lượng cao từ các KOLs/Community members.
- **Mở rộng lọc từ khóa:** Thêm node `If` hoặc tinh chỉnh logic Code để lọc ra các bài viết chứa từ khóa hot (như *AI, Automation, n8n*...) trước khi gửi cho OpenAI xử lý nhằm tiết kiệm token.
- **Sao lưu log lỗi:** Đặt thêm nhánh xử lý lỗi (Error Trigger) để tự động báo cáo nếu API LinkedIn hoặc OpenAI gặp sự cố gián đoạn.

### 📌 Kết luận
Với workflow Monitor LinkedIn Posts & Create AI Content Digests, việc theo dõi và tổng hợp nội dung từ mạng lưới quan hệ trên LinkedIn chưa bao giờ dễ dàng đến thế. Hãy "lên đồ" ngay hôm nay để tối ưu hóa năng suất làm nội dung và quản lý cộng đồng của các sếp!