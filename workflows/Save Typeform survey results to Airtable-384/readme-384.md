---
title: "🚀 Tự Động Lưu Kết Quả Cuộc Thăm Dò ý Kiến Typeform Vào Airtable - Không Cần Code!"
description: "Giải pháp tự động hóa hoàn toàn miễn phí giúp các sếp lưu trữ tất cả kết quả cuộc thăm dò Typeform vào Airtable một cách tự động, tiết kiệm thời gian và giảm thiểu sai sót. Hoạt động 24/7 mà không cần can thiệp thủ công."
slug: "tu-dong-luu-ket-qua-typeform-vao-airtable"
tags: [n8n, automation, no-code, typeform, airtable, marketing-automation]
keywords: [tự động hóa typeform airtable, lưu kết quả typeform tự động, n8n workflow marketing, tự động hóa không code, lưu dữ liệu airtable từ form]
---

# 🚀 **Tự Động Lưu Kết Quả Cuộc Thăm Dò Typeform Vào Airtable - Không Cần Code!**

### **Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Các sếp thường phải mất **giờ đồng hồ** để:
- **Tải xuống** kết quả từ Typeform sau mỗi cuộc thăm dò.
- **Chuyển dữ liệu** vào Airtable bằng tay, dẫn đến **sai sót** và **tốn thời gian**.
- **Không theo dõi được** kết quả thực thời, khiến việc phân tích trở nên khó khăn.

**Giải pháp?** Một **workflow tự động hóa hoàn toàn** chỉ với **2 node** giúp lưu trữ kết quả Typeform vào Airtable **ngay lập tức**, **không cần code** và hoạt động **24/7**!

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** – Không cần tải xuống và nhập liệu thủ công.
✅ **Chính xác 100%** – Dữ liệu tự động đồng bộ, không sai sót.
✅ **Hoạt động liên tục** – Lưu trữ kết quả ngay khi khách hàng trả lời.
✅ **Dễ dàng phân tích** – Dữ liệu luôn cập nhật trên Airtable, sẵn sàng cho báo cáo.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần:
✔ **Tài khoản Typeform** (để lấy **API Key**).
✔ **Tài khoản Airtable** (để lấy **API Key** và chọn **bảng dữ liệu** muốn lưu).
✔ **N8n Self-hosted** (để workflow hoạt động 24/7).
:::

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/384](https://n8n.io/workflows/384) hoặc copy toàn bộ JSON từ link trên.
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON hoặc tải file JSON đã tải xuống.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows chỉ hoạt động khi **cấu hình chính xác** các node sau:

##### **🔹 Node 1: Typeform Trigger**
- **Credentials:** Chọn **"typeformApi"** (nếu chưa có, tạo mới trong **Credentials Manager**).
  - **Cách lấy API Key Typeform:**
    1. Đăng nhập vào [Typeform Developer](https://admin.typeform.com/developer).
    2. Tạo **API Key** mới (nếu chưa có).
    3. Copy **API Key** và dán vào **Credentials** của n8n.
- **Trigger:** Chọn **"Form Submission"** (để kích hoạt khi có phản hồi mới).

##### **🔹 Node 2: Airtable (Append Data)**
- **Credentials:** Chọn **"airtableApi"** (nếu chưa có, tạo mới trong **Credentials Manager**).
  - **Cách lấy API Key Airtable:**
    1. Đăng nhập vào [Airtable API Docs](https://airtable.com/api).
    2. Tạo **API Key** mới (nếu chưa có).
    3. Copy **API Key** và dán vào **Credentials** của n8n.
- **Base ID & Table Name:**
  - **Base ID** là **ID của bảng Airtable** bạn muốn lưu dữ liệu.
    - Tìm **Base ID** trong URL của bảng Airtable (vd: `https://airtable.com/tblABC123...` → `ABC123` là Base ID).
  - **Table Name** là **tên bảng** bạn muốn lưu (vd: `Kết quả Thăm Dò`).
- **Operation:** Đảm bảo chọn **"Append"** (để thêm dữ liệu mới vào bảng).

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Nhấn **"Execute"** để kiểm tra workflow với **dữ liệu mẫu**.
- **Bật Active:** Sau khi test thành công, **bật workflow** để hoạt động tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM NỔI BẬT HƠN]
🔹 **Gửi thông báo Slack/Telegram khi có phản hồi mới:**
   - Thêm **Node Slack/Telegram Webhook** sau **Typeform Trigger** để thông báo ngay khi có phản hồi mới.

🔹 **Lưu log hoạt động:**
   - Thêm **Node Log** để theo dõi lịch sử lưu trữ (giúp debug nếu có lỗi).

🔹 **Tự động gửi báo cáo định kỳ:**
   - Sử dụng **Node Schedule** kết hợp **Node Airtable** để tạo báo cáo tổng hợp hàng tuần/tháng.
:::

---

### 📌 **Kết Luận**
**Không cần code, không cần mất thời gian tải xuống và nhập liệu thủ công!** Workflow này giúp các sếp **tự động lưu trữ tất cả kết quả Typeform vào Airtable một cách chính xác và liên tục**, tiết kiệm **giờ đồng hồ** mỗi tuần.

**🚀 Hãy áp dụng ngay và tự động hóa công việc của mình!**
Nếu có vấn đề, hãy để lại **comment** dưới đây hoặc liên hệ với **n8n Community** để được hỗ trợ!

---