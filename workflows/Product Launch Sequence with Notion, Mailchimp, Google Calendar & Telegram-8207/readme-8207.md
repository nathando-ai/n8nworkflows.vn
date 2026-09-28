---
title: "🚀 **Tự Động Hóa Chuỗi Lên Kênh Sản Phẩm với Notion, Mailchimp, Google Calendar & Telegram** – Giảm 90% Công Việc Quản Lý"
description: "Workflow này tự động hóa toàn bộ quy trình từ lên kế hoạch sản phẩm đến gửi thông báo định kỳ qua Email, Telegram và Google Calendar, giúp các sếp tiết kiệm thời gian và tối ưu hóa chiến dịch marketing."
slug: "tieu-dong-hoa-chuoi-len-kenh-san-pham-notion-mailchimp-google-calendar-telegram"
tags: [n8n, automation, no-code, marketing-automation, notion, google-calendar, telegram-bot, mailchimp]
keywords: [n8n workflow tự động hóa sản phẩm, tự động hóa marketing, tự động hóa lên kênh sản phẩm, tự động hóa Notion Mailchimp, tự động hóa Google Calendar Telegram]
---

# 🚀 **Tự Động Hóa Chuỗi Lên Kênh Sản Phẩm – Từ Lên Kế Hoạch Đến Gửi Thông Báo Định Kỳ**

### **Nỗi Đau Của Các Sếp Khi Lên Kênh Sản Phẩm**
Lên kênh sản phẩm là một trong những công việc tốn thời gian nhất cho các sếp, đặc biệt khi phải:
- **Quản lý nhiều ngày nhớ** (ngày 7, 30, 60) để gửi thông báo cho khách hàng.
- **Tập trung vào nhiều công cụ** (Notion, Mailchimp, Google Calendar, Telegram) mà không có sự đồng bộ.
- **Lo lắng quên gửi thông báo** hoặc gửi sai thời điểm, ảnh hưởng đến trải nghiệm khách hàng.
- **Cần phải làm thủ công** mỗi khi có sản phẩm mới, làm giảm hiệu quả marketing.

Workflow này **giải quyết tất cả những vấn đề trên** bằng cách tự động hóa **toàn bộ chuỗi lên kênh sản phẩm**, từ việc lấy thông tin sản phẩm từ Notion đến gửi thông báo qua Email, Telegram và Google Calendar.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 90% thời gian** quản lý lên kênh sản phẩm.
- **Gửi thông báo chính xác** vào ngày 7, 30 và 60 sau khi sản phẩm lên kênh.
- **Tự động đồng bộ** thông tin từ Notion sang Mailchimp, Google Calendar và Telegram.
- **Không lo quên** vì workflow hoạt động **24/7** mà không cần can thiệp thủ công.
- **Cá nhân hóa thông báo** cho từng khách hàng qua Email và Telegram.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Notion** (để lấy thông tin sản phẩm).
2. **API Key của Notion** (để truy cập dữ liệu).
3. **Tài khoản Mailchimp** (để gửi Email tự động).
4. **Tài khoản Google Calendar** (để thêm sự kiện tự động).
5. **Bot Telegram** (để gửi thông báo nhanh chóng).
6. **Tài khoản Email** (để gửi Email từ Mailchimp).
7. **VPS n8n** (để lưu trữ và chạy workflow 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập vào tài khoản.
2. Nhấn **"Create New Workflow"** và chọn **"Import from JSON"**.
3. Dán JSON từ [link workflow gốc](https://n8n.io/workflows/8207) hoặc tải file JSON từ đó.
4. Nhấn **"Import"** để hoàn tất.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **17 node** và cần cấu hình cẩn thận để hoạt động hiệu quả. Dưới đây là các node quan trọng cần chú ý:

##### **A. Cấu Hình Notion (Query Notion)**
- **Node:** `Query Notion`
- **Cách làm:**
  - Đăng nhập Notion và tạo **Database** để lưu thông tin sản phẩm (ví dụ: tên sản phẩm, ngày lên kênh, mô tả).
  - Trong node `Query Notion`, điền:
    - **URL:** `https://api.notion.com/v1/databases/{DATABASE_ID}/query`
    - **Headers:**
      - `Authorization: Bearer {NOTION_API_KEY}`
      - `Notion-Version: 2022-06-28`
      - `Content-Type: application/json`
    - **Body:**
      ```json
      {
        "filter": {
          "property": "Status",
          "status": {
            "equals": "Published"
          }
        }
      }
      ```
  - **Lưu ý:** Thay `{DATABASE_ID}` và `{NOTION_API_KEY}` bằng thông tin thực tế từ Notion.

##### **B. Cấu Hình Email (Email Day 7, 30, 60)**
- **Node:** `Email Day 7`, `Email Day 30`, `Email Day 60`
- **Cách làm:**
  - Đăng nhập Mailchimp và tạo **List** để lưu địa chỉ Email của khách hàng.
  - Trong node `Email Send`, điền:
    - **From Email:** `noreply@tên-dômin.com`
    - **Subject:** `🚀 Sản phẩm của bạn đã lên kênh! (Ngày 7/30/60)`
    - **Content:** Thay thế bằng nội dung tự động (ví dụ: `Xin chào {Customer Name}, sản phẩm {Product Name} đã chính thức lên kênh!`)
  - **Lưu ý:** Sử dụng **Merge Tags** trong Mailchimp để cá nhân hóa Email.

##### **C. Cấu Hình Google Calendar**
- **Node:** `Google Calendar`
- **Cách làm:**
  - Đăng nhập Google Calendar và tạo **Calendar mới** để lưu sự kiện tự động.
  - Trong node `Google Calendar`, điền:
    - **Calendar ID:** `primary` (hoặc ID Calendar cụ thể).
    - **Event Details:**
      - **Summary:** `Lên kênh: {Product Name}`
      - **Description:** `Sản phẩm đã chính thức lên kênh vào ngày {Date}`
      - **Start Time:** `{{ $node["Get Date"].json["$"].date }}`
  - **Lưu ý:** Đảm bảo **OAuth 2.0** được cấu hình trong n8n để kết nối Google Calendar.

##### **D. Cấu Hình Telegram**
- **Node:** `Telegram Notify`
- **Cách làm:**
  - Tạo **Bot Telegram** và lấy **API Token** từ [@BotFather](https://t.me/BotFather).
  - Trong node `Telegram`, điền:
    - **Chat ID:** ID của chat cá nhân hoặc nhóm (có thể lấy từ [@userinfobot](https://t.me/userinfobot)).
    - **Message:** `🚀 Sản phẩm {Product Name} đã lên kênh! (Ngày {{ $node["Get Date"].json["$"].date }})`
  - **Lưu ý:** Đảm bảo bot được thêm vào chat trước khi chạy workflow.

##### **E. Cấu Hình Webhook (Nếu Sử Dụng)**
- **Node:** `Webhook` và `Respond`
- **Cách làm:**
  - Nếu muốn kích hoạt workflow thủ công, cấu hình **Webhook URL** trong node `Webhook`.
  - Trong node `Respond`, trả về thông báo xác nhận (ví dụ: `Workflow đã được kích hoạt!`).

##### **F. Cấu Hình Schedule Trigger**
- **Node:** `Schedule Trigger`
- **Cách làm:**
  - Chọn **thời gian chạy định kỳ** (ví dụ: hàng ngày lúc 8h sáng).
  - **Lưu ý:** Đảm bảo thời gian này phù hợp với mục tiêu của bạn (ví dụ: gửi Email vào buổi sáng).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run Dữ Liệu Mẫu:**
   - Chạy workflow với **dữ liệu mẫu** từ Notion để kiểm tra các node hoạt động như mong đợi.
   - Kiểm tra Email, Telegram và Google Calendar để đảm bảo thông báo được gửi đúng.
2. **Bật Active Workflow:**
   - Sau khi kiểm tra thành công, chuyển workflow sang **Active** để nó chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**CÁC Ý TƯỞNG MỞ RỘNG**]
1. **Kết Nối Slack:**
   - Thêm node `Slack` để gửi thông báo lên kênh Slack của công ty.
2. **Lưu Log:**
   - Sử dụng node `Set` hoặc `Sticky Note` để lưu lịch sử hoạt động của workflow.
3. **Gửi Báo Cáo Định Kỳ:**
   - Tạo một workflow phụ để tổng hợp và gửi báo cáo lên Notion hoặc Google Sheets.
4. **Cá Nhân Hóa Thông Báo:**
   - Sử dụng **AI (LLM)** trong node `Code` để tự động tạo nội dung Email/Telegram phù hợp với từng khách hàng.
5. **Kết Nối với Shopify:**
   - Nếu sản phẩm bán trên Shopify, lấy thông tin từ API Shopify và đồng bộ vào Notion.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc quản lý lên kênh sản phẩm thủ công, đồng thời **tăng cường trải nghiệm khách hàng** bằng cách gửi thông báo chính xác và cá nhân hóa. **Hãy tự động hóa ngay hôm nay** và tập trung vào những việc quan trọng hơn!

👉 **Bắt đầu ngay:** [Tải workflow từ n8n.io](https://n8n.io/workflows/8207) và cài đặt trên VPS của bạn!

---
**Chúc các sếp thành công với tự động hóa!** 🚀