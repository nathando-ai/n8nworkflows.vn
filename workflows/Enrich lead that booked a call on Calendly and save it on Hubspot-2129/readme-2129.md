---
title: "🚀 Tự động làm giàu thông tin Lead từ Calendly và đồng bộ vào HubSpot với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động bắt sự kiện đặt lịch từ Calendly, tra cứu thông tin doanh nghiệp qua Clearbit và cập nhật dữ liệu chuyên nghiệp vào HubSpot CRM."
slug: "tu-dong-lam-giac-lead-calendly-hubspot-n8n"
tags: [n8n, automation, no-code, sales, marketing, crm]
keywords: [n8n workflow, tự động hóa calendly hubspot, clearbit enrichment, crm automation, n8n viet nam]
---

# 🚀 Tự động làm giàu thông tin Lead từ Calendly và đồng bộ vào HubSpot

Trong quy trình Sales và Marketing hiện đại, việc phản hồi nhanh chóng và nắm bắt đầy đủ thông tin về một khách hàng tiềm năng (lead) vừa đặt lịch hẹn là yếu tố sống còn để chốt sale. Tuy nhiên, việc thủ công tra cứu thông tin công ty, quy mô, ngành nghề của lead trên Google rồi nhập vào HubSpot CRM vừa tốn thời gian, vừa dễ sai sót.

Workflow n8n này do **Ricardo Espinoza (Software engineer tại n8n.io)** thiết kế sẽ giải quyết triệt để bài toán đó. Hệ thống sẽ tự động hóa 100% quy trình: Ngay khi có khách hàng đặt lịch qua Calendly, workflow sẽ lọc bỏ email cá nhân (Gmail, Yahoo,...), sử dụng **Clearbit** để làm giàu dữ liệu (data enrichment) công ty và tự động tạo/cập nhật thông tin chi tiết vào **HubSpot CRM**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian thủ công:** Không còn cảnh sales phải "soi" từng thông tin công ty của lead trước cuộc gọi.
- **Dữ liệu CRM luôn sạch và đầy đủ:** Tự động phân loại email doanh nghiệp, làm giàu thông tin công ty (quy mô, ngành nghề, mạng xã hội...) qua Clearbit trước khi lưu vào HubSpot.
- **Cá nhân hóa quy trình bán hàng:** Đội ngũ Sales có ngay bức tranh toàn cảnh về khách hàng ngay trong HubSpot CRM trước khi bước vào cuộc họp.
- **Hoạt động liên tục 24/7:** Bắt sự kiện thời gian thực (Real-time trigger) ngay khi khách vừa book lịch thành công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
1. **Tài khoản n8n** (Cloud hoặc Self-hosted).
2. **Tài khoản Calendly** kèm quyền truy cập API.
3. **Tài khoản Clearbit** kèm API Key để tra cứu dữ liệu doanh nghiệp và cá nhân.
4. **Tài khoản HubSpot CRM** kèm quyền cấu hình OAuth2.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ mã nguồn JSON của workflow (từ nguồn gốc n8n template #2129) và paste trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình kỹ các node sau:

- **Calendly Trigger**: Đây là điểm khởi đầu của workflow. Các sếp cần kết nối tài khoản Calendly của mình (`calendlyApi`). *Lưu ý: Nếu sau này các sếp đổi sang công cụ đặt lịch khác (như Cal.com, HubSpot Meeting,...), chỉ cần thay thế node này bằng webhook tương ứng.*
- **Filter out personal emails**: Node này giúp lọc ra các email cá nhân (như `@gmail.com`, `@yahoo.com`), đảm bảo chỉ làm giàu thông tin cho các email doanh nghiệp (B2B).
- **Enrich email & Enrich company (Clearbit)**: Cần điền `clearbitApi` credentials. Node này sẽ dựa vào domain email để quét thông tin doanh nghiệp. Các sếp hãy map đúng các trường thông tin công ty mà mình quan tâm theo hướng dẫn trên canvas.
- **Search company, Create company, Update company & Upsert lead (HubSpot)**: Kết nối tài khoản HubSpot (`hubspotOAuth2Api`). Workflow sẽ kiểm tra xem công ty đã tồn tại trên CRM hay chưa (`if company does not exist on CRM`):
  - Nếu **chưa có**: Tiến hành tạo mới công ty (`Create company`) với dữ liệu từ Clearbit và tạo/cập nhật liên hệ (`Upsert lead`).
  - Nếu **đã có**: Tiến hành cập nhật thông tin mới nhất cho công ty (`Update company`) và đồng bộ thông tin liên hệ.

#### 3. Kích hoạt ⚡️
- Nhấp vào nút **Test workflow** trên n8n.
- Thử tạo một lịch hẹn giả lập trên Calendly (hoặc dùng tài khoản thật book một lịch test) để kích hoạt sự kiện đầu vào.
- Kiểm tra xem dữ liệu đã được đẩy chuẩn chỉnh vào HubSpot CRM chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để workflow chính thức "chạy ngầm" 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm thông báo Telegram/Slack**: Gắn thêm một node Telegram hoặc Slack ngay sau bước tạo lead thành công để bắn thông báo nóng về group nội dung sales: *"🔥 Có lead mới [Tên Lead] từ [Tên Công Ty] vừa book lịch hẹn qua Calendly!"*.
- **Lưu trữ backup vào Google Sheets**: Thêm một node Google Sheets để lưu một bản sao danh sách lead nhằm phục vụ việc thống kê báo cáo hàng tuần.
- **Xử lý ngoại lệ (Error Handling):** Thêm Error Trigger để bắt lỗi nếu Clearbit không tìm thấy thông tin công ty, tránh làm gián đoạn workflow chính.

### 📌 Kết luận
Việc tự động hóa quy trình tiếp nhận và làm giàu thông tin lead từ Calendly vào HubSpot không chỉ giúp đội ngũ sales làm việc hiệu quả hơn mà còn nâng tầm chuyên nghiệp trong mắt khách hàng ngay từ điểm chạm đầu tiên. Chúc các sếp "lên đồ" thành công và chốt được nhiều hợp đồng lớn!