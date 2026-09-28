---
title: "🛒 **Hồi phục giỏ hàng bỏ quên Shopify với Email, SMS, WhatsApp & Quảng cáo Facebook Tự động - Không Cần Code!**"
description: "Workflow này tự động hồi phục đến 90% giỏ hàng bỏ quên Shopify bằng chuỗi hành động đa kênh (Email → SMS → WhatsApp) và quảng cáo Facebook retargeting. Giúp doanh nghiệp tăng doanh thu lên 20-30% mà không cần viết một dòng code nào!"
slug: "hui-phuc-gio-hang-bo-quen-shopify-email-sms-whatsapp-facebook"
tags: [n8n, automation, shopify, ecommerce, lead-nurturing, no-code, retargeting]
keywords: [n8n workflow shopify, tự động hóa hồi phục giỏ hàng, email marketing tự động, SMS marketing, quảng cáo facebook retargeting, tăng doanh thu shopify]
---

# 🚀 **Hồi phục giỏ hàng bỏ quên Shopify với Email, SMS, WhatsApp & Quảng cáo Facebook - Tự động hóa 100%**

## **💥 Nỗi đau của các sếp Shopify**
Bạn đã từng mất hàng chục triệu đồng mỗi năm vì khách hàng bỏ giỏ hàng? Theo thống kê, **trung bình 70% khách hàng bỏ giỏ hàng** nhưng chỉ **1-2%** sẽ quay lại mua nếu không có hành động hồi phục. Với workflow này, các sếp sẽ:
✅ **Hồi phục 70-90% giỏ hàng bỏ quên** chỉ trong 48 giờ
✅ **Tăng doanh thu lên 20-30%** mà không cần quảng cáo mới
✅ **Tự động hóa toàn bộ quy trình** từ Email → SMS → WhatsApp → Facebook Retargeting
✅ **Lưu trữ tất cả hành động** để phân tích hiệu quả (multi-touch attribution)

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Không cần theo dõi từng giỏ hàng thủ công
- **Tăng tỷ lệ hoàn thành đơn hàng**: Từ 70% → 90%+ với chiến lược đa kênh
- **Cá nhân hóa hoàn toàn**: Email/SMS/WhatsApp được tạo động dựa trên hành vi mua hàng trước đó
- **Quảng cáo Facebook tự động**: Chỉnh sửa audience retargeting một cách thông minh
- **Báo cáo chi tiết**: Theo dõi từng hành động (Email, SMS, WhatsApp) trong Google Sheets
- **Thông báo Slack**: Nhận cảnh báo khi có giỏ hàng giá trị cao được hồi phục
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Các sếp cần chuẩn bị các tài khoản và thông tin sau để workflow hoạt động:
1. **Shopify Store**:
   - API Key và Password (tạo trong **Settings → Apps → API**)
   - Domain Shopify (ví dụ: `tudong.vn`)

2. **Email Marketing**:
   - **SendGrid** (hoặc Mailgun/Postmark) với API Key
   - Email template chuẩn (có thể sử dụng **Shopify Email Templates** hoặc **Mailchimp**)

3. **SMS Marketing**:
   - **Twilio** với Account SID và Auth Token
   - Số điện thoại của khách hàng (cần được đồng ý theo GDPR)

4. **WhatsApp Business**:
   - **Meta Business Suite** (cài đặt WhatsApp Business API)
   - Phone Number ID và Access Token

5. **Quảng cáo Facebook**:
   - **Facebook Graph API** với Access Token (tạo trong **Meta Business Suite**)
   - Pixel ID và Audience Manager

6. **Lưu trữ dữ liệu**:
   - **Google Sheets** với Sheet ID và quyền chỉnh sửa
   - Sheet có cột: `Customer ID`, `Cart ID`, `Touchpoint Type`, `Timestamp`, `Status`

7. **Thông báo**:
   - **Slack Webhook URL** (để nhận cảnh báo giỏ hàng giá trị cao)

8. **Cấu hình bổ sung**:
   - **Ngưỡng giá trị giỏ hàng** (ví dụ: >500k sẽ được ưu tiên)
   - **URL Checkout** (cần phải là URL an toàn HTTPS)
   - **Mã giảm giá** (ví dụ: `DISCOUNT10` với 10% off)
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. **Tải file JSON** từ [n8n.io/workflows/11805](https://n8n.io/workflows/11805)
2. **Mở n8n Editor** → Nhấn **Import** → Chọn file JSON
3. **Hoặc copy toàn bộ JSON** vào **Import Workflow** trong n8n

:::note[**Lưu ý quan trọng**]
- **Không sử dụng phiên bản n8n Community** (cần **n8n Enterprise** hoặc **Self-hosted** để hỗ trợ nhiều node)
- **Không thay đổi cấu trúc node** nếu không hiểu rõ logic
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 1. Cấu hình Webhook (Abandoned Cart Webhook)**
- **Path**: `/abandoned-cart`
- **HTTP Method**: `POST`
- **URL Webhook** của Shopify:
  - Tạo trong **Shopify Admin → Settings → Notifications → Order Status Changes**
  - Chọn **Abandoned Cart** và nhập URL webhook từ n8n (ví dụ: `https://tudong.vn/n8n/webhook/abandoned-cart`)

#### **🔹 2. Workflow Configuration (Cấu hình toàn cầu)**
- **Shopify Domain**: `https://tudong.myshopify.com`
- **Checkout URL**: `https://tudong.myshopify.com/checkout`
- **Discount Code**: `DISCOUNT10` (10% off)
- **High-Value Threshold**: `500000` (giá trị giỏ hàng >500k sẽ được ưu tiên)
- **Google Sheets ID**: `1AbCdEfGhIjKlMnOpQrStUvWxYz` (Sheet dùng để lưu log)

#### **🔹 3. SendGrid (Gửi Email)**
- **API Key**: Tạo trong **SendGrid → Settings → API Keys**
- **From Email**: `no-reply@tudong.vn`
- **Template**: Sử dụng **Shopify Email Template** hoặc tạo mới trong SendGrid

#### **🔹 4. Twilio (Gửi SMS)**
- **Account SID**: Tạo trong **Twilio Console → Account SID**
- **Auth Token**: Tạo trong **Twilio Console → Auth Tokens**
- **From Number**: Số điện thoại Twilio (ví dụ: `+1234567890`)

#### **🔹 5. WhatsApp Business**
- **Phone Number ID**: Tạo trong **Meta Business Suite → WhatsApp Business API**
- **Access Token**: Tạo trong **Meta Developer → Tokens**

#### **🔹 6. Facebook Graph API**
- **Access Token**: Tạo trong **Meta Developer → Tokens** (chọn quyền `ads_management`, `pages_read_engagement`)
- **Pixel ID**: Tạo trong **Facebook Pixel Manager**

#### **🔹 7. Google Sheets**
- **Sheet ID**: `1AbCdEfGhIjKlMnOpQrStUvWxYz`
- **Sheet Name**: `Touchpoints`
- **Cột cần có**:
  - `Customer ID` (ID khách hàng Shopify)
  - `Cart ID` (ID giỏ hàng)
  - `Touchpoint Type` (Email/SMS/WhatsApp)
  - `Timestamp` (thời gian gửi)
  - `Status` (Recovered/Not Recovered)

#### **🔹 8. Slack Notification**
- **Webhook URL**: Tạo trong **Slack → Apps → Create App → Incoming Webhooks**

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với một giỏ hàng mẫu:
   - Gửi một giỏ hàng bỏ quên giả vào webhook Shopify
   - Kiểm tra các Email/SMS/WhatsApp có được gửi không
   - Xem log trong Google Sheets

2. **Bật Active Workflow**:
   - Nhấn **Active** trên n8n Editor
   - Kiểm tra **Execution Logs** để đảm bảo không có lỗi

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **🔹 1. Tối ưu hóa Email & SMS**
- **A/B Testing**: Thay đổi tiêu đề Email/SMS để tìm nội dung hiệu quả nhất
- **Personalization**: Sử dụng **n8n Code Node** để động thái tên khách hàng trong Email
  ```javascript
  // Ví dụ trong "Generate Email 1 Content":
  const emailSubject = `🚨 Đừng bỏ quên giỏ hàng của bạn, ${customer.firstName}!`;
  ```

### **🔹 2. Lọc giỏ hàng giá trị cao**
- **Thêm điều kiện lọc** trong `Check Cart Value Threshold`:
  ```javascript
  // Ví dụ: Chỉ hồi phục giỏ hàng >300k
  if (cart.total_price > 300000) {
    return true;
  } else {
    return false;
  }
  ```

### **🔹 3. Log & Báo cáo tự động**
- **Tạo Dashboard Google Data Studio** từ Google Sheets để theo dõi:
  - Tỷ lệ hồi phục giỏ hàng
  - Thời gian trung bình hồi phục
  - Doanh thu từ giỏ hàng hồi phục

### **🔹 4. Kết hợp với CRM**
- **Gửi dữ liệu vào HubSpot/ActiveCampaign** khi giỏ hàng được hồi phục
- **Tạo Task tự động** trong CRM để nhân viên theo dõi khách hàng

### **🔹 5. WhatsApp Business Advanced**
- **Sử dụng Rich Media** trong WhatsApp (ảnh sản phẩm, video)
- **Chatbot tự động** để trả lời khách hàng khi họ phản hồi

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để hồi phục giỏ hàng bỏ quên một cách **tự động hóa 100%**, không cần viết code. Với **Email → SMS → WhatsApp → Facebook Retargeting**, các sếp sẽ:
✔ **Tăng doanh thu lên 20-30%** chỉ trong 48 giờ
✔ **Tiết kiệm thời gian** so với cách làm thủ công
✔ **Cá nhân hóa hoàn toàn** từng khách hàng
✔ **Lưu trữ dữ liệu** để phân tích hiệu quả

**🚀 Hãy áp dụng ngay hôm nay!**
:::tip[**Lời khuyên cuối cùng**]
- **Test với giỏ hàng mẫu** trước khi bật cho toàn bộ store
- **Monitor Execution Logs** để phát hiện lỗi sớm
- **Tối ưu hóa nội dung Email/SMS** dựa trên dữ liệu thực tế
:::

---
:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Bắt đầu tự động hóa ngay hôm nay!** 🚀