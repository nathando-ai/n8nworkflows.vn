---
title: "🚀 Tự Động Phát Hiện Thay Đổi Công Việc & Công Ty Với Lusha Và HubSpot"
description: "Tự động hóa quy trình theo dõi biến động nhân sự và công ty của khách hàng tiềm năng bằng Lusha Bulk Enrichment và HubSpot CRM, giúp đội ngũ Sales không bỏ lỡ cơ hội."
slug: "phat-hien-thay-doi-cong-viec-cong-ty-lusha-hubspot"
tags: [n8n, automation, no-code, lusha, hubspot, lead-generation, crm]
keywords: [n8n workflow, tự động hóa lead generation, lusha enrichment, hubspot crm, theo dõi thay đổi công việc, sales automation]
---

# 🚀 Tự Động Phát Hiện Thay Đổi Công Việc & Công Ty Với Lusha Và HubSpot

Trong ngành Sales và B2B, việc nắm bắt thời điểm khách hàng cũ hoặc khách hàng tiềm năng chuyển sang công ty mới chính là "vàng mười" để chốt đơn. Tuy nhiên, việc thủ công kiểm tra hàng trăm, hàng nghìn liên hệ trên CRM mỗi ngày là điều bất khả thi, dẫn đến việc bỏ lỡ vô số cơ hội bán hàng quý giá. 

Workflow n8n này sẽ giúp các sếp giải quyết triệt để nỗi đau đó! Hệ thống sẽ tự động quét và đối chiếu dữ liệu từ HubSpot CRM thông qua Lusha Bulk Enrichment, phát hiện ngay khi có sự thay đổi về công việc hoặc công ty, đồng thời thông báo ngay lập tức để đội ngũ Sales kịp thời tiếp cận.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần tốn nhân lực kiểm tra thủ công danh sách liên hệ trên HubSpot.
- **Đón đầu cơ hội (Trigger Event):** Biết ngay khi khách hàng cũ đổi công ty để chào bán sản phẩm mới ở cương vị mới.
- **Cập nhật CRM liên tục:** Tự động đồng bộ thông tin chức vụ và công ty mới nhất vào HubSpot.
- **Thông báo thời gian thực:** Đẩy cảnh báo trực tiếp về Slack hoặc kênh liên lạc của đội Sales để chớp thời cơ ngay lập tức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **HubSpot CRM Account:** Tài khoản quản trị có quyền truy cập API/Contacts.
- **Lusha Account:** Tài khoản Lusha có gói dịch vụ hỗ trợ tính năng Bulk Enrichment hoặc API.
- **Slack Workspace:** (Tùy chọn) Để nhận thông báo thay đổi của lead.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Khi đưa workflow vào vận hành thực tế, các sếp cần cấu hình kỹ các node trọng điểm sau:
- **Schedule Trigger:** Cài đặt lịch chạy định kỳ (ví dụ: chạy mỗi tuần một lần hoặc mỗi tháng một lần) để quét dữ liệu khách hàng.
- **HubSpot Node:** Kết nối tài khoản HubSpot của doanh nghiệp. Cấu hình lấy danh sách (Get Contacts) các lead cần theo dõi (có thể lọc theo danh sách, lifecycle stage, hoặc deal đã đóng).
- **Lusha Node (`@lusha-org/n8n-nodes-lusha.lusha`):** Sử dụng các node tính năng làm giàu dữ liệu hàng loạt (Bulk Enrichment) của Lusha để kiểm tra trạng thái hiện tại của danh sách liên hệ.
- **If Node:** Bộ lọc thông minh dùng để so sánh dữ liệu cũ từ HubSpot với dữ liệu mới trả về từ Lusha, nhằm tách nhóm các liên hệ có sự thay đổi về chức vụ (Job Title) hoặc công ty (Company).
- **Slack Node:** Cấu hình kênh nhận thông báo (ví dụ: `#sales-alerts`) để đội ngũ kinh doanh nhận được thông tin chi tiết về khách hàng vừa thay đổi công việc.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một vài contact mẫu trên HubSpot để kiểm tra luồng dữ liệu qua Lusha và kết quả trả về.
- Sau khi chắc chắn hệ thống chạy mượt mà, gạt công tắc sang **Active** để workflow tự động làm việc 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tạo task tự động trên CRM:** Thay vì chỉ gửi tin nhắn Slack, có thể kết nối thêm node HubSpot để tự động tạo Task "Gọi điện chúc mừng vị trí mới" cho phụ trách sales tương ứng.
- **Gửi Email cá nhân hóa:** Kết hợp với Gmail/SMTP node để tự động gửi email chúc mừng khi khách hàng thăng chức hoặc đổi công ty.
- **Lưu log vào Google Sheets:** Ghi lại lịch sử thay đổi của khách hàng để phục vụ việc phân tích xu hướng thị trường hoặc đo lường hiệu quả outreach.

### 📌 Kết luận
Việc chủ động phát hiện thay đổi công việc của khách hàng tiềm năng là chìa khóa vàng giúp gia tăng tỷ lệ chuyển đổi trong bán hàng B2B. Hãy import ngay workflow này lên hệ thống n8n của các sếp để tối ưu hóa quy trình Sales ngay hôm nay!