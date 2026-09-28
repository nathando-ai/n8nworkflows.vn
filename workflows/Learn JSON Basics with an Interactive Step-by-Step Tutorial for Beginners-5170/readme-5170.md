---
title: "🚀 Học cơ bản về JSON trong n8n qua Workshop Tương tác Thực chiến"
description: "Hướng dẫn chi tiết cách làm chủ JSON, các kiểu dữ liệu và cách truyền dữ liệu giữa các node trong n8n thông qua workflow tương tác từng bước cực kỳ trực quan."
slug: "hoc-co-ban-ve-json-trong-n8n-workshop-tuong-tac"
tags: [n8n, automation, no-code, json, tutorial]
keywords: [n8n workflow, học json cơ bản, n8n expressions, tự động hóa no-code, dữ liệu json]
---

# 🚀 Học cơ bản về JSON trong n8n qua Workshop Tương tác Thực chiến

Các sếp mới bước chân vào thế giới tự động hóa với n8n chắc chắn sẽ có lúc cảm thấy bối rối trước các khái niệm như **JSON**, **Key/Value**, **Array**, **Object** hay cách dùng **Expressions** để truyền dữ liệu giữa các node. Đừng lo lắng! Thay vì phải đọc tài liệu khô khan, tác giả *Lucas Peyrin* đã thiết kế một workflow cực kỳ thông minh giúp các sếp vừa bấm nút vừa học trực tiếp trên giao diện n8n mà không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Hiểu sâu bản chất JSON:** Nắm vững cấu trúc Key & Value, các kiểu dữ liệu (String, Number, Boolean, Array, Object, Null).
- **Thành thạo n8n Expressions:** Biết cách dùng cú pháp `{{ }}` để "hút" dữ liệu từ node trước sang node sau cực kỳ linh hoạt.
- **Tự tin "lên đồ" workflow phức tạp:** Xử lý trơn tru các luồng dữ liệu tự động mà không sợ lỗi kiểu dữ liệu (data type mismatch).
- **Thực hành trực quan:** Vừa chạy test vừa quan sát kết quả trả về ngay trong panel của n8n.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một tài khoản **n8n** (Cloud hoặc Self-hosted phiên bản bất kỳ).
- Không cần API key hay tài khoản bên thứ ba nào khác vì workflow này chỉ dùng các node nội bộ (`Set` node).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow (hoặc tải file JSON từ trang gốc [n8n Workflow #5170](https://n8n.io/workflows/5170)).
- Mở n8n Editor của các sếp, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp vào vùng làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Vì đây là một tutorial dạng tương tác, các sếp không cần kết nối API hay tài khoản gì cả. Hãy thực hiện theo đúng quy trình sau để học:

1. **Bấm nút "Execute Workflow":** Bắt đầu từ node `Execute to Start` (Manual Trigger).
2. **Khám phá từng node theo thứ tự:** Bấm lần lượt vào từng node Set dưới đây và nhìn sang panel kết quả bên phải kết hợp đọc Sticky Notes trên canvas:
   - **Key & Value:** Tìm hiểu đơn vị cơ cấu cơ bản của JSON (`"key": "value"`).
   - **String:** Học về kiểu dữ liệu văn bản (luôn nằm trong dấu ngoặc kép `" "`).
   - **Number:** Hiểu sự khác biệt giữa số (`10`) và chuỗi số (`"10"`), cực kỳ quan trọng khi làm toán.
   - **Boolean:** Làm quen với giá trị `true` hoặc `false` không có dấu ngoặc kép (dùng cho logic điều kiện If/Then).
   - **Array:** Khám phá danh sách có thứ tự được bọc trong ngoặc vuông `[...]`.
   - **Object:** Hiểu cách tổ hợp nhiều key/value lại với nhau bằng ngoặc nhọn `{...}` để tạo thành một card thông tin hoàn chỉnh.
   - **Null:** Nhận diện giá trị trống (`null`), khác hoàn toàn với số `0` hay chuỗi rỗng `""`.
   - **Using JSON (Expressions):** Node quan trọng nhất! Quan sát cách dùng cú pháp `{{ $('Number').item.json.json_example_integer }}` để bốc dữ liệu từ node trước đó.
   - **Final Exam:** Bài kiểm tra tổng hợp cuối cùng khi node này gom data từ toàn bộ các node phía trên lại thành một object hoàn chỉnh.

#### 3. Kích hoạt ⚡️
- Sau khi click qua tất cả các node và hiểu rõ cách vận hành, các sếp đã hoàn thành khóa học nhập môn JSON xuất sắc!

### ✍️ Mẹo & gợi ý nâng cao
- **Ứng dụng thực tế:** Khi viết workflow tự động hóa gửi báo cáo qua Telegram/Slack, hãy áp dụng ngay cú pháp `{{ $json.ten_bien }}` để cá nhân hóa nội dung tin nhắn.
- **Xử lý lỗi:** Khi n8n báo lỗi dạng *ExpressionError*, hãy quay lại các node cơ bản này để kiểm tra xem kiểu dữ liệu đang là String hay Number trước khi thực hiện phép tính.

### 📌 Kết luận
JSON chính là "ngôn ngữ chung" của mọi hệ thống tự động hóa và n8n. Nắm vững JSON trong lòng bàn tay, các sếp sẽ tự tin xây dựng mọi kịch bản automation từ đơn giản đến phức tạp mà không gặp bất kỳ rào cản nào. Bắt tay vào import workflow và thực hành ngay thôi các sếp ơi!