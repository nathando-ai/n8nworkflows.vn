---
title: "🚀 Hướng dẫn sử dụng hàm itemMatching() trong n8n Code Node để đồng bộ dữ liệu thông minh"
description: "Khám phá cách sử dụng itemMatching() trong n8n Code Node để khôi phục và liên kết dữ liệu từ các bước trước đó một cách dễ dàng và chính xác."
slug: "huong-dan-su-dung-item-matching-trong-n8n"
tags: [n8n, automation, code-node, javascript, data-mapping]
keywords: [n8n workflow, itemMatching, n8n Code node, tự động hóa dữ liệu, javascript trong n8n]
---

# 🚀 Hướng dẫn sử dụng hàm itemMatching() trong n8n Code Node

Trong quá trình xây dựng các kịch bản tự động hóa nâng cao, các sếp thường xuyên phải đối mặt với bài toán: **Lọc bớt dữ liệu** (để tối ưu hóa tốc độ xử lý hoặc gọi API) ở các bước giữa, nhưng sau đó lại **cần khôi phục lại các trường thông tin ban đầu** (như email, số điện thoại, ID...) ở các bước tiếp theo. 

Nếu xử lý thủ công bằng các vòng lặp thông thường, code sẽ trở nên phức tạp và dễ phát sinh lỗi. May mắn thay, n8n cung cấp sẵn một "vũ khí bí mật" cực kỳ mạnh mẽ mang tên **`itemMatching()`**. Bài viết này sẽ hướng dẫn các sếp cách áp dụng hàm này thông qua workflow mẫu chính thức từ n8n Team!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Nắm vững kỹ thuật xử lý dữ liệu nâng cao:** Hiểu rõ cách liên kết dữ liệu giữa các nhánh hoặc các bước trước/sau trong n8n.
- **Tối ưu hóa Code Node:** Viết code ngắn gọn, sạch sẽ, tận dụng triệt để các hàm có sẵn của n8n thay vì tự viết logic phức tạp.
- **Linh hoạt biến đổi dữ liệu:** Dễ dàng lọc bỏ thông tin thừa để tiết kiệm tài nguyên, sau đó khôi phục lại khi cần thiết.
- **Áp dụng ngay vào thực chiến:** Giải quyết các bài toán đồng bộ CRM, cơ sở dữ liệu khách hàng phức tạp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n (Cloud hoặc Self-hosted).
- Workflow mẫu từ n8n Team (Workflow ID: 1966 - `itemMatching() usage example`).
- Kiến thức cơ bản về JavaScript (đối với Code node).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể truy cập kho workflow chính thức của n8n, tìm kiếm với từ khóa `itemMatching() usage example` (hoặc ID `1966`) và copy JSON để paste trực tiếp vào n8n Editor của mình.

Workflow này bao gồm 4 nodes cơ bản:
1. **When clicking "Execute Workflow" (`manualTrigger`):** Node kích hoạt thủ công để test.
2. **Customer Datastore (`n8nTrainingCustomerDatastore`):** Tạo dữ liệu mẫu (danh sách khách hàng gồm tên, email, v.v.).
3. **Code (`code`):** Nơi thực hiện việc lọc dữ liệu và ứng dụng `itemMatching()`.
4. **Edit Fields (`set`):** Node bổ trợ định dạng lại dữ liệu đầu ra nếu cần.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Hãy chú ý cách hoạt động của các khối logic bên trong workflow này thông qua 3 giai đoạn chính:

- **Generate example data (Tạo dữ liệu mẫu):** 
  Node `Customer Datastore` sẽ sinh ra một tập dữ liệu khách hàng ban đầu đầy đủ các thông tin (Tên, Email, ID,...).
- **Reduce the data (Thu gọn dữ liệu - Xóa bớt thông tin):** 
  Trong node **Code**, dữ liệu sẽ được xử lý để loại bỏ tất cả các trường, **chỉ giữ lại tên khách hàng** nhằm mô phỏng tình huống tối ưu hóa hoặc cắt giảm payload.
- **Restore (Khôi phục dữ liệu ban đầu):** 
  Sử dụng hàm **`itemMatching(itemIndex: Number)`** trong Code node để chiếu ngược lại dữ liệu hiện tại với dữ liệu gốc ban đầu, từ đó **lấy lại được địa chỉ email** hoặc các thông tin đã bị lược bỏ trước đó.
  
> *Lưu ý:* Ví dụ này sử dụng mã nguồn **JavaScript**. Nếu các sếp ưa chuộng Python, có thể tham khảo tài liệu [Retrieve linked items from earlier in the workflow](https://docs.n8n.io/code/cookbook/builtin/itemmatching/) trên trang chủ n8n để chuyển đổi cú pháp tương ứng.

#### 3. Kích hoạt ⚡️
- Nhấn nút **"Execute Workflow"** để chạy thử nghiệm thủ công.
- Kiểm tra kết quả trả về ở tab Output của Code node để thấy cách hàm `itemMatching()` khôi phục thành công các trường dữ liệu bị thiếu.
- Bật công tắc **Active** nếu muốn lưu trữ và đưa vào sử dụng trong các kịch bản thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Ứng dụng trong xử lý API lớn:** Khi gọi các API trả về lượng dữ liệu khổng lồ (hàng nghìn dòng), các sếp có thể lọc lấy các trường cần thiết để tính toán nhẹ nhàng, sau đó dùng `itemMatching()` gắn ngược lại ID gốc để update database.
- **Kết hợp thông báo:** Sau khi xử lý xong dữ liệu được khôi phục, có thể kết nối thêm các node **Slack** hoặc **Telegram** để bắn báo cáo danh sách khách hàng đã xử lý về điện thoại.
- **Lưu log tự động:** Đưa dữ liệu sau khi khôi phục vào **Google Sheets** hoặc **Notion** để làm kho lưu trữ lịch sử hoạt động.

### 📌 Kết luận
Hàm `itemMatching()` là một kỹ thuật cực kỳ giá trị giúp các sếp làm chủ hoàn toàn dòng chảy dữ liệu (data flow) trong n8n mà không gặp trở ngại khi phải biến đổi, thu gọn hay khôi phục thông tin. Hãy áp dụng ngay vào workflow của mình để tối ưu hóa hiệu suất tự động hóa nhé!