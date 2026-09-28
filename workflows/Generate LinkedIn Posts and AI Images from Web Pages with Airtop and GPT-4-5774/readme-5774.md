---
title: "🚀 Tự động tạo bài viết LinkedIn và hình ảnh AI từ bất kỳ trang web nào với Airtop & GPT-4"
description: "Biến mọi trang web thành bài đăng LinkedIn chuyên nghiệp kèm ảnh AI, tích hợp quy trình kiểm duyệt qua Slack một cách hoàn toàn tự động."
slug: "tu-dong-tao-bai-viet-linkedin-va-hinh-anh-ai-tu-trang-web"
tags: [n8n, automation, no-code, airtop, openai, slack, content-creation]
keywords: [n8n workflow, tự động hóa linkedin, airtop web scraping, gpt-4 content generation, tạo bài viết từ url]
---

# 🚀 Tự động tạo bài viết LinkedIn và hình ảnh AI từ trang web với Airtop & GPT-4

Các sếp làm content, marketing hay agency có tốn hàng giờ mỗi ngày chỉ để đọc một bài blog, tóm tắt lại, nghĩ ý tưởng viết bài LinkedIn rồi đi tìm hình ảnh minh họa không? Công việc thủ công này cực kỳ ngốn thời gian và làm giảm năng suất sáng tạo.

Giải pháp đây rồi! Workflow n8n này sẽ tự động hóa **100% quy trình từ URL trang web đến bài đăng LinkedIn hoàn chỉnh kèm hình ảnh AI**, kết hợp luôn cả quy trình kiểm duyệt (Human-in-the-loop) ngay trên Slack cực kỳ mượt mà.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian:** Biến bài viết dài thành bài post LinkedIn chuẩn SEO, hút tương tác chỉ trong vài phút.
- **Hình ảnh độc quyền:** Tự động tạo prompt và hình ảnh AI phù hợp với nội dung bài viết.
- **Kiểm soát tuyệt đối:** Tích hợp Slack `sendAndWait` cho phép đội ngũ duyệt, chỉnh sửa hoặc yêu cầu AI viết lại ngay trong chat.
- **Quy trình khép kín:** Không cần code, dễ dàng mở rộng kết nối trực tiếp lên LinkedIn trong tương lai.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Airtop API Key**: Dùng cho node trích xuất dữ liệu web (`Get Page`).
- **OpenAI API Key**: Cho các mô hình GPT-4 và trợ lý AI viết bài (`OpenAI Chat Model`, `Generate Post Text`, `Image Prompt Generator`).
- **Slack Workspace**: Kết nối Slack OAuth2 để nhận thông báo và tương tác duyệt bài (`Final Version`, `Human Revision of Text`, `Human Review of Visual`).
- **Sub-workflow**: Workflow con chuyên trách việc render ảnh thương hiệu (`Generate on-brand image`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn hoặc copy toàn bộ JSON.
- Trong giao diện n8n Editor, nhấn vào **Add workflow** -> Chọn dấu `...` ở góc trên bên phải -> **Import from File / Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **On form submission / Generate Image (Form Trigger):** 
  - Cấu hình form đầu vào để người dùng nhập **Page URL** (đường dẫn bài viết gốc) và **Instructions** (yêu cầu bổ sung về giọng văn, phong cách).
- **Get Page (Airtop Node):** 
  - Chọn credential `airtopApi`. Node này sẽ đóng vai trò như một AI browser tự động cào dữ liệu nội dung từ trang web được cung cấp, kể cả các trang web phức tạp.
- **OpenAI Chat Model & Generate Post Text:** 
  - Chọn credential `openAiApi`. Đảm bảo model được chọn là `gpt-4.1` (hoặc GPT-4 tương đương) để đảm bảo chất lượng ngôn từ sắc bén, chuẩn văn phong LinkedIn.
- **Human Revision of Text & Human Review of Visual (Slack Nodes):** 
  - Chọn credential `slackOAuth2Api`. 
  - Cấu hình tính năng `sendAndWait` để gửi nội dung và hình ảnh kèm các tùy chọn phản hồi (Phê duyệt, Yêu cầu sửa đổi) tới một channel Slack nội bộ cụ thể.
- **Generate on-brand image (Execute Workflow):** 
  - Trỏ đường dẫn tới sub-workflow chuyên xử lý việc tạo ảnh thương hiệu của doanh nghiệp các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền một URL bất kỳ vào Form.
- Kiểm tra kết quả trả về trên Slack, thử nghiệm tính năng phản hồi/chỉnh sửa.
- Nếu mọi thứ hoạt động hoàn hảo, gạt công tắc sang **Active** để đưa vào vận hành thực tế!

### ✍️ Mẹo & gợi ý nâng cao
- **Đăng bài trực tiếp:** Mở rộng workflow bằng cách gắn thêm node **LinkedIn** ở cuối luồng để khi bấm "Approve" trên Slack, bài viết sẽ tự động xuất bản lên trang cá nhân hoặc Fanpage doanh nghiệp.
- **Lưu trữ dữ liệu:** Thêm node **Google Sheets** hoặc **Airtable** để lưu lại lịch sử các bài post đã tạo, phục vụ việc đo lường hiệu quả content sau này.
- **Đa dạng phong cách:** Tạo thêm các tùy chọn Presets (chuyên gia, kể chuyện, ngắn gọn) ngay tại form đầu vào để AI linh hoạt biến hóa văn phong theo ý muốn.

### 📌 Kết luận
Tự động hóa quy trình sáng tạo nội dung chưa bao giờ dễ dàng đến thế với sự kết hợp của Airtop, GPT-4 và n8n. Hãy áp dụng ngay workflow này để tối ưu hóa năng suất đội ngũ marketing của các sếp ngay hôm nay!