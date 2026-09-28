---
title: "🏠 Tự động hóa quản lý yêu cầu bảo trì bất động sản qua WhatsApp với WATI và Google Sheets"
description: "Hướng dẫn xây dựng hệ thống chatbot tự động tiếp nhận, phân loại và lưu trữ yêu cầu sửa chữa nhà đất từ WhatsApp vào Google Sheets bằng n8n."
slug: "quan-ly-bao-tri-bat-dong-san-whatsapp-wati-google-sheets"
tags: [n8n, automation, no-code, wati, whatsapp, google-sheets, support-chatbot]
keywords: [n8n workflow, tự động hóa whatsapp, wati automation, google sheets bảo trì, chatbot bất động sản]
---

# 🏠 Tự động hóa quản lý yêu cầu bảo trì bất động sản qua WhatsApp với WATI và Google Sheets

Trong ngành quản lý bất động sản, việc khách thuê nhà liên tục gửi các yêu cầu sửa chữa, bảo trì (điện, nước, điều hòa...) qua tin nhắn điện thoại thường khiến đội ngũ vận hành quá tải, dễ bỏ sót thông tin và thiếu dữ liệu theo dõi minh họa. Việc ghi chép thủ công vào Excel hay CRM vừa tốn thời gian vừa thiếu tính đồng bộ.

Giải pháp là gì? Bài viết này sẽ hướng dẫn các sếp cách thiết lập một workflow n8n tự động hoàn toàn: Khách hàng nhắn tin báo hỏng qua **WhatsApp (thông qua WATI)**, hệ thống sẽ tự động phân tích, ghi nhận yêu cầu và lưu trữ trực tiếp vào **Google Sheets** để đội ngũ kỹ thuật xử lý kịp thời mà không cần tốn một phút nhập liệu thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và không lo bị gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Tiếp nhận và ghi nhận mọi yêu cầu bảo trì từ khách thuê qua WhatsApp ngay khi tin nhắn được gửi đến.
- **Dữ liệu tập trung:** Tất cả các ticket (yêu cầu) được lưu trữ gọn gàng, minh bạch trên Google Sheets, giúp dễ dàng phân công công việc và theo dõi tiến độ.
- **Loại bỏ sai sót:** Không còn tình trạng trôi tin nhắn Zalo/WhatsApp hay quên ghi nhận yêu cầu của khách hàng.
- **Hoạt động 24/7:** Hệ thống âm thầm làm việc kể cả ngoài giờ hành chính, mang lại trải nghiệm chuyên nghiệp cho khách thuê.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- Một tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **WATI** (WhatsApp Business API) đã kết nối số điện thoại.
- Một file **Google Sheets** mẫu được thiết kế sẵn các cột thông tin như: *Tên khách thuê, Số điện thoại, Nội dung yêu cầu, Thời gian, Trạng thái xử lý...*
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ kho lưu trữ n8n hoặc sao chép mã JSON nguồn.
- Trong giao diện n8n Editor, nhấn vào dấu **`+`** hoặc chọn **Add workflow** -> **Import from File** / **Paste JSON** để dán đoạn mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru với dữ liệu của doanh nghiệp, các sếp cần cấu hình chính xác các node sau:

- **WATI Trigger (`Wati Trigger`)**: Node này đóng vai trò "tai mắt", lắng nghe mọi tin nhắn đến từ khách hàng trên WhatsApp. Các sếp cần cấu hình Webhook URL từ WATI trỏ về n8n để kích hoạt workflow mỗi khi có tin nhắn mới.
- **Xử lý dữ liệu (`Code`)**: Node Code giúp bóc tách nội dung tin nhắn, số điện thoại người gửi và thời gian từ định dạng của WATI thành dữ liệu sạch để đưa vào các bước tiếp theo.
- **Phân loại yêu cầu (`Switch`)**: Dùng để phân loại nội dung tin nhắn (ví dụ: khẩn cấp, bảo trì thông thường, hỏi thông tin...) để có hướng xử lý hoặc phản hồi phù hợp.
- **Lưu trữ dữ liệu (`Google Sheets`)**: 
  - Chọn tài khoản Google Sheets Credentials đã được cấp quyền.
  - Chọn đúng File Google Sheet (Spreadsheet) và Sheet Name (Tên trang tính) quản lý bảo trì.
  - Map các trường dữ liệu từ tin nhắn WhatsApp (Tên, SĐT, Nội dung yêu cầu) vào đúng các cột tương ứng trong Sheet.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một tin nhắn thử nghiệm qua WhatsApp đến số WATI để kiểm tra xem dữ liệu có được đẩy lên Google Sheets chính xác hay không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để đưa workflow vào vận hành thực tế.

---

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống thông minh và hữu ích hơn nữa, các sếp có thể mở rộng workflow với các ý tưởng sau:
1. **Tích hợp AI/LLM (OpenAI):** Thêm một node AI để tự động phân loại mức độ khẩn cấp của yêu cầu (Khẩn cấp / Bình thường) dựa trên nội dung tin nhắn của khách.
2. **Cảnh báo qua Telegram/Slack:** Tự động bắn một thông báo khẩn vào nhóm chat nội bộ của đội ngũ kỹ thuật ngay khi có khách gửi yêu cầu bảo trì gấp.
3. **Gửi tin nhắn xác nhận tự động:** Sử dụng node WATI để tự động gửi lại một tin nhắn cho khách thuê với nội dung: *"Hệ thống đã ghi nhận yêu cầu của anh/chị. Đội ngũ kỹ thuật sẽ liên hệ lại trong thời gian sớm nhất."*

---

### 📌 Kết luận
Việc tự động hóa quy trình tiếp nhận yêu cầu bảo trì bất động sản không chỉ giúp tiết kiệm hàng chục giờ nhập liệu thủ công mỗi tuần mà còn nâng cao chất lượng dịch vụ chăm sóc khách hàng lên một tầm cao mới. Hãy triển khai ngay workflow này để tối ưu hóa vận hành doanh nghiệp của các sếp ngày hôm nay!