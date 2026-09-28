---
title: "🤖 **Tự Động Hóa Phân Loại Email Gmail Bằng AI GPT-4: Giúp Các Sếp Quên Lo Lắng Về Inbox Nổ Lở!**"
description: "Workflow tự động phân loại email Gmail dựa trên nội dung thông qua AI GPT-4, gắn nhãn tự động cho tin nhắn như 'Quotation', 'Inquiry', 'Project Progress'... Giúp các sếp tiết kiệm 5-10 giờ/ngày quản lý inbox và ưu tiên tin nhắn quan trọng."
slug: "tieu-dong-hoa-phan-loai-email-gmail-bang-gpt-4"
tags: [n8n, automation, gmail, ai, gpt-4, no-code, support, business-automation]
keywords: [tự động hóa email gmail, phân loại email bằng ai, gpt-4 trong n8n, tự động gắn nhãn email, quản lý inbox hiệu quả, workflow n8n gmail]
---

# 🚀 **Tự Động Phân Loại Email Gmail Bằng AI GPT-4: Giải Pháp "Hands-Free" Cho Inbox Nổ Lở**

## 💥 **Nỗi Đau Của Các Sếp Với Inbox Nổ Lở**
Hàng trăm email mỗi ngày, giữa đống tin nhắn "Quotation", "Inquiry", "Project Progress" và "Notification" lẫn lộn, các sếp phải mất **5-10 giờ/ngày** chỉ để:
- **Quét và phân loại** email thủ công.
- **Lo lắng bỏ lỡ** tin nhắn quan trọng giữa đống spam.
- **Chỉnh sửa nhãn** không nhất quán, gây rối loạn hệ thống.

**Giải pháp?** Một **workflow tự động hóa 100% không code** sử dụng **Gmail + AI GPT-4** để phân tích nội dung và gắn nhãn tự động—giúp các sếp **tự động hóa 90% công việc quản lý inbox**!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (Đảm bảo tốc độ nhanh, không lag)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 5-10 giờ/ngày** quản lý inbox.
✅ **Phân loại email chính xác** dựa trên nội dung (không phụ thuộc vào con người).
✅ **Ưu tiên tin nhắn quan trọng** tự động (Quotation, Inquiry, Project Progress...).
✅ **Hoạt động liên tục 24/7** (không cần can thiệp thủ công).
✅ **Cá nhân hóa** theo nhu cầu của team (thêm/loại nhãn tùy ý).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (đã kích hoạt **OAuth 2.0** trong n8n).
2. **API Key OpenAI** (để sử dụng GPT-4).
3. **Nhãn Gmail đã tạo sẵn** (ví dụ: "Quotation", "Inquiry", "Project Progress", "Notification").
4. **n8n Workflow Editor** (cài đặt trên máy chủ hoặc VPS).

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/4680](https://n8n.io/workflows/4680) (chọn **Download JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Workflow Name** (ví dụ: **"Auto-Gmail-Labeling"**).
4. Nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/4680](https://n8n.io/workflows/4680).
2. Trên **n8n Editor**, nhấn **Import** → Chọn **Paste JSON**.
3. Dán mã và nhấn **Import**.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này gồm **11 node** quan trọng, các sếp **cần chỉnh sửa** các phần sau:

#### **🔹 Node 1: Gmail Trigger (GmailTrigger)**
- **Cấu hình OAuth 2.0**:
  - Đăng nhập tài khoản Gmail vào n8n.
  - Chọn **Credentials**: `gmailOAuth2`.
  - **Polling Interval**: Đặt từ **30 giây đến 5 phút** (tùy vào lượng email).
- **Lưu ý**: Nếu không muốn poll liên tục, có thể kết nối với **Webhook** (nhưng yêu cầu người dùng kích hoạt thủ công).

#### **🔹 Node 2 & 3: Get Message Content (Gmail) + OpenAI GPT-4 (lmChatOpenAi)**
- **Điền API Key OpenAI**:
  - Trên node **OpenAI GPT-4**, chọn **Credentials**: `openAiApi`.
  - Nhập **API Key** từ tài khoản OpenAI.
- **Cấu hình mô hình GPT-4**:
  - Node đã mặc định sử dụng `gpt-4-turbo-preview` (mô hình mới nhất).
  - **Không cần chỉnh sửa** trừ khi muốn thay đổi mô hình.

#### **🔹 Node 4: Assign Labels (chainLlm)**
- **Chỉnh sửa Prompt AI**:
  - Mở node **Assign Labels** → Nhấn **Edit**.
  - **Thay đổi hệ thống prompt** để phù hợp với nhãn của các sếp:
    ```json
    "system": "You are an email categorization assistant. Analyze the email content and assign one or more labels from the following list: 'Quotation', 'Inquiry', 'Project Progress', 'Notification'. Return the result in JSON format with 'labels' key containing an array of strings."
    ```
  - **Lưu ý**: **Tên nhãn trong prompt phải trùng khớp** với nhãn đã tạo trên Gmail!

#### **🔹 Node 5: JSON Parser (outputParserStructured)**
- **Chỉnh sửa Schema JSON**:
  - Mở node **JSON Parser** → Nhấn **Edit**.
  - Đảm bảo **cấu trúc JSON** trùng khớp với output từ AI:
    ```json
    {
      "labels": ["Quotation", "Inquiry"]
    }
    ```
  - Nếu AI trả về định dạng khác, phải **cập nhật schema** để n8n hiểu được.

#### **🔹 Node 6-10: Merge & Add Labels (gmail)**
- **Kiểm tra nhãn đã tạo**:
  - Trước khi chạy, các sếp **phải tạo nhãn tương ứng** trên Gmail (ví dụ: "Quotation", "Inquiry").
  - Node **Get all labels** sẽ lấy danh sách nhãn hiện có.
- **Node Add Labels**:
  - Đảm bảo **ID của nhãn** trong workflow trùng khớp với Gmail.
  - Nếu nhãn bị xóa trên Gmail, workflow sẽ **báo lỗi**.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** với **1 email mẫu**.
   - Kiểm tra **nhãn đã được gắn** trên Gmail.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển **Workflow Status** sang **Active**.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tăng Độ Chính Xác Của AI**
- **Cập nhật Prompt**:
  - Thêm ví dụ cụ thể trong prompt để AI phân loại chính xác hơn:
    ```json
    "system": "Example: If the email contains 'price', 'quote', or 'bid', assign 'Quotation'. If it's about project updates, assign 'Project Progress'."
    ```
- **Sử dụng mô hình GPT-4 mới nhất**:
  - Thay đổi node **lmChatOpenAi** sang `gpt-4-1106-preview` (nếu có).

### **2. Gửi Báo Cáo Định Kỳ**
- **Kết hợp với Slack/Telegram**:
  - Thêm node **Slack Webhook** sau node **Add Labels** để thông báo khi email mới được phân loại.
  - Ví dụ:
    ```json
    "message": "📧 Email mới được phân loại: {{ $node["Add Labels"].json["labels"] }}"
    ```

### **3. Lưu Log Cho Theo Dõi**
- **Thêm Node StickyNote**:
  - Sử dụng node **StickyNote** để lưu lịch sử phân loại (ví dụ: ngày giờ, nội dung email, nhãn gắn).
  - Có thể kết nối với **Google Sheets** để tạo báo cáo định kỳ.

### **4. Tự Động Xóa Email Sau Phân Loại**
- **Thêm Node Gmail (Delete)**:
  - Sau khi gắn nhãn, có thể thêm node **gmail** với `operation: delete` để tự động xóa email không cần thiết.

---
## 📌 **Kết Luận: Tự Động Hóa Inbox Bằng AI GPT-4**
Workflow này **giải phóng các sếp khỏi công việc vặt** quản lý email, giúp:
✔ **Tiết kiệm thời gian** (5-10 giờ/ngày).
✔ **Tăng hiệu suất** với phân loại tự động.
✔ **Giảm stress** vì không lo bỏ lỡ tin nhắn quan trọng.

**Hành động ngay!**
1. **Import workflow** theo hướng dẫn trên.
2. **Chỉnh sửa nhãn** phù hợp với team.
3. **Bật Active** và **quên lo lắng về inbox nổ lở!**

👉 **Bắt đầu tự động hóa ngay [tại đây](https://n8n.io/workflows/4680)**!