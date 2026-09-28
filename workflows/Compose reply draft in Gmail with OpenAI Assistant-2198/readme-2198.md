---
title: "🤖 Tự Động Hóa Soạn Thảo Dự Thảo Trả Lời Email Bằng OpenAI Assistant (Gmail + AI)"
description: "Workflow tự động hóa hoàn toàn không cần code giúp các sếp tự động chuyển nội dung email có nhãn cụ thể sang OpenAI Assistant để tạo ra dự thảo trả lời thông minh, sau đó chèn vào Gmail và xóa nhãn kích hoạt. Tiết kiệm thời gian lên đến 80% cho công việc email hàng ngày."
slug: "tieu-dong-hoa-soan-thao-doi-thao-tra-loi-email-bang-openai-assistant"
tags: [n8n, automation, no-code, ai, gmail, openai, email-automation]
keywords: [n8n workflow gmail openai, tự động hóa email với ai, soạn thảo dự thảo trả lời email bằng chatgpt, tự động hóa công việc email, workflow ai cho doanh nghiệp]
---

# 🚀 **Tự Động Hóa Soạn Thảo Dự Thảo Trả Lời Email Bằng OpenAI Assistant**

## **Nỗi Đau Của Các Sếp Với Email Hàng Ngày**
Gửi và trả lời email là một phần không thể thiếu trong công việc hàng ngày của các sếp, nhưng việc soạn thảo từng câu trả lời một cách thủ công không chỉ tốn thời gian mà còn dễ gây mệt mỏi và thiếu nhất quán. Các sếp phải:
- **Lặp đi lặp lại** cùng một nội dung trả lời cho các câu hỏi tương tự.
- **Mất nhiều thời gian** để tìm kiếm thông tin liên quan trong email cũ.
- **Không đảm bảo tính chuyên nghiệp** khi trả lời nhanh chóng mà thiếu suy nghĩ.
- **Đối mặt với rủi ro** khi sai sót trong nội dung do mệt mỏi.

Workflow này **giải quyết tất cả những vấn đề trên** bằng cách tự động hóa toàn bộ quy trình từ nhận email đến tạo dự thảo trả lời thông minh bằng trí tuệ nhân tạo (AI), sau đó chèn vào Gmail và xóa nhãn kích hoạt.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted) để đảm bảo tính riêng tư và hiệu suất tối ưu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 80%** cho công việc trả lời email hàng ngày.
- **Trả lời email chuyên nghiệp và nhất quán** nhờ trí tuệ nhân tạo.
- **Tự động xóa nhãn kích hoạt** sau khi hoàn thành, tránh quên lãng.
- **Hoạt động liên tục 24/7** mà không cần can thiệp của con người.
- **Cá nhân hóa nội dung trả lời** dựa trên từng email cụ thể.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** và **API Key OAuth 2.0** để kết nối với Gmail API.
   - [Cài đặt OAuth 2.0 cho Gmail](https://developers.google.com/gmail/api/quickstart/python)
2. **Tài khoản OpenAI** và **API Key** để sử dụng OpenAI Assistant.
   - [Tạo API Key OpenAI](https://platform.openai.com/account/api-keys)
3. **OpenAI Assistant đã được cấu hình** trước khi chạy workflow.
   - Hướng dẫn tạo Assistant: [Tại đây](https://platform.openai.com/assistants)
4. **Nhãn kích hoạt (Trigger Label)** trong Gmail để workflow nhận diện email cần xử lý.
   - Ví dụ: `ai-reply` hoặc `auto-reply`.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập vào tài khoản.
2. Nhấn **Create Workflow** → **Import Workflow**.
3. Chọn file JSON hoặc dán JSON từ [đây](https://n8n.io/workflows/2198) (tải về trước).
4. Nhấn **Import** để workflow xuất hiện trên canvas.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **13 node** quan trọng, các sếp cần cấu hình kỹ lưỡng như sau:

##### **A. Cấu Hình Credentials**
- **Gmail OAuth 2.0**:
  - Đi đến **Credentials** → **Add New Credential** → Chọn **Gmail OAuth 2.0**.
  - Điền thông tin OAuth 2.0 đã tạo trước đó.
- **OpenAI API**:
  - Đi đến **Credentials** → **Add New Credential** → Chọn **OpenAI API**.
  - Điền **API Key** từ OpenAI và chọn **Assistant ID** (cần tạo trước).

##### **B. Cấu Hình Node Quan Trọng**
1. **`Get threads with specific labels` (gmail)**
   - **Credentials**: Chọn `gmailOAuth2`.
   - **Label**: Điền nhãn kích hoạt (ví dụ: `ai-reply`).
   - **Max Results**: Đặt số lượng email cần xử lý (ví dụ: `5`).

2. **`Ask OpenAI Assistant` (openAi)**
   - **Credentials**: Chọn `openAiApi`.
   - **Assistant ID**: Điền ID của OpenAI Assistant đã tạo.
   - **Prompt**: Sử dụng mặc định hoặc tùy chỉnh (ví dụ: `"Tóm tắt và trả lời email này một cách chuyên nghiệp"`).

3. **`Convert response to HTML` (markdown)**
   - Node này chuyển nội dung Markdown từ OpenAI thành HTML để Gmail hiển thị đúng định dạng.

4. **`Build email raw` (set) và `Convert raw to base64` (code)**
   - Các node này chuẩn bị dữ liệu để Gmail API nhận dạng và tạo draft.
   - **Lưu ý**: Node `code` cần sử dụng mã chuẩn RFC cho email (có trong tài liệu Gmail API).

5. **`Add email draft to thread` (httpRequest)**
   - Node này chèn dự thảo trả lời vào thread email.
   - **URL**: `https://gmail.googleapis.com/gmail/v1/users/me/drafts`.
   - **Headers**: Đảm bảo có `Authorization: Bearer {access_token}`.

6. **`Remove AI label from email` (gmail)**
   - Sau khi hoàn thành, node này xóa nhãn kích hoạt để workflow không xử lý lại.

##### **C. Kích Hoạt Workflow ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** và chọn một email có nhãn kích hoạt để kiểm tra.
   - Kiểm tra **Log** để đảm bảo không có lỗi.
2. **Bật Active**:
   - Sau khi test thành công, chuyển trạng thái workflow sang **Active**.
   - **Lưu ý**: Workflow sẽ chạy theo lịch trình **1 phút/lần** (do node `scheduleTrigger`).

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tùy Chỉnh Nhãn Kích Hoạt**:
   - Thay đổi nhãn trong node `Get threads with specific labels` để phù hợp với quy trình công việc của doanh nghiệp.

2. **Lưu Log Cho Theo Dõi**:
   - Sử dụng node **Sticky Note** hoặc **Google Sheets** để ghi lại lịch sử email đã xử lý và nội dung trả lời.

3. **Kết Hợp Với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** để thông báo khi workflow hoàn thành hoặc có lỗi.

4. **Tự Động Gửi Báo Cáo Hàng Tuần**:
   - Sử dụng node **Schedule Trigger** khác để gửi báo cáo tổng hợp về email đã tự động hóa.

5. **Cập Nhật OpenAI Assistant**:
   - Nếu cần thay đổi cách AI trả lời, chỉ cần cập nhật **Prompt** trong node `Ask OpenAI Assistant`.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa công việc email một cách thông minh và tiết kiệm thời gian. Bằng cách kết hợp **Gmail API** và **OpenAI Assistant**, các sếp không chỉ trả lời email nhanh hơn mà còn đảm bảo chất lượng cao nhất.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n trên VPS** để đảm bảo tính riêng tư và hiệu suất.
2. **Import workflow** và cấu hình credentials.
3. **Bật Active** và bắt đầu tự động hóa email của mình!

Nếu các sếp cần hỗ trợ thêm, hãy tham khảo [video hướng dẫn chi tiết](https://youtu.be/a8Dhj3Zh9vQ) từ tác giả Oskar. **Chúc các sếp thành công!** 🚀