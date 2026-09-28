---
title: "📢 Tự Động Hóa Báo Cáo Tóm Tắt Tin Tức Hàng Ngày với Gemini AI + Gmail (Không Cần Code)"
description: "Workflow tự động hóa thu thập, tóm tắt và gửi báo cáo tin tức hàng ngày từ Google Alerts bằng trí tuệ nhân tạo Gemini, giúp các sếp tiết kiệm thời gian theo dõi thị trường, đối thủ cạnh tranh và xu hướng ngành mà không phải đọc từng bài báo. Kết quả: Một email duy nhất chứa tất cả thông tin quan trọng được tóm tắt ngắn gọn và sắp xếp logic."
slug: "tieu-dong-hoa-bao-cao-tom-tat-tin-tuc-hang-ngay-gemini-gmail"
tags: [n8n, automation, ai-summarization, google-alerts, gmail-automation, no-code]
keywords: [n8n workflow google alerts, tự động hóa báo cáo hàng ngày, gemini ai tóm tắt tin tức, tự động hóa theo dõi thị trường, không cần code]
---

# 🚀 **Tự Động Hóa Báo Cáo Tóm Tắt Tin Tức Hàng Ngày với Gemini AI + Gmail**

### **Dừng việc bị "chìm" trong hàng trăm email thông báo Google Alerts!**
Hàng ngày, các sếp phải mở hàng chục email từ **Google Alerts**, đọc từng bài báo dài dòng, và tóm tắt nội dung để báo cáo cho ban lãnh đạo. **Workflow này giải quyết vấn đề đó 100% tự động hóa** bằng trí tuệ nhân tạo **Gemini AI** của Google, giúp bạn:
✅ **Thu thập** tất cả tin tức liên quan từ Google Alerts.
✅ **Tóm tắt** nội dung bằng AI trong **2-4 câu** (không cần đọc bài báo).
✅ **Sắp xếp** theo chủ đề và gửi **một email duy nhất** chứa tất cả thông tin quan trọng.
✅ **Làm sạch inbox** bằng cách đánh dấu email cũ là đã đọc.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7**, các sếp nên tự cài đặt n8n trên **VPS riêng** (Self-hosted) thay vì dùng phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao, phù hợp với AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải đọc hàng trăm email mỗi ngày.
- **Tóm tắt chính xác**: Gemini AI hiểu nội dung và tóm tắt **không mất ý chính**.
- **Báo cáo chuyên nghiệp**: Email cuối cùng có **bảng tin tức sắp xếp logic**, dễ đọc và chia sẻ.
- **Hoạt động tự động**: Chỉ cần **bật định kỳ** (ví dụ: 7h sáng hàng ngày), workflow sẽ làm tất cả.
- **Inbox sạch**: Email cũ được **đánh dấu là đã đọc**, không bị lặp lại.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Gmail** (đã cấp quyền OAuth2 cho n8n):
   - Cần **đăng ký OAuth2** trong n8n để workflow có thể đọc email từ `googlealerts-noreply@google.com` và gửi email kết quả.
   - **Lưu ý**: Nếu sử dụng Gmail với 2FA, cần tạo **App Password** (nếu không, OAuth2 sẽ không hoạt động).

✔ **API Key Google Gemini**:
   - Đăng ký tại [Google AI Studio](https://aistudio.google.com/) và lấy **API Key** để kết nối với node `lmChatGoogleGemini`.
   - **Model khuyến nghị**: `gemini-2.5-pro` (mô hình mạnh mẽ, phù hợp với tóm tắt).

✔ **Thời gian xử lý**:
   - Workflow có thể mất **5-15 phút** tùy thuộc vào số lượng email và tốc độ internet.
   - **Không nên chạy quá 100 email cùng lúc** (tránh bị giới hạn API của Google).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
**Cách 1: Từ file JSON**
1. Tải file workflow từ [n8n.io/workflows/11452](https://n8n.io/workflows/11452) (chọn **Export as JSON**).
2. Trong n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

**Cách 2: Copy/Paste JSON**
1. Mở n8n Editor → Tạo workflow mới.
2. Nhấn **Import** → Chọn **Paste JSON** và dán nội dung từ file JSON.
3. Chọn **Create new workflow**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này có **15 node**, nhưng các bước sau đây là **quan trọng nhất** cần điều chỉnh:

##### **🔹 Node 1: Manual Trigger → Thay bằng Schedule Trigger (BẮT BUỘC)**
- **Tại sao?** Workflow hiện chỉ chạy khi nhấn **Execute**, nhưng các sếp muốn **tự động hóa hàng ngày**.
- **Cách thay đổi**:
  1. Xóa node **Manual Trigger** đầu tiên.
  2. Thêm node **Schedule Trigger** (tìm kiếm trong **Base Nodes**).
  3. Cấu hình:
     - **Cron Expression**: `0 7 * * *` (chạy lúc 7h sáng hàng ngày).
     - **Time Zone**: Chọn **Asia/Ho Chi Minh** (hoặc khu vực phù hợp).

##### **🔹 Node 2 & 15: Gmail OAuth2 (BẮT BUỘC)**
- **Tạo credentials Gmail**:
  1. Trong n8n, nhấn **Credentials** → **Add new credential** → Chọn **Gmail OAuth2**.
  2. Đăng nhập Gmail và cấp quyền cho n8n.
  3. **Lưu ý**:
     - Node **Get Google Alerts** phải **lọc email từ `googlealerts-noreply@google.com`**.
     - Node **Mark Alert as read** sẽ tự động đánh dấu email cũ là đã đọc.

##### **🔹 Node 3: Google Gemini Chat Model**
- **Thêm credentials Google Palm API**:
  1. Tạo **credentials mới** trong n8n → Chọn **Google Palm API**.
  2. Điền **API Key** từ Google AI Studio.
  3. **Cấu hình Prompt** (nếu cần thay đổi):
     - Mặc định, AI tóm tắt trong **2-4 câu**. Các sếp có thể chỉnh sửa ở node **Create Summary** (node **Agent**).

##### **🔹 Node 8: Structured Output Parser (BẮT BUỘC)**
- **Định dạng JSON đầu ra**:
  - Workflow phụ thuộc vào **cấu trúc JSON** từ AI. Nếu không đúng, email cuối cùng sẽ bị lỗi.
  - **Mẫu mặc định**:
    ```json
    {
      "summary": "string",
      "topic": "string",
      "link": "string"
    }
    ```
  - **Không chỉnh sửa** trừ khi biết rõ cấu trúc JSON.

##### **🔹 Node 12: Send Google Alert Summary**
- **Cấu hình email kết quả**:
  - **From**: Điền email của bạn (hoặc email khác nếu muốn).
  - **To**: Điền email nhận (có thể là email cá nhân hoặc nhóm).
  - **Subject**: Mặc định là **"Daily Google Alerts Digest"**. Các sếp có thể thay đổi.

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Execute** và kiểm tra từng node (đặc biệt là **Get Google Alerts** và **Google Gemini Chat Model**).
   - Nếu có lỗi, kiểm tra **credentials** và **API Key**.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động theo lịch.

---

### ✍️ **Mẹo & gợi ý nâng cao**
#### **🔹 Tùy chỉnh Prompt cho AI (Node Agent)**
- Mặc định, AI tóm tắt **không phân tích sâu**. Các sếp có thể chỉnh sửa **Prompt** ở node **Create Summary** để:
  - **Yêu cầu đánh giá**: Ví dụ: *"Nếu bài báo nói về đối thủ cạnh tranh, hãy đánh giá mức độ ảnh hưởng (cao/thấp)."*
  - **Chọn ngôn ngữ**: *"Tóm tắt bằng tiếng Việt và sử dụng từ ngữ chuyên nghiệp."*
  - **Thêm thông tin bổ sung**: *"Nếu bài báo liên quan đến giá cả, hãy trích dẫn số liệu chính xác."*

#### **🔹 Gửi báo cáo định kỳ qua Slack/Telegram**
- Thay vì email, các sếp có thể **gửi kết quả qua Slack/Telegram**:
  1. Thêm node **Slack Webhook** hoặc **Telegram Bot** sau node **Send Email**.
  2. Cấu hình **webhook URL** từ Slack/Telegram.
  3. **Lưu ý**: Slack/Telegram có giới hạn nội dung HTML, nên cần **chỉ gửi văn bản tóm tắt** (không phải bảng HTML).

#### **🔹 Lưu log vào Google Sheets**
- Để theo dõi lịch sử, các sếp có thể **lưu tất cả tin tức vào Google Sheets**:
  1. Thêm node **Google Sheets** (n8n-nodes-base.googleSheets).
  2. Cấu hình **Sheet Name** và **Range** (ví dụ: `Sheet1!A1`).
  3. **Lưu ý**: Cần tạo **credentials Google Sheets** trong n8n.

#### **🔹 Chỉ xử lý email mới nhất**
- Nếu có quá nhiều email cũ, workflow có thể **chỉ lấy email trong 7 ngày gần nhất**:
  1. Trong node **Get Google Alerts**, thêm điều kiện:
     ```json
     {
       "filter": "after:2024-01-01"
     }
     ```
  2. **Lưu ý**: Cần chỉnh ngày theo định dạng `YYYY-MM-DD`.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tiết kiệm thời gian** theo dõi thị trường.
✔ **Nhận báo cáo chuyên nghiệp** hàng ngày.
✔ **Không cần viết code** hay học AI.

**Bước đầu tiên**: Import workflow, cấu hình **Gmail OAuth2** và **Google Gemini API Key**, sau đó **bật Schedule Trigger** để nó chạy tự động mỗi sáng.
**Kết quả**: Một email duy nhất chứa **tất cả tin tức quan trọng** được tóm tắt ngắn gọn, sắp xếp logic, và **inbox của bạn sẽ sạch sẽ**.

🚀 **Hãy thử ngay và tự động hóa công việc của mình!**