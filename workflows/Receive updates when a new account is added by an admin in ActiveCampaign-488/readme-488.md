---
title: "🚀 Tự Động Nhận Thông Báo Khi Tài Khoản Mới Được Thêm Vào ActiveCampaign (Không Cần Code)"
description: "Hiểu ngay cách tự động nhận thông báo tức thời khi quản trị viên thêm tài khoản mới vào ActiveCampaign, tiết kiệm thời gian theo dõi thủ công và tránh bỏ lỡ khách hàng tiềm năng."
slug: "tu-dong-nhan-thong-bao-tai-khoan-moi-activecampaign"
tags: [n8n, automation, marketing, activecampaign, no-code]
keywords: [n8n workflow activecampaign, tự động hóa marketing, nhận thông báo tài khoản mới, activecampaign trigger, tự động hóa không code]
---

# 🚀 **Tự Động Nhận Thông Báo Khi Tài Khoản Mới Được Thêm Vào ActiveCampaign**

### **Nỗi Đau Của Các Sếp Marketing**
Làm việc với ActiveCampaign, các sếp thường phải **thủ công theo dõi** danh sách tài khoản mới được quản trị viên thêm vào. Điều này không chỉ **tốn thời gian** mà còn **rủi ro bỏ lỡ** khách hàng tiềm năng hoặc cơ hội marketing quan trọng. Với workflow này, các sếp sẽ **tự động nhận thông báo tức thời** mỗi khi có tài khoản mới được tạo, giúp tối ưu hóa quy trình và tăng cường phản ứng nhanh chóng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 mà không gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải **check thủ công** danh sách tài khoản mới hàng ngày.
- **Phản ứng tức thời**: Nhận thông báo ngay khi tài khoản mới được thêm, giúp **khách hàng tiềm năng** được chăm sóc kịp thời.
- **Tối ưu hóa quy trình**: Giúp đội ngũ marketing **tự động hóa** việc theo dõi và phân loại khách hàng mới.
- **Không bỏ lỡ cơ hội**: Tránh tình trạng **quên hoặc quên theo dõi** tài khoản mới do bận rộn.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
- **Tài khoản ActiveCampaign**: Các sếp cần **API Key** của ActiveCampaign để kết nối với n8n.
- **Credentials trong n8n**:
  - **activeCampaignApi**: Tham số này sẽ được sử dụng để xác thực với ActiveCampaign.
- **Quản trị viên ActiveCampaign**: Người này phải có quyền **thêm tài khoản mới** để workflow hoạt động.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Truy cập [n8n Editor](https://n8n.io/) và chọn **"Import Workflow"**.
- **Bước 2**: Chọn file JSON từ [link gốc](https://n8n.io/workflows/488) hoặc **copy/paste** JSON từ trang này vào ô nhập liệu.
- **Bước 3**: Nhấn **"Import"** để workflow xuất hiện trong danh sách của bạn.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này chỉ có **1 node** duy nhất: **ActiveCampaign Trigger**, nhưng để hoạt động, các sếp cần:
- **Thiết lập credentials**:
  - Vào **"Credentials"** trong n8n Editor.
  - Tạo một **mới credential** với tên **"activeCampaignApi"**.
  - Điền **API Key** của ActiveCampaign (có thể lấy từ **Settings > API Keys** trong ActiveCampaign).
- **Cấu hình node**:
  - Trong node **ActiveCampaign Trigger**, chọn **credentials** vừa tạo (**activeCampaignApi**).
  - Chọn **event type** phù hợp (ví dụ: **"Account Created"**).

#### **3. Kích Hoạt ⚡️**
- **Bước 1**: Chọn workflow và nhấn **"Active"**.
- **Bước 2**: **Test Run** với dữ liệu mẫu (nếu có) để đảm bảo workflow hoạt động.
- **Bước 3**: Khi có tài khoản mới được thêm vào ActiveCampaign, các sếp sẽ **nhận thông báo tức thời** qua email hoặc Slack (nếu kết nối).

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
- **Kết hợp với Slack/Telegram**: Sử dụng node **Slack Webhook** hoặc **Telegram Bot** để nhận thông báo tức thời trên các kênh chat.
- **Lưu log hoạt động**: Sử dụng node **Google Sheets** hoặc **Airtable** để lưu lại lịch sử tài khoản mới được thêm.
- **Gửi báo cáo định kỳ**: Kết hợp với node **Email** hoặc **Google Calendar** để gửi báo cáo tổng hợp tài khoản mới hàng tuần.
- **Phân loại tài khoản**: Sử dụng node **ActiveCampaign** để **tự động thêm tài khoản mới vào danh sách marketing** hoặc **gửi email chào mừng**.

---

### 📌 **Kết Luận**
Với workflow này, các sếp **không cần code** mà vẫn có thể **tự động hóa việc theo dõi tài khoản mới** trong ActiveCampaign. **Tiết kiệm thời gian, tăng hiệu quả và không bỏ lỡ cơ hội** là những lợi ích mà các sếp sẽ nhận được. **Hãy áp dụng ngay và tối ưu hóa quy trình marketing của mình!**

---
**💡 Bạn có thể tùy chỉnh workflow này thêm nhiều chức năng khác như gửi email tự động, cập nhật CRM hoặc kết hợp với các công cụ khác như Zapier, Make (Integromat) để mở rộng tính năng.**