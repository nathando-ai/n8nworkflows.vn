---
title: "🎉 Tự Động Hóa Trivia Hàng Ngày Cho Slack Với OpenTDB & Google Sheets - Icebreaker Siêu Đơn Giản"
description: "Workflow tự động hóa gửi câu trivia ngẫu nhiên từ OpenTDB lên Slack hàng ngày và lưu trữ vào Google Sheets để xây dựng kho câu hỏi tái sử dụng. Giúp các sếp tiết kiệm thời gian và tạo không khí làm việc vui vẻ chỉ với 1 dòng code."
slug: "tieu-dong-hoa-trivia-hang-ngay-slack-opentdb-google-sheets"
tags: [n8n, automation, no-code, slack, google-sheets, opentdb, icebreaker, team-building]
keywords: [n8n workflow trivia, tự động hóa slack, câu hỏi trivia hàng ngày, tự động hóa google sheets, icebreaker tự động, tự động hóa team building]
---

# 🚀 **Tự Động Hóa Trivia Hàng Ngày Cho Slack Với OpenTDB & Google Sheets**

## **Giới Thiệu**
Bạn đã bao giờ muốn tạo một **icebreaker** (hoạt động phá băng) hàng ngày cho đội nhóm mình trên Slack mà không cần phải làm thủ công? Hay muốn xây dựng một **kho câu hỏi trivia** để tái sử dụng trong tương lai? Workflow này sẽ **tự động lấy câu hỏi trivia ngẫu nhiên từ OpenTDB**, gửi lên Slack và **lưu trữ vào Google Sheets** để bạn có thể theo dõi và sử dụng lâu dài.

Không cần viết một dòng code nào cả – chỉ cần **import workflow** và cấu hình vài bước đơn giản là xong!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** – Không cần phải tìm kiếm câu hỏi hàng ngày.
✅ **Tạo không khí làm việc vui vẻ** – Icebreaker tự động hàng ngày giúp đội nhóm gần gũi hơn.
✅ **Lưu trữ dài hạn** – Tất cả câu hỏi được ghi lại vào Google Sheets, có thể sử dụng lại cho các sự kiện khác.
✅ **Cá nhân hóa** – Chọn độ khó (dễ, trung bình, khó) và định thời gian tự động.
✅ **Hoạt động liên tục** – Workflow chạy tự động hàng ngày, không cần can thiệp.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Slack** (để gửi câu hỏi vào channel).
✔ **Tài khoản Google** (để lưu trữ câu hỏi vào Google Sheets).
✔ **API Key của OpenTDB** (không cần, vì workflow sử dụng API công khai).
✔ **File Google Sheets** (để lưu trữ lịch sử câu hỏi).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. Tải workflow từ [đây](https://n8n.io/workflows/11280) (nếu có link download) hoặc sao chép JSON từ trang gốc.
2. Trên **n8n Editor**, nhấn **Import** → **Paste JSON** và dán nội dung JSON vào.
3. Nhấn **Import** để hoàn tất.

#### **Cách 2: Copy/Paste JSON**
1. Mở **n8n Editor** và tạo một workflow mới.
2. Nhấn **Import** → **Paste JSON** và dán nội dung JSON từ [trang gốc](https://n8n.io/workflows/11280).
3. Nhấn **Import**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Cấu hình Schedule Trigger (Định thời gian chạy hàng ngày)**
- Node: **Schedule Trigger**
- Thay đổi **cron schedule** để workflow chạy vào thời gian mong muốn (ví dụ: `0 8 * * *` để chạy lúc 8h sáng hàng ngày).
- **Lưu ý:** Nếu muốn chạy vào giờ Việt Nam, hãy điều chỉnh UTC tương ứng (ví dụ: `0 1 * * *` để chạy lúc 9h sáng).

#### **🔹 Cấu hình Slack (Gửi câu hỏi lên channel)**
- Node: **Slack: Post Trivia**
- **Credentials:** Chọn hoặc tạo mới một **Slack OAuth 2.0** (nếu chưa có).
- **Channel:** Chọn channel Slack muốn gửi câu hỏi (ví dụ: `#general`).
- **Message Format:** Workflow đã định dạng sẵn, chỉ cần đảm bảo **`messageTitle`** và **`messageBody`** được truyền đúng.

#### **🔹 Cấu hình Google Sheets (Lưu câu hỏi)**
- Node: **Sheets: Append Trivia**
- **Credentials:** Chọn hoặc tạo mới một **Google Sheets OAuth 2.0**.
- **Spreadsheet:** Chọn file Google Sheets muốn lưu trữ.
- **Sheet Name:** Đảm bảo tên sheet phù hợp với cấu trúc dữ liệu (ví dụ: `Trivia_Archive`).
- **Columns:** Workflow tự động append dữ liệu vào các cột: `timestamp`, `date`, `difficulty`, `category`, `question`, `correct`, `incorrect`.

#### **🔹 Cấu hình Set: Choose Trivia Type (Chọn độ khó ngẫu nhiên)**
- Node: **Set: Choose Trivia Type**
- **Expression:** Workflow đã cấu hình sẵn để chọn ngẫu nhiên giữa `easy`, `medium`, `hard`.
- **Nếu muốn thay đổi tỷ lệ độ khó**, chỉnh sửa **`random()`** trong expression (ví dụ: `{{ $random(0, 1) === 0 ? "easy" : "medium" }}`).

#### **🔹 Cấu hình HTTP Request (Lấy câu hỏi từ OpenTDB)**
- Workflow đã cấu hình sẵn 3 branch cho **dễ, trung bình, khó** (`HTTP OpenTDB Easy`, `HTTP OpenTDB Medium`, `HTTP OpenTDB Hard`).
- **Không cần thay đổi gì** nếu muốn sử dụng API mặc định của OpenTDB.

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** để kiểm tra nếu tất cả node hoạt động đúng.
   - Kiểm tra Slack và Google Sheets xem câu hỏi đã được gửi và lưu trữ chưa.
2. **Bật Active Workflow**:
   - Sau khi test thành công, chuyển trạng thái từ **Inactive** sang **Active**.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **🔹 Kết hợp với Telegram/Email**
- Thay vì chỉ gửi lên Slack, các sếp có thể thêm **node Telegram Bot** hoặc **node Email** để gửi câu hỏi cho những người không sử dụng Slack.

### **🔹 Lưu log hoạt động**
- Thêm **node Sticky Note** hoặc **node Log** để ghi lại lịch sử câu hỏi đã chạy, giúp theo dõi và debug dễ dàng.

### **🔹 Gửi báo cáo định kỳ**
- Sử dụng **node Google Sheets** để tạo **báo cáo tổng hợp** về số lượng câu hỏi đã gửi theo tháng/năm.

### **🔹 Tăng tính tương tác**
- Thêm **node Slack Interactive Message** để cho phép người dùng trả lời câu hỏi trực tiếp trên Slack.

---

## 📌 **Kết luận**
Workflow này giúp các sếp **tự động hóa icebreaker hàng ngày** trên Slack một cách **đơn giản, hiệu quả và không cần code**. Bằng cách **lấy câu hỏi từ OpenTDB**, **gửi lên Slack** và **lưu vào Google Sheets**, bạn không chỉ tiết kiệm thời gian mà còn xây dựng một **kho câu hỏi trivia** để sử dụng lâu dài.

**Hãy import workflow ngay hôm nay và làm cho đội nhóm của mình vui vẻ hơn!** 🎉

---
**💡 Cần hỗ trợ thêm?** Hãy để lại comment bên dưới hoặc liên hệ với cộng đồng n8n để được hỗ trợ!