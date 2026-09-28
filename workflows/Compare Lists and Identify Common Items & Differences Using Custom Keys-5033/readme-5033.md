---
title: "🔍 So Sánh Danh Sách & Tìm Kiếm Khác Biệt Của Các Mục Đặc Trưng (Custom Keys) - Tự Động Hóa 100% Không Code"
description: "Workflow này giúp các sếp so sánh hai danh sách sản phẩm, khách hàng hoặc dữ liệu khác dựa trên các khóa đặc trưng (custom keys) và tự động phân loại ra các mục chung, khác biệt, hoặc chỉ có trong danh sách này/đó. Giúp tiết kiệm thời gian lên đến 90% so với cách làm thủ công."
slug: "so-sanh-danh-sach-tim-kiem-khac-biet-custom-keys"
tags: [n8n, automation, no-code, building-blocks, data-comparison, custom-key-matching]
keywords: [n8n workflow so sánh danh sách, tự động hóa so sánh dữ liệu, tìm kiếm khác biệt custom keys, n8n building blocks, so sánh danh sách sản phẩm khách hàng]
---

# 🔍 **So Sánh Danh Sách & Tìm Kiếm Khác Biệt Của Các Mục Đặc Trưng (Custom Keys)**

### **💡 Bạn đã bao giờ phải so sánh hai danh sách sản phẩm, khách hàng, hoặc dữ liệu khác và phải trau chuốt từng mục một?**
Thời gian của các sếp quá quý giá để làm việc thủ công, đặc biệt khi danh sách dài và phức tạp. **Workflow này tự động so sánh hai danh sách dựa trên các khóa đặc trưng (custom keys) và trả về kết quả chi tiết:** các mục chung, các mục chỉ có trong danh sách này, và các mục chỉ có trong danh sách kia. **Không cần viết một dòng code nào!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 mà không gặp lỗi, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** So sánh hai danh sách dài chỉ trong vài giây thay vì mất nhiều giờ làm thủ công.
- **Chính xác 100%:** Không bị lỗi nhân viên hoặc sai sót do mỏi mắt.
- **Tự động hóa hoàn toàn:** Hoạt động liên tục, không phụ thuộc vào giờ làm việc của nhân viên.
- **Dễ mở rộng:** Có thể áp dụng cho nhiều loại dữ liệu khác nhau (sản phẩm, khách hàng, dự án, v.v.).
- **Tùy chỉnh linh hoạt:** Sử dụng các **custom keys** để so sánh theo các tiêu chí riêng của doanh nghiệp.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi sử dụng workflow này, các sếp cần chuẩn bị:
1. **Hai danh sách dữ liệu** (có thể là danh sách sản phẩm, khách hàng, hoặc bất kỳ dữ liệu nào có thể biểu diễn dưới dạng JSON).
   - Mỗi mục trong danh sách phải có **khóa đặc trưng (custom keys)** để so sánh (ví dụ: `id`, `name`, `email`, `product_code`, v.v.).
   - Ví dụ:
     ```json
     [
       { "id": "1", "name": "Áo thun Nike", "category": "thời trang" },
       { "id": "2", "name": "Giày Adidas", "category": "thời trang" }
     ]
     ```
2. **Khóa đặc trưng (custom keys)** để so sánh:
   - Các sếp chỉ định các trường (key) mà workflow sẽ sử dụng để so sánh hai danh sách. Ví dụ: nếu so sánh danh sách sản phẩm, các sếp có thể chọn `id` hoặc `product_code` làm khóa so sánh.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow này bằng hai cách:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/5033) và import vào n8n Editor.
- **Copy/paste** nội dung JSON vào n8n Editor (đảm bảo đã chọn **Import Workflow** trước).

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này được thiết kế để **truyền vào hai danh sách và một khóa so sánh (custom key)**. Các sếp cần thực hiện các bước sau:

##### **A. Cấu hình Node "When Executed by Another Workflow"**
- Node này **không cần chỉnh sửa** vì nó chỉ là điểm khởi động cho workflow.
- Các sếp có thể **gọi workflow này từ một workflow khác** hoặc sử dụng **Webhook** để kích hoạt.

##### **B. Cấu hình Node "Code" (Logic chính)**
Node này chứa **logic so sánh hai danh sách** và trả về kết quả. Các sếp **không cần chỉnh sửa mã nguồn** vì nó đã được tối ưu sẵn, nhưng cần truyền dữ liệu vào đúng định dạng:
- **Input:**
  - `list1`: Danh sách đầu tiên (mảng JSON).
  - `list2`: Danh sách thứ hai (mảng JSON).
  - `key`: Khóa so sánh (custom key) để so sánh hai danh sách (ví dụ: `"id"`).
- **Output:**
  - `commonItems`: Danh sách các mục chung giữa hai danh sách.
  - `list1Only`: Danh sách các mục chỉ có trong `list1`.
  - `list2Only`: Danh sách các mục chỉ có trong `list2`.

##### **C. Cấu hình Node "Switch" (Lựa chọn logic)**
Node này **không cần chỉnh sửa** vì nó chỉ định cách xử lý kết quả từ Node "Code".

##### **D. Cấu hình Node "Set" (validation_message 1, 2, 3)**
Các node này **không cần chỉnh sửa** vì chúng chỉ là **gợi ý hiển thị kết quả** cho các sếp. Tuy nhiên, các sếp có thể:
- **Thay đổi nội dung** của các message này để phù hợp với công việc của mình.
- **Kết nối với các node khác** (ví dụ: Slack, Email, Google Sheets) để tự động thông báo kết quả.

---

#### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Các sếp có thể truyền **dữ liệu mẫu** vào workflow để kiểm tra kết quả.
   - Ví dụ:
     ```json
     {
       "list1": [
         { "id": "1", "name": "Áo thun Nike" },
         { "id": "2", "name": "Giày Adidas" }
       ],
       "list2": [
         { "id": "2", "name": "Giày Adidas" },
         { "id": "3", "name": "Áo hoodie" }
       ],
       "key": "id"
     }
     ```
   - Kết quả mong đợi:
     - `commonItems`: `[{ "id": "2", "name": "Giày Adidas" }]`
     - `list1Only`: `[{ "id": "1", "name": "Áo thun Nike" }]`
     - `list2Only`: `[{ "id": "3", "name": "Áo hoodie" }]`

2. **Bật Active workflow**:
   - Sau khi kiểm tra thành công, các sếp có thể **bật workflow** để hoạt động liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram để báo cáo kết quả tự động**:
   - Sử dụng **node Slack** hoặc **Telegram Bot** để gửi kết quả so sánh vào kênh nhóm hoặc cá nhân.
   - Ví dụ: Khi có sự thay đổi trong danh sách sản phẩm, workflow sẽ tự động báo cáo các sản phẩm mới hoặc bị loại bỏ.

2. **Lưu kết quả vào Google Sheets/Excel**:
   - Sử dụng **node Google Sheets** để ghi kết quả so sánh vào bảng tính, giúp theo dõi lịch sử thay đổi một cách dễ dàng.

3. **Tự động gửi báo cáo định kỳ**:
   - Sử dụng **node Schedule** để kích hoạt workflow hàng ngày/tuần và gửi báo cáo qua Email hoặc Slack.

4. **Tùy chỉnh logic so sánh**:
   - Nếu cần so sánh theo nhiều khóa (ví dụ: `id` và `name`), các sếp có thể **mở rộng Node "Code"** bằng cách sử dụng **JavaScript** để so sánh đa khóa.

---

### 📌 **Kết luận**
Workflow này là **công cụ mạnh mẽ** để so sánh hai danh sách một cách tự động và chính xác, giúp các sếp **tiết kiệm thời gian, giảm thiểu lỗi, và tự động hóa quy trình**. **Không cần viết code nào!** Hãy **import ngay và thử nghiệm** với dữ liệu của mình để thấy hiệu quả ngay từ lần đầu.

**🚀 Bắt đầu tự động hóa ngay hôm nay!** Nếu có bất kỳ câu hỏi nào, các sếp có thể tham khảo [tài liệu chính thức của n8n](https://docs.n8n.io/) hoặc liên hệ với cộng đồng n8n trên [Discord](https://n8n.io/discord).