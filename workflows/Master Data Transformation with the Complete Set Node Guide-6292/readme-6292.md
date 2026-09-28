---
title: "🚀 Làm Chủ Biến Dữ Liệu n8n Với Master Data Transformation Set Node"
description: "Hướng dẫn chi tiết toàn tập cách sử dụng n8n Set Node từ cơ bản đến nâng cao: xử lý kiểu dữ liệu, biểu thức, cấu trúc phức tạp và điều kiện rẽ nhánh."
slug: "lam-chu-set-node-trong-n8n-master-data-transformation"
tags: [n8n, automation, no-code, data-transformation, n8n-tutorial]
keywords: [n8n workflow, set node n8n, xu ly du lieu n8n, bieu thuc n8n, tu dong hoa]
keywords: [n8n workflow, set node n8n, xu ly du lieu n8n, bieu thuc n8n, tu dong hoa]
---

# 🚀 Làm Chủ Biến Dữ Liệu n8n Với Master Data Transformation Set Node

Trong quá trình xây dựng các luồng tự động hóa, việc xử lý, biến đổi và định hình lại dữ liệu giữa các bước là bài toán đau đầu nhất. Nếu xử lý thủ công bằng code phức tạp, bạn sẽ mất rất nhiều thời gian. Workflow này chính là giải pháp "tất cả trong một" giúp các sếp làm chủ hoàn toàn **Set Node** trong n8n - được mệnh danh là chiếc "dao Thụy Sĩ" của tự động hóa dữ liệu!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Nắm vững kỹ thuật xử lý dữ liệu:** Hiểu rõ cách gán giá trị cơ bản, dùng biểu thức (expressions) và thao tác với cấu trúc dữ liệu phức tạp (Objects, Arrays).
- **Làm chủ tính năng "Keep Only Set":** Biết cách dọn dẹp dữ liệu rác, chỉ giữ lại các trường cần thiết cho bước tiếp theo.
- **Xử lý logic có điều kiện:** Kết hợp IF Node và Set Node để rẽ nhánh dữ liệu linh hoạt theo từng đối tượng khách hàng.
- **Tăng tốc độ thiết kế workflow:** Không còn bối rối khi cần mapping hay transform dữ liệu giữa các dịch vụ API khác nhau.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một tài khoản n8n đang hoạt động (Cloud hoặc Self-hosted đều được).
- Không cần kết nối API bên ngoài nào vì workflow này dùng dữ liệu giả lập (Test Data Input) để thực hành trực tiếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp sao chép mã nguồn JSON của workflow hoặc tạo một workflow mới trên n8n, sau đó paste trực tiếp vào giao diện Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này được thiết kế dưới dạng một "khóa học tương tác" trực tiếp trên canvas thông qua các Sticky Note và chuỗi Set Node tuần tự:
- **`0. Test Data Input` & `1. Set Basic Values`**: Nơi khởi tạo dữ liệu mẫu và gán các giá trị cơ bản (String, Number, Boolean). Các sếp hãy thử thay đổi tuổi (`user_age`) hoặc điểm số để xem dữ liệu thay đổi ở các bước sau.
- **`2. Set with Expressions`**: Học cách sử dụng cú pháp `{{ $json.fieldname }}` để gọi dữ liệu cũ, dùng `$now` để lấy thời gian thực và thực hiện phép toán JavaScript đơn giản (`{{ $json.score * 2 }}`).
- **`3. Set Complex Data`**: Thử nghiệm với Object (dữ liệu lồng nhau) và Array (mảng danh sách quyền hạn, lịch sử điểm số).
- **`4. Set Clean Output`**: Khám phá tính năng **"Keep Only Set"**. Khi bật tính năng này, n8n sẽ xóa sạch dữ liệu cũ và chỉ giữ lại những trường được định nghĩa trong node này – cực kỳ hữu ích để làm sạch API Response.
- **`Age Check` (IF Node) & Rẽ nhánh (`5a. Set Adult Data` / `5b. Set Young Adult Data`)**: Xem cách phân loại dữ liệu theo điều kiện tuổi (>25 hoặc <=25) để đưa ra các gói ưu đãi/dữ liệu khác nhau.
- **`Merge Branches` & `6. Tutorial Summary`**: Tổng hợp lại dữ liệu sau khi rẽ nhánh và hoàn tất chuỗi bài học.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử từng node thủ công (Step-by-step) để quan sát kỹ dữ liệu đầu ra ở khung bên phải của n8n.
- Đọc kỹ các ghi chú (Sticky Notes) đính kèm trên từng khu vực để hiểu sâu hơn về bản chất của Set Node.

### ✍️ Mẹo & gợi ý nâng cao
- **Ứng dụng thực tế:** Áp dụng Set Node để chuẩn hóa dữ liệu khách hàng trước khi đẩy lên Google Sheets hoặc CRM (HubSpot, Saleforce).
- **Gửi thông báo lỗi/kết quả:** Kết hợp thêm node Telegram hoặc Slack ở cuối luồng để gửi báo cáo tổng hợp dữ liệu sau khi biến đổi.
- **Tối ưu hóa:** Sử dụng tính năng "Keep Only Set" triệt để ở các node cuối cùng trước khi gọi Webhook API bên thứ ba nhằm tiết kiệm băng thông và bộ nhớ.

### 📌 Kết luận
Set Node chính là trái tim của mọi quá trình xử lý dữ liệu trong n8n. Nắm vững Set Node giúp các sếp làm chủ toàn bộ luồng tự động hóa mà không cần viết những đoạn code phức tạp. Hãy import workflow ngay và thực hành cùng các ghi chú trực quan trên màn hình nhé!