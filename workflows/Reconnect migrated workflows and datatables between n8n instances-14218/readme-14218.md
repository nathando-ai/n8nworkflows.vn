---
title: "🔄 **Tự Động Hoàn Chỉnh & Kết Nối Workflows + Datatables Sau Migrate n8n (Không Cần Code!)**"
description: "Workflow này tự động hóa quá trình thay thế ID cũ bằng ID mới cho tất cả workflows và datatables sau khi di chuyển từ phiên bản n8n cũ sang mới, đảm bảo không mất kết nối và hoạt động liên tục 24/7."
slug: "tieu-chinh-cong-ve-workflows-datatable-sau-migrate-n8n"
tags: [n8n, automation, devops, migration, no-code, api-integration]
keywords: [tự động hóa n8n, migrate workflow n8n, datatable n8n, reconnect workflows, api n8n, tự động hóa devops]
---

# 🔄 **Tự Động Hoàn Chỉnh & Kết Nối Workflows + Datatables Sau Migrate n8n (Không Cần Code!)**

Migrate n8n từ phiên bản cũ sang mới là một trong những công việc phức tạp nhất trong quản lý tự động hóa quy trình. Sau khi di chuyển, các **workflows** và **datatables** cũ sẽ bị mất kết nối với nhau, dẫn đến lỗi "Node not found" hoặc "Invalid reference" khi chạy. Thay vì phải **sửa thủ công từng workflow** (có thể mất hàng giờ), **Workflow này tự động hóa toàn bộ quá trình**, thay thế tất cả ID cũ bằng ID mới một cách **tự động, chính xác và an toàn**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Không cần sửa từng workflow thủ công (có thể mất hàng giờ).
- **Chính xác 100%:** Thay thế ID cũ bằng ID mới **tự động**, không bỏ sót hoặc sai sót.
- **Hoạt động liên tục:** Sau migrate, tất cả workflows vẫn hoạt động như cũ, không cần restart.
- **An toàn:** Không làm mất dữ liệu, chỉ thay thế tham chiếu (references) giữa workflows và datatables.
- **Phù hợp cho doanh nghiệp lớn:** Duy trì tính liên tục của hệ thống tự động hóa khi scale.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Hai phiên bản n8n** (cũ và mới) đã được cài đặt và chạy.
2. **API Key của cả hai phiên bản n8n**:
   - **Original n8n instance** (cũ): Để lấy danh sách workflows và datatables cũ.
   - **New n8n instance** (mới): Để cập nhật workflows và datatables mới.
3. **URL API của hai phiên bản**:
   - Ví dụ: `http://old-n8n-instance:5678` (cũ)
   - `http://new-n8n-instance:5678` (mới)
4. **Tài khoản admin** có quyền quản lý workflows trên cả hai phiên bản.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/14218) hoặc copy/paste JSON từ canvas.
- Vào **n8n Editor** → Nhấn **"Import"** → Chọn file JSON hoặc dán JSON vào ô nhập.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **9 node** chính, chia thành **4 phần quan trọng**:

##### **A. Cấu hình URL (Node `config` - Type: Code)**
- **Mục đích:** Lưu trữ URL của hai phiên bản n8n (cũ và mới) dưới dạng biến để tránh phải nhập lại nhiều lần.
- **Cách chỉnh:**
  - Mở node `config` → Chỉnh sửa code như sau:
    ```javascript
    return {
      orig_url: "http://old-n8n-instance:5678", // URL phiên bản cũ
      new_url: "http://new-n8n-instance:5678"   // URL phiên bản mới
    };
    ```
  - **Lưu ý:** Đảm bảo URL kết thúc bằng `/api/v1/` (n8n API mặc định).

##### **B. Lấy dữ liệu từ phiên bản cũ (`orig datatables` & `orig workflows` - Type: HTTP Request)**
- **Mục đích:** Truy cập và lấy danh sách **datatables** và **workflows** từ phiên bản cũ.
- **Cách chỉnh:**
  1. Mở node `orig datatables`:
     - **Method:** `GET`
     - **URL:** `{{ $orig_url }}/workflows/datatables`
     - **Credentials:** Chọn **credential của phiên bản cũ** (tạo trước đó).
  2. Mở node `orig workflows`:
     - **Method:** `GET`
     - **URL:** `{{ $orig_url }}/workflows`
     - **Credentials:** Chọn **credential của phiên bản cũ**.

##### **C. Lấy dữ liệu từ phiên bản mới (`new datatables` & `new workflows` - Type: HTTP Request)**
- **Mục đích:** Truy cập và lấy danh sách **datatables** và **workflows** từ phiên bản mới.
- **Cách chỉnh:**
  1. Mở node `new datatables`:
     - **Method:** `GET`
     - **URL:** `{{ $new_url }}/workflows/datatables`
     - **Credentials:** Chọn **credential của phiên bản mới**.
  2. Mở node `new workflows`:
     - **Method:** `GET`
     - **URL:** `{{ $new_url }}/workflows`
     - **Credentials:** Chọn **credential của phiên bản mới**.

##### **D. Thay thế ID và cập nhật workflows (`map` & `update new workflows` - Type: Code & n8n)**
- **Mục đích:** Tạo bản đồ (map) giữa ID cũ và ID mới, sau đó cập nhật workflows mới với ID mới.
- **Cách chỉnh:**
  1. **Node `map` (Code):**
     - Code này tự động tạo một **bản đồ ID cũ → ID mới** từ dữ liệu lấy được.
     - **Không cần chỉnh sửa**, chỉ cần đảm bảo input từ `orig datatables` và `new datatables` đúng.
  2. **Node `update new workflows` (n8n):**
     - **Operation:** `update`
     - **Credentials:** Chọn **credential của phiên bản mới** (cẩn thận, không chọn sai!).
     - **Lưu ý:** Node này sẽ **cập nhật tất cả workflows mới** với ID mới. **Không thể undo**, nên **test run trước** với một workflow mẫu.

---

#### **3. Kích hoạt ⚡️**
1. **Test run với dữ liệu mẫu:**
   - Chọn node `When clicking ‘Execute workflow’` → Nhấn **"Execute"** để chạy thử.
   - Kiểm tra log để đảm bảo không có lỗi (ví dụ: lỗi credential, URL sai).
2. **Bật Active workflow:**
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Lưu log migration:**
   - Thêm node **Slack/Telegram** sau `update new workflows` để nhận thông báo khi migration hoàn tất.
   - Ví dụ:
     ```json
     {
       "node": "slack",
       "type": "slack",
       "credentials": "slack_credential",
       "method": "chat.postMessage",
       "data": {
         "channel": "#n8n-migration",
         "text": "Migration hoàn tất! {{ $json }}"
       }
     }
     ```

2. **Kiểm tra trước khi migrate:**
   - Chạy workflow trên **sandbox** (n8n test instance) trước khi áp dụng vào phiên bản sản xuất.

3. **Sử dụng biến môi trường (Environment Variables):**
   - Thay vì hardcode URL, các sếp có thể sử dụng **biến môi trường** để dễ dàng thay đổi giữa môi trường dev/staging/prod.

4. **Backup workflows trước khi migrate:**
   - Trước khi chạy workflow này, **export tất cả workflows** từ phiên bản cũ để phục hồi nếu cần.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp đang gặp khó khăn khi migrate n8n từ phiên bản cũ sang mới. Thay vì mất hàng giờ để sửa thủ công, **chỉ cần cấu hình URL và credential**, workflow sẽ tự động:
✅ **Tìm tất cả workflows và datatables cũ.**
✅ **Tạo bản đồ ID cũ → ID mới.**
✅ **Cập nhật tất cả tham chiếu trong workflows mới.**
✅ **Hoàn tất trong vài phút!**

**Hành động ngay:** Import workflow này và **tự động hóa quá trình migrate** của mình! Nếu có vấn đề, hãy để lại comment dưới đây, các sếp sẽ được hỗ trợ chi tiết.

---
**🚀 Cảm ơn các sếp đã đọc đến cuối!** 🚀