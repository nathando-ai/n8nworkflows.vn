---
title: "🚀 Tự Động Hồi Sinh Khách Hàng Shopify Đang Hoạt Động Nhờ Beex - Giảm 70% Thời Gian Tiếp Thị"
description: "Workflow tự động hóa 100% không code để phát hiện và tái kết nối khách hàng Shopify không hoạt động trong 30 ngày, tự động tạo leads trong Beex với dữ liệu chi tiết sản phẩm và lịch sử mua hàng."
slug: "tieu-dong-hoi-sinh-khach-hang-shopify-beex"
tags: [n8n, automation, shopify, beex, no-code, marketing-automation, ecommerce]
keywords: [tự động hóa shopify, tái kết nối khách hàng, beex automation, workflow n8n shopify, giảm thiểu khách hàng rời đi, tự động hóa tiếp thị]
---

# 🚀 **Tự Động Hồi Sinh Khách Hàng Shopify Đang Hoạt Động Nhờ Beex**

### **Giải pháp nào giúp các sếp:**
- **Tiết kiệm 10-15 giờ/tháng** trong việc theo dõi và tái kết nối khách hàng không hoạt động?
- **Tăng tỷ lệ tái mua** lên 20-30% nhờ gửi thông báo cá nhân hóa đến khách hàng cũ?
- **Tự động hóa toàn bộ quy trình** từ Shopify đến Beex mà không cần viết một dòng code?

Nếu câu trả lời là **Có**, thì workflow này chính là giải pháp hoàn hảo cho các sếp kinh doanh Shopify!

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tái kết nối khách hàng cũ** trong vòng 24h sau khi phát hiện họ không hoạt động.
- **Tự động tạo leads trong Beex** với thông tin chi tiết về sản phẩm và lịch sử mua hàng.
- **Tiết kiệm chi phí tiếp thị** bằng cách tập trung vào khách hàng có tiềm năng cao.
- **Hoạt động 24/7** nhờ tự động hóa, không cần can thiệp thủ công.
- **Tăng doanh thu** từ khách hàng cũ với tỷ lệ tái mua cao hơn.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
- **Tài khoản Shopify** với **API Access Token** (Shopify Access Token API).
- **Tài khoản Beex** và **Bearer Token** để tạo leads.
- **N8n Self-hosted** (không thể chạy trên n8n.cloud vì sử dụng node `n8n-nodes-beex`).
- **Dữ liệu sản phẩm** trong Shopify để phân tích hành vi mua hàng.
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Bước 1:** Tải file JSON từ [n8n.io/workflows/9160](https://n8n.io/workflows/9160) hoặc copy toàn bộ JSON từ link này.
- **Bước 2:** Mở **n8n Editor** và chọn **Import Workflow** → Dán JSON hoặc tải file JSON.
- **Bước 3:** Chọn **Active** để kích hoạt workflow.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **12 node** và cần cấu hình chi tiết như sau:

#### **🔹 Node 1: Schedule Trigger (Khởi động định kỳ)**
- **Cấu hình:**
  - Thời gian chạy: **Mỗi tháng 1 lần** (hoặc tùy chỉnh theo nhu cầu).
  - Ví dụ: Chạy vào ngày **15/01, 15/02, 15/03** để theo dõi khách hàng không mua hàng trong **30 ngày**.

#### **🔹 Node 2: Shopify (Lấy danh sách khách hàng)**
- **Cấu hình:**
  - **Credentials:** Chọn `shopifyAccessTokenApi`.
  - **Operation:** `get` (lấy tất cả khách hàng).
  - **Lưu ý:** Nếu store có nhiều khách hàng, có thể cần phân trang (`limit=100`).

#### **🔹 Node 3: Filter by Days (Lọc khách hàng không hoạt động)**
- **Cấu hình:**
  - **Điều kiện:** Loại bỏ khách hàng có `last_order_id = null` (không mua hàng trong thời gian định).
  - **Số ngày inactivity:** Cần **cấu hình trong Node 7 (Calculate Days)**.

#### **🔹 Node 4: Calculate Days (Tính ngày không hoạt động)**
- **Cấu hình:**
  - **Operation:** `getTimeBetweenDates`.
  - **Input:**
    - `date1`: `{{ $node["1. Shopify"].json["last_order_date"] }}` (ngày cuối cùng mua hàng).
    - `date2`: `{{ $node["Schedule Trigger"].json["$dateTimeTrigger"] }}` (ngày hiện tại).
  - **Lọc khách hàng:** Chỉ giữ khách hàng có `days > 30` (hoặc số ngày tùy chỉnh).

#### **🔹 Node 5: Extract Customer Data (Trích xuất thông tin khách hàng)**
- **Cấu hình:**
  - **Set:** Trích xuất trường cần thiết như `customer_id`, `email`, `first_name`, `last_name`.

#### **🔹 Node 6: Extract Product Data (Trích xuất thông tin sản phẩm)**
- **Cấu hình:**
  - **Operation:** `get` trên `product` với `customer_id` từ Node 5.
  - **Lưu ý:** Nếu khách hàng mua nhiều sản phẩm, có thể cần **Split Out** để xử lý từng sản phẩm riêng.

#### **🔹 Node 7: Merge Data (Gộp dữ liệu khách hàng & sản phẩm)**
- **Cấu hình:**
  - **Combine By Position** để kết hợp thông tin khách hàng và sản phẩm.

#### **🔹 Node 8: Create Lead (Tạo leads trong Beex)**
- **Cấu hình:**
  - **Credentials:** Chọn `beexBearerToken` (Bearer Token từ Beex).
  - **Resource:** `leads`.
  - **Mapping trường:**
    - `email` → `email` (Beex).
    - `first_name` → `first_name` (Beex).
    - `last_name` → `last_name` (Beex).
    - `product_purchased` → `custom_field` (thêm vào Beex để phân tích hành vi).
    - `days_since_last_purchase` → `custom_field` (thời gian inactivity).

---

### **3. Kích hoạt ⚡️**
- **Bước 1:** **Test Run** với dữ liệu mẫu để kiểm tra logic.
- **Bước 2:** Chọn **Active** để workflow chạy tự động theo lịch trình.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[NHỮNG Ý TƯỞNG TIẾP THEO]
- **Gửi thông báo cá nhân hóa:** Sử dụng **Beex** để gửi email/WhatsApp với nội dung như:
  > *"Chào [Tên Khách Hàng], chúng tôi thấy bạn đã lâu không mua hàng. Đây là sản phẩm mới nhất mà bạn từng quan tâm: [Sản Phẩm]. Đăng ký ngay để nhận 10% giảm giá!"*
- **Lưu log hoạt động:** Sử dụng **Sticky Note** trong n8n để ghi lại khách hàng đã được tái kết nối.
- **Tích hợp Slack/Telegram:** Khi workflow chạy, gửi thông báo đến nhóm quản lý để theo dõi.
- **Tùy chỉnh ngưỡng inactivity:** Thay đổi từ **30 ngày** thành **60 ngày** nếu khách hàng của bạn có chu kỳ mua hàng dài.
- **Tạo báo cáo định kỳ:** Sử dụng **Google Sheets** hoặc **Airtable** để lưu trữ danh sách khách hàng tái kết nối.
:::

---

## 📌 **Kết luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn quy trình tái kết nối khách hàng Shopify**, tiết kiệm thời gian và tăng tỷ lệ tái mua. **Chỉ cần cài đặt 1 lần**, workflow sẽ hoạt động 24/7, giúp doanh nghiệp **không bỏ lỡ bất kỳ khách hàng nào**.

:::success[🚀 **Hành động ngay!**]
1. **Cài đặt n8n Self-hosted** trên VPS (để sử dụng node Beex).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Chạy thử** và theo dõi kết quả!
:::

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::