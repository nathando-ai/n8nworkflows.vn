---
title: "🚀 Tự Động Hoàn Thành Lead Từ Google Maps + Tìm Email Tự Động Với Apify & Anymailfinder (N8N)"
description: "Workflow này tự động scrape thông tin từ Google Maps, tìm kiếm email liên hệ cho từng doanh nghiệp, và lưu trữ dữ liệu sạch vào NocoDB – tiết kiệm 10+ giờ công mỗi tháng cho bộ phận marketing. Hỗ trợ tự động hóa lead generation 24/7 mà không cần code."
slug: "tieu-dong-hoan-thanh-lead-tu-google-maps"
tags: [n8n, automation, lead-generation, scraping, apify, anymailfinder, nocoDB]
keywords: [n8n workflow scrape google maps, tự động tìm email từ google maps, lead generation tự động, apify n8n, anymailfinder api]
---

# 🚀 **Tự Động Hoàn Thành Lead Từ Google Maps + Tìm Email Tự Động Với Apify & Anymailfinder**

## **🔍 Nỗi Đau Của Các Sếp: Tìm Lead Từ Google Maps Làm Thủ Công?**
Bạn có bao giờ phải:
- **Tìm kiếm thủ công** trên Google Maps để lấy thông tin doanh nghiệp?
- **Gõ email liên hệ** cho từng lead một cách mệt mỏi?
- **Lưu trữ dữ liệu** vào Excel hay Google Sheets, rồi loay hoay tìm kiếm?
- **Bị mất thời gian** vì email không chính xác hoặc trùng lặp?

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Scrape** thông tin từ Google Maps (tên, địa chỉ, số điện thoại, website...)
✅ **Tìm kiếm email** cho từng doanh nghiệp bằng Anymailfinder
✅ **Lọc bỏ trùng lặp** và **sạch dữ liệu** (xóa URL sai, định dạng không chuẩn)
✅ **Lưu trữ vào NocoDB** (hoặc cơ sở dữ liệu khác) để dễ dàng quản lý
✅ **Hoạt động 24/7** mà không cần can thiệp của bạn

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** cho bộ phận marketing/sales.
- **Dữ liệu lead chính xác** (email, website, địa chỉ) được tự động cập nhật.
- **Không bị trùng lặp** nhờ cơ chế kiểm tra trước khi lưu.
- **Hoạt động liên tục** (self-hosted trên VPS) mà không cần can thiệp.
- **Dễ dàng mở rộng** (thêm Slack/Telegram báo cáo, gửi email tự động...).
:::

---
## **🔧 Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Apify** (để scrape Google Maps):
   - [Đăng ký miễn phí tại Apify](https://www.apify.com) (hoặc dùng [mã giới thiệu](https://www.apify.com?fpr=g5q0f) của tác giả).
   - **API Token Apify**: Tạo tại [Apify Console](https://console.apify.com/actors/nwua9Gu5YrADL7ZDj/input).

✔ **Tài khoản Anymailfinder** (để tìm email):
   - [Đăng ký tại Anymailfinder](https://anymailfinder.com?via=alexandra) (dùng mã giới thiệu để giảm giá).
   - **API Key Anymailfinder**: Tìm trong tài khoản của bạn.

✔ **Tài khoản NocoDB** (để lưu trữ dữ liệu):
   - [Đăng ký NocoDB](https://noco.db) (hoặc self-hosted).
   - **API Token NocoDB**: Tạo trong cài đặt tài khoản.

✔ **VPS cho n8n** (không thể chạy trên n8n.cloud vì giới hạn API call):
   - 👉 [Đăng ký VPS TinoHost (giảm 39%)](https://tino.vn/vps-n8n?affid=388) (mã giảm: **VPSN8N**).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/8472](https://n8n.io/workflows/8472).
2. **Mở n8n Editor** trên VPS của bạn.
3. **Nhấp vào "Import"** → Chọn file JSON vừa tải.
4. **Chọn "Import"** để hoàn tất.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải JSON** từ link trên.
2. **Mở n8n Editor** → Nhấp vào **"Import"** → Chọn **"Paste JSON"**.
3. **Dán JSON** và nhấn **"Import"**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 Node "Scrape Google Maps" (HTTP Request)**
- **Tham số cần thiết**:
  - **URL**: `https://console.apify.com/actors/nwua9Gu5YrADL7ZDj/calls?token={API_TOKEN_APIFY}`
    - Thay `{API_TOKEN_APIFY}` bằng **API Token** của bạn từ Apify.
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer {API_TOKEN_APIFY}",
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "input": {
        "searchTerm": "keyword", // Thay bằng từ khóa tìm kiếm (vd: "cửa hàng café Hà Nội")
        "maxItems": 50, // Số lead muốn scrape
        "country": "VN" // Mã quốc gia (VN cho Việt Nam)
      }
    }
    ```

#### **🔹 Node "Get Emails" (HTTP Request)**
- **Tham số cần thiết**:
  - **URL**: `https://api.anymailfinder.com/v1/emails`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer {API_KEY_ANYMAILFINDER}",
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "domain": "{{$json['website']}}", // Lấy từ dữ liệu scrape (vd: "cafevietnam.com")
      "limit": 1
    }
    ```

#### **🔹 Node "Clean Data" (Code)**
- **Mã JavaScript cần chỉnh**:
  ```javascript
  // Xóa URL không chuẩn và định dạng lại dữ liệu
  $input.all().forEach(item => {
    if (item.website) {
      item.website = item.website.replace(/^https?:\/\//, ''); // Xóa http:// hoặc https://
    }
    if (item.phone) {
      item.phone = item.phone.replace(/\D/g, ''); // Lọc chỉ số điện thoại (vd: "0323456789")
    }
  });
  return $input;
  ```

#### **🔹 Node "Avoid duplicates" (Code)**
- **Mã JavaScript kiểm tra trùng lặp**:
  ```javascript
  // Kiểm tra trước khi lưu vào NocoDB
  const existingItems = await $node["Get all the recorded placeIds"].execute();
  const existingIds = existingItems.json().map(item => item.placeId);

  return $input.filter(item => !existingIds.includes(item.placeId));
  ```

#### **🔹 Node "Create a row" (NocoDB)**
- **Tham số cần thiết**:
  - **Database URL**: `https://your-nocodb-url.noco.db` (thay bằng URL của bạn).
  - **Table Name**: Chọn bảng muốn lưu (vd: "Leads").
  - **Data**:
    ```json
    {
      "placeId": "{{$json['placeId']}}",
      "name": "{{$json['name']}}",
      "address": "{{$json['address']}}",
      "phone": "{{$json['phone']}}",
      "website": "{{$json['website']}}",
      "email": "{{$json['email']}}"
    }
    ```

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhập từ khóa tìm kiếm (vd: "cửa hàng café Hà Nội") vào **Form Trigger**.
   - Chạy workflow và kiểm tra **NocoDB** xem dữ liệu có được lưu đúng không.
2. **Bật Active**:
   - Nhấp vào nút **"Active"** ở góc trên bên phải.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **🔹 Thêm Giao Tiếp Slack/Telegram**
- **Sử dụng node Slack/Telegram** để báo cáo khi có lead mới:
  ```json
  {
    "text": "🚀 Lead mới được scrape:\n📍 {{$json['name']}}\n📧 {{$json['email']}}\n🌐 {{$json['website']}}"
  }
  ```

### **🔹 Gửi Email Tự Động**
- **Kết hợp với node Email (SendGrid/Mailgun)** để gửi tin nhắn chào hàng:
  ```json
  {
    "to": "{{$json['email']}}",
    "subject": "Chào mừng từ {{$json['name']}}!",
    "html": "<p>Xin chào, chúng tôi là {{$json['name']}} và muốn hợp tác với bạn!</p>"
  }
  ```

### **🔹 Lưu Log Dữ Liệu**
- **Sử dụng node "Set"** để lưu log vào Google Sheets/Excel:
  ```json
  {
    "sheetName": "Logs",
    "data": {
      "Timestamp": new Date().toISOString(),
      "Lead": "{{$json['name']}}",
      "Status": "Success"
    }
  }
  ```

### **🔹 Tự Động Cập Nhật Định Kỳ**
- **Sử dụng node "Schedule"** (n8n Pro) để chạy workflow hàng ngày/tuần:
  ```json
  {
    "cron": "0 0 * * *" // Chạy hàng ngày lúc 00:00
  }
  ```

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc scrape lead thủ công, đồng thời **tăng chất lượng dữ liệu** nhờ tự động tìm email và lọc trùng lặp. **Chỉ cần 10 phút setup**, bạn đã có một hệ thống **lead generation tự động 24/7**!

👉 **Bắt đầu ngay bằng cách:**
1. **Đăng ký VPS** (n8n + Apify + Anymailfinder).
2. **Import workflow** và cấu hình API keys.
3. **Chạy test** và **bật Active**!

**Cần hỗ trợ?** Đăng ký **consultation** với tác giả [Alexandra Spalato](https://n8n.io/workflows/8472) để tối ưu workflow cho doanh nghiệp của bạn!

---
**💡 Lời khuyên cuối cùng:**
Nếu workflow này quá phức tạp, các sếp có thể **tách nhỏ** thành các bước đơn giản hơn (vd: scrape Google Maps → lưu vào NocoDB, sau đó tìm email). **Tự động hóa từng bước một** để dễ dàng debug!