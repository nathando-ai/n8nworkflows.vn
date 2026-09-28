---
title: "🚀 Tự động lập kế hoạch chỗ ngồi & bố trí địa điểm với Google Sheets"
description: "Giải pháp tự động 100% không code giúp tạo bản đồ chỗ ngồi tối ưu, lưu trữ dữ liệu và trả về báo cáo ngay từ webhook."
slug: "tuyendung-lap-ke-hoach-cho-ngoi"
tags: [n8n, automation, no-code, google-sheets, seating-planner]
keywords: [n8n workflow, tự động hóa, kế hoạch chỗ ngồi, Google Sheets, AI seating]
---

# 🚀 Tự động lập kế hoạch chỗ ngồi & bố trí địa điểm với Google Sheets

Bạn đang phải mất hàng giờ, thậm chí cả ngày để tính toán, bố trí chỗ ngồi cho hội nghị, tiệc cưới hay banquet? Bạn phải mở nhiều bảng tính, tính toán thủ công, rồi gửi lại cho khách hàng. Điều này không chỉ tốn thời gian mà còn dễ gây sai sót, làm mất uy tín.  
Workflow **Create Dynamic Seating & Venue Layout Plans with Google Sheets** của Oneclick AI Squad sẽ giải quyết mọi nỗi lo đó: từ khi nhận yêu cầu qua webhook, lấy dữ liệu khách tham dự và mẫu địa điểm từ Google Sheets, tính toán tối ưu bố trí, lưu trữ bản đồ và trả về báo cáo ngay lập tức – hoàn toàn không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 <https://tino.vn/vps-n8n?affid=388> (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 <https://my.bnix.one/aff.php?aff=172> (VPS Xeon 4GB chỉ 50k/tháng)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ tính toán thủ công xuống chỉ vài phút.  
- **Độ chính xác cao**: Tự động tính toán, giảm thiểu sai sót do con người.  
- **Tự động lưu trữ**: Tất cả dữ liệu, bản đồ và báo cáo được ghi vào Google Sheets ngay lập tức.  
- **Tích hợp linh hoạt**: Dễ dàng mở rộng thêm Slack, Telegram, email hay báo cáo định kỳ.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Google API Credentials**: Tạo OAuth2 client ID/secret trong Google Cloud, cấp quyền truy cập Sheets.  
- **Google Sheets**:  
  - Sheet “Attendees” – chứa thông tin khách tham dự (tên, nhóm, nhu cầu đặc biệt, VIP).  
  - Sheet “VenueTemplates” – chứa mẫu bố trí địa điểm (kích thước, số ghế, lối thoát).  
  - Sheet “MasterPlan” – lưu bản đồ chỗ ngồi tổng hợp.  
  - Sheet “IndividualAssignments” – lưu danh sách chỗ ngồi từng khách.  
- **Webhook URL**: Địa chỉ endpoint n8n (ví dụ: `https://your-domain.com/webhook/seating-planner`).  
- **Node.js environment**: Đảm bảo n8n đã cài đặt các node cần thiết (code, googleSheets, respondToWebhook).  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON của workflow từ <https://n8n.io/workflows/10223> hoặc copy toàn bộ JSON.  
2. Mở n8n Editor → **Workflows** → **Import** → **Upload JSON**.  
3. Chọn file hoặc dán JSON, nhấn **Import**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên trong workflow | Tham số cần cấu hình | Hướng dẫn |
|------|--------------------|----------------------|-----------|
| Webhook Trigger | `Webhook Trigger` | `path`: `seating-planner` <br> `httpMethod`: `POST` | Đảm bảo URL khớp với endpoint bạn sẽ gọi. |
| Validate Request Data | `Validate Request Data` | N/A | Kiểm tra payload (eventType, venueCapacity, attendeeCount, layoutPreference). |
| Fetch Attendee Data | `Fetch Attendee Data` | `Sheet ID`: ID của sheet “Attendees” | Chọn sheet, đặt `range` (ví dụ: `A1:E1000`). |
| Fetch Venue Templates | `Fetch Venue Templates` | `Sheet ID`: ID của sheet “VenueTemplates” | Tương tự như trên. |
| Combine All Data | `Combine All Data` | N/A | Kết hợp dữ liệu từ hai sheet. |
| Optimize Seating Layout | `Optimize Seating Layout` | N/A | Thuật toán AI tính toán bố trí tối ưu. |
| Format Recommendations | `Format Recommendations` | N/A | Định dạng báo cáo (bản đồ, thống kê). |
| Save Master Plan | `Save Master Plan` | `operation`: `append` | Ghi dữ liệu vào sheet “MasterPlan”. |
| Save Individual Assignments | `Save Individual Assignments` | `operation`: `appendOrUpdate` | Ghi danh sách chỗ ngồi từng khách. |
| Split Seat Assignments | `Split Seat Assignments` | N/A | Phân chia chỗ ngồi cho từng nhóm. |
| Send Response | `Send Response` | N/A | Trả về JSON chứa bản đồ, danh sách, thống kê. |

> **Tip**: Mỗi node `googleSheets` cần chọn **Google API Credentials** đã tạo trước đó. Đảm bảo quyền truy cập đầy đủ (read/write).

### 3. Kích hoạt ⚡️

1. **Test run**: Gửi payload mẫu qua Postman hoặc curl:  
   ```bash
   curl -X POST https://your-domain.com/webhook/seating-planner \
     -H "Content-Type: application/json" \
     -d '{
           "eventType":"Conference",
           "venueCapacity":500,
           "attendeeCount":350,
           "layoutPreference":"Theater"
         }'
   ```
2. Kiểm tra logs, xem dữ liệu đã được ghi vào Google Sheets.  
3. Khi mọi thứ ổn, bật **Active** cho workflow.

## ✍️ Mẹo & gợi ý nâng cao

- **Thêm Slack**: Gửi thông báo khi bản đồ hoàn thành.  
- **Telegram Bot**: Gửi link PDF bản đồ ngay khi hoàn thành.  
- **Lưu log**: Dùng node `Code` để ghi log vào một sheet riêng.  
- **Báo cáo định kỳ**: Kết hợp với node `Cron` để gửi báo cáo hàng ngày/tuần.  
- **Tùy chỉnh AI**: Thay đổi thuật toán trong node `Optimize Seating Layout` để ưu tiên nhóm VIP hoặc nhu cầu đặc biệt.

## 📌 Kết luận

Workflow này giúp các sếp tiết kiệm thời gian, giảm sai sót và nâng cao chất lượng dịch vụ khi tổ chức sự kiện. Bạn chỉ cần cấu hình một vài thông số, gửi yêu cầu qua webhook, và n8n sẽ tự động lấy dữ liệu, tính toán, lưu trữ và trả về báo cáo.  
Hãy thử ngay hôm nay và trải nghiệm sự tự động hóa hoàn toàn không code!