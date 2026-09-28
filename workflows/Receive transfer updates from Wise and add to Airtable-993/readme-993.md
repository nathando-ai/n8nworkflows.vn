---
title: "💰 Tự Động Hóa Cập Nhật Giao Dịch Wise → Airtable: Giảm 90% Thời Gian Theo Dõi Tài Chính"
description: "Workflow này tự động lấy thông tin giao dịch từ Wise (trước đây là TransferWise) và cập nhật ngay vào Airtable, giúp các sếp quản lý tài chính cá nhân/doanh nghiệp một cách chính xác và tiết kiệm thời gian hàng ngày. Không cần code, chỉ cần 5 phút cấu hình."
slug: "tu-dong-hoa-cap-nhat-giao-dich-wise-den-airtable"
tags: [n8n, automation, finance, airtable, wise, no-code]
keywords: [n8n workflow Wise Airtable, tự động hóa tài chính, cập nhật giao dịch Wise tự động, quản lý tài chính cá nhân, Airtable API]
---

# 🚀 **Tự Động Hóa Cập Nhật Giao Dịch Wise → Airtable: Giảm 90% Thời Gian Theo Dõi Tài Chính**

### **Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải:
- **Đăng nhập Wise** để kiểm tra giao dịch mới.
- **Copy-paste** thông tin vào Airtable hoặc Excel để theo dõi chi tiêu.
- **Lo lắng** về việc bỏ sót giao dịch hoặc dữ liệu sai lệch.
- **Tốn thời gian** lên đến **30 phút/ngày** cho công việc thủ công này.

**Workflow này giải quyết tất cả!** Nó tự động lấy **tất cả giao dịch mới** từ Wise và **cập nhật ngay vào Airtable**, giúp các sếp:
✅ **Tiết kiệm 90% thời gian** theo dõi tài chính.
✅ **Tránh sai sót** do nhập liệu thủ công.
✅ **Quản lý chi tiêu** một cách minh bạch và dễ dàng.
✅ **Hoạt động 24/7** mà không cần can thiệp.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Không cần nhớ đăng nhập Wise hoặc nhập liệu.
- **Dữ liệu chính xác**: Tránh lỗi copy-paste, cập nhật tức thì.
- **Tiết kiệm thời gian**: Hàng ngày chỉ mất **5 phút** để kiểm tra Airtable thay vì 30 phút.
- **Hoạt động liên tục**: Workflow chạy 24/7, không bỏ sót giao dịch nào.
- **Dễ dàng theo dõi**: Airtable cung cấp **bảng điều khiển** để phân tích chi tiêu.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Wise** (cần **API Key** của Wise).
2. **Tài khoản Airtable** (cần **API Key** và **Base ID** của bảng cần cập nhật).
3. **Bảng Airtable** đã sẵn sàng để lưu giao dịch (các sếp có thể tạo một bảng mới với các trường như: `Date`, `Amount`, `Currency`, `Description`, `Status`).

---
:::info[CHUẨN BỊ]
- **API Key Wise**:
  - Truy cập [Wise Developer Portal](https://developers.wise.com/) để tạo API Key.
  - Chọn **Scope**: `transfers:read` (đọc giao dịch).
- **API Key Airtable**:
  - Truy cập [Airtable API Docs](https://airtable.com/api) để tạo API Key.
  - Chọn **Base ID** của bảng bạn muốn cập nhật.
- **Bảng Airtable**:
  - Đảm bảo bảng có các trường phù hợp với dữ liệu từ Wise (ví dụ: `Date`, `Amount`, `Currency`, `Description`).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. **Tải workflow** từ [link gốc](https://n8n.io/workflows/993).
2. **Nhấn "Import"** trong n8n Editor.
3. **Chọn "Import from JSON"** và dán nội dung JSON vào.

**Hoặc**:
- Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/993) và dán vào **n8n Editor** → **Create new workflow** → **Paste JSON**.

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **4 node chính**, các sếp cần cấu hình như sau:

##### **Node 1: Wise Trigger (n8n-nodes-base.wiseTrigger)**
- **Chức năng**: Khởi động workflow khi có giao dịch mới từ Wise.
- **Cấu hình**:
  - **Credentials**: Chọn `wiseApi` (đã tạo trước đó).
  - **Resource**: Để mặc định là `transfer` (giao dịch).

##### **Node 2: Wise (n8n-nodes-base.wise)**
- **Chức năng**: Lấy dữ liệu giao dịch từ Wise.
- **Cấu hình**:
  - **Credentials**: Chọn `wiseApi`.
  - **Resource**: Để mặc định là `transfer`.
  - **Parameters**:
    - `limit`: Số giao dịch muốn lấy (ví dụ: `10` để lấy 10 giao dịch mới nhất).
    - `status`: Lọc giao dịch theo trạng thái (ví dụ: `completed` để lấy giao dịch đã hoàn tất).

##### **Node 3: Set (n8n-nodes-base.set)**
- **Chức năng**: Chuẩn hóa dữ liệu trước khi gửi đến Airtable.
- **Cấu hình**:
  - **Chỉnh sửa JSON**: Các sếp có thể **biến đổi dữ liệu** để phù hợp với bảng Airtable (ví dụ: chuyển đổi định dạng ngày, tiền tệ).
  - **Ví dụ**:
    ```json
    {
      "Date": "$json["created_at"]",
      "Amount": "$json["amount"]",
      "Currency": "$json["currency"]",
      "Description": "$json["description"]",
      "Status": "$json["status"]"
    }
    ```

##### **Node 4: Airtable (n8n-nodes-base.airtable)**
- **Chức năng**: Cập nhật giao dịch vào Airtable.
- **Cấu hình**:
  - **Credentials**: Chọn `airtableApi`.
  - **Operation**: Chọn `append` (thêm mới).
  - **Table**: Chọn bảng Airtable muốn cập nhật.
  - **Fields**: Điền tên trường phù hợp với dữ liệu từ node **Set** (ví dụ: `Date`, `Amount`, `Currency`, `Description`, `Status`).
  - **Record**: Chọn `$json` để sử dụng dữ liệu đã chuẩn hóa.

---
:::note[LƯU Ý QUAN TRỌNG]
- **Kiểm tra định dạng dữ liệu**: Đảm bảo dữ liệu từ Wise phù hợp với bảng Airtable (ví dụ: ngày tháng phải là `YYYY-MM-DD`).
- **Test run trước khi bật workflow**: Sử dụng **Test tab** trong n8n để kiểm tra dữ liệu trước khi kích hoạt.
- **Bảng Airtable phải có sẵn**: Nếu bảng chưa có, các sếp cần tạo trước và **cập nhật API Key** trong n8n.
:::

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Test tab** trong n8n để chạy workflow với dữ liệu mẫu.
   - Kiểm tra kết quả trong **Airtable** để đảm bảo dữ liệu được cập nhật chính xác.
2. **Bật Workflow**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Lọc giao dịch quan trọng**:
   - Sử dụng **node Set** để lọc chỉ giao dịch có `status = "completed"` và `amount > 0` (chỉ lấy giao dịch thành công và có tiền vào).
   - **Ví dụ**:
     ```json
     {
       "Date": "$json["created_at"]",
       "Amount": "$json["amount"]",
       "Currency": "$json["currency"]",
       "Description": "$json["description"]",
       "Status": "$json["status"]"
     }
     ```
     Sau đó, thêm **node Filter** để chỉ giữ lại giao dịch phù hợp.

2. **Gửi thông báo Slack/Email khi có giao dịch mới**:
   - Thêm **node Slack** hoặc **node Email** sau node **Wise** để thông báo khi có giao dịch mới.
   - **Ví dụ**:
     - **Node Slack**: Gửi tin nhắn với nội dung: `💰 Giao dịch mới: $${{ $json["amount"] }} ${{ $json["currency"] }} - {{ $json["description"] }}`.

3. **Lưu log hoạt động**:
   - Thêm **node Log** sau node **Airtable** để ghi lại lịch sử hoạt động của workflow.
   - **Cách làm**:
     - Nhấn **+ Add node** → Chọn **Log**.
     - Chọn **Log data** và chọn `$json` để lưu toàn bộ dữ liệu.

4. **Tạo báo cáo định kỳ**:
   - Sử dụng **node Schedule** để chạy workflow hàng ngày/lần tuần và gửi báo cáo chi tiêu qua **Email** hoặc **Slack**.
   - **Ví dụ**:
     - **Node Schedule**: Chọn `cron` với biểu thức `0 0 * * *` (hàng ngày lúc 00:00).
     - Sau đó, thêm **node Email** để gửi báo cáo tổng hợp.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công theo dõi giao dịch Wise, đồng thời **đảm bảo dữ liệu chính xác và minh bạch** khi cập nhật vào Airtable. **Chỉ cần 5 phút cấu hình**, các sếp sẽ có một hệ thống **tự động hóa tài chính hoàn hảo**, hoạt động 24/7 mà không cần can thiệp.

**Hãy áp dụng ngay và tiết kiệm thời gian cho công việc quan trọng hơn!** 🚀

---
:::tip[LÀM SAO ĐỂ BẮT ĐẦU?]
1. **Cài đặt n8n** trên VPS (nếu chưa có).
2. **Tạo API Key** cho Wise và Airtable.
3. **Import workflow** và cấu hình các node theo hướng dẫn.
4. **Test run** và bật workflow.
5. **Thưởng thức thời gian tự do**! 🎉
:::

---
**Cần hỗ trợ?** Hãy để lại bình luận hoặc liên hệ với cộng đồng n8n tại [n8n Community](https://community.n8n.io/).