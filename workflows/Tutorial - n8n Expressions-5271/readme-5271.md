---
title: "🚀 Học Nhanh n8n Expressions: Tự Động Hóa Dữ Liệu Không Cần Code"
description: "Hướng dẫn chi tiết cách sử dụng biểu thức n8n để kết nối dữ liệu giữa các node trong workflow. Tiết kiệm thời gian xử lý dữ liệu thủ công với các ví dụ thực tế."
slug: "hoc-nhanh-n8n-expressions-tu-dong-hoa-du-lieu"
tags: [n8n, automation, no-code, json, data-processing]
keywords: [n8n workflow, tự động hóa dữ liệu, biểu thức n8n, xử lý dữ liệu, no-code]
---

# 🚀 Học Nhanh n8n Expressions: Tự Động Hóa Dữ Liệu Không Cần Code

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp ơi! Bạn đã biết JSON là gì rồi đúng không? Bây giờ hãy cùng học cách **sử dụng nó** để kết nối dữ liệu giữa các node trong workflow n8n. Workflow này sẽ dạy các sếp cách lấy dữ liệu từ một node và sử dụng nó trong node khác bằng cách sử dụng biểu thức mạnh mẽ của n8n.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý dữ liệu thủ công
- Tăng độ chính xác khi xử lý dữ liệu
- Tự động hóa các quy trình phức tạp
- Tạo ra các workflow linh hoạt và động态
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n đã cài đặt và cấu hình
- Kiến thức cơ bản về JSON
- Dữ liệu mẫu để thực hành
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của bạn, các sếp làm theo các bước sau:

1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import" ở góc trên bên phải
3. Chọn tùy chọn "Import from URL"
4. Dán link sau vào ô nhập: `https://n8n.io/workflows/5271`
5. Nhấn "OK" để hoàn tất import

Hoặc các sếp có thể tải file JSON từ link trên và import trực tiếp từ file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Source Data"**:
   - Đây là node chứa tất cả dữ liệu mẫu cho bài học
   - Chạy node này một lần để xem cấu trúc dữ liệu
   - Dữ liệu bao gồm: tên, tuổi, danh sách kỹ năng, danh sách dự án, thông tin liên hệ

2. **Node "1. The Basics"**:
   - Học cách truy cập giá trị đơn giản
   - Biểu thức: `{{ $('Source Data').item.json.name }}`
   - Các sếp có thể thay thế `name` bằng bất kỳ trường nào khác trong dữ liệu

3. **Node "3. Working with Arrays"**:
   - Học cách truy cập phần tử trong mảng
   - Biểu thức: `{{ $('Source Data').last().json.skills[1] }}`
   - Lưu ý: Mảng trong JavaScript bắt đầu từ chỉ số 0

4. **Node "4. Going Deeper"**:
   - Học cách truy cập dữ liệu lồng nhau
   - Biểu thức: `{{ $('Source Data').last().json.contact.email }}`
   - Cấu trúc dữ liệu lồng nhau thường có nhiều cấp độ

5. **Node "5. The Combo Move"**:
   - Kết hợp các kỹ thuật đã học
   - Biểu thức: `{{ $('Source Data').last().json.projects[0].status }}`
   - Các sếp cần chú ý đến cấu trúc mảng và đối tượng

6. **Node "6. A Touch of Magic"**:
   - Học cách sử dụng hàm JavaScript trong biểu thức
   - Các ví dụ:
     - Chuyển đổi chữ hoa: `{{ $('Source Data').last().json.name.toUpperCase() }}`
     - Tính toán toán học: `{{ Math.round($('Source Data').last().json.age / 7) }}`
     - Kiểm tra kiểu dữ liệu: `{{ typeof $('Source Data').last().json.age }}`

7. **Node "9. The \"All Items\" View"**:
   - Học cách làm việc với nhiều mục đầu ra
   - Biểu thức: `{{ $('Split Out Skills').all().map(item => item.json.skills).join(', ') }}`
   - Hàm mũi tên (arrow function) là cách ngắn gọn để lặp qua các mục

8. **Node "Final Exam"**:
   - Kiểm tra kiến thức đã học
   - Node này kết hợp tất cả các kỹ thuật đã học để tạo ra một đối tượng tóm tắt cuối cùng

9. **Node "2. The n8n Selectors"**:
   - Học cách sử dụng các bộ chọn n8n
   - Các bộ chọn bao gồm: `.first()`, `.last()`, `.all()`
   - Ví dụ: `{{ $('Source Data').last().json.name }}`

10. **Node "7. Inspecting Objects"**:
    - Học cách kiểm tra đối tượng
    - Biểu thức: `{{ Object.keys($('Source Data').last().json.contact) }}`
    - Hàm này trả về một mảng chứa tên của các khóa trong đối tượng

11. **Node "8. Utility Functions"**:
    - Học cách sử dụng các hàm tiện ích
    - Biểu thức: `{{ JSON.stringify($('Source Data').last().json.contact, null, 2) }}`
    - Hàm này chuyển đổi đối tượng JSON thành chuỗi định dạng đẹp

#### 3. Kích hoạt ⚡️
Sau khi đã cấu hình các node quan trọng, các sếp cần thực hiện các bước sau:

1. Chạy thử workflow với dữ liệu mẫu
2. Kiểm tra đầu ra của từng node để đảm bảo dữ liệu được xử lý đúng
3. Bật chế độ Active cho workflow để nó chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể kết hợp các biểu thức với các node khác như Google Sheets, Email, hoặc Slack để tạo ra các workflow tự động hóa hoàn chỉnh
- Để lưu log các hoạt động, các sếp có thể thêm node "Set" để lưu trữ dữ liệu vào một đối tượng JSON
- Các sếp có thể tạo các báo cáo tự động bằng cách kết hợp các biểu thức với các node gửi email hoặc lưu vào Google Sheets
- Để tối ưu hiệu suất, các sếp nên sử dụng các bộ chọn `.first()` hoặc `.last()` thay vì `.item` khi có thể

### 📌 Kết luận
Bài học này đã dạy các sếp cách sử dụng biểu thức n8n để kết nối dữ liệu giữa các node trong workflow. Các kỹ thuật đã học sẽ giúp các sếp tiết kiệm thời gian xử lý dữ liệu thủ công và tạo ra các workflow linh hoạt và động态. Hãy áp dụng ngay những kiến thức này vào các workflow của các sếp để tự động hóa các quy trình làm việc hàng ngày!