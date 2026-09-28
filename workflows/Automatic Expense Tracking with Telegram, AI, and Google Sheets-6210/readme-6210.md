---
title: "💰 **Tự Động Hóa Theo Dõi Chi Phí Hàng Ngày Với Telegram + AI + Google Sheets (Không Cần Code!)**"
description: "Workflow tự động hóa ghi chép, phân loại và tổng hợp chi phí từ Telegram sang Google Sheets với AI tóm tắt chi tiết, giúp các sếp tiết kiệm thời gian và quản lý tài chính cá nhân hiệu quả 24/7."
slug: "tieu-dong-hoa-theo-doi-chi-phi-voi-telegram-ai-google-sheets"
tags: [n8n, automation, no-code, ai-summarization, google-sheets, telegram-bot]
keywords: [tự động hóa theo dõi chi phí, n8n workflow, ai tổng hợp chi phí, google sheets tự động, telegram bot quản lý tài chính]
---

# 🚀 **Tự Động Hóa Theo Dõi Chi Phí Hàng Ngày Với Telegram + AI + Google Sheets**

### **Giải pháp cho các sếp "quên" ghi chép chi phí hàng ngày?**
Hàng ngày, các sếp phải mất **5-10 phút** để ghi chép từng khoản chi tiêu trên điện thoại, sau đó phải tổng hợp vào cuối tháng để kiểm tra ngân sách. Kết quả? **Quên mất nhiều khoản chi, sai sót trong phân loại, và mất thời gian quý báu** để phân tích tài chính cá nhân.

**Workflow này sẽ:**
✅ **Tự động ghi chép** mọi khoản chi phí từ Telegram vào Google Sheets.
✅ **Phân loại chi tiêu** theo danh mục (ăn uống, giao thông, giải trí...) với AI.
✅ **Tóm tắt chi tiết** mỗi ngày bằng **3 mô hình AI khác nhau** (OpenAI, Anthropic, Google Gemini) để các sếp lựa chọn kết quả tốt nhất.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo **tính riêng tư và hiệu suất cao**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 30 phút/ngày** không phải ghi chép thủ công.
- **Phân loại chi phí chính xác** với AI tự động nhận diện danh mục.
- **Tóm tắt chi tiết** bằng **3 mô hình AI khác nhau** (OpenAI, Claude, Gemini) để lựa chọn kết quả tốt nhất.
- **Báo cáo tự động** vào cuối tháng, giúp các sếp **quản lý ngân sách hiệu quả**.
- **Hoạt động liên tục** mà không cần can thiệp, ngay cả khi các sếp **ngủ hoặc đi công tác**.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Telegram** và **Bot Token** (để nhận chi phí từ Telegram).
✔ **API Key** của **3 dịch vụ AI**:
   - OpenAI (ChatGPT)
   - Anthropic (Claude)
   - Google Gemini (Palm API)
✔ **Google Sheets OAuth 2.0** (để ghi chép dữ liệu vào bảng tính).
✔ **Bảng Google Sheets** đã chuẩn bị sẵn với **cột: Ngày, Mô tả, Số tiền, Danh mục, Ghi chú**.

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow:
- **Tải file JSON** từ [n8n.io/workflows/6210](https://n8n.io/workflows/6210) và import vào **n8n Editor**.
- **Copy toàn bộ JSON** từ link trên và **dán vào n8n Editor** (tab "Import").

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này sử dụng **AI Agent** để xử lý logic, vì vậy các sếp cần **cấu hình chính xác các node quan trọng**:

##### **🔹 Node 1: Telegram Trigger**
- **Chọn credentials**: `telegramApi` (đã cấu hình sẵn trong n8n).
- **Cấu hình Webhook URL**: Các sếp cần **copy URL Webhook** từ n8n và **gắn vào Telegram Bot** (thông qua API Telegram).
- **Lưu ý**:
  - Bot Telegram phải **được cấu hình để nhận tin nhắn** dưới dạng:
    ```
    Ngày: 10/10/2024
    Mô tả: Đi ăn trưa
    Số tiền: 150.000 VND
    ```
  - Nếu không rõ cách cấu hình, các sếp có thể **tạo một bot Telegram mới** và sử dụng [API Telegram](https://core.telegram.org/bots/api) để thiết lập.

##### **🔹 Node 2: AI Agent (Agent)**
- **Cấu hình Prompt**:
  - Workflow đã **sẵn sàng prompt** để AI phân loại chi phí.
  - Các sếp **không cần chỉnh sửa** nếu muốn sử dụng mặc định.
  - Nếu muốn **tùy chỉnh**, các sếp có thể mở node **Code** (node cuối cùng) và thay đổi logic.

##### **🔹 Node 3-5: 3 Mô Hình AI (OpenAI, Anthropic, Google Gemini)**
- **OpenAI (o3)**:
  - Chọn **model**: `o3` (gợi ý sử dụng `gpt-4o` hoặc `gpt-4-turbo`).
  - **Credentials**: `openAiApi` (đã cấu hình sẵn).
- **Anthropic (Claude 3.5)**:
  - **Model**: `claude-3-5-haiku-20241022`.
  - **Credentials**: `anthropicApi`.
- **Google Gemini (2.5F)**:
  - **Model**: `gemini-1.5-flash`.
  - **Credentials**: `googlePalmApi`.

##### **🔹 Node 6: Parser (Structured Output)**
- **Không cần chỉnh sửa**, AI Agent sẽ tự động **trả về dữ liệu có cấu trúc** (Ngày, Mô tả, Số tiền, Danh mục).

##### **🔹 Node 7: Append Row in Google Sheets**
- **Chọn credentials**: `googleSheetsOAuth2Api`.
- **Chọn Sheet**: Các sếp phải **chọn bảng Google Sheets** đã chuẩn bị sẵn.
- **Lưu ý**:
  - Bảng phải có **cột: Ngày, Mô tả, Số tiền, Danh mục, Ghi chú**.
  - Nếu bảng chưa có, các sếp **tạo mới** và **cập nhật cấu trúc cột**.

##### **🔹 Node 8: Code (Custom Logic - Nếu cần)**
- **Không bắt buộc**, nhưng các sếp có thể mở node này để **tùy chỉnh logic** (ví dụ: thêm logic kiểm tra số tiền, tự động phân loại).

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Gửi **một tin nhắn mẫu** từ Telegram vào bot (dạng:
    ```
    Ngày: 10/10/2024
    Mô tả: Đi ăn trưa
    Số tiền: 150.000 VND
    ```
  - Kiểm tra **Google Sheets** xem dữ liệu có được ghi chép không.
- **Bật Active**:
  - Sau khi test thành công, **bật workflow** để nó hoạt động 24/7.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram để báo cáo hàng tháng**:
   - Sử dụng **node Slack** hoặc **Telegram** để gửi **báo cáo tổng hợp chi phí** vào cuối tháng.
   - Ví dụ: "Tháng này bạn đã chi **5.000.000 VND** cho ăn uống, **3.000.000 VND** cho giao thông..."

2. **Lưu log chi phí vào cơ sở dữ liệu**:
   - Thay vì chỉ ghi vào Google Sheets, các sếp có thể **lưu vào Firebase** hoặc **PostgreSQL** để phân tích sâu hơn.

3. **Tự động cảnh báo khi chi tiêu quá ngưỡng**:
   - Sử dụng **node Code** để thêm logic:
     ```javascript
     if (amount > 2000000) {
       sendNotification("Chi phí quá cao! Hãy kiểm tra lại ngân sách.");
     }
     ```

4. **Dùng AI để dự đoán chi tiêu tháng sau**:
   - Sử dụng **node Code** để tính toán **trung bình chi tiêu** và dự đoán tháng tiếp theo.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc ghi chép chi phí thủ công, đồng thời **tự động phân loại và tổng hợp** thông tin một cách chính xác. Với **3 mô hình AI khác nhau**, các sếp có thể **lựa chọn kết quả tốt nhất** và **quản lý tài chính cá nhân hiệu quả hơn bao giờ hết**.

**Hãy áp dụng ngay và bắt đầu tự động hóa tài chính của mình!** 🚀

---
**🔗 [Tải workflow từ n8n.io](https://n8n.io/workflows/6210)**
**💬 Có thắc mắc? Hãy để lại comment bên dưới!**