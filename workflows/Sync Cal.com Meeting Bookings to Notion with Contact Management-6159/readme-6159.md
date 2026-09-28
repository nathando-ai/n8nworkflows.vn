---
title: "🚀 Tự động hóa đồng bộ lịch hẹn Cal.com với Notion cùng quản lý liên hệ"
description: "Hướng dẫn chi tiết cách tự động đồng bộ lịch hẹn từ Cal.com sang Notion và quản lý thông tin liên hệ khách hàng một cách hiệu quả"
slug: "tu-dong-hoa-dong-bo-lich-hen-cal-com-voi-notion"
tags: [n8n, automation, no-code, CRM, Notion, Cal.com]
keywords: [n8n workflow, tự động hóa, Cal.com, Notion, quản lý liên hệ, đồng bộ lịch hẹn]
---

# 🚀 Tự động hóa đồng bộ lịch hẹn Cal.com với Notion cùng quản lý liên hệ

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có thể đã từng gặp tình trạng này: khi sử dụng Cal.com để quản lý lịch hẹn, thông tin lại phải được nhập lại vào Notion để quản lý liên hệ. Quá trình này tốn thời gian, dễ gây lỗi và không đồng bộ. Với workflow này, các sếp có thể tự động đồng bộ tất cả lịch hẹn từ Cal.com sang Notion cùng với thông tin liên hệ khách hàng, giúp tiết kiệm thời gian và đảm bảo dữ liệu luôn đồng bộ.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Không cần nhập lại thông tin lịch hẹn và liên hệ từ Cal.com sang Notion.
- Dữ liệu đồng bộ: Thông tin lịch hẹn và liên hệ luôn được cập nhật tự động.
- Quản lý hiệu quả: Tất cả thông tin liên hệ và lịch hẹn được lưu trữ trong một hệ thống duy nhất.
- Tăng tính chuyên nghiệp: Hệ thống quản lý thông tin được tự động hóa giúp các sếp tập trung vào công việc quan trọng hơn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Cal.com và API key (tạo tại [đây](https://app.cal.com/settings/developer/api-keys)).
- Tài khoản Notion và API key (tạo tại [đây](https://developers.notion.com/docs/authorization#internal-integration-auth-flow-set-up)).
- Notion Meetings & Contacts databases với quyền truy cập cho integration.
- Thêm thuộc tính "cal id" vào Meetings database trong Notion.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/6159).
2. Click vào nút "Download" để tải file JSON.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON đã tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Cal.com Trigger**:
   - Kết nối tài khoản Cal.com.
   - Tạo API key tại [đây](https://app.cal.com/settings/developer/api-keys).
   - Thực hiện test node này bằng cách đặt workflow ở trạng thái OFF và chọn "Execute step".

2. **Route based on trigger event type**:
   - Node này sẽ định tuyến các sự kiện từ Cal.com (tạo, cập nhật, hủy lịch hẹn).

3. **get contact**:
   - Kết nối tài khoản Notion.
   - Nhập ID của Contacts database vào trường "Database ID".
   - Thiết lập điều kiện lọc để tìm kiếm liên hệ dựa trên email hoặc thông tin khác từ Cal.com.

4. **doesn't exist**:
   - Node này kiểm tra xem liên hệ đã tồn tại trong Notion hay chưa.

5. **create contact**:
   - Nhập ID của Contacts database vào trường "Database ID".
   - Thiết lập các thuộc tính cần thiết cho liên hệ mới (tên, email, số điện thoại, v.v.).

6. **create meeting**:
   - Nhập ID của Meetings database vào trường "Database ID".
   - Thiết lập các thuộc tính cần thiết cho lịch hẹn mới (tiêu đề, mô tả, thời gian, v.v.).

7. **get meeting**:
   - Nhập ID của Meetings database vào trường "Database ID".
   - Thiết lập điều kiện lọc để tìm kiếm lịch hẹn dựa trên "cal id".

8. **update meeting**:
   - Nhập ID của Meetings database vào trường "Database ID".
   - Thiết lập các thuộc tính cần cập nhật cho lịch hẹn (thời gian, trạng thái, v.v.).

9. **get meeting1**:
   - Nhập ID của Meetings database vào trường "Database ID".
   - Thiết lập điều kiện lọc để tìm kiếm lịch hẹn dựa trên "cal id".

10. **delete**:
    - Node này sẽ xóa lịch hẹn trong Notion khi sự kiện hủy lịch hẹn từ Cal.com được kích hoạt.

#### 3. Kích hoạt ⚡️
- Thực hiện test toàn bộ workflow bằng cách đặt workflow ở trạng thái ON và chọn "Execute workflow".
- Kiểm tra dữ liệu đầu ra và đảm bảo thông tin được đồng bộ chính xác.
- Bật Active workflow để chạy tự động khi có sự kiện mới từ Cal.com.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để thông báo khi có lịch hẹn mới hoặc thay đổi.
- Lưu log các hoạt động để theo dõi và kiểm tra.
- Gửi báo cáo định kỳ về các lịch hẹn và liên hệ mới.

### 📌 Kết luận
Workflow này giúp các sếp tự động đồng bộ lịch hẹn từ Cal.com sang Notion cùng với thông tin liên hệ khách hàng, tiết kiệm thời gian và đảm bảo dữ liệu luôn đồng bộ. Hãy áp dụng ngay để nâng cao hiệu quả quản lý và tập trung vào công việc quan trọng hơn.