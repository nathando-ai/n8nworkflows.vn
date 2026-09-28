---
title: "🤖 Tự Động Chuyển Phiên Bản Ghi Âm Fireflies Sang Tóm Tắt AI + Slack & ClickUp - Khai Phóng Thời Gian Cho Các Sếp"
description: "Workflow này tự động chuyển phiên bản ghi âm cuộc họp từ Fireflies thành tóm tắt AI bằng Gemini, đồng thời gửi kết quả lên Slack và tạo nhiệm vụ trong ClickUp - tiết kiệm 80% thời gian tổng hợp báo cáo sau cuộc họp."
slug: "tieu-dong-chuyen-phien-ban-fireflies-sang-tom-tat-ai-slack-clickup"
tags: [n8n, automation, ai-summarization, fireflies-ai, slack, clickup, google-gemini, no-code]
keywords: [tự động hóa cuộc họp, tóm tắt AI Fireflies, n8n workflow, tự động hóa ClickUp Slack, Gemini AI, tự động hóa không code]
---

# 🚀 **Tự Động Chuyển Phiên Bản Ghi Âm Fireflies Sang Tóm Tắt AI + Slack & ClickUp**

### **Giải pháp hoàn hảo cho các sếp muốn:**
- **Tiết kiệm 80% thời gian** sau mỗi cuộc họp (không còn phải đọc lại ghi âm 1 giờ để tóm tắt).
- **Tự động hóa hoàn toàn** quá trình tổng hợp báo cáo, từ ghi âm → tóm tắt → gửi Slack → tạo nhiệm vụ ClickUp.
- **Cá nhân hóa tóm tắt** với AI Gemini, bao gồm cả danh sách **action items** (nhiệm vụ cần thực hiện).
- **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng thay vì dùng phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần đọc lại ghi âm 1 giờ để tóm tắt.
✅ **Chính xác & chuyên nghiệp**: Tóm tắt được AI Gemini với định dạng chuẩn (5-6 dòng + danh sách nhiệm vụ).
✅ **Tự động hóa hoàn toàn**: Từ ghi âm Fireflies → Slack → ClickUp, **không cần can thiệp thủ công**.
✅ **Duy trì tính liên tục**: Workflow hoạt động **24/7**, ngay cả khi các sếp nghỉ ngơi.
✅ **Tích hợp đa nền tảng**: Kết nối Slack (gửi thông báo) và ClickUp (tạo nhiệm vụ) một cách tự động.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
📌 **Tài khoản & API Keys:**
- **Fireflies.ai**: Tài khoản Fireflies và **API Key** (để lấy phiên bản ghi âm).
- **Google Gemini API**: **API Key** từ [Google AI Studio](https://makersuite.google.com/) (để sử dụng mô hình AI).
- **Slack**: **OAuth Token** (để gửi thông báo tóm tắt).
- **ClickUp**: **OAuth Token** (để tạo nhiệm vụ từ action items).

📌 **Cấu hình Fireflies:**
- **Webhook URL** của workflow (sẽ được tạo tự động khi import).
- **Cài đặt Webhook** trong Fireflies để gửi **meetingId** khi cuộc họp kết thúc.

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/8592](https://n8n.io/workflows/8592) (chọn **Download JSON**).
2. **Mở n8n Editor** (trên VPS hoặc n8n.cloud).
3. Nhấn **Import** → Chọn file JSON vừa tải → **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/8592](https://n8n.io/workflows/8592).
2. Trong **n8n Editor**, nhấn **Import** → Chọn **Paste JSON** → Dán mã → **Import**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Node 1: Firefly Webhook (Trigger)**
- **Không cần chỉnh sửa** (n8n sẽ tự động tạo URL webhook).
- **Cần thiết**: Các sếp phải **cài đặt Webhook** trong Fireflies:
  - Mở **Settings** → **Webhooks** → **Add Webhook**.
  - **URL**: `https://[your-n8n-domain]/fireflies-n8n-core47-agent` (URL này sẽ được hiển thị khi import xong).
  - **Event**: Chọn **Meeting Completed**.
  - **Payload**: Chọn **Meeting ID**.

#### **🔹 Node 2: Get a transcript (Lấy phiên bản ghi âm)**
- **Credentials**: Chọn **firefliesApi** (đã tạo khi import).
- **Không cần chỉnh sửa** (n8n sẽ tự động lấy phiên bản ghi âm từ **meetingId** được gửi từ Webhook).

#### **🔹 Node 3: Split Out & Aggregate (Xử lý văn bản)**
- **Không cần chỉnh sửa** (n8n sẽ tự động chia phiên bản thành câu và ghép lại thành một khối văn bản).

#### **🔹 Node 4: Google Gemini Chat Model (AI Tóm Tắt)**
- **Credentials**: Chọn **googlePalmApi** (đã tạo khi import).
- **Không cần chỉnh sửa** (n8n sẽ tự động gửi văn bản đến Gemini với **prompt** đã định sẵn):
  ```plaintext
  "Act as a professional meeting summarizer. Generate:
  1. A concise summary (5-6 lines, simple wording).
  2. A list of action items (each with a title and description)."
  ```

#### **🔹 Node 5: Summary Generator (AI Agent)**
- **Không cần chỉnh sửa** (n8n sẽ tự động xử lý văn bản qua mô hình AI).

#### **🔹 Node 6: Cleans AI response (Làm sạch kết quả AI)**
- **Không cần chỉnh sửa** (n8n sẽ tự động **xóa code fences** và **parse JSON** để lấy kết quả sạch).

#### **🔹 Node 7: Extracts action items (Trích xuất nhiệm vụ)**
- **Không cần chỉnh sửa** (n8n sẽ tự động **tách danh sách nhiệm vụ** thành định dạng `{title, description}`).

#### **🔹 Node 8: Send a message (Gửi Slack)**
- **Credentials**: Chọn **slackOAuth2Api** (đã tạo khi import).
- **Chỉnh sửa (nếu cần)**:
  - **Channel**: Chọn kênh Slack muốn gửi tóm tắt (ví dụ: `#meeting-summaries`).
  - **Message Format**: Có thể chỉnh sửa **template** để thay đổi nội dung thông báo.

#### **🔹 Node 9: Create a task (Tạo nhiệm vụ ClickUp)**
- **Credentials**: Chọn **clickUpOAuth2Api** (đã tạo khi import).
- **Chỉnh sửa (nếu cần)**:
  - **List Name**: Chọn danh sách ClickUp muốn tạo nhiệm vụ (ví dụ: `Action Items`).
  - **Task Name**: Có thể thay đổi **template** để tự động đặt tên nhiệm vụ (ví dụ: `📝 [Action] {title}`).

---

### **3. Kích hoạt ⚡️**
1. **Test Run (Kiểm tra thử)**:
   - Nhấn **Run Workflow** và chọn **meetingId** từ một cuộc họp đã hoàn thành.
   - Kiểm tra kết quả trên **Slack** và **ClickUp** để đảm bảo workflow hoạt động đúng.

2. **Bật Active**:
   - Sau khi test thành công, chuyển **status** từ **Inactive** sang **Active**.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **🔹 Mở rộng với Telegram/Email**
- **Thêm node Telegram Bot** (n8n-nodes-base.telegram) để gửi tóm tắt qua Telegram.
- **Thêm node Email** (n8n-nodes-base.email) để gửi báo cáo định kỳ cho các sếp.

### **🔹 Lưu log & Monitoring**
- **Thêm node Sticky Note** (n8n-nodes-base.stickyNote) để lưu **log** của mỗi cuộc họp.
- **Kết nối với Google Sheets** (n8n-nodes-base.googleSheets) để lưu tất cả tóm tắt vào một bảng Excel.

### **🔹 Tùy chỉnh Prompt cho Gemini**
- Nếu muốn **tóm tắt chuyên sâu hơn**, chỉnh sửa **prompt** trong node **Google Gemini Chat Model**:
  ```plaintext
  "Act as a professional meeting summarizer. Generate:
  1. A detailed summary (10 lines, include key decisions).
  2. A list of action items with deadlines and assigned owners."
  ```

### **🔹 Tự động gửi báo cáo định kỳ**
- **Thêm node Set Interval** (n8n-nodes-base.setInterval) để gửi **báo cáo tuần/month** từ ClickUp.

---

## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công tóm tắt ghi âm, đồng thời **tự động hóa hoàn toàn** quá trình từ ghi âm → tóm tắt → gửi Slack → tạo nhiệm vụ ClickUp.

**🚀 Hãy áp dụng ngay để:**
✔ **Tiết kiệm 80% thời gian** sau mỗi cuộc họp.
✔ **Tăng cường hiệu quả làm việc** với tóm tắt AI chuyên nghiệp.
✔ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**Bắt đầu ngay!** Import workflow, cấu hình các API Key, và **khám phá sức mạnh của tự động hóa không code**. 💪

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/8592)** | **📌 [Cài đặt VPS cho n8n](https://tino.vn/vps-n8n?affid=388)**