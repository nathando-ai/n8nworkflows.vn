---
title: "🚀 Tự động làm giàu dữ liệu công ty (Company Enrichment) với Airtop và HubSpot trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình làm giàu thông tin doanh nghiệp, chấm điểm ICP và đồng bộ dữ liệu vào HubSpot qua Airtop."
slug: "tu-dong-lam-giàu-du-lieu-cong-ty-airtop-hubspot"
tags: [n8n, automation, hubspot, airtop, crm-enrichment, sales-automation]
keywords: [n8n workflow, làm giàu dữ liệu công ty, airtop hubspot, tự động hóa sales, icp scoring]
---

# 🚀 Tự động làm giàu dữ liệu công ty (Company Enrichment) với Airtop và HubSpot

Các sếp trong ngành sales và growth thường xuyên phải đối mặt với bài toán tốn hàng giờ đồng hồ để tra cứu thông tin công ty, lọc email cá nhân rác và cập nhật thủ công vào HubSpot. Việc này không chỉ chậm trễ mà còn dễ xảy ra sai sót, làm giảm tỷ lệ chuyển đổi khách hàng tiềm năng.

Giải pháp ở đây là gì? Workflow n8n này sẽ tự động hóa 100% quy trình: tiếp nhận thông tin từ form hoặc hệ thống khác, lọc email doanh nghiệp, cào dữ liệu công ty qua Airtop (tích hợp AI browser automation), tính điểm chân dung khách hàng lý tưởng (ICP Score) và đồng bộ trực tiếp lên HubSpot CRM mà không cần đụng tay vào code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần tra cứu thủ công LinkedIn hay website công ty.
- **Lọc sạch dữ liệu rác:** Tự động loại bỏ các email cá nhân (Gmail, Yahoo, .edu...) ngay từ bước đầu.
- **Chấm điểm ICP thông minh:** Tự động đánh giá chất lượng lead dựa trên quy mô, vị trí và hồ sơ công nghệ.
- **Đồng bộ CRM tức thì:** Tự động cập nhật hoặc tạo mới bản ghi công ty trên HubSpot một cách chính xác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Self-hosted hoặc Cloud).
- [Airtop API Key](https://portal.airtop.ai/api-keys) và [Airtop Profile](https://portal.airtop.ai/browser-profiles) đã đăng nhập sẵn tài khoản LinkedIn.
- Tài khoản HubSpot và thông tin xác thực API/Integration được bật.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ n8n template (ID: 4259) và import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm các node chính sau đây, các sếp cần chú ý cấu hình kỹ:
- **On form submission** & **When Executed by Another Workflow**: Điểm khởi đầu của quy trình. Các sếp có thể cấu hình form thu thập lead hoặc nhận dữ liệu từ các webhook/workflow khác truyền vào (Yêu cầu cung cấp: *Contact email*, *Company domain*, *Company LinkedIn*).
- **Is corporate email?** (`filter`): Node này đóng vai trò bộ lọc, chỉ giữ lại các email doanh nghiệp hợp lệ (chặn Gmail, Yahoo...).
- **Unify Params** & **Map information** (`set`): Chuẩn hóa các tham số đầu vào và mapping dữ liệu trước khi gửi đi xử lý.
- **Company info** (`executeWorkflow`): Gọi luồng xử lý của Airtop để cào dữ liệu LinkedIn/Web và tính điểm ICP score. Cần kết nối với **Airtop Profile** đã xác thực.
- **Save company Hubspot** (`executeWorkflow`): Đồng bộ toàn bộ thông tin đã làm giàu (tên, website, số nhân sự, địa điểm, điểm ICP) vào đối tượng Công ty trên HubSpot.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một vài email và domain mẫu để kiểm tra dữ liệu trả về từ Airtop và HubSpot.
- Sau khi test thành công, bật công tắc **Active** để workflow chính thức vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Kết hợp thêm node Slack hoặc Telegram để bắn thông báo về team sales ngay khi có một công ty có điểm ICP cao được cập nhật.
- **Lưu log dự phòng:** Thêm node Google Sheets để lưu lại lịch sử enrich dữ liệu phục vụ việc tra cứu và đối soát.
- **Đa dạng hóa CRM:** Các sếp hoàn toàn có thể thay thế bước HubSpot bằng Salesforce, Pipedrive hoặc Close CRM tùy theo nhu cầu sử dụng của doanh nghiệp.

### 📌 Kết luận
Việc tự động hóa quy trình làm giàu dữ liệu công ty và đồng bộ CRM chưa bao giờ dễ dàng đến thế với sự kết hợp giữa n8n và Airtop. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa năng suất đội ngũ Sales ngay hôm nay!