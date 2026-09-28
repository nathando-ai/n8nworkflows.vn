---
title: "🚀 Tự động tạo báo giá xây dựng chuyên nghiệp từ JotForm, Supabase CRM và gửi Email"
description: "Hướng dẫn xây dựng hệ thống tự động hóa n8n: Nhận form JotForm, xử lý dữ liệu chuẩn hóa, tính toán báo giá thông minh qua Supabase CRM và gửi email báo giá chuyên nghiệp."
slug: "tu-dong-tao-bao-gia-xay-dung-jotform-supabase-crm-email"
tags: [n8n, automation, no-code, supabase, crm, jotform, gmail]
keywords: [n8n workflow, tự động hóa báo giá, jotform supabase, crm automation, tạo báo giá tự động]
---

# 🚀 Tự động hóa tạo báo giá xây dựng chuyên nghiệp từ JotForm, Supabase và Email

Các doanh nghiệp xây dựng, thầu thợ hay dịch vụ cải tạo thường mất từ 30 đến 60 phút thủ công cho mỗi lần nhận yêu cầu khảo sát, tính toán khối lượng vật tư, chi phí nhân công, làm file PDF và gửi email báo giá cho khách hàng. Quy trình thủ công này không chỉ chậm trễ, dễ nhầm lẫn mà còn khiến khách hàng nguội lạnh cảm xúc khi phải chờ đợi lâu.

Workflow n8n mạnh mẽ này ra đời như một giải pháp **tự động hóa 100% không cần code**, giúp biến các biểu mẫu yêu cầu từ khách hàng thành các bản báo giá chuyên nghiệp trong tích tắc.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tốc độ chớp nhoáng:** Rút ngắn thời gian từ 30 phút xuống chưa đầy 1 phút cho mỗi báo giá.
- **Loại bỏ sai sót:** Áp dụng bộ quy tắc tính giá (Pricing Rules) cấu hình sẵn trên Database, không lo lệch giá hay sai thuế VAT.
- **Đồng bộ CRM toàn diện:** Tự động lưu trữ thông tin khách hàng, chi tiết deal, lịch sử submit form vào Supabase database.
- **Email chuyên nghiệp:** Gửi email HTML cá nhân hóa cực kỳ đẹp mắt với đầy đủ chi tiết khối lượng, đơn giá, tổng tiền và nút kêu gọi hành động (CTA).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **JotForm** để tạo form nhận yêu cầu từ khách hàng.
- Tài khoản **Supabase** để lưu trữ database (Customer, Deal, Pricing Rules, Estimate).
- Tài khoản **Gmail** (hoặc dịch vụ gửi mail tương đương) để gửi email báo giá tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, vào giao diện n8n Editor, chọn **New Workflow**, nhấn tổ hợp `Ctrl + V` (hoặc `Cmd + V`) để dán trực tiếp lên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 21 nodes được chia thành 4 giai đoạn chính. Các sếp cần cấu hình kỹ các điểm sau:
- **Webhook Node:** Cấu hình đường dẫn URL endpoint để nhận dữ liệu POST từ JotForm mỗi khi có khách hàng gửi form.
- **Supabase Nodes (Save Form Submission, Upsert Customer, Create Deal, Fetch Pricing Rules, Save Estimate Header, Insert Line Items, Fetch Complete Quote, Fetch Mapping Rules):** Kết nối các node này với dự án Supabase của các sếp bằng `supabaseApi` credentials. Đảm bảo cấu hình đúng schema và các bảng dữ liệu theo schema SQL đi kèm.
- **Calculate Quote Line Items & Generate Email HTML (Code Nodes):** Chứa các đoạn mã JavaScript xử lý logic tính toán đơn giá, thuế VAT và dựng template HTML cho email. Có thể tinh chỉnh nội dung text, màu sắc thương hiệu tại đây.
- **Send Email node (Gmail):** Kết nối tài khoản Gmail qua `gmailOAuth2` để hệ thống tự động gửi email báo giá trực tiếp đến khách hàng.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** và gửi thử một bản ghi mẫu từ JotForm để kiểm tra luồng chạy qua từng node.
- Sau khi kiểm tra dữ liệu trả về chính xác ở email và Supabase, hãy gạt công tắc sang **Active** để hệ thống tự động hóa 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo nội bộ:** Thêm node Telegram hoặc Slack sau bước *Create Deal* để đội ngũ sales nhận ngay thông báo khi có khách hàng mới đăng ký báo giá.
- **Tự động tạo lịch hẹn:** Kết hợp thêm Google Calendar API vào workflow để tự động lên lịch khảo sát công trình cho đội ngũ kỹ thuật.
- **Lưu file PDF:** Sử dụng thêm dịch vụ HTML-to-PDF để đính kèm file báo giá PDF chuyên nghiệp vào email gửi khách hàng.

### 📌 Kết luận
Hệ thống tự động hóa tạo báo giá xây dựng này là vũ khí tối tân giúp tối ưu hóa vận hành, nâng cao trải nghiệm khách hàng và gia tăng tỷ lệ chốt đơn nhờ tốc độ phản hồi thần tốc. Hãy áp dụng ngay vào doanh nghiệp của các sếp!