---
title: "🚀 Tự động làm giàu thông tin Lead từ Form với Lusha, HubSpot và Slack"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình xác thực email, quét trùng lặp HubSpot, làm giàu data với Lusha và cảnh báo SDR tức thì qua Slack."
slug: "tu-dong-lam-giac-lead-lusha-hubspot-slack"
tags: [n8n, automation, lead-generation, hubspot, slack, lusha]
keywords: [n8n workflow, tu dong hoa lead, lusha api, hubspot crm, slack alert, form enrichment]
---

# 🚀 Tự động làm giàu thông tin Lead từ Form với Lusha, HubSpot và Slack

Các sếp có bao giờ cảm thấy đau đầu khi đội ngũ Sales (SDR) phải mất hàng giờ tra cứu thủ công thông tin của khách hàng đăng ký qua form trên website? Việc thiếu thông tin chi tiết (số điện thoại, chức vụ, quy mô công ty) khiến việc tiếp cận trở nên chậm trễ, dẫn đến việc mất đi những khách hàng tiềm năng nóng hổi vào tay đối thủ.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code, giúp các sếp xử lý trọn gói quy trình: Nhận dữ liệu form 👉 Kiểm tra trùng lặp 👉 Làm giàu thông tin (Enrich) bằng Lusha 👉 Đồng bộ CRM HubSpot 👉 Cảnh báo đội ngũ sales qua Slack ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Tự động hóa hoàn toàn khâu tra cứu thông tin cá nhân và công ty của lead.
- **Dữ liệu chính xác, sạch sẽ:** Lọc bỏ email rác, kiểm tra trùng lặp trên HubSpot trước khi tạo contact mới.
- **Tăng tỷ lệ chuyển đổi (Conversion Rate):** SDR nhận thông báo chi tiết trên Slack ngay khi lead vừa submit form, chớp lấy "thời điểm vàng" để gọi điện chốt sale.
- **Hoạt động 24/7:** Hệ thống ngầm tự động làm việc không nghỉ ngơi, kể cả ban đêm hay ngày lễ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
1. **n8n Instance:** Đã cài đặt n8n (Khuyên dùng bản Self-hosted hoặc n8n Cloud).
2. **Lusha Account & API Key:** Tài khoản Lusha để lấy dữ liệu contact (Cài đặt thêm community node `@lusha-org/n8n-nodes-lusha`).
3. **HubSpot CRM:** Tài khoản HubSpot để quản lý quan hệ khách hàng (Cần quyền kết nối OAuth2).
4. **Slack Workspace:** Kênh Slack nội bộ (ví dụ `#inbound-leads`) để nhận thông báo lead mới.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow và paste trực tiếp vào n8n Editor, hoặc import file JSON thông qua menu giao diện của n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Receive Form Submission (`webhook`):** 
  - Lấy đường dẫn Webhook URL và trỏ action URL của form trên website của các sếp về đây (hỗ trợ phương thức `POST`).
- **Validate Email & Merge Form + Lusha Data (`code`):** 
  - Các node JavaScript có sẵn logic kiểm tra định dạng email và gom nhóm dữ liệu. Các sếp có thể tùy chỉnh lại logic regex kiểm tra email nếu cần thiết.
- **Check HubSpot Duplicate & Create/Update HubSpot Contact (`hubspot`):** 
  - Chọn Credentials loại `hubspotOAuth2Api`.
  - Cấu hình trường dùng để check trùng lặp (thường là `email`).
  - Đảm bảo mapping đúng các trường thông tin từ form và Lusha vào các property tương ứng trong HubSpot.
- **Enrich with Lusha (`@lusha-org/n8n-nodes-lusha.lusha`):** 
  - Cài đặt community node Lusha nếu chưa có.
  - Nhập Lusha API Key vào phần credentials và chọn operation `enrichSingle` dựa trên email của lead.
- **Alert SDR on Slack (`slack`):** 
  - Kết nối `slackOAuth2Api`.
  - Chọn kênh nhận thông báo (ví dụ: `#inbound-leads`) và tùy chỉnh lại mẫu tin nhắn (Markdown) để hiển thị đầy đủ tên, chức vụ, số điện thoại và công ty của lead cho đội sales dễ đọc.
- **Return Enriched Lead (`respondToWebhook`):** 
  - Trả về dữ liệu đã được làm giàu dưới dạng JSON phản hồi về cho form của website (nếu cần hiển thị trực tiếp cho khách hàng).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một dữ liệu test từ form trên website để kiểm tra luồng chạy.
- Sau khi test thành công không lỗi, bật nút **Active** góc trên cùng bên phải để workflow chính thức chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Zalo OA:** Ngoài Slack, các sếp có thể nhân bản node thông báo sang Telegram để đội ngũ Sales nhận ping trên điện thoại cá nhân nhanh hơn.
- **Lưu Log vào Google Sheets:** Thêm một node Google Sheets để ghi lại toàn bộ lịch sử lead về hàng ngày nhằm phục vụ việc báo cáo Marketing.
- **Phân loại Lead (Routing):** Thêm node `If` sau bước Lusha enrichment để phân loại lead theo quy mô công ty (Enterprise/SMB) và bắn vào các kênh Slack riêng biệt cho từng team sales.

### 📌 Kết luận
Workflow tự động hóa làm giàu lead với Lusha, HubSpot và Slack là một trợ thủ đắc lực không thể thiếu cho bất kỳ đội ngũ Growth hay Marketing nào muốn tối ưu hóa quy trình tiếp cận khách hàng. Hãy triển khai ngay hôm nay để tăng tốc độ phản hồi sales và bứt phá doanh thu cho doanh nghiệp của các sếp!