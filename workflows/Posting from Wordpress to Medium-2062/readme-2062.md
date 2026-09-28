---
title: "🚀 Tự Động Hóa Bài Viết Từ WordPress Sang Medium - Giảm Thời Gian Tạo Nội Dung Gấp 10 Lần"
description: "Workflow này tự động lấy tất cả bài viết từ WordPress, xử lý nội dung và đăng lên Medium chỉ với một lần nhấp chuột. Giúp các sếp tiết kiệm thời gian, tránh sai sót và mở rộng phạm vi tiếp cận nội dung."
slug: "tu-dong-hoa-bai-viet-tu-wordpress-sang-medium"
tags: [n8n, automation, marketing, content-automation, wordpress-medium]
keywords: [n8n workflow tự động hóa, đăng bài từ WordPress sang Medium, tự động hóa nội dung marketing, giảm thời gian tạo bài viết, API WordPress và Medium]
---

# 🚀 **Tự Động Hóa Bài Viết Từ WordPress Sang Medium - Không Cần Code**

### **💡 Giải quyết vấn đề gì?**
Các sếp đang phải **thủ công copy-paste** bài viết từ WordPress sang Medium? Hay phải **tìm kiếm và xử lý nội dung** một cách tẻ nhạt? Workflow này sẽ **tự động hóa toàn bộ quy trình**, giúp bạn:
- **Lấy tất cả bài viết** từ WordPress một cách nhanh chóng.
- **Xử lý nội dung** (lọc, sắp xếp, trích xuất HTML).
- **Đăng tự động lên Medium** chỉ với một lần nhấp chuột.
- **Tiết kiệm thời gian** lên đến **gấp 10 lần** so với làm thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** – Không phải copy-paste từng bài viết.
✅ **Đăng bài tự động** – Không cần phải nhớ đăng lên Medium.
✅ **Nội dung sạch sẽ** – Xử lý HTML để bài viết Medium đẹp mắt.
✅ **Hoạt động liên tục** – Workflow chạy 24/7, không cần can thiệp.
✅ **Dễ mở rộng** – Thêm bài viết mới chỉ cần chạy workflow lại.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
✔ **Tài khoản WordPress** (URL blog, API Key nếu cần).
✔ **Tài khoản Medium** (API Key hoặc OAuth Token).
✔ **Thông tin URL nguồn** (ví dụ: `https://mailsafi.com/blog`).
✔ **Thông tin đăng nhập Medium** (Email và Password hoặc API Key).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/2062](https://n8n.io/workflows/2062).
- **Mở n8n Editor** và chọn **Import Workflow** (từ menu).
- **Chọn file JSON** vừa tải và nhấn **Import**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **9 node chính**, các sếp cần chú ý cấu hình như sau:

##### **🔹 Node 1: Manual Trigger (Bắt đầu workflow)**
- **Không cần cấu hình gì**, chỉ cần nhấn **"Execute Workflow"** để chạy.

##### **🔹 Node 2: HTTP Request (Lấy danh sách bài viết từ WordPress)**
- **URL**: Điền vào **URL của blog WordPress** (ví dụ: `https://mailsafi.com/blog`).
- **Method**: `GET`.
- **Headers**:
  - `Accept: application/json`.
  - Nếu cần API Key, thêm vào `Authorization: Bearer YOUR_API_KEY`.

##### **🔹 Node 3: HTML (Trích xuất nội dung HTML)**
- **Operation**: `extractHtmlContent`.
- **Lưu ý**: Node này sẽ **lọc nội dung HTML** từ trang WordPress để chuẩn bị đăng lên Medium.

##### **🔹 Node 4: Item Lists (Lọc và sắp xếp bài viết)**
- **Operation**: `limit` (nếu cần chỉ lấy một số bài viết nhất định).
- **Tham số**:
  - `limit`: Số bài viết muốn lấy (ví dụ: `10`).
  - `offset`: Bắt đầu từ bài viết thứ mấy (nếu cần).

##### **🔹 Node 5: Loop Over Items (Xử lý từng bài viết)**
- **Split In Batches**: Chia bài viết thành các batch để xử lý từng bài một.
- **Lưu ý**: Node này đảm bảo **mỗi bài viết được xử lý riêng biệt**.

##### **🔹 Node 6: HTML1 (Trích xuất nội dung chi tiết)**
- **Operation**: `extractHtmlContent` (lần thứ hai để lấy nội dung bài viết cụ thể).
- **Lưu ý**: Node này sẽ **lấy toàn bộ nội dung HTML** của bài viết để chuẩn bị đăng.

##### **🔹 Node 7: HTTP Request1 (Lấy thông tin bài viết chi tiết)**
- **URL**: Điền vào **URL cụ thể của bài viết** (ví dụ: `https://mailsafi.com/blog/bai-viet-1`).
- **Method**: `GET`.
- **Headers**: `Accept: application/json`.

##### **🔹 Node 8: Medium (Đăng bài lên Medium)**
- **API Key**: Điền **API Key của Medium** (cần tạo từ [Medium Developer Console](https://medium.com/developer)).
- **Thông tin bài viết**:
  - `title`: Tiêu đề bài viết.
  - `content`: Nội dung HTML từ Node 6.
  - `tags`: Thẻ liên quan (nếu có).
- **Lưu ý**:
  - Nếu không có API Key, có thể sử dụng **OAuth Token** thay thế.
  - Kiểm tra **quyền đăng bài** của tài khoản Medium.

##### **🔹 Node 9: Sticky Note (Ghi chú - không bắt buộc)**
- **Không cần cấu hình**, chỉ dùng để **ghi chú** trong workflow.

---

#### **3. Kích hoạt ⚡️**
- **Test Run**: Nhấn **"Execute Workflow"** và kiểm tra **log** để đảm bảo không có lỗi.
- **Active Workflow**: Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Lọc bài viết theo tiêu chí**:
   - Sử dụng **Node Item Lists** để **lọc bài viết mới nhất** hoặc **bài viết có tag nhất định**.
   - Ví dụ: `operation: filter` với điều kiện `date > "2024-01-01"`.

2. **Tự động gửi thông báo khi đăng bài thành công**:
   - Thêm **Node Slack/Telegram** sau Node Medium để **gửi thông báo** khi bài viết được đăng lên.

3. **Lưu log hoạt động**:
   - Sử dụng **Node Google Sheets** hoặc **Node Notion** để **ghi lại lịch sử hoạt động** của workflow.

4. **Chạy định kỳ**:
   - Sử dụng **Node Cron** (nếu self-hosted) để **chạy workflow hàng ngày/tuần**.

5. **Tối ưu nội dung trước khi đăng**:
   - Thêm **Node LLM (AI)** để **tối ưu tiêu đề, abstract** hoặc **chỉnh sửa ngữ pháp** trước khi đăng.

---

### 📌 **Kết luận**
Workflow này **giúp các sếp tự động hóa hoàn toàn quy trình đăng bài từ WordPress sang Medium**, tiết kiệm **thời gian và công sức** đáng kể. **Không cần code**, chỉ cần **cấu hình vài bước đơn giản**, bạn đã có thể **đăng bài tự động** và mở rộng nội dung trên Medium một cách hiệu quả.

**Hãy thử ngay và xem kết quả!** 🚀
Nếu có vấn đề, các sếp có thể **comment bên dưới** hoặc liên hệ với **Imperol** (tác giả của workflow) để hỗ trợ.

---
**💡 Mẹo cuối:** Nếu muốn **tăng tốc độ**, các sếp có thể **tăng số lượng batch** trong Node `splitInBatches` để xử lý nhiều bài viết cùng một lúc.