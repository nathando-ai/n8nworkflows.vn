---
title: "🚀 Tự Động Hái Bài TechCrunch Mới Nhất - Scrape 20 Bài TechCrunch Mới Nhất Mỗi Ngày (Không Code)"
description: "Workflow tự động scrape 20 bài viết mới nhất từ TechCrunch mỗi ngày, lưu trữ dữ liệu bài viết (tiêu đề, nội dung, ngày đăng) vào n8n Database hoặc Google Sheets. Giúp các sếp tiết kiệm thời gian theo dõi tin tức tech hàng ngày."
slug: "tieu-dong-scrape-techcrunch"
tags: [n8n, automation, web-scraping, tech-news, no-code]
keywords: [scrape techcrunch, tự động hóa scrape bài viết, n8n workflow scrape, scrape tin tức tech, lưu trữ bài viết tech]
---

# 🚀 **Tự Động Hái Bài TechCrunch Mới Nhất - Scrape 20 Bài TechCrunch Mới Nhất Mỗi Ngày (Không Code)**

### **Nỗi Đau Của Các Sếp?**
Hàng ngày, các sếp phải mất **30-60 phút** để:
- **Tìm kiếm** và **lọc** 20 bài viết tech mới nhất từ TechCrunch.
- **Đọc kỹ** để đánh giá xu hướng, công nghệ mới.
- **Lưu trữ** thông tin để tham khảo sau.

**Workflow này giải quyết tất cả!** Nó tự động **scrape 20 bài viết mới nhất** từ TechCrunch mỗi ngày, **lọc nội dung chính**, và **lưu trữ** vào **n8n Database** hoặc **Google Sheets** để các sếp dễ dàng theo dõi.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** (không phải thủ công scrape mỗi ngày).
✅ **Dữ liệu chính xác** (scrape từ nguồn chính thức TechCrunch).
✅ **Lưu trữ tự động** (cập nhật mỗi ngày vào Database/Google Sheets).
✅ **Dễ dàng theo dõi xu hướng tech** (tất cả bài viết mới nhất trong một nơi).
✅ **Không cần code** (sử dụng n8n, công cụ tự động hóa no-code).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (cài trên VPS hoặc dùng phiên bản cloud).
- **Không cần API key** (scrape trực tiếp từ TechCrunch).
- **Lựa chọn lưu trữ**:
  - **n8n Database** (nếu đã cài đặt).
  - **Google Sheets** (nếu muốn lưu vào Google Drive).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/2832) hoặc copy toàn bộ JSON dưới đây vào **n8n Editor**.
- **Nhấn "Import"** để thêm workflow vào n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này **không cần cấu hình API key**, nhưng cần **chọn nơi lưu trữ** (n8n Database hoặc Google Sheets).

##### **A. Chọn Node "Save the values" (n8n-nodes-base.set)**
- **Nếu dùng n8n Database**:
  - Chọn **n8n Database** trong danh sách credentials.
  - Đặt tên **Collection** (ví dụ: `techcrunch_articles`).
  - Chọn **fields** cần lưu (tiêu đề, nội dung, ngày đăng, link).

- **Nếu dùng Google Sheets**:
  - Thêm **Google Sheets credential** vào n8n (cài node `n8n-nodes-googleSheets`).
  - Chọn **Google Sheet** và **Sheet Name** (ví dụ: `TechCrunch_Articles`).
  - Đảm bảo **Google Sheets có quyền truy cập** vào n8n.

##### **B. Test Run (Kiểm Tra Trước Khi Bật)**
- Nhấn **"Test Workflow"** để scrape **một bài viết mẫu**.
- Kiểm tra **dữ liệu trả về** có đầy đủ không (tiêu đề, nội dung, ngày đăng).
- Nếu có lỗi, **sửa lại XPath** trong các node `html` (nếu cần).

#### **3. Kích Hoạt ⚡️**
- Sau khi **test thành công**, bật **Active workflow**.
- **Lưu workflow** và **đặt lịch chạy hàng ngày** (ví dụ: **lúc 8h sáng**).

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram** để **báo cáo tin tức mới nhất** mỗi sáng.
   - Sử dụng node `n8n-nodes-slack` hoặc `n8n-nodes-telegram` để gửi thông báo.
2. **Lưu log scrape** vào **Google Drive** hoặc **n8n Database** để theo dõi lịch sử.
3. **Lọc bài viết theo keyword** (ví dụ: AI, blockchain) bằng **node `n8n-nodes-base.if`**.
4. **Gửi email báo cáo** hàng tuần cho team bằng **node `n8n-nodes-n8n-email`**.

---

### 📌 **Kết Luận**
Workflow này **giúp các sếp tự động scrape và lưu trữ 20 bài TechCrunch mới nhất mỗi ngày**, tiết kiệm **thời gian và công sức** trong việc theo dõi tin tức tech.

**🚀 Hãy áp dụng ngay và bắt đầu scrape tự động hôm nay!**
Nếu có vấn đề, **hãy comment bên dưới** hoặc liên hệ với tác giả Teddy (South Korea) qua [n8n Community](https://community.n8n.io/).

---
**#n8n #Automation #TechNews #WebScraping #NoCode**