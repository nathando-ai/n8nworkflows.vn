---
title: "🤖 Tự Động Hóa Gmail: Phân Loại Email Với GPT-4o Mini + Gửi Thông Báo Telegram (Tiết Kiệm 20 Phút/Ngày)"
description: "Workflow tự động phân loại email Gmail bằng AI (GPT-4o Mini) và gửi thông báo Telegram ngay khi nhận được tin nhắn quan trọng. Giúp các sếp loại bỏ công việc thủ công, giảm stress và tập trung vào những nhiệm vụ chiến lược."
slug: "tieu-dong-hoa-gmail-phan-loai-voi-gpt-4o-mini-va-telegram"
tags: [n8n, automation, ai-summarization, gmail, telegram, no-code, openai]
keywords: [tự động hóa gmail, phân loại email bằng ai, gpt-4o mini n8n, gửi thông báo telegram tự động, tiết kiệm thời gian email]
---

# 🚀 **Tự Động Hóa Phân Loại Email Gmail Với AI + Telegram: Giúp Các Sếp Loại Bỏ 20 Phút Công Việc Thủ Công Hàng Ngày**

### **Nỗi Đau Của Các Sếp Với Email**
Hàng ngày, các sếp phải mất **20 phút** để:
- **Lọc email** giữa tin nhắn quan trọng (đơn hàng, hợp đồng, yêu cầu khẩn cấp) và spam/quảng cáo.
- **Phân loại thủ công** email vào các folder/nhãn (Work Related, High Priority, Promotions...).
- **Quên kiểm tra** một số email quan trọng trong hộp thư nháp hoặc nhãn chưa được theo dõi.

**Workflow này giải quyết tất cả!** Sử dụng **GPT-4o Mini** (mô hình AI hiệu quả của OpenAI) để tự động phân loại email và **Telegram** để gửi thông báo ngay khi có tin nhắn quan trọng. **Không cần code, chỉ cần copy/paste!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 20 phút/ngày** (tương đương **100 giờ/năm**) bằng cách loại bỏ công việc thủ công.
✅ **Phân loại email chính xác** với AI (GPT-4o Mini) thay vì phải đọc từng email.
✅ **Nhận thông báo Telegram ngay lập tức** khi có email quan trọng (High Priority, Work Related).
✅ **Hộp thư Gmail luôn được sắp xếp** theo nhãn tự động (không cần nhấp chuột).
✅ **Hoạt động liên tục 24/7** (không phụ thuộc vào thời gian làm việc của bạn).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (đã kích hoạt OAuth 2.0 cho n8n).
2. **API Key OpenAI** (để sử dụng GPT-4o Mini).
   - Mua tại: [OpenAI API](https://platform.openai.com/account/api-keys)
   - **Mô hình được sử dụng**: `gpt-4o-mini` (rẻ và hiệu quả).
3. **Bot Telegram** (để gửi thông báo).
   - Tạo bot tại: [@BotFather](https://t.me/BotFather) (gửi lệnh `/newbot`).
   - Lấy **Chat ID** của mình:
     - Gửi tin nhắn cho bot: `/start`
     - Trả lời bot bằng tin nhắn: `https://api.telegram.org/bot<TOKEN>/getUpdates` (thay `<TOKEN>` bằng token bot).
     - Copy `chat.id` từ kết quả JSON.
4. **Nhãn Gmail đã tồn tại** (ví dụ: `High Priority`, `Work Related`, `Promotions`).
   - Nếu chưa có, tạo tại: **Gmail → Nhãn → Tạo nhãn mới**.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
**Cách 1: Từ file JSON**
- Tải workflow từ [đây](https://n8n.io/workflows/7553) (nút "Download").
- Trên n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.

**Cách 2: Copy/Paste JSON**
- Trên n8n Editor, nhấn **Import** → Chọn **Paste JSON**.
- Dán toàn bộ mã JSON từ [đây](https://n8n.io/workflows/7553) (nút "Raw").

---

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow có **9 node** chính. Các sếp cần cấu hình **cẩn thận** các node sau:

##### **A. Gmail Trigger (GmailTrigger)**
- **Credentials**: Chọn `gmailOAuth2` (đã cấu hình trước khi import).
- **Polling Interval**: Để mặc định (**1 phút**) hoặc thay đổi thành **30 giây** nếu muốn phản ứng nhanh hơn.

##### **B. AI Classification (TextClassifier)**
- **Prompt Customization**:
  - Node này sử dụng **AI Agent** để phân loại email. Các sếp có thể **tùy chỉnh danh sách nhãn** trong **AI Agent1** (node `agent`).
  - **Ví dụ prompt mặc định**:
    ```
    Phân loại email này vào một trong các nhãn sau:
    - High Priority: Email liên quan đến hợp đồng, đơn hàng, yêu cầu khẩn cấp.
    - Work Related: Email công việc (meeting, báo cáo, yêu cầu nội bộ).
    - Promotions: Email quảng cáo, newsletter, ưu đãi.
    Trả về kết quả dưới dạng JSON: {"label": "High Priority", "reason": "..."}
    ```
  - **Lưu ý**: Nếu muốn thay đổi danh sách nhãn, chỉnh sửa **AI Agent1** (node `agent`) hoặc **Classification Agent** (node `textClassifier`).

##### **C. Gmail Label (Gmail - Add Labels)**
Workflow có **3 node** để thêm nhãn:
1. **High Priority** (nhãn `High Priority`).
2. **Work Related** (nhãn `Work Related`).
3. **Promotions** (nhãn `Promotions`).
- **Kiểm tra lại tên nhãn**:
  - Nếu nhãn không tồn tại, **node này sẽ thất bại**.
  - **Giải pháp**: Tạo nhãn trước trên Gmail (như hướng dẫn ở phần **Yêu cầu cần thiết**).

##### **D. Telegram Notification (Telegram)**
- **Credentials**: Chọn `telegramApi` (đã cấu hình token bot).
- **Chat ID**: Điền **Chat ID** của mình (lấy từ bước 3 trong **Yêu cầu cần thiết**).
- **Message Template**:
  - Thay đổi nội dung thông báo nếu muốn (ví dụ: thêm link email hoặc tóm tắt ngắn).
  - **Ví dụ**:
    ```
    🚨 Email mới được phân loại: {json["label"]}
    Tiêu đề: {json["subject"]}
    Link: {json["link"]}
    ```

##### **E. AI Agent (Agent & LMChatOpenAI)**
- **Node `4o-mini` (lmChatOpenAi)**:
  - **Model**: Đã cấu hình mặc định là `gpt-4o-mini`.
  - **API Key**: Đã liên kết với `openAiApi` (cần điền trước khi import).
- **Node `AI Agent1` (agent)**:
  - **Prompt**: Sử dụng prompt mặc định để phân loại email.
  - **Lưu ý**: Nếu muốn cải thiện độ chính xác, **tùy chỉnh prompt** theo nhu cầu cụ thể của công ty.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** và gửi một email mẫu đến Gmail của mình.
   - Kiểm tra:
     - Email có được phân loại vào nhãn đúng không?
     - Thông báo Telegram có được gửi không?
2. **Active Workflow**:
   - Sau khi kiểm tra thành công, chuyển **Active** sang **ON**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tùy Chỉnh Danh Sách Nhãn**:
   - Thêm/loại nhãn trong **AI Agent1** để phù hợp với công việc của công ty.
   - **Ví dụ**: Thêm nhãn `Customer Support` cho email liên quan đến khách hàng.

2. **Gửi Thông Báo Slack Thay Vì Telegram**:
   - Thay thế node `telegram` bằng node `slack` (n8n-nodes-base.slack).
   - Cấu hình credentials `slackApi` và chat channel.

3. **Lưu Log Email Vào Google Sheets**:
   - Thêm node `googleSheets` sau node `GmailTrigger` để ghi lại lịch sử email.
   - **Cách làm**:
     - Tạo một sheet mới trên Google Sheets.
     - Thêm node `googleSheets` → Chọn sheet và cấu hình headers (`subject`, `from`, `label`, `timestamp`).

4. **Tự Động Xóa Email Sau Phân Loại**:
   - Thêm node `gmail` với `operation: delete` sau khi email đã được phân loại.
   - **Lưu ý**: Chỉ áp dụng cho email không quan trọng (ví dụ: spam).

5. **Cập Nhật Thường Xuyên AI**:
   - Nếu muốn cải thiện độ chính xác của AI, **cập nhật prompt** trong node `AI Agent1` hoặc sử dụng mô hình mới hơn (ví dụ: `gpt-4o`).

---

### 📌 **Kết Luận: Bắt Đầu Tự Động Hóa Ngay Hôm Nay!**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào những nhiệm vụ chiến lược thay vì mất thời gian lọc email. Với **GPT-4o Mini** và **Telegram**, các sếp sẽ:
✔ **Không bao giờ bỏ lỡ email quan trọng** nữa.
✔ **Hộp thư Gmail luôn được sắp xếp** một cách tự động.
✔ **Tiết kiệm 20 phút mỗi ngày** (tương đương **100 giờ/năm**).

**Hành động ngay!**
1. **Import workflow** theo hướng dẫn trên.
2. **Cấu hình credentials** (Gmail, OpenAI, Telegram).
3. **Test và active** workflow.
4. **Tùy chỉnh** để phù hợp với công việc của công ty.

**🚀 Các sếp đã sẵn sàng tự động hóa email chưa?** Nếu có thắc mắc, để lại comment bên dưới! 👇