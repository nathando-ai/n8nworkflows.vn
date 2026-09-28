---
title: "🚀 Kiểm tra kỹ năng JSON với thử thách tương tác và phản hồi ngay lập tức"
description: "Workflow tương tác giúp người dùng luyện tập tạo JSON cho các kiểu dữ liệu cơ bản (string, number, boolean, null, array, object) và nhận phản hồi tức thời."
slug: "kiem-tra-ky-nang-json-thu-thach-tuong-tac"
tags: [n8n, automation, no-code, json, learning, interactive]
keywords: [n8n workflow, tự động hóa, luyện tập json, json basics, n8n tutorial]
---

# 🚀 Kiểm tra kỹ năng JSON với thử thách tương tác và phản hồi ngay lập tức

Bạn thường cảm thấy bối rối khi làm việc với JSON trong n8n? Việc nhớ sự khác biệt giữa `null` và chuỗi rỗng, giữa số và chuỗi số, hoặc cách khai báo mảng và đối tượng có thể làm chậm tiến độ xây dựng workflow. Workflow **"Test Your JSON Skills with Interactive Challenges and Instant Feedback"** của Lucas Peyrin giải quyết chính xác nỗi đau này bằng cách đưa ra một môi trường thực hành trực tiếp trong n8n: bạn sửa các node **Test - …**, chạy workflow và ngay lập tức thấy đường xanh (đúng) hoặc đỏ (sai) để điều chỉnh cho đến khi thành công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 (đặc biệt nếu bạn muốn chia sẻ với team hoặc dùng làm bài kiểm tra nội bộ), các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Luyện tập thực tế**: Thực hiện ngay trong n8n mà không cần công cụ bên ngoài.
- **Phản hồi tức thời**: Mỗi lần chạy workflow cho bạn biết ngay kết quả đúng/sai.
- **Nắm vững các kiểu dữ liệu JSON cơ bản**: string, number, boolean, null, array, object – nền tảng cho mọi thao tác dữ liệu sau này.
- **Tự tin áp dụng**: Sau khi hoàn thành test, bạn sẽ viết JSON trong các node Set, Function, HTTP Request… mà không ngại.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n**: Đã cài đặt (local, Docker, hoặc VPS) và có quyền truy cập vào Editor.
- **Không cần credentials bên ngoài**: Workflow chỉ sử dụng các node nội bộ (Manual Trigger, Set, If, NoOp, Stop and Error, HTML). Do đó, bạn không phải cấu hình API key hoặc kết nối dịch vụ nào.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Sao chép toàn bộ JSON workflow từ trang gốc (nút **Download** hoặc **Copy to Clipboard**).
2. Trong n8n Editor, chọn **Import** → **Upload file** hoặc **Paste** JSON vào ô và nhấn **Import**.
3. Workflow sẽ xuất hiện với tên **🧑‍🎓 Test Your JSON Skills with Interactive Challenges and Instant Feedback**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow được thiết kế để bạn **sửa các node "Test - …"** theo hướng dẫn trên sticky note. Dưới đây là danh sách các node cần quan tâm và cách cấu hình:

| Node (tên chính xác) | Loại | Mục tiêu chỉnh sửa |
|----------------------|------|-------------------|
| **Start Test!** | manualTrigger | Node khởi động – không cần chỉnh sửa, chỉ nhấn **Execute Workflow** để bắt đầu. |
| **Test - String** | set | Tạo JSON `{ "my_string": "I love automation" }`. |
| **Test - Number** | set | Tạo JSON `{ "product_id": 12345, "price": 99.99 }`. |
| **Test - Boolean** | set | Tạo JSON `{ "is_active": true, "has_permission": false }`. |
| **Test - Null** | set | Tạo JSON `{ "middle_name": null }`. |
| **Test - Array** | set | Tạo JSON `{ "tags": ["n8n", "automation", 2024] }`. |
| **Test - Object** | set | Tạo JSON `{ "user": { "name": "Alex", "id": 987 } }`. |
| **Answer - …** (string, number, boolean, null, array, object) | set | Node này chứa **đáp án đúng** – chỉ dùng để tham khảo, không cần sửa. |
| **Check - …** (string, number, boolean, null, array, object) | if | Node kiểm tra; không cần chỉnh sửa, nhưng quan sát kết nối để biết đường đi đúng/sai. |
| **Success - …** | noOp | Node báo thành công (đường xanh). |
| **Error - …** | stopAndError | Node báo lỗi (đường đỏ). |
| **🎉 SUCCESS 🎉** | html | Hiển thị thông báo chúc mừng khi tất cả các bước đều đúng. |

**Chi tiết chỉnh sửa từng bước (theo sticky note trên canvas):**

- **Step 1: The String** → Mở node **Test - String**, trong trường **JSON** (Set options → Keep Only Set → Set JSON) nhập:
  ```json
  {
    "my_string": "I love automation"
  }
  ```
- **Step 2: Number** → Mở node **Test - Number**, nhập:
  ```json
  {
    "product_id": 12345,
    "price": 99.99
  }
  ```
- **Step 3: Boolean** → Mở node **Test - Boolean**, nhập:
  ```json
  {
    "is_active": true,
    "has_permission": false
  }
  ```
- **Step 4: Null** → Mở node **Test - Null**, nhập:
  ```json
  {
    "middle_name": null
  }
  ```
- **Step 5: Array** → Mở node **Test - Array**, nhập:
  ```json
  {
    "tags": ["n8n", "automation", 2024]
  }
  ```
- **Step 6: Object** → Mở node **Test - Object**, nhập:
  ```json
  {
    "user": {
      "name": "Alex",
      "id": 987
    }
  }
  ```

Sau khi chỉnh sửa mỗi node, nhấn **Execute Workflow** (nút màu xanh trên thanh trên). Nếu đường đi từ node **Check - …** sang **Success - …** trở nên xanh → bạn đã đúng; nếu đỏ → đọc gợi ý (hint) trên sticky note và sửa lại cho đến khi xanh.

#### 3. Kích hoạt ⚡️
- Sau khi tất cả các bước đều xanh, đường dẫn sẽ dẫn tới node **🎉 SUCCESS 🎉** và hiển thị GIF chúc mừng.
- Bạn có thể bật toggle **Active** ở góc trên bên phải nếu muốn workflow luôn sẵn sàng chạy khi nhấn **Execute Workflow** (không cần thay đổi gì nữa vì workflow là manual trigger).

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm thông báo Slack/Telegram**: Sau node **🎉 SUCCESS 🎉**, chèn node **Slack** hoặc **Telegram** để gửi thông báo cho team khi một thành viên hoàn thành test.
- **Lưu log kết quả**: Kết nối node **Google Sheets** (hoặc **Airtable**) sau mỗi **Success - …** để ghi lại thời gian, tên người dùng và kết quả (đúng/sai) – hữu ích cho việc đánh giá kỹ năng nội bộ.
- **Tạo phiên bản competição**: Sao chép workflow, thay **Manual Trigger** bằng **Webhook** và xây dựng một form đơn giản (HTML hoặc Typeform) để người dùng gửi câu trả lời; workflow sẽ tự động chấm điểm và trả về điểm số.
- **Mở rộng các kiểu dữ liệu phức tạp**: Thêm các bước test cho nested objects, mảng của đối tượng, hoặc sử dụng **Function** node để kiểm tra tính hợp lệ của JSON sâu hơn.

### 📌 Kết luận
Workflow "Test Your JSON Skills with Interactive Challenges and Instant Feedback" là một công cụ học tập tuyệt vời giúp bạn và team nắm vững nền tảng JSON – yếu tố then chốt để làm việc với dữ liệu trong n8n. Thay vì đọc tài liệu khô khan, bạn sẽ thực hành ngay trong môi trường thực tế, nhận phản hồi ngay lập tức và xây dựng niềm tin trước khi áp dụng vào các workflow tự động hoá thực tế.

Hãy import ngay, thử thách bản thân và chia sẻ thành công với cộng đồng n8n nhé! 🚀