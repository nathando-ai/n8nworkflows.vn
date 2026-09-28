---
title: "🚀 Tự Động Hóa Lấy Toàn Bộ Dữ Liệu Monday.com (Including Subitems & Relations) Mới Chỉ Với 1 Node - Không Cần Code!"
description: "Workflow này giúp các sếp tự động lấy toàn bộ dữ liệu của một item Monday.com (bao gồm subitems, relations và tất cả cột dữ liệu) trong một lần gọi duy nhất, tiết kiệm thời gian và tránh sai sót khi làm thủ công."
slug: "tieu-dung-monday-com-toan-bo-du-lieu"
tags: [n8n, Monday.com, automation, no-code, monday-api]
keywords: [tự động hóa Monday.com, lấy dữ liệu Monday.com, workflow Monday.com, n8n Monday.com, tự động hóa không code]
---

# 🚀 **Tự Động Hóa Lấy Toàn Bộ Dữ Liệu Monday.com (Including Subitems & Relations) Mới Chỉ Với 1 Node**

### **🔥 Nỗi Đau Của Các Sếp Khi Lấy Dữ Liệu Monday.com Thủ Công**
Làm việc với **Monday.com** thường đòi hỏi các sếp phải:
- **Lấy dữ liệu của một item** (ví dụ: một task, project, hoặc deal) và **tìm kiếm thủ công** các subitems liên quan (nested items).
- **Tách riêng các relations** (ví dụ: tasks phụ thuộc, files đính kèm, hoặc comments) và **lấy dữ liệu của chúng** một cách riêng biệt.
- **Gộp tất cả dữ liệu** (cột dữ liệu, subitems, relations) thành một **JSON duy nhất** để phân tích hoặc xuất báo cáo.
- **Sai sót khi làm thủ công** (quên lấy một cột, hoặc subitem nào đó) và **tốn thời gian** để kiểm tra lại.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Lấy toàn bộ dữ liệu của một item Monday.com (bao gồm subitems và relations) trong một lần gọi duy nhất.**
✅ **Tự động gộp tất cả dữ liệu** (cột dữ liệu, subitems, relations) thành một **JSON cấu trúc rõ ràng**.
✅ **Không cần viết code** – chỉ cần cấu hình và chạy.
✅ **Hoạt động liên tục 24/7** khi self-hosted trên VPS.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần lấy dữ liệu từng phần, tránh làm lại nhiều lần.
- **Dữ liệu chính xác 100%**: Không bỏ sót subitem hoặc relation nào.
- **Dễ dàng phân tích**: Dữ liệu được gộp thành **JSON chuẩn**, có thể export ra Excel, Google Sheets, hoặc gửi qua API khác.
- **Hoạt động tự động**: Cấu hình một lần, chạy mãi – không cần can thiệp thủ công.
- **Cá nhân hóa**: Sử dụng biến `pulse` để lấy dữ liệu của **item cụ thể** mà không cần chỉnh sửa workflow.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow này, các sếp cần:
1. **Tài khoản Monday.com** và **API Key** của Monday.com:
   - Mở **Settings** → **Integrations** → **API Keys** → **Create API Key**.
   - Lưu **API Key** này để sử dụng trong n8n (credentials `mondayComApi`).
2. **Workflow n8n** được self-hosted (để chạy 24/7):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
3. **ID của Board và Item** (cần điền vào biến `pulse` trong node `Edit Fields`).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/2086](https://n8n.io/workflows/2086) và import vào n8n Editor.
- **Copy JSON** từ link trên và **paste** vào n8n Editor (tab `Import`).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **21 node** và có **3 bước cấu hình quan trọng**:

##### **A. Cấu Hình Credentials Monday.com**
- Mở node **`PULL LINKEDPULSES1`**, **`GET EACH SUBITEM1`**, và **`GET ITEM`**.
- Chọn **credentials** là `mondayComApi` (đã tạo trước đó).
- Đảm bảo **API Key** được điền chính xác.

##### **B. Đặt ID của Item Cần Lấy Dữ Liệu (Biến `pulse`)**
- Mở node **`Edit Fields`** (node cuối cùng trước khi `Execute Workflow`).
- Trong **JSON Path**, thay thế giá trị của `pulse` bằng **ID của item Monday.com** bạn muốn lấy dữ liệu.
  - Ví dụ: `"pulse": "123456789"` (ID này lấy từ URL của item trong Monday.com).
- **Lưu ý**: ID này sẽ được truyền vào workflow con để lấy dữ liệu.

##### **C. Cấu Hình Workflow Con (Execute Workflow)**
- Mở node **`Execute Workflow`** (node thứ 19).
- Trong **Workflow ID**, điền **ID của workflow con** (nếu có) hoặc để trống nếu không cần.
- **Test Run** trước khi kích hoạt để đảm bảo dữ liệu lấy đúng.

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chọn **`Execute Workflow Trigger`** (node cuối cùng).
   - Nhấn **Run Workflow** và kiểm tra kết quả JSON.
2. **Bật Active** nếu kết quả đúng.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::note[CÁCH SỬ DỤNG HIỆU QUẢ NHẤT]
1. **Lưu JSON kết quả vào Google Sheets/Excel**:
   - Sau khi workflow chạy, sử dụng node **`Google Sheets`** để ghi dữ liệu vào bảng.
   - Cấu hình **`Append Row`** với JSON output từ workflow này.

2. **Gửi báo cáo qua Email/Slack**:
   - Sử dụng node **`Email`** hoặc **`Slack`** để thông báo khi workflow hoàn thành.
   - Ví dụ: Gửi email báo cáo hàng ngày với dữ liệu mới nhất.

3. **Tự động cập nhật khi có thay đổi**:
   - Sử dụng **`Webhook`** để kích hoạt workflow khi có sự thay đổi trong Monday.com (ví dụ: item mới được tạo).
   - Cấu hình **`Trigger`** là `mondayCom` với event `item.created`.

4. **Lọc dữ liệu theo điều kiện**:
   - Sử dụng node **`Code`** để lọc JSON output (ví dụ: chỉ lấy subitems có trạng thái `Done`).
   - Ví dụ mã JavaScript:
     ```javascript
     $input.all().map(item => {
       if (item.status === "Done") {
         return item;
       }
     });
     ```

5. **Kết hợp với LLM (ChatGPT, Claude)**:
   - Sử dụng node **`LLM`** để tổng hợp và phân tích dữ liệu (ví dụ: tóm tắt tình trạng project).
   - Ví dụ prompt:
     ```
     "Tóm tắt tình trạng project ID {pulse} từ dữ liệu sau: {jsonData}"
     ```
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tự động hóa lấy dữ liệu Monday.com** một cách **chính xác và nhanh chóng**.
✔ **Tránh sai sót** khi làm thủ công và **tiết kiệm thời gian** cho công việc phân tích.
✔ **Hoạt động liên tục** 24/7 khi self-hosted trên VPS.

**🚀 Hãy áp dụng ngay và tự động hóa công việc của mình!**
- **Import workflow** từ [n8n.io/workflows/2086](https://n8n.io/workflows/2086).
- **Cấu hình biến `pulse`** với ID của item cần lấy.
- **Test Run** và **bật Active** để bắt đầu!

---
**💡 Cần hỗ trợ thêm?**
- **Join Community n8n Việt Nam** tại [Facebook Group](https://www.facebook.com/groups/n8nvietnam).
- **Đăng ký VPS** để self-host n8n: [TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N**).