---
title: "🚀 Tự Động Hoà AI Tạo Thư Tình Trái Đất - NASA Space Postcards Sang Slack (Không Cần Code)"
description: "Workflow tự động hóa lấy ảnh NASA, tạo bài thơ AI, chèn văn bản lên ảnh, và chia sẻ ngay Slack - hoàn toàn miễn phí và không cần viết code. Phù hợp cho các sếp marketing, content creator hay người yêu thích không gian."
slug: "tự-dộng-hoa-tao-thu-tinh-nasa-slack"
tags: [n8n, automation, ai-content-creation, nasa-api, slack-integration, multimodal-ai]
keywords: [n8n workflow tự động hóa, tạo thư tình không gian, chia sẻ ảnh NASA Slack, AI viết thơ, tự động hóa content marketing, không gian tự động hóa]
---

# 🚀 **Tự Động Hoà AI Tạo Thư Tình Trái Đất - NASA Space Postcards Sang Slack**

### **Giải pháp nào giúp các sếp:**
- **Tạo nội dung độc đáo** chỉ với một click, không cần viết code hay thiết kế?
- **Chia sẻ hình ảnh NASA kèm bài thơ AI** tự động lên Slack, giúp team có thêm nội dung hấp dẫn?
- **Tiết kiệm thời gian** lên đến 90% so với cách làm thủ công?

Workflow này **lấy ảnh NASA ngẫu nhiên**, **AI viết bài thơ ngắn**, **chèn văn bản lên ảnh**, và **chia sẻ ngay Slack** - hoàn toàn tự động hóa! Đặc biệt, nó phù hợp cho các sếp **marketing, content creator, hoặc người yêu thích không gian**.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 ổn định, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) thay vì dùng phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tạo nội dung AI độc đáo** chỉ trong vài giây, không cần viết thủ công.
- **Chia sẻ hình ảnh NASA kèm bài thơ** lên Slack, giúp team có thêm nội dung hấp dẫn.
- **Tiết kiệm thời gian** lên đến 90% so với cách làm thủ công.
- **Hoạt động liên tục** 24/7, không cần can thiệp của con người.
- **Phù hợp cho marketing, content creator, hoặc người yêu thích không gian**.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản NASA API** (miễn phí, đăng ký tại [NASA API](https://api.nasa.gov/)).
2. **Tài khoản OpenAI API** (đăng ký tại [OpenAI](https://platform.openai.com/), chọn mô hình `gpt-4.1-mini`).
3. **Tài khoản Slack** và **credential Slack App** (cài đặt tại [Slack API](https://api.slack.com/)).
4. **Channel Slack** để chia sẻ kết quả (cần chọn trong workflow).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Mở [n8n Editor](https://n8n.io/editor).
2. Nhấn **Import** và chọn file JSON (hoặc paste JSON từ [link gốc](https://n8n.io/workflows/10872)).
3. Chọn **Create Workflow** để bắt đầu cấu hình.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **10 node**, các sếp cần chú ý cấu hình các node sau:

##### **🔹 Node "Get NASA APOD" (nasa)**
- **Tham số cần điền:**
  - `apiKey`: API Key từ NASA (mượn từ tài khoản đăng ký).
  - `count`: Đặt giá trị `1` (lấy 1 ảnh ngẫu nhiên).

##### **🔹 Node "OpenAI Chat Model" (lmChatOpenAi)**
- **Tham số cần điền:**
  - `apiKey`: API Key từ OpenAI.
  - `model`: Chọn `gpt-4.1-mini` (đã mặc định trong workflow).
  - **Prompt mẫu (cần chỉnh sửa):**
    ```plaintext
    Tôi là một nhà thơ không gian. Viết một bài thơ ngắn (4-6 dòng) về ảnh này, mô tả cảm xúc và ý nghĩa của nó. Kết thúc bằng một câu hỏi thú vị về không gian.
    ```
    *Lưu ý:* Các sếp có thể tùy chỉnh prompt theo phong cách riêng.

##### **🔹 Node "Edit Image" (editImage)**
- **Tham số cần điền:**
  - **Operation:** Chọn `text` (để chèn văn bản lên ảnh).
  - **Text:** Sử dụng dữ liệu từ node AI (cần kết nối với node `OpenAI Chat Model`).
  - **Font, size, position:** Các sếp có thể điều chỉnh để bài thơ đẹp mắt.

##### **🔹 Node "Upload a file" & "Send a message" (slack)**
- **Tham số cần điền:**
  - **Slack Credential:** Chọn credential Slack App đã tạo.
  - **Channel:** Chọn **channel Slack** muốn chia sẻ (cần chọn **cùng channel** trong cả 2 node).
  - **File:** Chọn file ảnh đã chỉnh sửa từ node `Edit Image`.
  - **Message:** Có thể thêm văn bản bổ sung (ví dụ: "Thư tình không gian mới từ NASA!").

##### **🔹 Node "AI Agent" (agent)**
- **Tham số mặc định:**
  - Node này tự động kết nối với `OpenAI Chat Model` và `Edit Image`, không cần chỉnh sửa.

---

#### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu:**
   - Nhấn **Run Workflow** và kiểm tra kết quả trên Slack.
   - Nếu có lỗi, kiểm tra lại **credentials** và **prompt**.
2. **Bật Active workflow:**
   - Sau khi test thành công, chuyển trạng thái sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh prompt AI:**
   - Thay đổi prompt để bài thơ phù hợp với phong cách riêng (ví dụ: thơ cổ điển, thơ hiện đại, hoặc thơ khoa học viễn tưởng).
2. **Chia sẻ trên nhiều kênh:**
   - Sử dụng node **Telegram** hoặc **Email** để chia sẻ thư tình ngoài Slack.
3. **Lưu log hoạt động:**
   - Thêm node **Google Sheets** hoặc **Notion** để ghi lại lịch sử tạo thư tình.
4. **Tạo danh sách ảnh NASA:**
   - Sử dụng node **Set** để lưu danh sách ảnh NASA đã lấy trước đó.

---

### 📌 **Kết luận**
Workflow này giúp các sếp **tạo nội dung AI độc đáo chỉ trong vài giây**, chia sẻ ngay Slack mà **không cần viết code**. Phù hợp cho:
✅ **Marketing** muốn nội dung độc đáo.
✅ **Content creator** tìm kiếm ý tưởng mới.
✅ **Người yêu thích không gian** muốn chia sẻ hình ảnh NASA.

**Hãy áp dụng ngay và làm cho team mình có thêm những thư tình không gian độc đáo!** 🚀

---