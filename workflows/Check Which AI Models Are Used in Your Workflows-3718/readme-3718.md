---
title: "🤖 **Kiểm Tra Tất Cả Các Mô Hình AI Đang Sử Dụng Trong Workflow n8n Của Bạn - Tự Động Hóa 100% Không Code**"
description: "Workflow này tự động quét toàn bộ các workflow n8n của bạn và báo cáo chi tiết các mô hình AI (LLM, Vision, Audio...) đang được sử dụng, giúp tối ưu hóa chi phí và quản lý hiệu quả. Kết quả được lưu vào Google Sheets với định dạng dễ đọc."
slug: "kiem-tra-cac-mo-hinh-ai-trong-workflow-n8n"
tags: [n8n, automation, ai, it-ops, google-sheets]
keywords: [n8n workflow, tự động hóa AI, kiểm tra mô hình AI, quản lý workflow n8n, tiết kiệm chi phí AI]
---

# 🚀 **Tự Động Kiểm Tra & Quản Lý Các Mô Hình AI Trong Workflow n8n Của Bạn**

### **Nỗi Đau Của Các Sếp**
Hiện nay, khi xây dựng các workflow tự động hóa với n8n, nhiều doanh nghiệp và cá nhân thường **không biết chính xác các mô hình AI (LLM, Vision, Audio...) đang được sử dụng** trong hệ thống. Điều này dẫn đến:
- **Chi phí AI không kiểm soát**: Các mô hình đắt đỏ như GPT-4, Claude, hoặc Stable Diffusion có thể được gọi nhiều lần mà không được theo dõi.
- **Rủi ro an toàn dữ liệu**: Một số mô hình AI có thể xử lý dữ liệu nhạy cảm mà không được ý thức.
- **Tối ưu hóa hiệu suất kém**: Không biết mô hình nào đang được sử dụng nhiều nhất để điều chỉnh chiến lược.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Quét toàn bộ workflow** của bạn và **lọc ra các node sử dụng mô hình AI**.
✅ **Lưu kết quả vào Google Sheets** với thông tin chi tiết (tên workflow, node, mô hình AI, số lần gọi).
✅ **Cung cấp báo cáo định kỳ** để theo dõi và tối ưu hóa chi phí.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm chi phí AI**: Biết được mô hình nào tốn kém nhất và có thể thay thế bằng mô hình rẻ hơn.
- **Quản lý an toàn dữ liệu**: Theo dõi các mô hình xử lý dữ liệu nhạy cảm.
- **Tối ưu hóa hiệu suất**: Sắp xếp lại workflow để giảm thời gian xử lý.
- **Hoạt động liên tục 24/7**: Không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI SỬ DỤNG**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu kết quả):
   - Một **Google Workspace** hoặc tài khoản cá nhân.
   - **Bảng tính mới** (sẽ được xóa dữ liệu cũ trước khi lưu kết quả mới).
   - **Chia sẻ quyền chỉnh sửa** cho n8n (nếu self-hosted).

2. **API Key của n8n** (nếu self-hosted):
   - **Tạo API Key** trong **Settings > API Keys** của n8n (self-hosted).
   - **Lưu API Key** này trong **Credentials** của n8n (để workflow có quyền truy cập API).

3. **Domain của n8n** (nếu self-hosted):
   - Ví dụ: `https://n8n.tinohost.vn` (nếu cài trên VPS TinoHost).
   - **Thay thế giá trị này trong node `n8n-get all workflow`** (xem phần hướng dẫn dưới đây).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow bằng **2 cách**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/3718) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và **paste vào n8n Editor** (trong tab **Import/Export**).

:::note[**Lưu ý về dung lượng**]
Nếu bạn có **hơn 100 workflow**, việc quét toàn bộ có thể gây **tải nặng hệ thống**. Để tránh tình trạng này:
- **Chia nhỏ workflow** thành nhiều batch (ví dụ: quét 50 workflow/lần).
- **Sử dụng VPS mạnh** (n8n trên máy chủ shared có thể bị chậm).
:::

---

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Sau khi import, các sếp cần **cấu hình lại các node quan trọng** như sau:

##### **A. Thay đổi Domain n8n (nếu self-hosted)**
- **Node:** `n8n-get all workflow`
- **Thao tác:**
  1. Nhấp chuột phải vào node → **Edit**.
  2. Trong **URL**, thay thế `https://n8n.io` bằng **domain của n8n self-hosted** (ví dụ: `https://n8n.tinohost.vn`).
  3. **Lưu lại**.

##### **B. Cấu Hình Credentials cho Google Sheets**
- **Node:** `Google Sheets-Clear Sheet Data` và `Google Sheets-Save node and workflow data`
- **Thao tác:**
  1. Nhấp chuột phải vào node → **Edit**.
  2. Trong **Credentials**, chọn **`googleSheetsOAuth2Api`** (nếu đã cấu hình trước đó).
  3. **Chọn bảng tính** (Sheet) muốn lưu kết quả.
  4. **Lưu lại**.

##### **C. Kiểm Tra Node Filter (Lọc Workflow Chứa `modelId`)**
- **Node:** `Filter-get workflow contain modelid` và `Filter-node contain modelId`
- **Thao tác:**
  - Các node này **sẽ tự động lọc** các workflow chứa từ khóa `modelId` (đặc trưng của node AI).
  - **Không cần chỉnh sửa** nếu muốn quét tất cả mô hình AI.

##### **D. Thiết Lập Tên Sheet (Tùy Chọn)**
- **Node:** `Google Sheets-Save node and workflow data`
- **Thao tác:**
  - Trong **Key Parameters**, thay đổi **Sheet Name** thành tên mong muốn (ví dụ: `Báo cáo mô hình AI - [Ngày tháng]`).

---

#### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run với Dữ liệu Mẫu**:
   - Nhấp vào **Test Workflow** để kiểm tra nếu có lỗi.
   - Kiểm tra **Google Sheets** xem kết quả có được lưu không.

2. **Bật Workflow**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**CÁCH SỬ DỤNG HIỆU QUẢ HƠN**]
1. **Kết hợp với Slack/Telegram**:
   - Sau khi lưu vào Google Sheets, **gửi báo cáo tự động** qua Slack/Telegram bằng node **`webhook`** hoặc **`slack`**.
   - **Cách làm:**
     - Thêm node **`webhook`** sau `Google Sheets-Save node and workflow data`.
     - Cấu hình **payload** để gửi thông báo như:
       ```json
       {
         "text": "🚀 Báo cáo mô hình AI mới được cập nhật! Kiểm tra tại: [Link Google Sheets]"
       }
       ```

2. **Lưu Log Lịch Sử**:
   - Thêm node **`set`** trước khi lưu vào Google Sheets để **ghi ngày giờ** và **tên người chạy workflow**.
   - **Cách làm:**
     - Thêm node **`set`** sau `Filter-node contain modelId`.
     - Thêm trường mới như `timestamp` và `user`.

3. **Tự Động Xóa Dữ liệu Cũ**:
   - Nếu không muốn dữ liệu tích lũy, **xóa sheet cũ** trước khi lưu mới bằng node **`googleSheets`** với `operation: delete`.
   - **Lưu ý:** Đảm bảo **không xóa sheet đang sử dụng**.

4. **Quét Chỉ Các Workflow Chỉnh Sửa Gần Đây**:
   - Thêm node **`filter`** để chỉ quét workflow được **cập nhật trong 7 ngày qua**.
   - **Cách làm:**
     - Thêm node **`set`** sau `n8n-get all workflow` để thêm trường `lastModified`.
     - Thêm node **`filter`** với điều kiện:
       ```json
       {{ $json["lastModified"] > $now - 7*24*60*60*1000 }}
       ```
:::

---

### 📌 **Kết Luận**
Workflow này là **công cụ không thể thiếu** cho các sếp muốn **quản lý và tối ưu hóa chi phí AI** trong n8n. Bằng cách **quét toàn bộ hệ thống và lưu báo cáo chi tiết**, bạn có thể:
✔ **Tiết kiệm hàng nghìn đồng** mỗi tháng với các mô hình AI đắt đỏ.
✔ **Tránh rủi ro an toàn dữ liệu** bằng cách theo dõi các mô hình xử lý thông tin nhạy cảm.
✔ **Tối ưu hóa hiệu suất** bằng cách sắp xếp lại workflow.

**👉 Hãy áp dụng ngay và bắt đầu tự động hóa quản lý AI của bạn!**

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**📢 Cảm ơn các sếp đã đọc!** Nếu có thắc mắc, hãy để lại comment bên dưới. 🚀