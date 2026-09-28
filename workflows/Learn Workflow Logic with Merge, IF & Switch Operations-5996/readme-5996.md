---
title: "🚀 Hướng dẫn làm chủ Logic n8n với Merge, IF và Switch Nodes"
description: "Khám phá cách điều hướng và xử lý dữ liệu thông minh trong n8n qua mô hình trung tâm phân loại bưu kiện thực chiến. Phù hợp cho người mới bắt đầu."
slug: "huong-dan-logic-n8n-merge-if-switch"
tags: [n8n, automation, no-code, workflow-logic, tutorial]
keywords: [n8n workflow, logic n8n, merge node n8n, if node n8n, switch node n8n, tự động hóa]
---

# 🚀 Hướng dẫn làm chủ Logic n8n với Merge, IF và Switch Nodes

Trong quá trình tự động hóa, việc điều hướng luồng dữ liệu (Data Flow) sao cho thông minh, rẽ nhánh linh hoạt và tổng hợp chính xác là kỹ năng cốt lõi. Nếu các sếp đang cảm thấy bối rối không biết khi nào nên dùng **Merge**, khi nào dùng **IF** hay **Switch**, thì đây chính là workflow "gối đầu giường" dành cho các sếp. Được xây dựng bởi chuyên gia Lucas Peyrin, template này sẽ biến các khái niệm lập trình phức tạp thành một mô hình trung tâm phân loại bưu kiện cực kỳ trực quan!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Nắm vững 3 node logic tối quan trọng:** Hiểu sâu cách hoạt động của `Merge`, `IF`, và `Switch` mà không cần biết code.
- **Áp dụng mô hình chuẩn "Split -> Process -> Merge":** Biết cách chia nhỏ dữ liệu để xử lý và gom nhóm lại mượt mà.
- **Tối ưu hóa cấu trúc workflow:** Thay vì dùng hàng loạt node IF lồng nhau gây rối mắt, các sếp sẽ biết cách dùng Switch để rẽ nhánh khoa học.
- **Tự tin thiết kế hệ thống tự động hóa phức tạp:** Giải quyết gọn gàng các bài toán phân loại dữ liệu theo điều kiện thực tế của doanh nghiệp.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một tài khoản n8n (Cloud hoặc Self-hosted đều được).
- Không cần bất kỳ API Key hay tài khoản bên thứ ba nào khác vì đây là workflow thuần túy học tập logic dữ liệu (sử dụng các node thủ công và `Set` cơ bản).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp truy cập vào n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc copy toàn bộ JSON của workflow từ nguồn gốc và paste trực tiếp vào màn hình n8n).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này mang tính chất hướng dẫn (Tutorial) với các node trực quan:
- **Start Sorting (`manualTrigger`):** Điểm khởi đầu để kích hoạt chạy thử thủ công.
- **Create Letter, Create Parcel (`set`):** Các node tạo dữ liệu mẫu (bưu kiện và thư từ) để đưa lên "băng chuyền" dữ liệu.
- **1. Merge Node (`merge`):** Được thiết lập ở chế độ **Append**, đóng vai trò gộp các dòng dữ liệu riêng lẻ từ các nguồn khác nhau thành một danh sách duy nhất.
- **2. IF Node (`if` đóng vai trò cổng gác):** Kiểm tra xem bưu kiện có thuộc tính `is_fragile` (dễ vỡ) hay không. Nhánh `True` sẽ đi qua phần xử lý hàng dễ vỡ, nhánh `False` dành cho thư từ thông thường.
- **Re-group All Packages (`merge` thứ hai):** Kỹ thuật gom nhóm lại (Merge) sau khi đã rẽ nhánh xử lý ở node IF, đưa tất cả về chung một luồng trước khi bước vào khâu phân loại tiếp theo.
- **3. Switch Node (`switch`):** Thay thế cho hàng loạt node IF rườm rà. Node này kiểm tra trường `destination` (Điểm đến) để điều hướng bưu kiện đi các cửa tương ứng:
  - Output 0: **Send to London Bin**
  - Output 1: **Send to New York Bin**
  - Default: Các thành phố khác sẽ rơi vào **Default Bin**.
- **Final Sorted Packages (`noOp`):** Điểm cuối cùng ghi nhận toàn bộ bưu kiện đã được phân loại thành công.

#### 3. Kích hoạt ⚡️
- Click vào nút **"Execute Workflow"** ở góc dưới bên phải.
- Click lần lượt vào từng node từ trái sang phải để quan sát sự thay đổi của dữ liệu (Data Output) trên từng "băng chuyền".

### ✍️ Mẹo & gợi ý nâng cao
Sau khi đã nắm vững logic cơ bản từ template này, các sếp có thể mở rộng ứng dụng vào thực tế doanh nghiệp:
- **Tích hợp thông báo:** Thay vì chỉ dừng ở các node `Set` giả lập, hãy gắn thêm node Telegram hoặc Slack vào các nhánh phân loại để thông báo khi có đơn hàng VIP hoặc đơn hàng cần xử lý đặc biệt.
- **Lưu trữ Google Sheets:** Đưa dữ liệu đã qua node `Switch` lưu vào cácSheet tương ứng theo từng khu vực/chi nhánh.
- **Xử lý lỗi (Error Handling):** Tận dụng nhánh `Default` của node Switch để bắt các trường hợp dữ liệu không hợp lệ và gửi cảnh báo về cho bộ phận vận hành.

### 📌 Kết luận
Việc làm chủ ba node `Merge`, `IF`, và `Switch` chính là chìa khóa mở cánh cửa bước lên chuyên gia tự động hóa n8n. Hãy import workflow này ngay hôm nay, tự tay chạy thử và cảm nhận sự logic mượt mà trong từng luồng dữ liệu nhé các sếp!