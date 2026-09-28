---
title: "📊 Tự động báo cáo hàng tuần HubSpot sang Slack - Giải pháp tiết kiệm thời gian cho Marketing"
description: "Workflow n8n tự động tổng hợp và gửi báo cáo số liệu leads, deals hàng tuần từ HubSpot sang Slack, giúp các sếp Marketing theo dõi hiệu quả kinh doanh một cách chuyên nghiệp."
slug: "tu-dong-bao-cao-hubspot-sang-slack-hang-tuan"
tags: [n8n, automation, no-code, hubspot, slack]
keywords: [n8n workflow, tự động hóa báo cáo, hubspot leads, slack notification]
---

# 📊 Tự động báo cáo hàng tuần HubSpot sang Slack - Giải pháp tiết kiệm thời gian cho Marketing

[Các sếp Marketing] có bao giờ cảm thấy mệt mỏi khi phải tổng hợp dữ liệu từ HubSpot hàng tuần để gửi báo cáo cho team? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài phút, giúp tiết kiệm thời gian quý giá và giảm thiểu lỗi con người.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động tổng hợp dữ liệu từ HubSpot mà không cần can thiệp thủ công.
- **Chính xác**: Giảm thiểu lỗi do nhập liệu tay.
- **Cá nhân hóa**: Có thể tùy chỉnh nội dung báo cáo theo nhu cầu của team.
- **Hoạt động liên tục**: Báo cáo được gửi tự động hàng tuần, đảm bảo không bỏ sót dữ liệu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản HubSpot với quyền truy cập API.
- Tài khoản Slack với quyền gửi tin nhắn vào channel.
- API keys cho cả HubSpot và Slack.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/8970](https://n8n.io/workflows/8970).
3. Hoặc tải file JSON về và import trực tiếp từ máy tính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get all contacts"**:
   - Chọn credentials cho HubSpot.
   - Đảm bảo tài khoản HubSpot có quyền truy cập vào dữ liệu contacts.

2. **Node "Filter leads added last week"**:
   - Cấu hình bộ lọc để chỉ lấy những leads được thêm vào trong tuần trước.
   - Có thể điều chỉnh điều kiện lọc theo nhu cầu cụ thể của team.

3. **Node "Send report to a Slack channel"**:
   - Chọn credentials cho Slack.
   - Chỉ định channel mà bạn muốn gửi báo cáo.
   - Tùy chỉnh nội dung tin nhắn theo mẫu có sẵn.

4. **Node "Schedule the report"**:
   - Điều chỉnh ngày và giờ gửi báo cáo theo lịch trình của team.
   - Mặc định là gửi vào thứ Hai hàng tuần.

5. **Node "Get all deals"**:
   - Chọn credentials cho HubSpot.
   - Đảm bảo tài khoản HubSpot có quyền truy cập vào dữ liệu deals.

6. **Node "Filter won deals last week"**:
   - Cấu hình bộ lọc để chỉ lấy những deals được thắng trong tuần trước.
   - Có thể điều chỉnh điều kiện lọc theo nhu cầu cụ thể của team.

7. **Node "Sum deal value"**:
   - Tùy chỉnh công thức tính tổng giá trị deals theo nhu cầu của team.

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, nhấn vào nút "Execute Workflow" để test chạy dữ liệu mẫu.
2. Kiểm tra kết quả trên Slack để đảm bảo báo cáo được gửi đúng như mong đợi.
3. Nếu mọi thứ ổn, nhấn vào nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Telegram**: Thay vì gửi báo cáo sang Slack, các sếp có thể cấu hình để gửi sang Telegram để team có thể nhận thông báo ngay trên điện thoại di động.
- **Lưu log**: Thêm node để lưu log các báo cáo đã gửi để theo dõi lịch sử.
- **Gửi báo cáo định kỳ**: Có thể cấu hình để gửi báo cáo hàng tháng hoặc hàng quý để đánh giá hiệu quả kinh doanh dài hạn.
- **Tùy chỉnh nội dung báo cáo**: Có thể thêm các chỉ số khác như số lượng leads theo nguồn, giá trị trung bình của deals, v.v. để báo cáo trở nên phong phú hơn.

### 📌 Kết luận
Workflow "Weekly HubSpot Lead Report to Slack" là giải pháp hoàn hảo cho các sếp Marketing muốn tự động hóa quy trình báo cáo hàng tuần. Với việc tích hợp HubSpot và Slack, các sếp có thể tiết kiệm thời gian quý giá và tập trung vào những việc quan trọng hơn. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của team!