---
title: "🚀 Tự động làm giàu dữ liệu (Enrich) contact HubSpot mới với Lusha và cảnh báo Sales trên Slack"
description: "Hướng dẫn tự động hóa quy trình enrich thông tin contact mới trên HubSpot bằng Lusha, kiểm tra chất lượng dữ liệu và bắn cảnh báo Slack cho cấp quản lý/sales team ngay lập tức."
slug: "tu-dong-enrich-hubspot-contact-voi-lusha-va-slack"
tags: [n8n, automation, no-code, hubspot, lusha, slack, lead-generation]
keywords: [n8n workflow, hubspot automation, lusha enrich, slack alert, tự động hóa sales, revops]
---

# 🚀 Tự động làm giàu dữ liệu (Enrich) contact HubSpot mới với Lusha và cảnh báo Sales trên Slack

Các sếp làm trong ngành Sales và RevOps chắc chắn hiểu rõ nỗi đau: Khi có một lead mới đổ về HubSpot, thông tin thường rất sơ sài (chỉ có tên và email). Đội ngũ sales phải mất hàng giờ tra cứu thủ công trên LinkedIn, Google để tìm số điện thoại, chức vụ, quy mô công ty trước khi có thể gọi điện. Việc này vừa chậm trễ, vừa lãng phí nhân lực.

Workflow n8n này sẽ giải quyết triệt để vấn đề trên bằng cách **tự động hóa 100%**: Ngay khi có contact mới, hệ thống sẽ gọi Lusha để "làm giàu" dữ liệu, cập nhật ngược lại HubSpot, và nếu đó là sếp lớn (C-Suite, VP, Director), Slack sẽ ngay lập tức reo chuông báo cáo cho Sales Rep!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian research:** Sales không còn phải tra cứu thủ công từng lead.
- **Dữ liệu CRM luôn sạch và đầy đủ:** Số điện thoại, chức vụ, thông tin công ty được cập nhật chuẩn xác từ Lusha.
- **Phản hồi lead "thần tốc":** Phát hiện ngay các lead chất lượng cao (C-Suite, VP...) để sales tiếp cận đầu tiên.
- **Hoạt động 24/7:** Chạy ngầm liên tục theo thời gian thực mà không cần con người can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản HubSpot** (đã cấu hình OAuth2).
- **Tài khoản Lusha** (có API Key và đã cài đặt Lusha Community Node).
- **Workspace Slack** (để cấu hình bot gửi thông báo).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tạo một workflow mới trong n8n, sao chép đoạn JSON của workflow (tác giả: Daniel Turgeman) và dán trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình kỹ các node sau:

- **Cài đặt Lusha Community Node:** Trước tiên, hãy đảm bảo n8n của các sếp đã cài đặt package `@lusha-org/n8n-nodes-lusha`.
- **Node `New Contact Created in HubSpot` (HubSpot Trigger):** Kết nối tài khoản HubSpot qua OAuth2 để trigger kích hoạt ngay khi có contact mới được tạo. *(Mẹo: Các sếp có thể thay đổi bằng trigger Salesforce nếu dùng hệ thống khác).*
- **Node `Enrich Contact with Lusha`:** Chọn credential Lusha API, cấu hình thao tác `enrichSingle` sử dụng email từ contact vừa tạo.
- **Node `Data Quality Check` & `Was Enriched?` (Code & IF):** Đoạn mã JavaScript kiểm tra xem Lusha có trả về dữ liệu hợp lệ hay không trước khi ghi đè vào CRM.
- **Node `Update HubSpot Contact`:** Cập nhật các trường thông tin mới (số điện thoại, chức vụ, firmographics) vào hồ sơ contact trên HubSpot.
- **Node `Check Seniority Level` & `Is High Seniority?`:** Lọc các contact có chức danh cấp cao (VP, Director, C-Suite).
- **Node `Alert Rep on Slack`:** Kết nối Slack OAuth2, chọn channel nhận thông báo và tùy chỉnh nội dung tin nhắn gửi cho Sales Rep.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test workflow**) với một contact mẫu trên HubSpot để kiểm tra toàn bộ luồng chạy từ Lusha đến Slack.
- Bật công tắc **Active** để workflow chính thức trực chiến 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài Slack, các sếp có thể nhân bản nhánh cảnh báo để gửi thông tin lead nóng về **Telegram** hoặc **Zalo OA**.
- **Lưu log lỗi:** Thêm một nhánh Error Trigger để ghi nhận lại nếu Lusha không tìm thấy thông tin hoặc API gặp sự cố.
- **Giao việc tự động:** Kết hợp thêm node phân công (Assign) lead trong HubSpot dựa trên khu vực hoặc quy mô công ty.

### 📌 Kết luận
Quy trình tự động hóa này là "vũ khí bí mật" giúp đội ngũ RevOps và Sales tối ưu hóa hiệu suất làm việc, không bỏ lỡ bất kỳ khách hàng tiềm năng chất lượng cao nào. Hãy "lên đồ" và áp dụng ngay vào hệ thống của doanh nghiệp các sếp nhé!