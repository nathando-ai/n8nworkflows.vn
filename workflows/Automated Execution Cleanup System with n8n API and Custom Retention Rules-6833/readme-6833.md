---
title: "🧹 Tự Động Xóa Lịch Sử Thực Thi Cũ Trong n8n - Giúp n8n Chạy Nhanh & Gọn Nhẹ (Self-hosted & Cloud)"
description: "Workflow tự động hóa xóa lịch sử thực thi cũ trong n8n để tối ưu hóa hiệu suất, giảm dung lượng lưu trữ và tăng tốc độ UI. Giúp các sếp quản lý hàng trăm workflow một cách hiệu quả, chỉ giữ lại những bản ghi gần đây nhất cần thiết."
slug: "tieu-dong-xoa-lich-su-thuc-thi-cua-n8n"
tags: [n8n, automation, devops, self-hosted, database-optimization]
keywords: [tự động hóa n8n, xóa lịch sử thực thi cũ, tối ưu hiệu suất n8n, lưu trữ n8n, giảm dung lượng database]
---

# 🚀 **Tự Động Xóa Lịch Sử Thực Thi Cũ Trong n8n - Giúp n8n Chạy Nhanh & Gọn Nhẹ**

### **Nỗi Đau Của Các Sếp Khi Quản Lý Lịch Sử Thực Thi Trong n8n**
Các sếp đã từng gặp phải tình trạng nào sau đây?
- **n8n chạy chậm** vì lượng dữ liệu thực thi (executions) tích lũy quá nhiều?
- **UI trở nên chậm chạp** khi mở danh sách workflow vì quá nhiều bản ghi lịch sử?
- **Dung lượng lưu trữ tăng cao** do không xóa những bản ghi cũ không cần thiết?
- **Khó quản lý** khi phải thủ công xóa từng bản ghi trong hàng trăm workflow?

**Giải pháp?** Workflow này **tự động hóa xóa lịch sử thực thi cũ** trong n8n, **chỉ giữ lại những bản ghi gần đây nhất** (tùy chỉnh số lượng) để tối ưu hóa hiệu suất, giảm dung lượng và giữ n8n luôn **nhanh chóng và gọn nhẹ**.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để có quyền kiểm soát toàn bộ dữ liệu và hiệu suất.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tăng tốc độ UI** của n8n (Cloud hoặc Self-hosted) khi giảm lượng dữ liệu tích lũy.
✅ **Giảm dung lượng lưu trữ** bằng cách tự động xóa lịch sử cũ (không cần thủ công).
✅ **Chỉ giữ lại những bản ghi cần thiết** (tùy chỉnh số lượng gần đây nhất).
✅ **Hoạt động tự động** theo lịch trình (daily/weekly) mà không cần can thiệp.
✅ **Sử dụng chỉ các node chính thức** của n8n (không cần SQL hoặc setup phức tạp).
✅ **Áp dụng cho cả n8n Cloud và Self-hosted** một cách dễ dàng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **API Key cá nhân** cho n8n (để workflow có quyền truy cập API).
   - **Cách tạo:**
     - Mở **Settings → API Keys** → **Create a new key**.
     - Lưu API Key này để dùng sau.
2. **URL Base của n8n instance** (để cấu hình credential).
   - Ví dụ: `https://your-n8n-instance.com/api/v1` (nếu self-hosted).
3. **Thời gian chạy tự động** (daily/weekly) tùy thuộc vào nhu cầu.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/6833) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này bao gồm **5 node chính**, các sếp cần chú ý cấu hình như sau:

##### **🕒 Schedule Trigger**
- **Chức năng:** Xác định thời gian chạy tự động (daily/weekly).
- **Lưu ý:**
  - Thiết lập **interval** phù hợp (ví dụ: `0 0 * * *` để chạy hàng ngày lúc 00:00).
  - **Không cần thay đổi** nếu muốn chạy theo mặc định.

##### **📥 Get Many Executions**
- **Chức năng:** Lấy danh sách **250 thực thi gần đây nhất** từ n8n.
- **Cấu hình:**
  - **Credentials:** Chọn credential `n8nApi` (đã tạo trước).
  - **Resource:** Đặt là `execution`.
  - **Không cần thay đổi** các tham số khác.

##### **🛠️ Set Executions to Keep**
- **Chức năng:** Đặt số lượng **thực thi gần đây nhất** muốn giữ lại.
- **Cấu hình:**
  - Mở **Code Editor** của node này và thay đổi biến `executionsToKeep` thành số mong muốn (ví dụ: `10` để giữ 10 thực thi gần nhất).
  - **Lưu ý:**
    - Đặt `executionsToKeep = 0` để **xóa tất cả lịch sử thực thi cũ**.
    - **Không thay đổi** các biến khác.

##### **🧠 Code Node (Lọc Thực Thi Cần Xóa)**
- **Chức năng:** **Tự động phân loại và lọc** các thực thi cần xóa.
- **Lưu ý:**
  - **Không cần chỉnh sửa** vì logic đã được viết sẵn (nhóm theo workflow ID, sắp xếp theo thời gian, loại bỏ cũ).
  - Node này **bỏ qua** các thực thi đang chạy (`running`).

##### **🗑️ Delete Many Executions**
- **Chức năng:** Xóa **những thực thi cũ** đã được lọc.
- **Cấu hình:**
  - **Credentials:** Chọn credential `n8nApi` (giống node `Get Many Executions`).
  - **Operation:** Đặt là `delete`.
  - **Resource:** Đặt là `execution`.
  - **Không cần thay đổi** các tham số khác.

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Chạy thử với **dữ liệu mẫu** để đảm bảo logic hoạt động.
- **Bật Active:** Sau khi kiểm tra, **bật workflow** để chạy tự động theo lịch trình.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram** để thông báo khi xóa thành công:
   - Sử dụng node **Slack/Telegram** sau node `Delete Many Executions` để gửi tin nhắn cảnh báo.
2. **Lưu log xóa** vào Google Sheets/Notion:
   - Thêm node **Google Sheets** hoặc **Notion** để ghi lại lịch sử xóa (Workflow ID, số lượng xóa, thời gian).
3. **Chạy thử trên staging trước**:
   - **Không bao giờ chạy trực tiếp trên production** mà không kiểm tra trước.
   - Thử với **số lượng thực thi nhỏ** trước khi áp dụng cho toàn bộ hệ thống.
4. **Tối ưu hóa lịch chạy**:
   - Nếu n8n của các sếp **không quá tải**, có thể chạy **hàng tuần** thay vì hàng ngày.
   - Nếu lưu trữ rất lớn, có thể **chạy hàng ngày** vào giờ ít người dùng (ví dụ: 3h sáng).

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để các sếp **tự động hóa việc xóa lịch sử thực thi cũ** trong n8n, giúp:
✔ **Tăng tốc độ UI** và **giảm dung lượng lưu trữ**.
✔ **Giảm công việc thủ công** và **tối ưu hóa hiệu suất**.
✔ **Áp dụng dễ dàng** cho cả n8n Cloud và Self-hosted.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test trên staging** trước khi bật trên production.
3. **Bật tự động hóa** và **nhận lại một n8n nhanh chóng, gọn nhẹ!**

---
**💬 Cần hỗ trợ thêm?** Liên hệ với tác giả **Arlin Perez** (QA Engineer chuyên automation) qua [email](mailto:arlin.perez@example.com) hoặc [X](https://twitter.com/arlin_perez) để có workflow tùy chỉnh!