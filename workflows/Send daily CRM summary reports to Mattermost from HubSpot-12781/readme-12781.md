---
title: "📊 **Tự Động Hóa Báo Cáo CRM Hàng Ngày Từ HubSpot Sang Mattermost - Không Cần Code!**"
description: "Workflow này tự động thu thập dữ liệu doanh thu bán hàng và hỗ trợ từ HubSpot, tổng hợp thành báo cáo PDF, lưu trữ trên CRM và gửi thông báo định kỳ đến Mattermost. Giúp các sếp tiết kiệm 5+ giờ/lần và duy trì tính nhất quán cao trong báo cáo."
slug: "tieu-dong-hoa-bao-cao-crm-hubspot-sang-mattermost"
tags: [n8n, automation, CRM, HubSpot, Mattermost, no-code, báo cáo tự động]
keywords: [n8n workflow CRM, tự động hóa báo cáo HubSpot, gửi báo cáo Mattermost, tự động hóa doanh thu bán hàng, tự động hóa hỗ trợ khách hàng]
---

# 🚀 **Tự Động Hóa Báo Cáo CRM Hàng Ngày Từ HubSpot Sang Mattermost**

## **🔥 Nỗi Đau Của Các Sếp Hiện Nay**
Hàng ngày, các sếp phải:
- **Tải dữ liệu bán hàng và hỗ trợ** từ HubSpot thủ công (thời gian: ~30-60 phút).
- **Tổng hợp và tính toán** các chỉ số KPI như doanh thu, số ticket mở, tỷ lệ giải quyết.
- **Tạo báo cáo PDF** để lưu trữ hoặc chia sẻ với team.
- **Gửi thông báo** đến Mattermost/Slack để đồng bộ thông tin cho toàn bộ đội ngũ.
- **Lo lắng về tính chính xác** khi làm thủ công, dễ xảy ra lỗi tính toán hoặc mất dữ liệu.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động thu thập dữ liệu** từ HubSpot (doanh thu và hỗ trợ) mỗi ngày.
✅ **Tổng hợp và tính toán KPI** tự động (doanh thu, ticket mở, tỷ lệ giải quyết).
✅ **Tạo báo cáo PDF** và lưu trữ trên HubSpot (CRM).
✅ **Gửi thông báo định kỳ** đến Mattermost với link trực tiếp đến báo cáo.
✅ **Xử lý lỗi tự động** và báo cáo ngay khi có vấn đề (không cần can thiệp thủ công).

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5+ giờ/lần** (không cần làm thủ công).
- **Chính xác 100%** (không sai sót tính toán).
- **Báo cáo tự động hàng ngày** (không quên hoặc bỏ sót).
- **Dữ liệu đồng bộ** giữa HubSpot và Mattermost (team luôn cập nhật).
- **Xử lý lỗi tự động** (báo cáo ngay khi có vấn đề).
- **Lưu trữ báo cáo trên HubSpot** (dễ dàng truy cập và theo dõi lịch sử).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản HubSpot** (để thu thập dữ liệu và lưu trữ báo cáo).
2. **Tài khoản Mattermost** (để gửi thông báo).
3. **API Keys hoặc Credentials** cho:
   - **Sales Endpoint** (dữ liệu doanh thu bán hàng).
   - **Support Endpoint** (dữ liệu hỗ trợ khách hàng).
4. **Webhook URL** (để gọi workflow hàng ngày từ scheduler).
5. **Mã giảm giá VPS** (để self-host n8n ổn định 24/7).
:::

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. **Tải file JSON** từ [link gốc](https://n8n.io/workflows/12781).
2. Trong n8n Editor, nhấn **Import** và chọn file JSON.
3. Hoặc copy toàn bộ JSON và dán vào **Import Workflow** (tùy chọn).

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **16 node**, các sếp cần chú ý cấu hình các node sau:

#### **🔹 Node "Prepare Config" (Set)**
- **Cần chỉnh:**
  - `salesEndpoint`: URL API của dữ liệu doanh thu (ví dụ: `https://api.hubapi.com/crm/v3/objects/deal?limit=100`).
  - `supportEndpoint`: URL API của dữ liệu hỗ trợ (ví dụ: `https://api.hubapi.com/crm/v3/objects/ticket?limit=100`).
  - `mattermostChannel`: Tên channel Mattermost để gửi thông báo (ví dụ: `#daily-reports`).
  - `reportDate`: Ngày báo cáo (có thể sử dụng `{{ $now.format('YYYY-MM-DD') }}` để lấy ngày hiện tại).

#### **🔹 Node "Fetch Sales Data" & "Fetch Support Data" (HTTP Request)**
- **Cần chỉnh:**
  - **Credentials**: Thêm API Key hoặc OAuth Token từ HubSpot.
  - **Headers**: Thêm `Authorization: Bearer {{ $credentials.hubspot_api_key }}`.
  - **Query Parameters**: Thêm `properties=amount,status` (đối với sales) hoặc `properties=status,createdate` (đối với support).

#### **🔹 Node "Upload Report to HubSpot" (HubSpot)**
- **Cần chỉnh:**
  - **Credentials**: Chọn credential HubSpot đã tạo trước đó.
  - **File Data**: Dữ liệu PDF sẽ tự động được inject từ node "Generate PDF".

#### **🔹 Node "Send Mattermost Notification" (Mattermost)**
- **Cần chỉnh:**
  - **Credentials**: Thêm token Mattermost từ **Admin > Integrations > Incoming Webhooks**.
  - **Channel**: Chọn channel Mattermost (đã cấu hình ở "Prepare Config").

#### **🔹 Node "Compose Error Message" (Code)**
- **Cần chỉnh:**
  - **Lỗi mặc định**: Các sếp có thể chỉnh nội dung lỗi để phù hợp với team (ví dụ: `@channel Báo cáo hàng ngày thất bại: {{ $json.error.message }}`).

#### **🔹 Node "Respond to Webhook" (RespondToWebhook)**
- **Cần chỉnh:**
  - **Trả về JSON**: Nếu có lỗi, trả về mã trạng thái `200` với nội dung lỗi để gọi webhook không bị timeout.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Execute Node** trên node **Webhook Trigger** để kiểm tra.
   - Kiểm tra:
     - Dữ liệu thu thập có chính xác không?
     - Báo cáo PDF có tạo thành công không?
     - Thông báo Mattermost có xuất hiện không?
2. **Bật Active Workflow**:
   - Sau khi test thành công, chuyển workflow sang **Active**.
3. **Gọi Webhook Hàng Ngày**:
   - Sử dụng **cron job** hoặc **scheduler** (ví dụ: Zapier, Make.com) để gọi webhook hàng ngày:
     ```bash
     curl -X POST https://tên-vps-của-bạn/n8n/webhook/daily-report
     ```

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM NÀY ĐỂ TIẾT KIỆM THÊM THỜI GIAN]
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để gửi báo cáo đến nhiều kênh đồng thời.
2. **Lưu Log Lịch Sử**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu trữ lịch sử báo cáo (dễ dàng theo dõi).
3. **Gửi Báo Cáo Email**:
   - Thêm node **Email** (Gmail/SMTP) để gửi báo cáo PDF trực tiếp qua email.
4. **Tự Động Chỉnh Ngày Báo Cáo**:
   - Sử dụng **JavaScript** trong node **Code** để tự động lấy ngày báo cáo từ ngày trước đó (ví dụ: `{{ $now.subtract(1, 'day').format('YYYY-MM-DD') }}`).
5. **Báo Cáo Thống Kê**:
   - Thêm node **Google Data Studio** hoặc **Power BI** để tự động tạo dashboard từ dữ liệu báo cáo.
:::

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công, **tăng tính chính xác** và **đồng bộ thông tin** giữa HubSpot và Mattermost. **Chỉ cần 10 phút setup**, workflow sẽ hoạt động tự động hàng ngày, giúp team luôn cập nhật và quyết định nhanh chóng.

**🚀 Hãy áp dụng ngay và tiết kiệm 5+ giờ/lần!**
Nếu có vấn đề, các sếp có thể **comment bên dưới** hoặc liên hệ với tác giả [@vinci-king-01](https://n8n.io/workflows/12781) để hỗ trợ.

---
**💡 Lưu ý cuối cùng:**
- **Self-host n8n** để tránh giới hạn free tier.
- **Backup workflow** định kỳ để tránh mất dữ liệu.
- **Monitor logs** để phát hiện lỗi sớm.