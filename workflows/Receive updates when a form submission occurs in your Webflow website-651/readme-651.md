---
title: "🚀 Tự Động Nhận Thông Báo Khi Có Giao Diện Trên Website Webflow (Không Cần Code)"
description: "Workflow tự động hóa nhận thông báo tức thời khi có giao diện mới trên trang Webflow, giúp các sếp tiết kiệm thời gian theo dõi thủ công và không bỏ lỡ bất kỳ cơ hội nào."
slug: "tu-dong-nhan-thong-bao-webflow-form-submission"
tags: [n8n, automation, marketing, webflow, no-code]
keywords: [n8n workflow webflow, tự động hóa webflow, nhận thông báo form submission, marketing automation]
---

# 🚀 **Tự Động Nhận Thông Báo Khi Có Giao Diện Trên Website Webflow**

### **Nỗi Đau Của Các Sếp**
Các sếp thường phải **thủ công theo dõi** các form submission trên trang Webflow, mất thời gian quét email hoặc vào trang quản lý để kiểm tra. Điều này không chỉ **tốn công sức** mà còn **rất dễ bỏ lỡ** những cơ hội quan trọng như yêu cầu từ khách hàng, đăng ký dịch vụ hoặc phản hồi từ người dùng.

**Workflow này giải quyết vấn đề đó bằng cách:**
✅ **Tự động nhận thông báo tức thời** khi có giao diện mới trên Webflow.
✅ **Không cần code** – chỉ cần cấu hình đơn giản.
✅ **Hoạt động 24/7** – không phụ thuộc vào thời gian làm việc của bạn.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian** lên đến **50%** trong việc theo dõi form submission.
- **Không bỏ lỡ bất kỳ giao diện nào**, đảm bảo phản hồi nhanh chóng.
- **Tự động hóa hoàn toàn**, không cần can thiệp thủ công.
- **Dễ dàng mở rộng** để kết nối với Slack, Email hoặc các hệ thống khác.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
- **Tài khoản Webflow** với quyền quản trị (để kết nối API).
- **API Key OAuth2** của Webflow (cần tạo trong **Settings > API Keys**).
- **n8n Self-hosted** (để workflow hoạt động liên tục 24/7).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Workflow này **chỉ có 1 node** (`webflowTrigger`), nhưng vẫn cần cấu hình chính xác để hoạt động.

**Bước 1:** Tải file JSON từ [n8n.io/workflows/651](https://n8n.io/workflows/651) hoặc copy toàn bộ JSON dưới đây vào **n8n Editor**.

**Bước 2:** Nhấn **Import Workflow** và chọn file JSON đã tải.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
:::warning[CẦN CHỈNH TRƯỚC KHI KÍCH HOẠT]
- **Node: Webflow Trigger**
  - **Credentials:** Chọn `webflowOAuth2Api` (nếu chưa tạo, tham khảo [hướng dẫn tạo OAuth2 API Webflow](https://webflow.com/api/docs)).
  - **Project ID:** Điền **ID của dự án Webflow** bạn muốn theo dõi (tìm trong URL quản lý Webflow: `https://app.webflow.com/projects/[PROJECT_ID]`).
  - **Form ID:** Điền **ID của form** bạn muốn theo dõi (tìm trong **Settings > Forms** của trang Webflow).
  - **Webhook URL:** Điền **URL Webhook** của n8n (thường là `https://[YOUR_N8N_URL]/webhook/[WEBHOOK_ID]`).
:::

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Nhấn **Run Workflow** với dữ liệu mẫu (nếu có) để kiểm tra.
- **Bật Active:** Sau khi cấu hình xong, **bật workflow** để nó hoạt động tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[Mở Rộng Tính Năng]
- **Gửi thông báo Slack/Telegram:** Kết nối với **Slack** hoặc **Telegram Bot** để nhận thông báo tức thời.
- **Gửi Email tự động:** Sử dụng **n8n-nodes-base.email** để gửi email cảnh báo khi có form mới.
- **Lưu log vào Google Sheets:** Kết nối với **Google Sheets** để ghi lại tất cả các form submission.
- **Phân loại và xử lý tự động:** Sử dụng **LLM (n8n-nodes-base.llm)** để phân tích nội dung form và gửi phản hồi tự động.
:::

---

### 📌 **Kết Luận**
Workflow này giúp **các sếp tự động hóa việc theo dõi form submission trên Webflow**, tiết kiệm thời gian và đảm bảo không bỏ lỡ bất kỳ cơ hội nào. **Hãy áp dụng ngay để tối ưu hóa quy trình marketing của mình!**

:::success[Hành Động Ngay]
👉 [Tải workflow này](https://n8n.io/workflows/651) và **cài đặt trên VPS** để hoạt động 24/7.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N** (giảm tới 39%).
:::