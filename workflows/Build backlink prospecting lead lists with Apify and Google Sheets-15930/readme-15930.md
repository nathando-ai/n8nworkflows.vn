---
title: "🔍 **Tự Động Xây Dựng Danh Sách Lead Backlink Từ Apify & Google Sheets (Không Cần Code!)**"
description: "Workflow tự động hóa tìm kiếm và xây dựng danh sách lead backlink chất lượng từ các từ khóa và domain, đồng thời tự động cập nhật vào Google Sheets. Giúp các sếp tiết kiệm thời gian lên tới 20 giờ/tháng và tránh lặp lại công việc thủ công."
slug: "tieu-dong-xay-dung-danh-sach-lead-backlink-apify-google-sheets"
tags: [n8n, automation, market-research, backlink, apify, google-sheets, seo]
keywords: [n8n workflow backlink, tự động hóa tìm lead backlink, apify n8n, xây dựng danh sách lead seo, tự động hóa marketing, tự động hóa google sheets]
---

# 🚀 **Tự Động Xây Dựng Danh Sách Lead Backlink Từ Apify & Google Sheets**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp SEO**
Bạn có bao giờ phải:
- **Tìm kiếm thủ công** hàng trăm domain tiềm năng để xây dựng backlink?
- **Lặp lại công việc** vì không lưu trữ kết quả từ các lần chạy trước?
- **Tốn thời gian** vào việc format dữ liệu và nhập liệu vào Google Sheets?
- **Không biết cách tối ưu** từ khóa và domain để tăng hiệu quả?

Workflow này **tự động hóa toàn bộ quy trình** từ tìm kiếm lead backlink đến cập nhật kết quả vào Google Sheets, giúp các sếp **tiết kiệm 20+ giờ/tháng** và **tăng hiệu quả SEO** một cách hiệu quả.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
✅ **Tự động hóa 100%** từ tìm kiếm lead đến cập nhật kết quả (không cần code).
✅ **Tránh lặp lại công việc**: Danh sách domain đã xử lý sẽ được **tự động blacklist** để không bị lặp lại.
✅ **Cập nhật liên tục**: Kết quả từ Apify được **ghi lại vào Google Sheets** ngay lập tức.
✅ **Tối ưu từ khóa**: Chỉ cần nhập **từ khóa và domain** vào Sheets, workflow sẽ tự động xử lý.
✅ **Chạy 24/7**: Dùng **trigger định kỳ** (tháng) hoặc **manual trigger** khi cần.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Lên Đồ**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Google Sheets** (đã tạo **template** theo [đây](https://docs.google.com/spreadsheets/d/1ONk8m88kmYjl7R7CP0ixAYYNUgo5FHO50Im5QCAyJjs/edit?usp=sharing)).
2. **Tài khoản Apify** (đăng ký tại [apify.com](https://apify.com/)).
3. **API Key của Apify** (tạo tại [Apify Dashboard](https://apify.com/dashboard/keys)).
4. **Credentials Google Sheets** trong n8n (cài đặt tại **Credentials → Add → Google Sheets**).
5. **Webhook URL** từ Apify (sẽ được hướng dẫn sau).
:::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [đây](https://n8n.io/workflows/15930) (chọn **Export as JSON**).
2. Trong n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở n8n Editor → Nhấn **Create new workflow**.
2. Chọn **Import from JSON** → Dán JSON từ [đây](https://n8n.io/workflows/15930) (chọn **Export as JSON**).
3. Nhấn **Import**.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **14 node**, nhưng các node quan trọng nhất cần cấu hình kỹ là:

#### **🔹 Node "Read Queries from Sheets" & "Read Blacklist Domains"**
- **Chọn Credentials**: Đảm bảo chọn **Google Sheets credentials** đã cấu hình trước.
- **Chọn Sheet & Range**:
  - **Queries**: Tab **"Queries"** (cột `Query`).
  - **Blacklist**: Tab **"Blacklist"** (cột `Domain`).

#### **🔹 Node "Execute Link Prospecting" (Apify)**
- **Chọn Actor**: Chọn **Link Prospecting** (của Apify).
- **Input Fields**:
  - **Brand**: Tên brand/công ty bạn muốn tìm lead.
  - **ownDomains**: Danh sách domain của bạn (nếu có).
  - **organicResults**: Số lượng kết quả tìm kiếm tối đa (ví dụ: `100`).
- **Credentials**: Chọn **Apify API Key** đã cấu hình.

#### **🔹 Node "Webhook POST Handler"**
- **URL Webhook**: Sau khi chạy Apify, bạn sẽ có **URL callback** từ Apify.
  - Mở **Actor → Link Prospecting → Integration → Add Integration → HTTP Request**.
  - Chọn **"Run succeeded"** → Dán **URL Webhook** từ node này vào Apify.
  - **Path**: `4e22d4fb-6915-4351-9d8b-216941002b65` (không cần thay đổi).

#### **🔹 Node "Append to Blacklist Domains"**
- **Chọn Sheet & Range**: Tab **"Blacklist"** (cột `Domain`).
- **Operation**: Đảm bảo chọn **Append** (để thêm mới).

#### **🔹 Node "Scheduled Monthly Trigger" (Nếu muốn chạy tự động)**
- **Chọn ngày giờ**: Ví dụ, **mỗi đầu tháng** (ngày 1, 8, 15, 22).
- **Time Zone**: Chọn **UTC+7** (hoặc khu vực của bạn).

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** (nếu muốn kiểm tra trước):
   - Chọn **Manual Trigger Execution** → Nhấn **Execute**.
   - Kiểm tra kết quả trong **Google Sheets** (tab **Leads** và **Batch 1**).
2. **Bật Active**:
   - Nhấn **Active** trên workflow.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **🔹 Kết hợp với Slack/Telegram để thông báo kết quả**
- Thêm **node Slack/Telegram Webhook** sau **node "Append Leads to Sheets"** để nhận thông báo khi workflow hoàn thành.

### **🔹 Tạo báo cáo định kỳ**
- Sử dụng **node Google Sheets → Append** để ghi lại **tổng số lead mới** vào một tab **Report**.
- Sau đó, **export thành PDF** và gửi qua email (sử dụng **node Email**).

### **🔹 Tối ưu từ khóa**
- Nếu muốn **tăng hiệu quả**, thêm **cột "Priority"** vào tab **Queries** (ví dụ: `High`, `Medium`, `Low`).
- Sử dụng **node Code** để **lọc từ khóa ưu tiên** trước khi gửi vào Apify.

### **🔹 Sử dụng nhiều tab Sheets cho nhiều dự án**
- Mỗi **dự án SEO** có thể có **1 tab Sheets riêng** để quản lý lead.
- Cấu hình **node "Read Queries from Sheets"** để đọc từ tab tương ứng.

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp SEO để tập trung vào **strategy** thay vì công việc thủ công. Bằng cách **tự động hóa tìm kiếm lead, blacklist domain và cập nhật Sheets**, bạn sẽ:
✔ **Tiết kiệm 20+ giờ/tháng**.
✔ **Tránh lặp lại công việc**.
✔ **Tăng hiệu quả backlink** một cách khoa học.

**🚀 Hãy áp dụng ngay và bắt đầu tự động hóa SEO của mình!**

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💬 Cần hỗ trợ thêm?** Hãy để lại comment bên dưới hoặc liên hệ với tôi qua [LinkedIn](https://linkedin.com/in/fabianmaume) (tác giả gốc của workflow). 🚀