---
title: "📱 Gửi SMS Tự Động 100% Miễn Phí Với Textbelt API trên n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n để gửi tin nhắn SMS hàng loạt hoặc cá nhân hóa chỉ với 3 nodes, không cần code, sử dụng Textbelt API."
slug: "gui-sms-tu-dong-textbelt-n8n"
tags: [n8n, automation, no-code, sms, textbelt, marketing]
keywords: [n8n workflow, gửi sms tự động, textbelt api, tự động hóa tin nhắn, n8n tutorial]
---

# 📱 Gửi SMS Tự Động 100% Miễn Phí Với Textbelt API trên n8n

Trong kỷ nguyên số, việc liên lạc với khách hàng hoặc đối tác qua SMS vẫn là một kênh truyền thông cực kỳ hiệu quả, đặc biệt cho các thông báo quan trọng như xác thực (OTP), nhắc lịch hẹn, hay khuyến mãi. Tuy nhiên, việc nhập tay từng tin nhắn vào điện thoại hoặc sử dụng các phần mềm gửi tin nhắn thủ công không chỉ tốn thời gian mà còn dễ gây sai sót.

Workflow **"Simple SMS Messaging System with Textbelt API Integration"** chính là giải pháp tối giản nhưng mạnh mẽ, giúp các sếp tự động hóa quy trình gửi SMS chỉ với 3 nodes cơ bản trong n8n. Không cần viết một dòng code nào, các sếp có thể tích hợp Textbelt API để gửi tin nhắn tức thì, chính xác và có thể mở rộng quy mô bất kỳ lúc nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Gửi hàng trăm tin nhắn chỉ với một cú click, thay vì phải thao tác thủ công.
- **Độ chính xác cao:** Loại bỏ hoàn toàn lỗi đánh máy số điện thoại hay nội dung tin nhắn.
- **Chi phí tối ưu:** Textbelt cung cấp gói miễn phí (Free Tier) cho phép gửi một số lượng tin nhắn nhất định mỗi tháng, phù hợp cho test hoặc quy mô nhỏ.
- **Dễ dàng mở rộng:** Cấu trúc workflow đơn giản giúp các sếp dễ dàng thêm các bước xử lý dữ liệu phức tạp hơn (như đọc từ Excel, lọc dữ liệu) sau này.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Đã cài đặt và chạy n8n (Local hoặc Cloud).
2. **Tài khoản Textbelt:** Đăng ký tại [textbelt.com](https://textbelt.com/) để lấy API Key.
   - *Lưu ý:* Gói miễn phí của Textbelt thường giới hạn số lượng tin nhắn gửi đi mỗi tháng (ví dụ: 50 tin/tháng). Các sếp cần kiểm tra hạn mức này.
3. **Số điện thoại đích:** Số điện thoại của người nhận tin nhắn (cần ở định dạng quốc tế, ví dụ: `+84912345678`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow này vào n8n của mình theo 2 cách:
- **Cách 1 (Khuyến nghị):** Tải file JSON của workflow từ link gốc [n8n.io/workflows/6228](https://n8n.io/workflows/6228) và chọn **Import from File** trong n8n Editor.
- **Cách 2:** Copy toàn bộ code JSON của workflow và dán vào n8n Editor bằng cách chọn **Import from Clipboard**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này rất gọn gàng với 3 nodes chính. Các sếp cần cấu hình cụ thể như sau:

**1. Node: `Set Data` (n8n-nodes-base.set)**
Đây là node quan trọng nhất, nơi các sếp định nghĩa nội dung tin nhắn.
- **Phone:** Điền số điện thoại người nhận.
  - *Lưu ý quan trọng:* Textbelt yêu cầu định dạng số điện thoại chuẩn quốc tế. Ví dụ: `+84912345678` (cho Việt Nam), `+12025550123` (cho Mỹ).
- **Message:** Nội dung tin nhắn muốn gửi.
  - *Mẹo:* Các sếp có thể sử dụng biến (variables) nếu muốn cá nhân hóa, ví dụ: `Xin chào {{ $json.name }}, mã OTP của bạn là...`
- **Key:** API Key của Textbelt.
  - Các sếp cần vào trang cá nhân Textbelt, tìm mục **API Key** và dán vào đây.
  - *Bảo mật:* Để an toàn hơn, các sếp nên tạo một **Credential** mới trong n8n (loại "Header Auth" hoặc "Basic Auth" tùy cấu hình API, nhưng với Textbelt thường là tham số body) và tham chiếu vào node này thay vì hardcode trực tiếp. Tuy nhiên, với workflow mẫu này, việc điền trực tiếp vào node Set là cách nhanh nhất để test.

**2. Node: `HTTP Request` (n8n-nodes-base.httpRequest)**
Node này chịu trách nhiệm gọi API của Textbelt.
- **Method:** POST
- **URL:** `https://textbelt.com/text` (Đảm bảo URL đúng, workflow mẫu có thể viết tắt hoặc cần kiểm tra lại chính xác là `/text`).
- **Body:** Các sếp cần đảm bảo rằng body của request chứa đúng 3 trường: `phone`, `message`, và `key` (hoặc `api_key` tùy tài liệu Textbelt, thường là `key`).
  - Trong workflow mẫu, node này thường được cấu hình để lấy dữ liệu từ node `Set Data` phía trước. Các sếp chỉ cần kiểm tra xem các trường trong Body có khớp với tên trường trong node `Set Data` không.

**3. Node: `When clicking ‘Execute workflow’` (n8n-nodes-base.manualTrigger)**
- Đây là nút khởi động. Các sếp chỉ cần click vào nút **Execute Workflow** trên thanh công cụ của n8n để chạy thử.

#### 3. Kích hoạt ⚡️
1. **Test Run:** Click vào nút **Execute Workflow**.
2. Kiểm tra kết quả:
   - Nếu thành công, node `HTTP Request` sẽ trả về một JSON chứa thông báo `success: true` và ID của tin nhắn.
   - Kiểm tra điện thoại đích xem đã nhận được tin nhắn chưa.
3. **Bật Active:** Nếu test thành công, các sếp có thể bật nút **Active** ở góc trên bên phải.
   - *Lưu ý:* Với trigger `Manual`, workflow chỉ chạy khi các sếp click. Nếu muốn tự động hóa hoàn toàn (ví dụ: gửi khi có dữ liệu mới từ Google Sheets), các sếp cần thay thế node `Manual Trigger` bằng node trigger phù hợp (Webhook, Schedule, hoặc Google Sheets Trigger).

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi hàng loạt từ Excel/Google Sheets:** Thay vì dùng `Set Data` để nhập tay, các sếp có thể thêm node **Google Sheets** hoặc **Excel** để đọc danh sách số điện thoại và nội dung tin nhắn. Sau đó, dùng node **Split Out** hoặc **Loop Over Items** để gửi từng tin một.
- **Cá nhân hóa nội dung:** Sử dụng các trường dữ liệu từ nguồn (ví dụ: Tên khách hàng, Mã đơn hàng) để chèn vào nội dung tin nhắn, tạo trải nghiệm chuyên nghiệp hơn.
- **Ghi log lịch sử:** Thêm node **Google Sheets** hoặc **Database** sau node `HTTP Request` để lưu lại lịch sử gửi tin (thời gian, số điện thoại, nội dung, trạng thái thành công/thất bại).
- **Tích hợp với CRM:** Kết nối với HubSpot, Salesforce hoặc Zoho để tự động gửi SMS khi có sự kiện xảy ra trong CRM (ví dụ: khi một lead mới được tạo).

### 📌 Kết luận
Workflow **Simple SMS Messaging System with Textbelt API** là một công cụ cực kỳ hữu ích cho các sếp cần gửi tin nhắn nhanh chóng và tự động hóa quy trình liên lạc. Với chỉ 3 nodes, các sếp có thể triển khai ngay lập tức mà không cần kiến thức lập trình sâu. Hãy bắt đầu bằng việc test với một số điện thoại của chính mình, sau đó mở rộng quy mô bằng cách tích hợp với các nguồn dữ liệu khác. Chúc các sếp thành công!