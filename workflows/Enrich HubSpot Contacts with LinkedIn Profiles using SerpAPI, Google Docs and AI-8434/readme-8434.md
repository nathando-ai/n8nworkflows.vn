---
title: "🚀 Tự động làm giàu thông tin liên hệ HubSpot với LinkedIn Profile dùng AI, SerpAPI và Google Docs"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động tìm kiếm, làm giàu thông tin profile LinkedIn cho contact mới trên HubSpot bằng AI Agent, SerpAPI và Google Docs."
slug: "tu-dong-lam-giau-hubspot-contacts-linkedin-ai-serpapi"
tags: [n8n, automation, hubspot, ai-agent, serpapi, openrouter]
keywords: [n8n workflow, hubspot enrichment, tự động hóa linkedin, ai agent n8n, serpapi google docs]
---

# 🚀 Tự động làm giàu thông tin liên hệ HubSpot với LinkedIn Profile dùng AI, SerpAPI và Google Docs

Các sếp có đang đau đầu vì tốn quá nhiều thời gian thủ công để tra cứu thông tin, tìm kiếm trang LinkedIn của khách hàng mới trên HubSpot để phục vụ cho đội Sales và Marketing không? Việc này vừa chậm chạp, vừa dễ sai sót và làm giảm năng suất của đội ngũ.

Giải pháp ở đây là gì? Hãy để chiếc workflow n8n này "gánh" thay các sếp! Workflow này tích hợp AI Agent thông minh, tự động kích hoạt khi có contact mới trên HubSpot, sử dụng SerpAPI để tìm kiếm web, đọc tài liệu hướng dẫn trực tiếp từ Google Docs để thực hiện quy trình nghiên cứu, làm sạch dữ liệu bằng Code node và tự động cập nhật lại link LinkedIn vào HubSpot hoàn toàn tự động 100% không cần can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Khách hàng mới vừa đổ vào HubSpot là được AI tra cứu và điền link LinkedIn ngay lập tức.
- **Linh hoạt tuyệt đối:** Quy trình và hướng dẫn nghiên cứu của AI nằm gọn trong một Google Doc. Các sếp muốn thay đổi cách AI tìm kiếm chỉ cần sửa Google Doc mà **không cần sửa lại workflow n8n**.
- **Tiết kiệm chi phí tối đa:** Sử dụng SerpAPI kết hợp mô hình qua OpenRouter giúp tối ưu token và chi phí chạy API tìm kiếm.
- **Dữ liệu sạch sẽ:** Node Code tự động loại bỏ các thẻ "think" thừa thãi từ LLM, đảm bảo chỉ lưu dữ liệu chuẩn xác vào HubSpot.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **HubSpot Account:** Có quyền tạo Private App Token hoặc Developer Account (nếu dùng HubSpot Trigger).
- **OpenRouter Account:** Lấy API Key cho OpenRouter Chat Model.
- **SerpAPI Account:** Lấy API Key để AI Agent thực hiện tìm kiếm Google.
- **Google Cloud / Google Service Account:** Để đọc file Google Docs hướng dẫn nghiên cứu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp tải file JSON của workflow từ nguồn cung cấp (hoặc copy toàn bộ JSON).
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào menu 3 chấm ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công, các sếp cần cấu hình các node cốt lõi sau:

- **HubSpot Trigger & HubSpot (Get recently created/updated contacts / Update Hubspot Contact):**
  - Tạo một Private App trên HubSpot, cấp quyền đọc/ghi cho Contacts và copy **Access Token**.
  - Đảm bảo trong HubSpot của các sếp đã tạo trường thông tin liên hệ tùy chỉnh (custom property) tên là `linkedinUrl` (kiểu dữ liệu Text).
  - Chọn credential `hubspotAppToken` cho các node tương ứng.
- **Read Google Docs:**
  - Copy mẫu tài liệu hướng dẫn tại [Sample configuration doc file](https://docs.google.com/document/d/1nn69H3wdwXJolDwu0avlFw7sIwnX_Hpr3bmOD6PgdW4/edit?usp=sharing) về tài khoản Google Drive của sếp.
  - Chia sẻ (Share) file Google Doc này cho email của Google Service Account (quyền Viewer là đủ).
  - Dán URL của Google Doc vào tham số cấu hình của node `Read Google Docs`.
- **OpenRouter Chat Model:**
  - Tạo kết nối credential `openRouterApi` bằng cách nhập API Key từ OpenRouter của các sếp.
- **SerpAPI:**
  - Nhập SerpAPI Key vào credential của node `SerpAPI`.
- **AI Agent & Code - Remove Think part:**
  - Kiểm tra prompt trong AI Agent để đảm bảo nó lấy đúng các trường dữ liệu từ node `Edit Fields` (First Name, Last Name, Email) truyền vào.

#### 3. Kích hoạt ⚡️
- Bấm nút **‘Execute workflow’** hoặc dùng `Manual Trigger` kết hợp data mẫu để test thử một vài contact.
- Kiểm tra kết quả trả về ở node HubSpot Update xem link LinkedIn đã được cập nhật chính xác chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node Slack hoặc Telegram sau bước cập nhật HubSpot thành công để đội ngũ Sales nhận được thông báo ngay khi có lead mới được làm giàu thông tin.
- **Lưu log lỗi:** Thêm nhánh Error Trigger để gửi email hoặc tin nhắn cảnh báo nếu AI không tìm thấy profile LinkedIn hoặc gặp lỗi API.
- **Mở rộng trường dữ liệu:** Không chỉ dừng lại ở link LinkedIn, các sếp có thể sửa Google Doc hướng dẫn AI tìm thêm chức vụ, tên công ty, quy mô công ty để lưu thêm vào các custom property khác trên HubSpot.

### 📌 Kết luận
Việc tự động hóa quy trình làm giàu thông tin khách hàng từ HubSpot chưa bao giờ dễ dàng và linh hoạt đến thế nhờ sự kết hợp giữa n8n, AI Agent và Google Docs. Hãy triển khai ngay hôm nay để giải phóng thời gian cho đội ngũ và tăng tốc tỷ lệ chốt sales của doanh nghiệp các sếp nhé!