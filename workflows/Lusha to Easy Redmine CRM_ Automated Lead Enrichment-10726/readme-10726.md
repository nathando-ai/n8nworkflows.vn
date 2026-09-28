---
title: "🚀 Tự động hóa làm giàu dữ liệu Lead từ Lusha vào Easy Redmine CRM với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy danh sách lead từ Easy Redmine, quét thông tin chi tiết qua Lusha và cập nhật ngược lại CRM hoàn toàn tự động."
slug: "tu-dong-hoa-lam-giau-lead-lusha-easy-redmine-crm"
tags: [n8n, automation, crm, lead-generation, easy-redmine, lusha]
keywords: [n8n workflow, easy redmine crm, lusha enrichment, tự động hóa crm, lead enrichment n8n]
---

# 🚀 Tự động hóa làm giàu dữ liệu Lead từ Lusha vào Easy Redmine CRM

Các sếp trong đội ngũ Sales và Marketing chắc chắn đã quá ngán ngẩm cảnh phải copy/paste thủ công từng thông tin của khách hàng tiềm năng (lead) từ các nền tảng tra cứu như Lusha vào CRM, chưa kể dữ liệu rất dễ bị thiếu sót số điện thoại, quy mô nhân sự hay link LinkedIn. Công việc lặp đi lặp lại này vừa tốn thời gian, vừa làm giảm năng suất chốt đơn.

Giải pháp ở đây là gì? Workflow n8n này sẽ tự động hóa toàn bộ quy trình: lấy danh sách lead từ **Easy Redmine**, gọi API sang **Lusha** để làm giàu dữ liệu (enrichment), làm sạch dữ liệu qua mã nguồn tùy chỉnh và cập nhật lại thông tin mới nhất vào CRM mà không cần con người nhúng tay vào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chạy theo lịch trình định sẵn (Schedule), không cần thao tác thủ công.
- **Dữ liệu CRM luôn sạch và đầy đủ:** Tự động bổ sung số điện thoại, số lượng nhân viên, LinkedIn của công ty/lead.
- **Tối ưu thời gian cho Sales:** Đội ngũ kinh doanh có ngay thông tin chi tiết để tiếp cận khách hàng mà không mất công tra cứu.
- **Chính xác và mượt mà:** Lọc bỏ các dòng dữ liệu trống và chuẩn hóa định dạng trước khi đẩy vào CRM.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Hạ tầng n8n:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Easy Redmine:** Tài khoản ứng dụng Easy Redmine (khuyến nghị dùng tài khoản kỹ thuật có quyền API cụ thể) và thông tin cấu hình `easyRedmineApi`.
- **Lusha Account:** Tài khoản Lusha có hạn mức API để truy vấn thông tin công ty/lead (`httpHeaderAuth`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc sao chép toàn bộ mã nguồn JSON từ n8n.io và paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình kỹ các node trọng điểm sau:
- **Schedule Trigger**: Thiết lập khoảng thời gian chạy workflow (ví dụ: chạy mỗi ngày một lần hoặc theo giờ làm việc).
- **Get Leads from Easy Redmine**: Kết nối tài khoản Easy Redmine (`easyRedmineApi`), chọn resource `easy_leads` và áp dụng bộ lọc đã lưu (ID Query) để nhắm đúng tập dữ liệu cần quét.
- **Get Data from Lusha**: Cấu hình thông tin xác thực `httpHeaderAuth` để gọi API Lusha lấy thông tin chi tiết cho từng lead.
- **Filter Leads Found in Lusha**: Đảm bảo node này loại bỏ các bản ghi không tìm thấy dữ liệu từ Lusha để tránh làm rác CRM.
- **Contact Data Transformation for CRM (Code Node)**: Tùy chỉnh đoạn code chuyển đổi dữ liệu (ví dụ: chuyển định dạng "1,000-5,000" thành giá trị số nguyên `5000`, loại bỏ ký tự đặc biệt).
- **Update Leads in Easy Redmine CRM**: Gửi yêu cầu PUT để cập nhật thông tin liên hệ và công ty đã làm giàu vào Easy Redmine.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một vài mẫu dữ liệu nhỏ để kiểm tra xem thông tin đã được đẩy đúng vào Easy Redmine CRM chưa.
- Sau khi kiểm tra mọi thứ trơn tru, hãy bật công tắc **Active** để workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Slack/Telegram:** Thêm một node gửi tin nhắn thông báo về kênh chat nội bộ của team Sales mỗi khi có lead mới được làm giàu thành công.
- **Xử lý lỗi (Error Handling):** Thêm nhánh `Error Trigger` để ghi log lại nếu API Lusha hoặc Easy Redmine gặp sự cố gián đoạn.
- **Báo cáo định kỳ:** Kết hợp thêm Google Sheets hoặc Email node để tổng hợp số lượng lead được làm giàu mỗi tuần gửi cho quản lý.

### 📌 Kết luận
Workflow tự động hóa kết hợp giữa **Lusha** và **Easy Redmine CRM** này chính là vũ khí giúp đội ngũ B2B tiết kiệm hàng giờ đồng hồ mỗi tuần. Hãy triển khai ngay hôm nay để tối ưu hóa quy trình vận hành sales của doanh nghiệp các sếp nhé!