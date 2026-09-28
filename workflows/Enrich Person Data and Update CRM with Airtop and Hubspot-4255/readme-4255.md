---
title: "🚀 Tự động làm giàu dữ liệu khách hàng (Enrichment) và cập nhật CRM với Airtop & HubSpot"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình làm giàu thông tin cá nhân qua Airtop, chấm điểm ICP và đồng bộ dữ liệu vào HubSpot CRM không cần code."
slug: "tu-dong-lam-giao-du-lieu-khach-hang-airtop-hubspot"
tags: [n8n, automation, crm, hubspot, airtop, lead-enrichment]
keywords: [n8n workflow, làm giàu dữ liệu khách hàng, airtop automation, hubspot crm, tự động hóa sales]
---

# 🚀 Tự động làm giàu dữ liệu khách hàng (Enrichment) và cập nhật CRM với Airtop & HubSpot

Trong các chiến dịch Sales và Marketing, việc thu thập thông tin thủ công từ LinkedIn hay các mạng xã hội để làm giàu hồ sơ khách hàng (Data Enrichment) tốn rất nhiều thời gian. Chưa kể việc đánh giá xem khách hàng đó có phù hợp với chân dung khách hàng lý tưởng (ICP) hay không lại càng ngốn thêm nguồn lực. 

Nếu các sếp đang đau đầu vì đội ngũ sales phải "lướt tay" từng profile rồi copy-paste vào HubSpot, thì workflow n8n này chính là cứu cánh. Sự kết hợp giữa **Airtop** (tự động hóa trình duyệt thông minh bằng AI) và **HubSpot** sẽ giúp tự động hóa 100% quy trình: Nhận thông tin -> Khai thác dữ liệu chuyên sâu -> Chấm điểm ICP -> Cập nhật CRM.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian**: Tự động hóa hoàn toàn việc tra cứu profile LinkedIn, vị trí công việc, số lượng người theo dõi và độ sâu kỹ thuật.
- **Chấm điểm ICP tự động**: Hệ thống tự động phân tích và đánh giá mức độ phù hợp của khách hàng với chân dung mục tiêu (ICP Score).
- **Đồng bộ CRM tức thì**: Đẩy toàn bộ thông tin đã làm giàu vào HubSpot mà không cần thao tác thủ công.
- **Linh hoạt kích hoạt**: Có thể chạy thông qua Form biểu mẫu trực tuyến hoặc gọi tự động từ các workflow khác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- [Airtop API Key](https://portal.airtop.ai/api-keys) và [Airtop Profile](https://portal.airtop.ai/browser-profiles) (đã đăng nhập sẵn tài khoản LinkedIn).
- Tài khoản HubSpot CRM kèm quyền truy cập để cập nhật dữ liệu Contact/Object.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow (hoặc import file JSON tương ứng từ kho lưu trữ n8n.io với ID `4255`) vào trình chỉnh sửa n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 7 nodes chính được thiết kế để xử lý dữ liệu đầu vào và đẩy lên CRM:

- **On form submission (`formTrigger`) & When Executed by Another Workflow (`executeWorkflowTrigger`)**: 
  - Đây là 2 điểm khởi đầu (Triggers). Tùy thuộc vào cách vận hành, các sếp chọn bật Form để khách hàng tự điền hoặc cấu hình nhận dữ liệu từ các workflow CRM khác.
- **Unify Params (`set`) & Edit Fields (`set`)**: 
  - Nơi chuẩn hóa các tham số đầu vào bao gồm: Tên đầy đủ (`Person name`), Email công việc (`Work email`), Airtop Profile ID, và HubSpot Object ID. Hãy đảm bảo các biến này khớp với dữ liệu đầu vào của các sếp.
- **Extract person info and calculate ICP (`executeWorkflow`)**: 
  - Node này gọi sub-workflow sử dụng **Airtop API** để cào dữ liệu LinkedIn (trang cá nhân, trang công ty, phần giới thiệu, chức danh, địa điểm) và tính toán điểm ICP, cấp bậc, mức độ quan tâm AI. Cần cấu hình đúng thông tin xác thực (Credentials) của Airtop.
- **Aggregate (`aggregate`)**: 
  - Gom nhóm và tổng hợp các trường dữ liệu đã được làm giàu trước khi chuyển sang bước tiếp theo.
- **Save data in Hubspot (`executeWorkflow`)**: 
  - Node thực thi việc đẩy dữ liệu đã làm giàu vào HubSpot dựa trên ID đối tượng (`Hubspot object id`). Các sếp nhớ kết nối tài khoản HubSpot API / Credentials chuẩn xác tại đây.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm với một bộ dữ liệu mẫu (Tên + Email thật).
- Kiểm tra kết quả trả về trong HubSpot xem dữ liệu đã được cập nhật chính xác chưa.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để hệ thống tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp thông báo Slack/Telegram**: Thêm node gửi tin nhắn thông báo về kênh nội bộ mỗi khi có một Lead VIP (điểm ICP cao) được làm giàu và cập nhật thành công vào HubSpot.
- **Lưu trữ backup**: Thêm node Google Sheets để lưu lại lịch sử các contact đã được enrich nhằm phục vụ cho việc đối soát dữ liệu sau này.
- **Mở rộng nguồn dữ liệu**: Kết hợp thêm các công cụ tìm kiếm khác qua Airtop để vét cạn thông tin mạng xã hội ngoài LinkedIn (Twitter/X, GitHub...).

### 📌 Kết luận
Việc tự động hóa quy trình làm giàu dữ liệu và cập nhật CRM chưa bao giờ dễ dàng đến thế nhờ sự kết hợp giữa n8n, Airtop AI và HubSpot. Hãy triển khai ngay hôm nay để giải phóng đội ngũ sales khỏi những tác vụ thủ công nhàm chán và tập trung vào việc chốt đơn!