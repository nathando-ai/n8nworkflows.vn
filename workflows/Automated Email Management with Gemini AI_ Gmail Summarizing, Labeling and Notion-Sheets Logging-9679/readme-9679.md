---
title: "🤖 Tự Động Hóa Quản Lý Email Gmail Với Gemini AI: Tóm Tắt, Nhãn & Ghi Chép Notion - Không Cần Code"
description: "Workflow tự động hóa quản lý email Gmail bằng AI Gemini: tóm tắt nội dung, gán nhãn tự động và ghi chép vào Notion/Google Sheets. Giúp các sếp tiết kiệm 8+ giờ/ngày và duy trì trật tự trong hộp thư."
slug: "tieu-dong-hoa-quan-ly-email-gmail-voi-gemini-ai"
tags: [n8n, automation, gmail, gemini-ai, notion, google-sheets, no-code]
keywords: [tự động hóa email gmail, gemini ai tóm tắt email, gmail tự động gán nhãn, lưu email vào notion, quản lý email không code]
---

# 🚀 **Tự Động Hóa Quản Lý Email Gmail Với Gemini AI: Tóm Tắt, Nhãn & Ghi Chép Notion**

### **Giải pháp cho các sếp bị "chìm" trong hàng trăm email hàng ngày**
Hàng ngày, các sếp phải mất **8+ giờ** để:
✅ **Lọc và đọc** hàng trăm email từ khách hàng, đồng nghiệp, và hệ thống.
✅ **Tóm tắt** nội dung dài dòng của email để nhớ lại sau này.
✅ **Gán nhãn** cho từng email để quản lý hiệu quả.
✅ **Ghi chép** thông tin quan trọng vào Notion/Google Sheets để theo dõi sau.

**Workflow này tự động hóa toàn bộ quy trình đó chỉ trong vài giây!** Bằng cách kết hợp **Gmail Trigger**, **Gemini AI** (Google’s LLM mạnh nhất hiện nay), và **Notion/Google Sheets**, các sếp sẽ:
✔ **Tiết kiệm 100% thời gian** đọc và phân loại email thủ công.
✔ **Nhận tóm tắt chính xác** của email bằng AI, không cần đọc lại.
✔ **Gán nhãn tự động** dựa trên nội dung email (ví dụ: "Khách hàng", "Hợp đồng", "Yêu cầu hỗ trợ").
✔ **Ghi chép tự động** vào Notion/Google Sheets để theo dõi lịch sử.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 8+ giờ/ngày** để làm việc có giá trị hơn.
- **Tóm tắt email chính xác** bằng Gemini AI, không bỏ sót chi tiết.
- **Gán nhãn tự động** dựa trên nội dung, giúp quản lý email hiệu quả.
- **Ghi chép tự động** vào Notion/Google Sheets, không cần nhớ thủ công.
- **Hoạt động liên tục** 24/7, không phụ thuộc vào thời gian làm việc của cá nhân.
- **Cá nhân hóa** theo nhu cầu: Thay đổi nhãn hoặc cách tóm tắt dễ dàng.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (đã cấp quyền OAuth2 cho n8n).
2. **API Key của Google Gemini** (để sử dụng AI tóm tắt và phân loại).
   - [Đăng ký API Key Google Gemini](https://makersuite.google.com/app/apikey) (nếu chưa có).
3. **Tài khoản Notion** (để ghi chép email vào database).
   - [Tạo API Key Notion](https://www.notion.so/my-integrations) (để n8n có quyền ghi dữ liệu).
4. **Tài khoản Google Sheets** (để lưu log email).
   - [Tạo file Google Sheets mới](https://sheets.google.com) và chia sẻ với n8n (quyền chỉnh sửa).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1: Import từ file JSON**
  1. Tải workflow từ [n8n.io/workflows/9679](https://n8n.io/workflows/9679) (chọn "Export").
  2. Trong n8n Editor, nhấn **"Import"** và chọn file JSON vừa tải.
  3. Chọn **"Create new workflow"** và nhấn **"Import"**.

- **Cách 2: Copy/Paste JSON**
  1. Mở n8n Editor và tạo workflow mới.
  2. Nhấn **"Import"** → **"Paste JSON"** và dán nội dung JSON từ workflow gốc.
  3. Chọn **"Create new workflow"**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **11 node** quan trọng, các sếp cần cấu hình kỹ lưỡng:

##### **A. Cấu hình Gmail Trigger (Node: "On new Email")**
- **Credentials**: Chọn `gmailOAuth2` (đã cấu hình trước khi import).
- **Lưu ý**:
  - Nếu muốn **không kích hoạt liên tục**, thay đổi **"Polling Interval"** từ `59 minutes` thành `60 minutes` (hoặc tắt hoàn toàn nếu dùng Webhook).
  - **Không cần thay đổi** nếu muốn workflow hoạt động tự động khi có email mới.

##### **B. Cấu hình Gemini AI (Node: "Google Gemini Chat Model")**
- **Credentials**: Chọn `googlePalmApi` (đã điền API Key từ Google).
- **Lưu ý**:
  - **Prompt mặc định** đã được tối ưu để tóm tắt và gán nhãn. **Không cần chỉnh** nếu muốn sử dụng mặc định.
  - Nếu muốn **cải thiện kết quả**, các sếp có thể chỉnh sửa prompt trong node **"AI Email Analyzer"** (node `agent`).

##### **C. Cấu hình Tạo & Gán Nhãn (Node: "Create Gmail Label" và "Add Label to Email")**
- **Credentials**: Chọn `gmailOAuth2`.
- **Lưu ý**:
  - **Node "Create Gmail Label"** sẽ tạo nhãn mới nếu không tồn tại.
  - **Node "Add Label to Email"** **BẮT BUỘC** phải điền **Label ID** (không phải tên nhãn). Các sếp cần:
    1. Mở Gmail → Nhấn `>` trên nhãn → Chọn **"Label settings"** → Sao chép **Label ID** (dòng cuối cùng).
    2. Trong node **"Add Label to Email"**, điền **Label ID** vào trường `"labelId"` (thay vì tên nhãn).

##### **D. Cấu hình Ghi Chép vào Notion/Google Sheets**
- **Notion (Node: "Logs in Notion")**:
  - **Credentials**: Chọn `notionApi`.
  - **Database Page**: Chọn **database Notion** đã tạo trước (ví dụ: "Email Logs").
  - **Lưu ý**: Các sếp cần **chia sẻ database với n8n** (quyền chỉnh sửa).

- **Google Sheets (Node: "Logs in Google Sheets")**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.
  - **Sheet Name**: Chọn **tên file Google Sheets** đã tạo (ví dụ: "Email Logs").
  - **Lưu ý**: File phải có **cột phù hợp** với dữ liệu từ email (tên, nội dung, nhãn, ngày gửi...).

##### **E. Cấu hình Agent (Node: "AI Email Analyzer" và "Label Agent")**
- **Lưu ý**:
  - **Node "AI Email Analyzer"** sẽ **tóm tắt email** và **gợi ý nhãn**.
  - **Node "Label Agent"** sẽ **lấy nhãn** từ AI và **gửi Label ID** cho node **"Add Label to Email"**.
  - **Không cần chỉnh** nếu muốn sử dụng logic mặc định.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với email mẫu:
   - Gửi email mẫu đến Gmail của mình.
   - Trong n8n Editor, nhấn **"Run Workflow"** và kiểm tra:
     - Email có được tóm tắt không?
     - Nhãn có được gán không?
     - Dữ liệu có ghi vào Notion/Google Sheets không?

2. **Bật Active**:
   - Sau khi test thành công, nhấn **"Active"** để workflow chạy tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Slack/Telegram Notifications**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo khi email mới được xử lý.
   - Ví dụ: `"Email mới được xử lý: [Tên] - Nhãn: [Label]"`.

2. **Lưu Log vào Database Dedicates**:
   - Thay vì ghi vào Notion/Google Sheets, các sếp có thể tạo **database riêng** trong n8n để lưu log dài hạn.

3. **Tự động Xóa Email Sau Xử Lý**:
   - Thêm node **Gmail** với operation `"delete"` để xóa email sau khi đã ghi chép.

4. **Cập Nhật Nhãn Theo Thời Gian**:
   - Sử dụng node **Date/Time** để gán nhãn như `"Urgent"` nếu email cũ hơn 24h.

5. **Tối ưu Prompt cho Gemini**:
   - Nếu muốn **tóm tắt chi tiết hơn**, chỉnh sửa prompt trong node **"AI Email Analyzer"**:
     ```json
     "prompt": "Tóm tắt email này trong 3 câu ngắn gọn, nhấn mạnh vào:
     - Yêu cầu cụ thể của người gửi.
     - Thời hạn hoàn thành (nếu có).
     - Điểm cần hành động (Action Items).
     Gợi ý 1-2 nhãn phù hợp cho email này (ví dụ: 'Hợp đồng', 'Yêu cầu hỗ trợ')."
     ```

---

### 📌 **Kết luận**
Workflow này **giải phóng các sếp khỏi công việc nhàn nhạt** đọc và phân loại email, thay vào đó **cho phép họ tập trung vào công việc có giá trị**. Với **Gemini AI**, các sếp sẽ **không bao giờ bỏ sót thông tin quan trọng** trong email, và với **Notion/Google Sheets**, mọi thông tin đều được **ghi chép tự động** để theo dõi sau này.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với email mẫu** để đảm bảo hoạt động.
3. **Bật Active** và **nghỉ ngơi** trong khi n8n làm việc cho bạn!

👉 **Bạn có câu hỏi?** Hãy để lại comment bên dưới hoặc chat với tôi trên [n8n Community](https://community.n8n.io/). Chúc các sếp thành công! 🚀