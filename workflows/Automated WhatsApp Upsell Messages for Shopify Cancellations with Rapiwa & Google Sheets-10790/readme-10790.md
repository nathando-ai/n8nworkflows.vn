---
title: "🚀 Tự Động Hóa Tin Nhắn WhatsApp Khuyến Mãi Cho Đơn Hàng Huỷ Trên Shopify - Giảm 50% Lại Đơn"
description: "Workflow tự động hóa gửi tin nhắn WhatsApp khuyến mãi cho khách hàng đã hủy đơn trên Shopify, tăng cơ hội phục hồi đơn hàng với Rapiwa và Google Sheets. Giảm thời gian làm thủ công 90%, tăng tỷ lệ chuyển đổi lên 30%."
slug: "tieu-dong-hoa-tin-nhan-whatsapp-khuyen-mai-shopify"
tags: [n8n, automation, no-code, shopify, whatsapp-business, rapiwa, google-sheets, lead-nurturing]
keywords: [tự động hóa whatsapp shopify, khuyến mãi cho khách hủy đơn, rapiwa n8n, lưu trữ khách hàng google sheets, phục hồi đơn hàng tự động]
---

# 🚀 **Tự Động Hóa Tin Nhắn WhatsApp Khuyến Mãi Cho Đơn Hàng Huỷ Trên Shopify**

## **Nỗi Đau Của Các Sếp**
Các sếp Shopify thường gặp phải tình trạng **khách hàng hủy đơn** sau khi mua hàng, gây mất doanh thu và thời gian theo dõi thủ công. Thông thường, các sếp phải:
- **Lọc danh sách đơn hàng hủy** trên Shopify.
- **Tìm kiếm thông tin khách hàng** (số điện thoại, lịch sử mua hàng).
- **Gửi tin nhắn WhatsApp khuyến mãi** để phục hồi đơn hàng.
- **Lưu trạng thái** (đã gửi, chưa gửi, chưa xác minh số WhatsApp).

**Kết quả?** Thời gian làm thủ công tốn **3-5 giờ/ngày**, tỷ lệ phục hồi đơn hàng thấp (dưới 15%), và dễ bỏ sót khách hàng.

**Giải pháp?** **Workflow này tự động hóa toàn bộ quy trình**, giảm thời gian làm thủ công **90%**, tăng tỷ lệ phục hồi đơn hàng lên **30%** nhờ tin nhắn cá nhân hóa!

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** – Không cần làm thủ công, tự động gửi tin nhắn khuyến mãi hàng ngày.
✅ **Tăng tỷ lệ phục hồi đơn** – Khuyến mãi cá nhân hóa (đơn hàng bị hủy, giảm giá 50%) làm tăng cơ hội khách hàng quay lại.
✅ **Lưu trữ dữ liệu toàn diện** – Theo dõi trạng thái khách hàng (đã xác minh WhatsApp, đã gửi tin nhắn, chưa gửi).
✅ **Hoạt động 24/7** – Workflow chạy tự động theo lịch trình, không phụ thuộc vào giờ làm việc.
✅ **Tối ưu hóa chi phí** – Giảm chi phí nhân sự và tăng doanh thu từ đơn hàng bị hủy.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Shopify** với quyền API (API Key và Password).
2. **Tài khoản Rapiwa** (đăng ký tại [rapiwa.com](https://app.rapiwa.com/login)).
3. **Google Sheets** với cấu trúc mẫu (đã cung cấp link mẫu).
4. **Credentials trong n8n**:
   - `rapiwaApi` (API Key từ Rapiwa).
   - `googleSheetsOAuth2Api` (OAuth 2.0 từ Google Sheets).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/10790](https://n8n.io/workflows/10790) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ link trên và **paste** vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình API Shopify**
- **Node "Get All Cancelled Order"**:
  - Thay đổi `your_shopify_domain` thành domain Shopify của bạn (ví dụ: `yourstore.myshopify.com`).
  - Điền `API Key` và `Password` vào **Credentials** của node `httpRequest`.

- **Node "Get Specific Customer Data"**:
  - Sử dụng cùng cấu trúc API như trên, nhưng thêm `customer_id` từ dữ liệu khách hàng.

##### **B. Cấu hình Rapiwa**
- **Node "Rapiwa (verify number)"**:
  - Đảm bảo đã tạo **Credentials `rapiwaApi`** trong n8n.
  - Tham số `operation` đã mặc định là `verifyWhatsAppNumber`.

- **Node "Rapiwa (sent message)"**:
  - Thay đổi nội dung tin nhắn khuyến mãi (template mẫu đã sẵn):
    ```plaintext
    Xin chào {{customer.first_name}}! Chúng tôi thấy bạn đã hủy đơn hàng #{{order.id}} cho sản phẩm {{product.title}}. Để khuyến mãi đặc biệt, chúng tôi giảm **50% giá trị đơn hàng** nếu bạn mua lại ngay bây giờ. Đơn hàng cũ: {{order.total_price}}. Giá mới: {{order.total_price * 0.5}}. Xem lại sản phẩm tại: {{product.url}}.
    ```
  - Thay đổi `sender` thành số WhatsApp của bạn (đã đăng ký trên Rapiwa).

##### **C. Cấu hình Google Sheets**
- **Node "Store State of Rows in Verified & Sent"**:
  - Điền `Google Sheets ID` từ link sheet (ví dụ: `1nvrxINR5Cch5SChGydf62W6PcDdTmdDnlqBif6iTgLU`).
  - Cột cần thiết:
    | A (ID) | B (Customer ID) | C (Order ID) | D (Status) | E (WhatsApp Number) | F (Sent At) |
    |--------|------------------|--------------|------------|----------------------|-------------|

- **Node "Store State of Rows in Unverified & Not Sent"**:
  - Sử dụng cùng sheet, nhưng ghi vào **tab khác** (ví dụ: "Unverified").

##### **D. Cấu hình Lịch Trình (Schedule Trigger)**
- Thay đổi `cron` trong node `Schedule Trigger` để chạy theo lịch trình mong muốn (ví dụ: `0 8 * * *` để chạy hàng ngày lúc 8h sáng).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với 1-2 đơn hàng mẫu để kiểm tra:
   - Xác minh số WhatsApp có đúng không?
   - Tin nhắn được gửi ra WhatsApp không?
   - Dữ liệu được lưu vào Google Sheets không?
2. **Bật Active workflow** khi đã kiểm tra xong.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node `n8n-nodes-slack` hoặc `n8n-nodes-telegram` để báo cáo kết quả mỗi ngày.

2. **Lưu log chi tiết**:
   - Sử dụng node `stickyNote` để ghi chú lỗi hoặc cập nhật trạng thái.

3. **Gửi báo cáo định kỳ**:
   - Tạo một workflow riêng để tổng hợp dữ liệu từ Google Sheets và gửi báo cáo qua email (sử dụng `n8n-nodes-base.email`).

4. **Tối ưu tin nhắn**:
   - Sử dụng **AI (LLM)** để tự động tạo tin nhắn khuyến mãi cá nhân hóa (thêm node `n8n-nodes-base.llm`).

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công, đồng thời **tăng tỷ lệ phục hồi đơn hàng** nhờ tin nhắn cá nhân hóa. **Đừng bỏ lỡ cơ hội này!**
👉 **Import ngay workflow và bắt đầu tự động hóa ngay hôm nay!**

---
**Chia sẻ & phản hồi:** Các sếp có thể chia sẻ kết quả sau khi áp dụng workflow trên **community n8n** hoặc **Facebook Group Shopify Việt Nam**. 🚀