---
title: "🚀 Tự động thêm dữ liệu vào Notion database qua WhatsApp với URL công khai"
description: "Hướng dẫn xây dựng workflow n8n tự động trích xuất thông tin từ URL công khai gửi qua WhatsApp và lưu trực tiếp vào Notion database một cách nhanh chóng."
slug: "tu-dong-them-du-lieu-notion-tu-whatsapp"
tags: [n8n, automation, no-code, notion, whatsapp, serpapi]
keywords: [n8n workflow, notion database, whatsapp automation, trích xuất dữ liệu url, serpapi]
---

# 🚀 Tự động thêm dữ liệu vào Notion database qua WhatsApp với URL công khai

Trong công việc hằng ngày, việc bắt gặp các bài viết, tài liệu hay trang web hữu ích và muốn lưu lại vào Notion để nghiên cứu sau là nhu cầu rất thường xuyên. Tuy nhiên, thao tác thủ công mở Notion, tạo trang mới, copy và paste link tốn khá nhiều thời gian. 

Giải pháp là gì? Bài viết này sẽ hướng dẫn các sếp cách tự động hóa toàn bộ quy trình: chỉ cần gửi một đường link bất kỳ qua **WhatsApp**, workflow n8n sẽ tự động xử lý, cào dữ liệu liên quan và lưu thẳng vào **Notion Database** mà không cần đụng đến một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tối đa**: Gom mọi thông tin từ web vào Notion chỉ bằng một tin nhắn WhatsApp trên điện thoại.
- **Tự động hóa thông minh**: Kết hợp HTTP Request, SerpApi và Code node để làm sạch và bóc tách dữ liệu chuẩn xác.
- **Hoạt động 24/7**: Lắng nghe tin nhắn và xử lý ngầm liên tục mà không bỏ sót bất kỳ tài liệu nào.
- **Tổ chức khoa học**: Xây dựng kho lưu trữ tri thức cá nhân hoặc đội ngũ trên Notion cực kỳ ngăn nắp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Self-hosted hoặc n8n Cloud).
- **Meta (WhatsApp) Business Account**: Để cấu hình Webhook nhận tin nhắn (`whatsAppTrigger`).
- **Tài khoản Notion & Integration Token**: Đã cấp quyền truy cập vào Database cần lưu dữ liệu (`notion`).
- **SerpApi Account**: Dùng để hỗ trợ tìm kiếm và bổ sung metadata cho URL (tùy chọn theo cấu hình).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ n8n template (Link gốc: [Insert Notion database fields from a public URL via WhatsApp](https://n8n.io/workflows/13638)).
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc copy toàn bộ JSON và paste trực tiếp vào màn hình workflow).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình các node chủ chốt sau:

- **WhatsApp Trigger (`whatsAppTrigger`)**: 
  - Kết nối với tài khoản Meta WhatsApp Business API của các sếp.
  - Cấu hình Webhook URL để nhận sự kiện tin nhắn đến (`messages`).
- **HTTP Request & SerpApi (`httpRequest`, `serpApi`)**:
  - Kiểm tra lại các endpoint gọi API để lấy nội dung từ URL công khai mà người dùng gửi qua WhatsApp.
  - Cung cấp API Key cho SerpApi nếu workflow sử dụng để trích xuất thông tin tìm kiếm bổ sung.
- **Code Node (`code`)**:
  - Dùng để xử lý chuỗi, lọc URL và định dạng lại dữ liệu thô trước khi đẩy vào Notion. Các sếp có thể tinh chỉnh đoạn code JavaScript bên trong nếu muốn thay đổi cách bóc tách tiêu đề hoặc mô tả trang web.
- **Notion Node (`notion`)**:
  - Chọn **Credential** kết nối với tài khoản Notion.
  - Chọn thao tác **Create Database Page**.
  - Map (ánh xạ) các trường dữ liệu từ kết quả xử lý của Code node vào đúng các cột (Properties) tương ứng trong Notion Database của các sếp (Ví dụ: Tiêu đề, URL, Ngày tạo, Thẻ phân loại...).

#### 3. Kích hoạt ⚡️
- Gửi thử một tin nhắn chứa đường dẫn URL bất kỳ tới số WhatsApp bot của các sếp.
- Kiểm tra phần **Execution History** trong n8n để xem dữ liệu chạy qua từng node có bị lỗi hay không.
- Nếu mọi thứ xanh mướt (Success), hãy bật nút **Active** ở góc trên bên phải để workflow chính thức đi vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo ngược lại qua WhatsApp**: Thêm một node WhatsApp ở cuối workflow để gửi tin nhắn phản hồi như *"Đã lưu thành công bài viết vào Notion cho sếp!"*.
- **Tích hợp AI (OpenAI / Anthropic)**: Chèn thêm một LLM node trước khi đẩy vào Notion để tự động tóm tắt nội dung trang web thành 3 ý chính, giúp kho Notion phong phú hơn.
- **Lưu log lỗi**: Thiết lập nhánh Error Trigger để gửi cảnh báo về Telegram hoặc Slack nếu URL không hợp lệ hoặc lỗi kết nối Notion.

### 📌 Kết luận
Với workflow tự động hóa kết nối WhatsApp và Notion này, việc sưu tầm tài liệu trên không gian mạng chưa bao giờ tiện lợi đến thế. Hãy cài đặt ngay để tối ưu hóa năng suất cá nhân và quản lý tri thức hiệu quả hơn các sếp nhé!