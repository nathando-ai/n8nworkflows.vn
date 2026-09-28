---
title: "🔍 Tự Động Hoá Reverse Lookup Email & Sync Contact Sang HubSpot CRM Với ScraperCity (N8n)"
description: "Workflow tự động tìm kiếm thông tin chi tiết từ email (tên, số điện thoại, địa chỉ) bằng ScraperCity và đồng bộ hóa liên lạc vào HubSpot CRM một cách hoàn toàn không cần code. Giúp các sếp tiết kiệm 10+ giờ/lần tìm kiếm thủ công và nâng cao hiệu suất lead generation."
slug: "tieu-dong-hoa-reverse-lookup-email-sync-hubspot-scrapercity"
tags: [n8n, automation, lead-generation, hubspot, scrapercity, no-code]
keywords: [n8n reverse lookup email, tự động hóa tìm kiếm thông tin người dùng, sync contact hubspot, lead generation tự động, scrapercity api, tự động hóa CRM]
---

# 🚀 **Tự Động Hoá Reverse Lookup Email & Sync Contact Sang HubSpot CRM**

### **Giải pháp cho các sếp muốn:**
- **Tìm kiếm thông tin chi tiết** (tên, số điện thoại, địa chỉ) từ email một cách **tự động hóa 100%**?
- **Tiết kiệm 10+ giờ/lần** tìm kiếm thủ công trên Google, LinkedIn, hoặc các công cụ tìm kiếm?
- **Dồng bộ hóa liên lạc** vào HubSpot CRM để quản lý lead hiệu quả hơn?
- **Không cần viết một dòng code** nhưng vẫn đạt kết quả chuyên nghiệp?

Workflow này **giải quyết tất cả** bằng cách kết hợp **ScraperCity** (công cụ web scraping chuyên nghiệp) và **n8n** (tự động hóa quy trình không code). Dưới đây là hướng dẫn chi tiết để **cài đặt, chạy và tối ưu hóa** workflow này cho doanh nghiệp của các sếp.

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Thay vì mất 2-3 giờ để tìm kiếm thông tin từ email trên các trang web, workflow này hoàn thành trong **vài phút**.
- **Dữ liệu chính xác**: ScraperCity sử dụng **12+ scraper** (bao gồm Apollo, Google Maps, People Finder) để lấy thông tin chi tiết từ nhiều nguồn khác nhau.
- **Dồng bộ hóa tự động**: Liên lạc được **tự động thêm/sửa** vào HubSpot CRM, giúp quản lý lead trở nên **liên tục và chính xác**.
- **Không giới hạn quy mô**: Có thể **reverse lookup hàng ngàn email** một lúc mà không lo lỗi hoặc chậm trễ.
- **Tích hợp hoàn hảo**: Kết hợp với **Slack/Telegram** để báo cáo kết quả hoặc **lưu log** để theo dõi hiệu suất.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản ScraperCity**:
   - [Đăng ký ScraperCity](https://scrapercity.com/) (nếu chưa có).
   - **API Key** để kết nối với n8n (mã này sẽ được sử dụng trong **HTTP Header Auth**).
   - **People Finder Scraper** (đã bao gồm trong gói của ScraperCity).

2. **Tài khoản HubSpot**:
   - [Đăng ký HubSpot](https://www.hubspot.com/) (nếu chưa có).
   - **Private App Token** để kết nối với n8n (hướng dẫn tạo [tại đây](https://developers.hubspot.com/docs/api/private-apps)).

3. **n8n Self-hosted** (không dùng phiên bản miễn phí):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

4. **Danh sách email mục tiêu**:
   - Các sếp cần **danh sách email** (cách nhau bởi dấu phẩy) muốn reverse lookup (ví dụ: `a@example.com,b@example.com,c@example.com`).
   - **Khuyến nghị**: Đối với hiệu quả tốt nhất, sử dụng **danh sách email B2B** (doanh nghiệp).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào n8n Editor. Dưới đây là cách thực hiện:

#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/13975](https://n8n.io/workflows/13975) (chọn **Download JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Tải JSON từ [đây](https://raw.githubusercontent.com/n8n-io/workflows/master/workflows/13975/main.json).
2. Trên **n8n Editor**, nhấn **Import** → Chọn **Paste JSON** và dán nội dung JSON vào.
3. Chọn **Create new workflow** và nhấn **Import**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **15 node**, nhưng chỉ **3 node quan trọng** cần cấu hình trước khi chạy:

#### **A. Thiết lập Credentials (BẮT BUỘC)**
1. **ScraperCity API Key**:
   - Trên n8n, nhấn **Credentials** → **Add new credential** → Chọn **HTTP Header Auth**.
   - **Header Name**: `Authorization`
   - **Header Value**: `Bearer YOUR_SCRAPERCITY_API_KEY` (thay `YOUR_SCRAPERCITY_API_KEY` bằng API Key của các sếp).
   - **Lưu credential** với tên **`httpHeaderAuth`**.

2. **HubSpot Private App Token**:
   - Trên n8n, nhấn **Credentials** → **Add new credential** → Chọn **HubSpot App Token**.
   - Nhập **Private App Token** của các sếp (tạo từ [HubSpot Developer Portal](https://developers.hubspot.com/docs/api/private-apps)).
   - **Lưu credential** với tên **`hubspotAppToken`**.

#### **B. Cấu hình Node "Configure Lookup Parameters"**
- Node này **chỉ cần chỉnh 1 tham số**:
  - **Email List**: Nhập danh sách email mục tiêu (cách nhau bởi dấu phẩy, ví dụ: `a@example.com,b@example.com`).
  - **max_results**: Số lượng kết quả tối đa ScraperCity trả về cho mỗi email (mặc định là `3`).

#### **C. Kiểm tra Node "Upsert Contact in HubSpot"**
- Node này **tự động đồng bộ hóa** liên lạc vào HubSpot.
- Các sếp cần **đảm bảo**:
  - **Email** là trường duy nhất (unique key) để tránh trùng lặp.
  - Các trường **Name, Phone, Address** sẽ được **auto-mapped** từ ScraperCity sang HubSpot.

---

### **3. Kích hoạt ⚡️**
1. **Test Run (Kiểm tra trước khi chạy chính thức)**:
   - Nhấn **Execute workflow** với **dữ liệu mẫu** (ví dụ: `test@example.com`).
   - Kiểm tra **HubSpot** để xác nhận liên lạc đã được thêm/sửa thành công.

2. **Bật Active Workflow**:
   - Sau khi kiểm tra thành công, các sếp có thể **bật Active** để workflow chạy tự động khi kích hoạt.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::info[TIẾP CẬN HƠN]
1. **Kết hợp với Slack/Telegram**:
   - Thêm **node Slack/Telegram** sau **Upsert Contact in HubSpot** để **báo cáo kết quả** mỗi khi workflow hoàn thành.
   - Ví dụ: Gửi tin nhắn như: *"Reverse lookup hoàn tất! Tìm thấy 10 liên lạc mới trong HubSpot."*

2. **Lưu log hoạt động**:
   - Thêm **node `n8n-nodes-base.stickyNote`** để ghi lại **Run ID**, **thời gian bắt đầu/hoàn thành**, và **số lượng liên lạc được xử lý**.
   - Giúp các sếp **theo dõi hiệu suất** và **sửa lỗi** nếu có.

3. **Tối ưu hóa max_results**:
   - Nếu ScraperCity trả về **nhiều kết quả không cần thiết**, giảm **max_results** xuống (ví dụ: `max_results: 1`).
   - Ngược lại, nếu muốn **nhận nhiều lead hơn**, tăng **max_results** lên (tối đa 5-10).

4. **Lọc email theo domain**:
   - Thêm **node `n8n-nodes-base.filter`** trước **Start People Finder Scrape** để chỉ reverse lookup email từ **domain cụ thể** (ví dụ: `@gmail.com`, `@yahoo.com`).

5. **Chạy định kỳ với n8n Cron**:
   - Sử dụng **n8n Cron** để **chạy workflow hàng ngày/tuần** (ví dụ: reverse lookup email mới từ danh sách lead).
   - Hướng dẫn [cài đặt Cron tại đây](https://docs.n8n.io/integrations/builtins/n8n-nodes-base.manualTrigger.html#cron).

---

## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc **tìm kiếm thủ công** và đồng thời **nâng cao chất lượng lead** bằng cách tự động hóa reverse lookup email và đồng bộ hóa vào HubSpot.

### **Bước tiếp theo:**
1. **Cài đặt n8n Self-hosted** (nếu chưa có) và **import workflow**.
2. **Cấu hình ScraperCity API Key** và **HubSpot Private App Token**.
3. **Nhập danh sách email mục tiêu** và **bắt đầu chạy**.
4. **Kết hợp với Slack/Telegram** để theo dõi kết quả.

**🚀 Hãy áp dụng ngay và xem cách workflow này **tự động hóa lead generation** cho doanh nghiệp của các sếp!**

---
**🔗 [Tải workflow nguyên bản tại n8n.io](https://n8n.io/workflows/13975)**
**📌 [Hướng dẫn tạo Private App Token HubSpot](https://developers.hubspot.com/docs/api/private-apps)**