---
title: "🚀 Tự động hóa báo cáo thông tin quảng cáo Facebook hàng tuần với Airtop và Gmail"
description: "Tiết kiệm thời gian nghiên cứu thủ công bằng cách tự động hóa việc theo dõi quảng cáo Facebook của đối thủ và nhận báo cáo thông tin hàng tuần qua email."
slug: "tu-dong-hoa-bao-cao-thong-tin-quang-cao-facebook-hang-tuan-voi-airtop-va-gmail"
tags: [n8n, automation, no-code, market-research, multimodal-ai]
keywords: [n8n workflow, tự động hóa, nghiên cứu thị trường, quảng cáo Facebook, báo cáo thông tin]
---

# 🚀 Tự động hóa báo cáo thông tin quảng cáo Facebook hàng tuần với Airtop và Gmail

[Các sếp đang phải tốn nhiều thời gian và công sức để theo dõi thủ công quảng cáo Facebook của đối thủ? Hãy để workflow này tự động hóa quy trình này và nhận báo cáo thông tin hàng tuần qua email một cách dễ dàng và hiệu quả.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian nghiên cứu thủ công.
- Nhận báo cáo thông tin quảng cáo hàng tuần một cách tự động.
- Theo dõi thông tin quảng cáo của đối thủ một cách hiệu quả.
- Tăng cường khả năng phân tích và đưa ra quyết định kinh doanh chính xác hơn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Airtop và API Key (có thể tạo tại [đây](https://portal.airtop.ai/api-keys)).
- Tài khoản Gmail để gửi báo cáo.
- URL của thư viện quảng cáo Facebook của đối thủ.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL".
3. Dán link sau vào ô nhập liệu: `https://n8n.io/workflows/7272`.
4. Nhấn "OK" để hoàn tất quá trình import.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Schedule Trigger**:
   - Cấu hình thời gian chạy hàng tuần (ví dụ: mỗi Chủ Nhật lúc 9:00 AM).

2. **Node Query Facebook Ad Library**:
   - Thêm credentials "airtopApi" và điền API Key của bạn.
   - Thay đổi URL của thư viện quảng cáo Facebook trong prompt để phù hợp với đối thủ của bạn.

3. **Node Send Report**:
   - Thêm credentials "gmailOAuth2" để kết nối với tài khoản Gmail.
   - Cấu hình địa chỉ email nhận báo cáo.

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút "Execute Node" để kiểm tra dữ liệu mẫu.
2. Sau khi kiểm tra thành công, nhấn vào nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Thêm nhiều node Airtop để theo dõi nhiều đối thủ khác nhau.
- Kết hợp với Slack để nhận thông báo tức thời khi có quảng cáo mới.
- Lưu trữ báo cáo trong Google Drive hoặc OneDrive để tham khảo sau này.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và công sức trong việc theo dõi quảng cáo Facebook của đối thủ. Bằng cách tự động hóa quy trình này, các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn và đưa ra quyết định kinh doanh chính xác hơn. Hãy áp dụng ngay để nhận báo cáo thông tin quảng cáo hàng tuần một cách dễ dàng và hiệu quả!