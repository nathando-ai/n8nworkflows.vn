---
title: "🚀 Tự Động Hóa Lặp Lại Dữ Liệu Mỗi 2 Giây - Cách Sử Dụng Node Set + Interval Trong n8n (Không Cần Code)"
description: "Hướng dẫn chi tiết cách tạo workflow n8n cơ bản để tự động thực hiện một hành động lặp lại định kỳ (ví dụ: cập nhật dữ liệu, gọi API, hoặc xử lý logic) mỗi 2 giờ. Phù hợp cho các sếp muốn tự động hóa quy trình đơn giản mà không cần viết code."
slug: "tieu-dong-hoa-lap-lai-moi-2-gio-voi-n8n"
tags: [n8n, automation, no-code, node-set, node-interval, workflow-cơ-bản]
keywords: [n8n workflow cơ bản, tự động hóa lặp lại, node set n8n, interval trigger, tự động hóa không code]
---

# 🚀 **Tự Động Hóa Lặp Lại Dữ Liệu Mỗi 2 Giây - Cách Sử Dụng Node Set + Interval Trong n8n**

Bạn có bao giờ phải làm một việc lặp lại như **cập nhật dữ liệu, gọi API, hoặc xử lý logic** mà không muốn phải nhớ hoặc lập trình? Ví dụ như:
- **Cập nhật giá trị biến** cho một quy trình khác sau mỗi 2 giờ.
- **Gọi một API** định kỳ để lấy thông tin mới nhất.
- **Xử lý logic** (như tính toán, chuyển đổi dữ liệu) tự động mỗi khi có yêu cầu.

Thì **workflow này** chính là giải pháp **100% không code** giúp bạn tự động hóa những tác vụ lặp lại một cách dễ dàng và hiệu quả!

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhớ hoặc lập trình để chạy tác vụ lặp lại.
- **Chính xác và đáng tin cậy**: Workflow chạy tự động theo lịch trình đã thiết lập.
- **Dễ dàng mở rộng**: Có thể kết hợp với các node khác (ví dụ: **Slack, Email, Google Sheets**) để tự động hóa quy trình phức tạp hơn.
- **Không phụ thuộc vào người dùng**: Chạy 24/7 mà không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu cầu cần thiết**
Để workflow này hoạt động, các sếp cần:
- **Tài khoản n8n** (cài đặt trên máy chủ riêng hoặc sử dụng n8n.cloud).
- **Không cần API Key hoặc tài khoản bên thứ ba** (workflow này chỉ sử dụng các node cơ bản của n8n).

---

### 🚀 **Cách Import & Lưu ý khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Bước 1: Tải file JSON của workflow từ [đây](https://n8n.io/workflows/18) (hoặc copy/paste JSON từ link trên vào n8n Editor).

Bước 2: Mở **n8n Editor** và chọn **Import Workflow** (hoặc tạo workflow mới và paste JSON).

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **3 node chính**:
1. **`2 hours Interval` (Node Interval)**
   - **Chức năng**: Gọi workflow sau mỗi **2 giờ** (hoặc thời gian khác tùy chỉnh).
   - **Cách cấu hình**:
     - Đặt **Interval** thành `2 hours` (hoặc `2h`).
     - Đảm bảo **Active** được bật.

2. **`Set` (Node Set)**
   - **Chức năng**: **Cập nhật hoặc tạo một biến** để sử dụng trong workflow.
   - **Cách cấu hình**:
     - Trong **Properties**, chọn **Operation** là `Set` (để cập nhật giá trị).
     - Đặt **Key** là tên biến bạn muốn tạo (ví dụ: `myVariable`).
     - Đặt **Value** là giá trị bạn muốn lưu (ví dụ: `"Hello, Automation!"` hoặc một giá trị động từ node trước đó).
     - **Lưu ý**: Nếu bạn muốn **gọi lại giá trị cũ**, hãy chọn **Operation** là `Get` và **Key** là tên biến đã tồn tại.

3. **`FunctionItem` (Node Function)**
   - **Chức năng**: **Xử lý logic** (nếu cần) trước khi lưu hoặc gọi lại biến.
   - **Cách cấu hình**:
     - Nếu không cần logic phức tạp, có thể bỏ qua node này hoặc đặt **JavaScript** là `return $input.all()` (để giữ nguyên dữ liệu đầu vào).
     - Nếu cần xử lý, bạn có thể viết một hàm đơn giản như:
       ```javascript
       return {
         output: {
           myVariable: "Giá trị mới sau mỗi 2 giờ"
         }
       };
       ```

#### **3. Kích hoạt ⚡️**
- **Test Run**: Chọn **Run Workflow** để kiểm tra xem nó hoạt động như mong muốn.
- **Active Workflow**: Sau khi kiểm tra, bật **Active** để workflow chạy tự động theo lịch trình.

---

### ✍️ **Mẹo & Gợi ý Nâng Cao**
1. **Kết hợp với Slack/Email**:
   - Thêm node **Slack** hoặc **Email** sau node `Set` để thông báo khi workflow chạy.
   - Ví dụ: Sau khi cập nhật biến, gửi tin nhắn Slack như:
     ```
     "Workflow đã chạy! Giá trị mới: {{ $json.myVariable }}"
     ```

2. **Lưu log vào Google Sheets**:
   - Thêm node **Google Sheets** để ghi lại lịch sử cập nhật biến.
   - Cấu hình node để ghi dữ liệu vào một sheet mới với cột `Thời gian` và `Giá trị`.

3. **Tùy chỉnh thời gian Interval**:
   - Thay đổi `2 hours` thành `1 hour`, `6 hours`, hoặc `1 day` tùy nhu cầu.

4. **Sử dụng biến trong workflow khác**:
   - Biến được tạo bởi node `Set` có thể được gọi lại trong các workflow khác bằng cách sử dụng **`{{ $json.myVariable }}`**.

---

### 📌 **Kết Luận**
Workflow này là **cơ sở cho tất cả các tự động hóa lặp lại** trong n8n. Bằng cách kết hợp **node `Set`** và **node `Interval`**, các sếp có thể:
✅ **Tự động hóa cập nhật dữ liệu** định kỳ.
✅ **Gọi API hoặc xử lý logic** một cách tự động.
✅ **Kết hợp với nhiều node khác** để xây dựng quy trình phức tạp hơn.

**Hãy thử ngay và tự động hóa những tác vụ lặp lại của mình mà không cần viết một dòng code!** 🚀

---
**💡 Gợi ý tiếp theo**: Nếu muốn tự động hóa **gửi email định kỳ** hoặc **cập nhật dữ liệu vào Google Sheets**, hãy tham khảo workflow [n8n Email Automation](link-workflow) hoặc [n8n Google Sheets Update](link-workflow).