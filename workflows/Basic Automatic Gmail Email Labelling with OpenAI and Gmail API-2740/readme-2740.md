---
title: "🤖 **Tự Động Hóa Nhãn Email Gmail Thông Minh với OpenAI – Không Cần Code!**"
description: "Workflow tự động phân loại email Gmail thông minh bằng AI (OpenAI), tự động tạo nhãn mới hoặc gán nhãn phù hợp cho email mới đến. Giúp các sếp tiết kiệm 5+ giờ/ngày quản lý email thủ công."
slug: "tieu-dong-hoa-nhan-email-gmail-voi-openai"
tags: [n8n, automation, no-code, ai, gmail-api, openai, email-management]
keywords: [tự động hóa email gmail, nhãn email tự động, openai gmail, workflow n8n ai, phân loại email bằng ai, tự động tạo nhãn gmail]
---

# 🚀 **Tự Động Hóa Nhãn Email Gmail Thông Minh với OpenAI – Không Cần Code!**

### **Giải pháp cho nỗi đau "Email rối rắm, mất thời gian phân loại"**
Các sếp đã bao giờ cảm thấy **mệt mỏi** khi phải mở email một cách thủ công, đọc từng tin nhắn, rồi phân loại vào các nhãn như *"Project Alpha"*, *"Vendor Inquiry"*, hay *"Reclame"*? Hay thậm chí phải **tạo nhãn mới** mỗi khi có chủ đề mới xuất hiện?

Với **workflow này**, các sếp sẽ **tự động hóa 100% quá trình phân loại email** bằng AI (OpenAI) kết hợp với **Gmail API**, giúp:
✅ **Tiết kiệm 5-10 giờ/ngày** quản lý email thủ công.
✅ **Giảm sai sót** khi phân loại nhãn (AI phân tích chủ đề, nội dung, và gợi ý nhãn chính xác).
✅ **Tự động tạo nhãn mới** nếu không có nhãn phù hợp (với cấu trúc logic theo quy tắc của doanh nghiệp).
✅ **Giải phóng inbox** bằng cách **xóa nhãn "Inbox"** cho email không quan trọng (quảng cáo, spam) tự động.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng (không phụ thuộc vào phiên bản cloud).
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao cho AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động phân loại email** trong giây lát (không cần đọc từng tin nhắn).
- **Tạo nhãn mới tự động** với cấu trúc logic (ví dụ: *"Vendor Inquiry"* dưới nhãn *"AI"* nếu chưa tồn tại).
- **Giải phóng inbox** bằng cách **xóa nhãn "Inbox"** cho email không quan trọng (quảng cáo, spam).
- **Duy trì trật tự** trong Gmail với hệ thống nhãn thống nhất (không rối loạn nhãn tự tạo).
- **Hoạt động liên tục** 24/7, không phụ thuộc vào thời gian làm việc của các sếp.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (đã kích hoạt **Gmail API** và **OAuth 2.0**).
2. **API Key OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/account/api-keys)).
3. **Danh sách nhãn Gmail hiện có** (để AI tham khảo khi tạo nhãn mới).

---
:::note[Cách kích hoạt Gmail API]
1. Truy cập [Google Cloud Console](https://console.cloud.google.com/).
2. Tạo **projekt mới** và kích hoạt **Gmail API**.
3. Tạo **OAuth 2.0 Client ID** và cấu hình cho ứng dụng.
4. Sau đó, trong **n8n**, thêm **credentials** `gmailOAuth2` với thông tin OAuth 2.0.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow:
- **Tải file JSON** từ [n8n.io/workflows/2740](https://n8n.io/workflows/2740) và import vào **n8n Editor**.
- **Copy/paste JSON** từ link trên vào **n8n Editor** (tab "Import").

---
#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **9 node** quan trọng, các sếp cần **cấu hình kỹ** như sau:

##### **A. Cấu hình Gmail API**
- **Node: `Gmail Trigger`**
  - Chọn **credentials**: `gmailOAuth2` (đã cấu hình trước).
  - Cài đặt **thời gian poll** (ví dụ: **5 phút/lần**) để n8n kiểm tra email mới.
  - **Lưu ý**: Nếu không cấu hình OAuth 2.0, workflow **không hoạt động**.

- **Node: `Gmail - read labels`**
  - Chọn **credentials**: `gmailOAuth2`.
  - **Không cần chỉnh sửa** thêm tham số (n8n sẽ tự đọc tất cả nhãn hiện có).

- **Node: `Gmail - get message`**
  - Chọn **credentials**: `gmailOAuth2`.
  - **Không cần chỉnh sửa** (n8n sẽ lấy nội dung email từ `Gmail Trigger`).

- **Node: `Gmail - add label to message`**
  - Chọn **credentials**: `gmailOAuth2`.
  - **Không cần chỉnh sửa** (AI sẽ tự động gán nhãn sau khi phân tích).

- **Node: `Gmail - create label`**
  - Chọn **credentials**: `gmailOAuth2`.
  - **Không cần chỉnh sửa** (AI sẽ tự động tạo nhãn mới nếu cần).

##### **B. Cấu hình OpenAI**
- **Node: `OpenAI Chat Model1`**
  - Chọn **credentials**: `openAiApi` (đã thêm API Key trước).
  - **Cấu hình Prompt** (nếu cần chỉnh sửa):
    ```json
    {
      "role": "user",
      "content": "Analyze the email with subject: {{$json.subject}}, sender: {{$json.from}}, and body: {{$json.body}}. Based on existing Gmail labels, suggest the best label to assign. If no suitable label exists, create a new label under 'AI' or an existing main label. Follow these rules:
      1. If email is spam/promotion, remove 'Inbox' label.
      2. If label exists (e.g., 'Project Alpha'), use it.
      3. If no label matches, create a new label under 'AI' (e.g., 'Vendor Inquiry').
      4. Always use consistent capitalization and delimiters (e.g., '[Project Alpha]').
      Return only the label name in JSON format: {'label': 'Project Alpha'}"
    }
    ```
  - **Lưu ý**: Nếu prompt không hiệu quả, các sếp có thể **test với dữ liệu mẫu** trước khi chạy live.

##### **C. Cấu hình Agent AI**
- **Node: `Gmail labelling agent`**
  - **Không cần chỉnh sửa** (n8n sẽ tự động kết nối với `OpenAI Chat Model1` và `Gmail Tool`).
  - **Lưu ý**: Nếu AI trả lời sai, các sếp có thể **cập nhật prompt** trong `OpenAI Chat Model1`.

- **Node: `Window Buffer Memory`**
  - **Không cần chỉnh sửa** (n8n sẽ lưu lịch sử phân loại để AI học tập).

- **Node: `Wait`**
  - **Không cần chỉnh sửa** (n8n sẽ tự động chờ AI xử lý).

---
#### **3. Kích hoạt ⚡️**
1. **Test Run** với **dữ liệu mẫu**:
   - Gửi một email mẫu (ví dụ: *"Project Alpha Update"*) và kiểm tra AI có phân loại đúng không.
   - Nếu AI sai, **cập nhật prompt** trong `OpenAI Chat Model1` và **test lại**.
2. **Bật Active workflow**:
   - Chuyển **switch Active** sang **ON** trong n8n Editor.

---
### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm **node `slack`** hoặc **`telegram`** để báo cáo khi AI tạo nhãn mới.
   - Ví dụ: *"AI đã tạo nhãn mới: [Vendor Inquiry] cho email từ [sender]."*

2. **Lưu log phân loại**:
   - Thêm **node `google sheets`** để ghi lại lịch sử phân loại (giúp theo dõi hiệu quả).

3. **Tự động xóa email không quan trọng**:
   - Sử dụng **node `gmailTool`** với **operation: `delete`** để xóa email spam sau khi gỡ nhãn "Inbox".

4. **Cập nhật nhãn theo mùa**:
   - Sử dụng **node `stickyNote`** để ghi chú các quy tắc mới (ví dụ: *"Tạo nhãn 'Holiday 2024' vào tháng 12"*).

---
### 📌 **Kết luận**
Với **workflow này**, các sếp sẽ **tự động hóa hoàn toàn quá trình phân loại email**, tiết kiệm **thời gian và giảm sai sót**. AI (OpenAI) sẽ **phân tích email, gợi ý nhãn phù hợp**, và **tự động tạo nhãn mới** nếu cần – **không cần code, không cần học AI**.

**Hành động ngay!**
1. **Import workflow** và cấu hình Gmail + OpenAI.
2. **Test với email mẫu** và điều chỉnh prompt nếu cần.
3. **Bật Active** và **nhận email được phân loại tự động**!

👉 **[Tải workflow ngay](https://n8n.io/workflows/2740)** và **cài đặt VPS n8n** để chạy 24/7! 🚀