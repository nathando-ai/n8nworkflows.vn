---
title: "🚀 Tự động làm giàu dữ liệu công ty HubSpot bằng Coresignal API qua n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động bắt sự kiện công ty mới trên HubSpot, truy vấn dữ liệu B2B từ Coresignal và cập nhật ngược lại hoàn toàn tự động."
slug: "tu-dong-lam-giau-du-lieu-cong-ty-hubspot-voi-coresignal"
tags: [n8n, automation, no-code, hubspot, coresignal, lead-generation]
keywords: [n8n workflow, hubspot automation, coresignal enrich, lam giai du lieu b2b, tu dong hoa n8n]
---

# 🚀 Tự động làm giàu dữ liệu công ty HubSpot bằng Coresignal API

Các sếp làm sales và marketing chắc chắn hiểu cảm giác mệt mỏi khi phải thủ công tra cứu thông tin của từng công ty mới tạo trên CRM. Việc thiếu thông tin chi tiết (quy mô nhân sự, doanh thu, công nghệ sử dụng, thông tin LinkedIn...) khiến đội ngũ sales mất rất nhiều thời gian nghiên cứu trước khi outreach.

Giải pháp ở đây là gì? Workflow n8n này sẽ tự động hóa 100% quy trình: ngay khi có một công ty mới được tạo trên HubSpot, hệ thống sẽ chờ các tiến trình khác hoàn tất, gọi dữ liệu từ **Coresignal API** để làm giàu (enrich) thông tin, và cập nhật ngược lại vào HubSpot mà không cần một chạm tay thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm hàng chục giờ thủ công:** Không cần copy-paste thông tin công ty từ Google hay LinkedIn vào CRM nữa.
- **Dữ liệu B2B chất lượng cao:** Khai thác kho dữ liệu phong phú từ Coresignal dựa trên tên miền website công ty.
- **Đồng bộ hóa liền mạch:** Cập nhật thông tin chi tiết của công ty ngay lập tức lên HubSpot khi vừa khởi tạo.
- **Hoạt động 24/7 không gián đoạn:** Tự động chạy ngầm mỗi khi có khách hàng doanh nghiệp mới bước vào phễu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **HubSpot** có quyền tạo Webhook / Developer API hoặc OAuth2.
- Tài khoản **Coresignal** kèm theo API Key để gọi dịch vụ dữ liệu công ty.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của template này và paste trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 5 nodes chính được chia thành 2 nhóm nhiệm vụ:

- **When Company Created in HubSpot (`hubspotTrigger`):**
  - Cần kết nối `hubspotDeveloperApi` credentials.
  - Node này đóng vai trò là "còi báo", lắng nghe sự kiện khi có một Company (Công ty) mới được tạo trên HubSpot.
- **Wait 10 Seconds for Action (`wait`):**
  - Node chờ 10 giây nhằm đảm bảo các tiến trình ngầm khác của HubSpot (như workflow nội bộ hoặc app bên thứ 3) đã ghi nhận xong dữ liệu trước khi chúng ta bốc thông tin đi xử lý.
- **Retrieve Company from HubSpot (`hubspot`):**
  - Chọn resource là `company`, operation là `get`.
  - Sử dụng `hubspotOAuth2Api` credentials để lấy toàn bộ thông tin chi tiết mới nhất của công ty dựa vào ID từ Trigger.
- **Fetch Details from Coresignal (`n8n-nodes-coresignal-api.coresignal`):**
  - Chọn resource là `company`, operation là `enrich`.
  - Cấu hình `coresignalApi` credentials. Node này sẽ dùng website URL của công ty vừa lấy từ HubSpot để truy vấn dữ liệu đa nguồn từ Coresignal.
- **Update Company in HubSpot (`hubspot`):**
  - Chọn resource là `company`, operation là `update`.
  - Ánh xạ (Map) các trường dữ liệu phong phú nhận được từ Coresignal vào các custom fields tương ứng trên HubSpot của các sếp.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test Run) bằng cách tạo một công ty giả lập trên HubSpot có điền website chính xác.
- Kiểm tra xem Coresignal có trả về data và HubSpot có cập nhật thành công hay không.
- Bật công tắc **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Slack/Telegram:** Thêm một node thông báo vào kênh sales ngay sau khi update thành công để đội ngũ nắm bắt khách hàng tiềm năng lớn vừa xuất hiện.
- **Lọc dữ liệu (Filter):** Thêm node Filter để chỉ enrich những công ty có quy mô nhân sự hoặc quốc gia thỏa mãn điều kiện của doanh nghiệp, giúp tiết kiệm quota gọi API Coresignal.
- **Ghi Log lỗi:** Bổ sung nhánh Error Trigger để gửi cảnh báo nếu Coresignal không tìm thấy thông tin hoặc API gặp sự cố.

### 📌 Kết luận
Việc làm giàu dữ liệu B2B tự động chưa bao giờ dễ dàng đến thế với sự kết hợp giữa n8n, HubSpot và Coresignal. Hãy thiết lập ngay hôm nay để đội ngũ sales của các sếp luôn có trong tay những thông tin khách hàng sắc bén nhất!