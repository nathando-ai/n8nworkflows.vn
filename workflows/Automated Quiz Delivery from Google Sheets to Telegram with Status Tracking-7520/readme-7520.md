---
title: "🚀 Tự Động Gửi Đề Thi Trắc Nghiệm Từ Google Sheets Sang Telegram Với Theo Dõi Trạng Thái - Không Cần Code"
description: "Tự động hóa việc gửi đề thi trắc nghiệm từ Google Sheets sang Telegram với theo dõi trạng thái, tiết kiệm thời gian quản lý và đảm bảo không bỏ sót bất kỳ câu hỏi nào. Phù hợp cho giáo viên, quản lý khóa học online hoặc tổ chức khảo sát."
slug: "tieu-dong-gui-de-thi-trac-nghiem-tu-google-sheets-sang-telegram"
tags: [n8n, automation, google-sheets, telegram-bot, no-code, education, survey]
keywords: [n8n workflow tự động hóa, gửi đề thi từ Google Sheets sang Telegram, theo dõi trạng thái câu hỏi, tự động hóa giáo dục, bot Telegram API]
---

# 🚀 **Tự Động Gửi Đề Thi Trắc Nghiệm Từ Google Sheets Sang Telegram Với Theo Dõi Trạng Thái**

### **Giải quyết vấn đề gì?**
Các sếp giáo viên, quản lý khóa học online hoặc tổ chức khảo sát thường phải **thủ công** gửi đề thi trắc nghiệm qua Telegram cho học viên, đồng thời theo dõi trạng thái đã gửi hay chưa. Điều này gây **tốn thời gian, dễ bỏ sót** và khó quản lý khi số lượng đề thi tăng cao.

**Workflow này tự động hóa toàn bộ quá trình:**
✅ **Đọc dữ liệu** từ Google Sheets (các câu hỏi trắc nghiệm + trạng thái).
✅ **Lọc ra đề thi chưa gửi** (đánh dấu 🟨 trong cột `status`).
✅ **Gửi dưới dạng poll** qua Telegram Bot API (học viên trả lời trực tiếp).
✅ **Cập nhật trạng thái** thành ✅ để tránh gửi lại.
✅ **Thông báo** nếu không có đề thi nào cần gửi (tránh lỗi nhầm lẫn).

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7**, các sếp nên **self-host n8n** trên VPS để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần gửi thủ công mỗi đề thi.
- **Đảm bảo không bỏ sót**: Theo dõi trạng thái tự động, không có đề thi nào bị quên.
- **Trải nghiệm học viên tốt hơn**: Học viên trả lời ngay qua Telegram (không cần mở email/Google Sheets).
- **Hoạt động liên tục**: Workflow chạy tự động mỗi khi có dữ liệu mới trong Sheets.
- **Dễ dàng mở rộng**: Thêm cột mới vào Sheets mà không cần sửa code.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets**:
   - Một **bảng Google Sheets** với **các cột sau** (định dạng chính xác):
     ```
     quiz_number (Số thứ tự đề thi), question (Câu hỏi), option_a, option_b, option_c, option_d (Đáp án), status (Trạng thái: 🟨=Chưa gửi, ✅=Đã gửi)
     ```
   - Ví dụ:
     | quiz_number | question               | option_a | option_b | option_c | option_d | status |
     |-------------|------------------------|----------|----------|----------|----------|--------|
     | 1           | "Capital of Vietnam?"   | Hanoi    | Ho Chi Minh | Da Nang | Haiphong | 🟨     |

2. **Bot Telegram**:
   - Tạo **bot Telegram** từ [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Thêm bot vào **nhóm Telegram** cần gửi đề thi (bot phải là admin).

3. **Credentials trong n8n**:
   - **Google Sheets**: API Key hoặc OAuth 2.0 (cài đặt trong `n8n Credentials`).
   - **Telegram**: API Token của bot (điền vào `n8n Credentials`).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7520](https://n8n.io/workflows/7520).
- **Import vào n8n Editor**:
  - Mở n8n Dashboard → **Import** → Chọn file JSON → **Import**.
  - **Hoặc** copy toàn bộ JSON vào **Create Workflow** → Paste.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này có **7 node chính**, các sếp cần chú ý cấu hình sau:

##### **A. Node "Read Quiz Data" (googleSheets)**
- **Chọn Credential**: Chọn OAuth 2.0 hoặc API Key đã cài đặt.
- **Sheet Name**: Điền tên **exact** của bảng Sheets (không dấu cách).
- **Range**: Điền `Sheet1!A:F` (giả sử dữ liệu ở Sheet1, cột A-F).

##### **B. Node "Filter Pending Quiz" (code)**
- **Script mặc định** đã lọc ra các hàng có `status = "🟨"` và sắp xếp theo `quiz_number`.
- **Không cần chỉnh** nếu Sheets định dạng đúng.

##### **C. Node "Check Quiz Exists" (if)**
- **Cấu hình**:
  - **If**: `$.json.length > 0` (kiểm tra có đề thi nào chưa gửi không).
  - **Else**: Chạy node "Notify Missing Quiz (Telegram)" (thông báo nếu không có đề thi).

##### **D. Node "Send Telegram Poll" (httpRequest)**
- **URL**: `https://api.telegram.org/bot<API_TOKEN>/sendPoll`
  - Thay `<API_TOKEN>` bằng token bot Telegram của bạn.
- **Headers**:
  - `Content-Type: application/json`
- **Body (JSON)**:
  ```json
  {
    "chat_id": "<CHAT_ID>",
    "question": "{{ $node["Read Quiz Data"].json[0].question }}",
    "options": [
      "{{ $node["Read Quiz Data"].json[0].option_a }}",
      "{{ $node["Read Quiz Data"].json[0].option_b }}",
      "{{ $node["Read Quiz Data"].json[0].option_c }}",
      "{{ $node["Read Quiz Data"].json[0].option_d }}"
    ],
    "is_anonymous": false,
    "type": "quiz"
  }
  ```
  - Thay `<CHAT_ID>` bằng ID nhóm Telegram (lấy từ `@username_to_id_bot` hoặc Telegram API).

##### **E. Node "Update Quiz Status" (googleSheets)**
- **Operation**: `update` (cập nhật trạng thái).
- **Range**: `Sheet1!F2` (giả sử dữ liệu bắt đầu từ hàng 2, cột F).
- **Value**: `{{ $json["status"] }}` (đổi thành ✅).

##### **F. Node "Notify Missing Quiz (Telegram)" (telegram)**
- **Chỉ chạy khi không có đề thi nào chưa gửi**.
- **Message**: `"Không có đề thi nào cần gửi. Hãy kiểm tra Google Sheets!"`

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chạy **manual test** với dữ liệu mẫu trong Sheets (đánh dấu `status = 🟨`).
   - Kiểm tra Telegram có nhận được poll không.
2. **Active Workflow**:
   - Bật **Active** và chọn **Trigger Type**: `Polling` (kiểm tra Sheets mỗi 5 phút).
   - **Hoặc** sử dụng **Webhook** nếu muốn kích hoạt từ bên ngoài.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm thông báo cho admin**:
   - Sử dụng node **Telegram** để gửi tin nhắn khi có đề thi mới được gửi.
   - Ví dụ: `"Đề thi #{{ $node["Read Quiz Data"].json[0].quiz_number }} đã được gửi!"`

2. **Lưu log hoạt động**:
   - Thêm node **StickyNote** hoặc **Google Sheets** để ghi lại lịch sử gửi (thời gian, ID đề thi, người nhận).

3. **Kết hợp với Slack**:
   - Thay vì Telegram, có thể gửi thông báo qua **Slack Webhook** để quản lý dễ dàng hơn.

4. **Tự động tạo đề thi từ file Excel**:
   - Sử dụng node **HTTP Request** để upload file Excel từ máy tính vào Sheets trước khi chạy workflow.

5. **Thêm thời gian gửi tự động**:
   - Sử dụng node **Set** để đặt thời gian gửi (ví dụ: chỉ gửi vào buổi sáng 8h).

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp giáo viên, quản lý khóa học hoặc tổ chức khảo sát khỏi công việc **nhân công gửi đề thi**. Với **cấu hình đơn giản** và **không cần code**, các sếp chỉ cần:
1. Chuẩn bị **Google Sheets** với định dạng đúng.
2. **Cấu hình Telegram Bot** và Credentials.
3. **Import workflow** và kích hoạt.

**Hãy áp dụng ngay để tự động hóa quản lý đề thi của mình!** 🚀
Nếu có vấn đề, các sếp có thể **comment dưới bài** hoặc liên hệ với tác giả Ninja trên [n8n Community](https://community.n8n.io/).

---