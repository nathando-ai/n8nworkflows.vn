---
title: "🎬 Tự Động Hóa Video Review Sách Sci-Fi Với AI (ChatGPT + Nexrender)"
description: "Workflow n8n giúp các sếp tạo hàng loạt video review sách khoa học viễn tưởng chuyên nghiệp bằng ChatGPT và Nexrender, không cần kỹ năng dựng phim."
slug: "tu-dong-hoa-video-review-sach-scifi-ai"
tags: [n8n, automation, no-code, ai-video, nexrender, chatgpt]
keywords: [n8n workflow, tự động hóa video, nexrender, chatgpt, review sách, ai content]
---

# 🎬 Tự Động Hóa Video Review Sách Sci-Fi Với AI (ChatGPT + Nexrender)

Trong kỷ nguyên nội dung số, video ngắn (Shorts/Reels/TikTok) là kênh tiếp cận khách hàng hiệu quả nhất. Tuy nhiên, việc sản xuất video chuyên nghiệp đòi hỏi thời gian, kỹ năng dựng phim và chi phí lớn. Đặc biệt với ngách nội dung như **Review Sách Khoa Học Viễn Tưởng (Sci-Fi)**, việc tìm kiếm hình ảnh minh họa, viết kịch bản và render video thủ công là một gánh nặng khổng lồ.

Workflow này chính là "trợ lý ảo" giúp các sếp giải quyết bài toán đó. Chỉ với một cú click, hệ thống sẽ tự động:
1.  Sử dụng **ChatGPT** để viết kịch bản review cuốn sách hấp dẫn.
2.  Gọi API **Fal.ai** (thường dùng để sinh hình ảnh hoặc xử lý đa phương tiện) để tạo visual phù hợp.
3.  Sử dụng **Nexrender** (nền tảng render video từ After Effects template) để ghép chữ, hình ảnh và âm thanh thành video hoàn chỉnh.

Kết quả: Hàng loạt video review sách chất lượng cao, đồng nhất thương hiệu, được tạo ra trong vài phút mà không cần mở phần mềm dựng phim.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi cần render video (tốn tài nguyên), các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian sản xuất:** Từ ý tưởng đến video thành phẩm chỉ mất vài phút thay vì hàng giờ.
- **Độ chính xác & Đồng nhất:** Kịch bản và visual luôn tuân thủ template thương hiệu, tránh sai sót do con người.
- **Cá nhân hóa hàng loạt:** Dễ dàng tạo video cho 100 cuốn sách khác nhau chỉ bằng cách thay đổi tên sách trong input.
- **Hoạt động liên tục:** Có thể lên lịch chạy tự động mỗi ngày để duy trì tần suất đăng bài đều đặn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1.  **Tài khoản n8n:** Bản Self-hosted hoặc Cloud.
2.  **OpenAI API Key:** Để sử dụng ChatGPT viết kịch bản.
3.  **Fal.ai API Key:** Để sinh hình ảnh minh họa (nếu workflow có bước này).
4.  **Nexrender Account & API Key:**
    -   Tài khoản Nexrender.
    -   Một **After Effects Template** đã được upload lên Nexrender (Template này cần có các layer text, image, audio có thể thay đổi).
    -   API Key từ Nexrender.
5.  **Dữ liệu đầu vào:** Danh sách các cuốn sách Sci-Fi muốn review (tên sách, tác giả, mô tả ngắn).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1.  Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/12270).
2.  Mở n8n Editor, chọn **Import from File** hoặc **Import from URL**.
3.  Sau khi import, các sếp sẽ thấy các node chính: `Manual Trigger`, `Code`, `OpenAI`, `Nexrender`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là các node quan trọng cần cấu hình chi tiết:

*   **Node: Manual Trigger**
    *   Đây là nút khởi động. Các sếp có thể thay thế bằng `Cron` (chạy định kỳ) hoặc `Webhook` (nhận dữ liệu từ Google Sheets/Database) nếu muốn tự động hóa hoàn toàn.

*   **Node: Code (Prepare Data)**
    *   Node này thường dùng để định dạng dữ liệu đầu vào (tên sách, tác giả) thành dạng JSON phù hợp cho các bước sau.
    *   **Lưu ý:** Kiểm tra phần `Code` trong node này để đảm bảo biến `bookTitle`, `author` khớp với dữ liệu các sếp muốn xử lý.

*   **Node: OpenAI (ChatGPT)**
    *   **Credentials:** Chọn hoặc tạo mới credentials OpenAI.
    *   **Model:** Chọn model phù hợp (ví dụ: `gpt-4o` hoặc `gpt-3.5-turbo`).
    *   **System Prompt:** Chỉnh sửa prompt để ChatGPT đóng vai một "Nhà phê bình sách Sci-Fi" chuyên nghiệp. Yêu cầu output phải ngắn gọn, phù hợp cho video ngắn (ví dụ: 3-5 câu review).
    *   **User Prompt:** Đảm bảo prompt tham chiếu đúng biến tên sách từ node trước đó.

*   **Node: Fal.ai (nếu có)**
    *   **Credentials:** Thêm API Key của Fal.ai.
    *   **Model:** Chọn model sinh hình ảnh phù hợp (ví dụ: `flux` hoặc `stable-diffusion`).
    *   **Prompt:** Prompt sinh ảnh nên dựa trên thể loại sách (ví dụ: "futuristic city, neon lights, sci-fi book cover style").

*   **Node: Nexrender**
    *   **Credentials:** Chọn credentials Nexrender.
    *   **Template ID:** Đây là phần quan trọng nhất. Các sếp cần lấy **Template ID** từ tài khoản Nexrender của mình (ID của template After Effects đã upload).
    *   **Elements:** Cấu hình ánh xạ (mapping) dữ liệu từ các node trước vào các layer của template:
        *   `text`: Gắn với output kịch bản từ ChatGPT.
        *   `image`: Gắn với URL hình ảnh từ Fal.ai (nếu có).
        *   `audio`: Gắn với file âm thanh nền (nếu có).
    *   **Output Format:** Chọn định dạng video (MP4, MOV) và độ phân giải (1080x1920 cho Shorts/Reels).

#### 3. Kích hoạt ⚡️
1.  **Test Run:** Nhấn nút **Execute Workflow** với dữ liệu mẫu (ví dụ: sách "Dune" của Frank Herbert).
2.  Kiểm tra output:
    *   Kịch bản từ ChatGPT có hay không?
    *   Hình ảnh (nếu có) có phù hợp không?
    *   Video từ Nexrender có render đúng text và hình ảnh không?
3.  Nếu mọi thứ ổn, bật **Active** để workflow sẵn sàng chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Google Sheets:** Thay vì nhập tay, dùng node `Google Sheets` để đọc danh sách sách từ bảng tính. Mỗi dòng là một cuốn sách, workflow sẽ tự động tạo video cho từng dòng.
- **Gửi kết quả qua Telegram/Slack:** Thêm node `Telegram` hoặc `Slack` để gửi link video thành phẩm ngay khi render xong, tiện cho việc đăng bài lên mạng xã hội.
- **Lưu log vào Database:** Dùng node `Postgres` hoặc `MySQL` để lưu lịch sử các video đã tạo, tránh trùng lặp và theo dõi hiệu quả.
- **A/B Testing:** Tạo 2 phiên bản prompt khác nhau cho ChatGPT để test xem phong cách review nào thu hút người xem hơn.

### 📌 Kết luận
Workflow này là công cụ mạnh mẽ giúp các sếp biến quy trình sản xuất video review sách từ thủ công sang tự động hóa hoàn toàn. Với sự kết hợp của ChatGPT (nội dung), Fal.ai (hình ảnh) và Nexrender (video), các sếp có thể tạo ra lượng lớn nội dung chất lượng cao, tiết kiệm thời gian và chi phí đáng kể. Hãy thử ngay và trải nghiệm sức mạnh của AI trong sản xuất nội dung!