---
title: "🍽️ **Nutrition Tracker & Meal Logger AI: Theo Dõi Thức Ăn & Báo Cáo Dinh Dưỡng Tự Động Với Telegram + Gemini AI**"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp theo dõi thực đơn hàng ngày, phân tích dinh dưỡng qua hình ảnh/âm thanh, và nhận báo cáo cá nhân hóa thông qua Telegram. Sử dụng Google Sheets lưu trữ dữ liệu và Gemini AI để phân tích thông minh - không cần viết code!"
slug: "nutrition-tracker-ai-telegram-gemini"
tags: [n8n, automation, ai-chatbot, google-sheets, telegram-bot, no-code, gemini-ai, dinh-dưỡng]
keywords: [n8n workflow dinh dưỡng, tự động hóa theo dõi thực đơn, gemini ai phân tích hình ảnh, telegram bot dinh dưỡng, google sheets tự động hóa, meal logger tự động]
---

# 🚀 **Nutrition Tracker AI: Theo Dõi Thức Ăn & Báo Cáo Dinh Dưỡng Tự Động Với Telegram + Gemini AI**

---
## **🔥 Bạn đang gặp phải những vấn đề này?**
- **Phải ghi chép thực đơn hàng ngày bằng tay?** → Tốn thời gian và dễ quên.
- **Không biết chính xác lượng calo, protein đã tiêu thụ?** → Dinh dưỡng không được tối ưu.
- **Muốn báo cáo dinh dưỡng cá nhân hóa nhưng không có công cụ tự động?** → Phải tính toán thủ công.
- **Sợ quên mục tiêu dinh dưỡng hàng ngày?** → Không có cảnh báo tự động.

**Workflow này giải quyết tất cả!** Với **Nutrition Tracker AI**, các sếp có thể:
✅ **Ghi chép thực đơn một cách tự động** qua Telegram (text, hình ảnh, âm thanh).
✅ **Phân tích dinh dưỡng thông minh** bằng Gemini AI (Google’s AI) từ hình ảnh thức ăn.
✅ **Nhận báo cáo cá nhân hóa hàng ngày** với tiến độ dinh dưỡng (calo, protein, carbohydrate).
✅ **Cập nhật mục tiêu dinh dưỡng** một cách dễ dàng qua chatbot.
✅ **Lưu trữ dữ liệu an toàn** trên Google Sheets, dễ dàng theo dõi lịch sử.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần ghi chép thủ công, chỉ cần gửi tin nhắn Telegram.
- **Dinh dưỡng chính xác**: Gemini AI phân tích hình ảnh thức ăn với độ chính xác cao.
- **Báo cáo cá nhân hóa**: Nhận tiến độ dinh dưỡng hàng ngày với biểu đồ tiến độ.
- **Hoạt động liên tục**: Workflow chạy tự động 24/7, không phụ thuộc vào thời gian làm việc.
- **Dữ liệu an toàn**: Tất cả thông tin lưu trữ trên Google Sheets, dễ dàng quản lý.
- **Cập nhật mục tiêu dễ dàng**: Thay đổi calo/protein mục tiêu chỉ bằng một tin nhắn.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo bot Telegram và lấy **API Key** (xem hướng dẫn [tại đây](https://core.telegram.org/bots/api)).
   - Thêm bot vào nhóm hoặc chat cá nhân để test.

2. **Google Sheets**:
   - Tạo **2 bảng Google Sheets** với cấu trúc sau:
     - **Profile** (dành cho thông tin người dùng: Tên, Calories_target, Protein_target).
     - **Meals** (dành cho lịch sử ăn uống: Ngày, Thức ăn, Calo, Protein, Carbs, Fats).
   - Cấp quyền cho n8n truy cập bằng **OAuth 2.0** (xem hướng dẫn [tại đây](https://developers.google.com/sheets/api/quickstart/python)).

3. **Google Gemini API**:
   - Đăng ký API Key từ [Google AI Studio](https://aistudio.google.com/).
   - Chọn **Gemini Pro** hoặc **Gemini Vision** (phù hợp với phân tích hình ảnh).

4. **n8n Self-hosted**:
   - Cài đặt n8n trên VPS (đã đề xuất trên phần trên) hoặc sử dụng n8n.cloud (miễn phí cho các sếp mới).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Import từ file JSON:
  1. Tải workflow từ [n8n.io/workflows/7756](https://n8n.io/workflows/7756) (chọn "Export").
  2. Trên n8n Editor, nhấn **"Import"** và chọn file JSON vừa tải.
- **Cách 2**: Copy/Paste JSON:
  1. Copy toàn bộ mã JSON từ file export.
  2. Trên n8n Editor, nhấn **"Import"** > **"Paste JSON"**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này có **3 khu vực chính** cần cấu hình:
##### **🔹 Khu vực 1: Telegram & Google Sheets (Cấu hình chung)**
- **Node "Telegram Trigger"**:
  - Điền **credentials**: `telegramApi` (API Key bot Telegram).
  - Chọn **Chat ID** (lấy từ `/getUpdates` trên Telegram Bot API).

- **Node "Registered?" & "Get User Info"**:
  - Điền **credentials**: `googleSheetsOAuth2Api` (OAuth 2.0 từ Google Sheets).
  - Chọn **Sheet Name**: `Profile` (bảng chứa thông tin người dùng).

- **Node "Get Meals Info"**:
  - Chọn **Sheet Name**: `Meals` (bảng chứa lịch sử ăn uống).

##### **🔹 Khu vực 2: Gemini AI (Phân tích hình ảnh/âm thanh)**
- **Node "Analyze image" & "Analyze voice message"**:
  - Điền **credentials**: `googlePalmApi` (API Key Gemini).
  - Cấu hình **custom prompt** (nếu cần):
    ```json
    {
      "prompt": "Analyze the food in this image and provide detailed nutrition information (Calories, Protein, Carbs, Fats) in Vietnamese. Return the result in a structured format."
    }
    ```

- **Node "Google Gemini Chat Model"**:
  - Điền **credentials**: `googlePalmApi`.
  - Cấu hình **model**: `gemini-pro` (hoặc `gemini-vision` nếu phân tích hình ảnh).

##### **🔹 Khu vực 3: Register Agent (Đăng ký người dùng mới)**
- **Node "Register User"**:
  - Chọn **Sheet Name**: `Profile`.
  - Cấu hình **columns**:
    - `Name`, `Calories_target`, `Protein_target` (cần điền mặc định nếu người dùng chưa chỉ định).

- **Node "Update Profile Data"**:
  - Chọn **Sheet Name**: `Profile`.
  - Cấu hình **columns** tương tự như trên.

##### **🔹 Node "Append Meal Data"**:
- Chọn **Sheet Name**: `Meals`.
- Cấu hình **columns**:
  - `Date`, `Food`, `Calories`, `Protein`, `Carbs`, `Fats`.

##### **🔹 Node "Get Report" (Báo cáo hàng ngày)**:
- Cấu hình **subworkflow** để lấy dữ liệu từ `Meals` và `Profile`.
- **Node "Get chart message" (Code)**:
  - Sửa code để hiển thị biểu đồ tiến độ (ví dụ: `📊 Calories: 50% of 2000`).
  - Dùng **Markdown** để format báo cáo đẹp mắt:
    ```markdown
    ### **Báo cáo Dinh Dưỡng Hôm Nay**
    - **Calories**: 🍎 1200/2000 (60%)
    - **Protein**: 🥩 80g/100g (80%)
    - **Carbs**: 🍞 150g/200g (75%)
    - **Fats**: 🧈 50g/70g (71%)

    **Gợi ý**: Bạn nên tăng lượng protein hôm nay!
    ```

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi tin nhắn test đến bot Telegram (ví dụ: `/start` để đăng ký).
   - Kiểm tra các node trong **Zone Red (Register Agent)** và **Zone Blue (Message Processing)**.
2. **Bật Active**:
   - Nhấn **"Active"** trên workflow để chạy liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp với Slack/Email**:
   - Thêm node **Slack** hoặc **Email** để gửi báo cáo hàng ngày thay vì Telegram.
   - Cấu hình trong **Node "Send a text message"** bằng cách thay đổi **credentials** thành `slackApi` hoặc `email`.

2. **Lưu log hoạt động**:
   - Thêm node **Google Sheets** để ghi lại lịch sử hoạt động (ví dụ: ngày giờ gửi báo cáo, nội dung tin nhắn).
   - Cấu hình **Sheet Name**: `Logs`.

3. **Báo cáo tuần/tháng**:
   - Sử dụng **Node "Execute Workflow Trigger"** để chạy báo cáo định kỳ (ví dụ: hàng tuần).
   - Cấu hình **cron job** trong n8n (ví dụ: `0 0 * * 0` để chạy Chủ Nhật 00:00).

4. **Cập nhật mục tiêu dinh dưỡng tự động**:
   - Thêm node **Google Assistant** hoặc **Fitness API** để tự động cập nhật mục tiêu dựa trên dữ liệu sức khỏe.

5. **Hỗ trợ nhiều ngôn ngữ**:
   - Sử dụng **Node "Translate"** (n8n-nodes-base.translate) để chuyển đổi báo cáo sang nhiều ngôn ngữ.

---

### 📌 **Kết luận**
**Nutrition Tracker AI** là giải pháp hoàn chỉnh để các sếp **tự động hóa theo dõi dinh dưỡng** một cách thông minh, tiết kiệm thời gian và tăng hiệu quả. Với sự kết hợp giữa **Telegram, Gemini AI và Google Sheets**, workflow này không chỉ ghi chép thực đơn mà còn **phân tích, báo cáo và tối ưu hóa** dinh dưỡng hàng ngày.

**Hành động ngay!**
1. Import workflow và cấu hình theo hướng dẫn trên.
2. Thử nghiệm với bot Telegram và cập nhật mục tiêu dinh dưỡng.
3. Nhận báo cáo cá nhân hóa hàng ngày và theo dõi tiến độ!

**💡 Lưu ý**: Nếu gặp vấn đề, liên hệ với tác giả [John Silva](mailto:johnsilva11031@gmail.com) hoặc tham khảo [diễn đàn n8n](https://community.n8n.io/) để hỗ trợ kỹ thuật.

---
**🚀 Chúc các sếp thành công với việc tự động hóa dinh dưỡng!** 🍏🥩🥑