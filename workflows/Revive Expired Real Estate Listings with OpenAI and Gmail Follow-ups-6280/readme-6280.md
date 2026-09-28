---
title: "🏡 **Tự Động Hồi Sinh Danh Sách Bất Động Sản Hết Hạn Với AI + Email Follow-up (N8N)**"
description: "Workflow tự động hóa phát hiện và hồi sinh danh sách bất động sản hết hạn (>30 ngày) bằng AI OpenAI, gửi email cá nhân hóa để relisting. Giúp các sếp bất động sản tiết kiệm thời gian, tăng cơ hội đóng gói giao dịch và tối ưu hóa danh sách hiện có."
slug: "tieu-dong-hoi-sinh-danh-sach-bat-dong-san-het-han"
tags: [n8n, automation, real-estate, ai-openai, gmail, google-sheets, lead-nurturing]
keywords: [tự động hóa bất động sản, hồi sinh danh sách hết hạn, AI OpenAI trong n8n, email follow-up bất động sản, n8n workflow real estate]
---

# 🚀 **Hồi Sinh Danh Sách Bất Động Sản Hết Hạn Với AI + Email Tự Động (N8N)**

### **Nỗi Đau Của Các Sếp Bất Động Sản**
Trong ngành bất động sản, danh sách bất động sản (listings) thường bị "quên lãng" sau **30 ngày không hoạt động**. Những danh sách này không chỉ bị bỏ qua mà còn **tốn chi phí quảng cáo, thời gian quản lý**, và **giảm cơ hội relisting** khi chủ sở hữu vẫn có nhu cầu bán/mua. Theo thống kê, **tỷ lệ relisting thành công sau 30 ngày chỉ còn ~15%** so với khi được theo dõi kịp thời.

**Workflow này giải quyết vấn đề bằng cách:**
✅ **Phát hiện tự động** danh sách hết hạn (>30 ngày) từ Google Sheets.
✅ **Sử dụng AI OpenAI** tạo email cá nhân hóa, mời chủ sở hữu relisting.
✅ **Gửi email tự động** qua Gmail, tăng cơ hội phản hồi và relisting.
✅ **Tối ưu hóa danh sách** bằng cách cập nhật trạng thái theo dõi.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7 không gián đoạn**, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi thủ công hàng trăm danh sách.
- **Tăng tỷ lệ relisting**: Email cá nhân hóa từ AI có **tỷ lệ mở email cao hơn 30%** so với email thông thường.
- **Tối ưu hóa danh sách**: Loại bỏ danh sách không hoạt động, tập trung vào những cơ hội thực sự.
- **Hoạt động liên tục**: Workflow chạy tự động hàng ngày, không phụ thuộc vào nhân viên.
- **Cải thiện CRM**: Cập nhật trạng thái danh sách, giúp quản lý dễ dàng hơn.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets**:
   - Một **Google Sheet** chứa danh sách bất động sản với các cột bắt buộc:
     - `title` (Tiêu đề danh sách)
     - `owner_name` (Tên chủ sở hữu)
     - `email` (Email liên lạc)
     - `property_type` (Loại bất động sản: Nhà riêng, căn hộ, đất...)
     - `location` (Địa chỉ)
     - `last_activity` (Ngày cuối cùng có hoạt động, định dạng: `YYYY-MM-DD`).
   - **Chia sẻ Sheet với n8n** bằng quyền **Đọc/Ghi**.

2. **Tài khoản Gmail**:
   - Một **tài khoản Gmail** để gửi email follow-up (không phải tài khoản chính của công ty).
   - **Bật OAuth 2.0** trong cài đặt Gmail (để n8n có quyền gửi email).

3. **API Key OpenAI**:
   - Đăng ký tài khoản [OpenAI](https://platform.openai.com/) và lấy **API Key**.
   - Chọn mô hình **GPT-4** (hoặc GPT-3.5) để đảm bảo chất lượng email.

4. **Credentials trong n8n**:
   - **Google Sheets OAuth 2.0**: Tạo trong **Credentials Manager** của n8n.
   - **Gmail OAuth 2.0**: Tạo tương tự.
   - **OpenAI API Key**: Thêm vào **Credentials Manager**.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/6280](https://n8n.io/workflows/6280).
- Trong **n8n Editor**, nhấp **Import** → Chọn file JSON vừa tải.
- **Hoặc** copy toàn bộ JSON từ file và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này gồm **5 node chính**, các sếp cần cấu hình kỹ lưỡng:

##### **🔹 Node 1: Schedule Trigger (Động cơ Khởi Động Lịch)**
- **Cấu hình**:
  - **Frequency**: Chọn **Daily** (hoặc tùy chỉnh theo nhu cầu).
  - **Time**: Đặt giờ chạy vào **sáng sớm** (ví dụ 7h sáng) để email được gửi trước giờ làm việc.
  - **Time Zone**: Chọn **UTC+7** (hoặc khu vực của bạn).

##### **🔹 Node 2: Google Sheets (Lấy Danh Sách)**
- **Credentials**: Chọn `googleSheetsOAuth2Api` (đã tạo trước).
- **Sheet Name**: Điền tên **Google Sheet** của bạn.
- **Range**: Điền `Sheet1!A:F` (hoặc tên sheet + phạm vi cột).
- **Test Run**: Nhấp **Test** để kiểm tra dữ liệu được lấy đúng.

##### **🔹 Node 3: If (Lọc Danh Sách Hết Hạn)**
- **Condition**:
  - Chọn `last_activity` (cột ngày cuối cùng hoạt động).
  - So sánh với `less than` và nhập `{{ $now.subtract(30, 'days').format('YYYY-MM-DD') }}` (để lọc danh sách >30 ngày).
  - **Lưu ý**: Nếu `last_activity` là ngày tháng Việt Nam (dd/mm/yyyy), cần chuyển sang định dạng `YYYY-MM-DD` trong Sheet.

##### **🔹 Node 4: OpenAI (Tạo Email Cá Nhân Hóa)**
- **Credentials**: Chọn `openAiApi`.
- **Model**: Chọn **GPT-4** (hoặc GPT-3.5).
- **Prompt Template**:
  ```plaintext
  Tôi là một đại lý bất động sản. Hãy viết một email cá nhân hóa để mời chủ sở hữu relisting cho danh sách {{ $json.title }} tại {{ $json.location }}.
  Email phải:
  1. Chào tên chủ sở hữu: "Chào {{ $json.owner_name }},"
  2. Nêu lý do relisting: "Chúng tôi nhận thấy danh sách của bạn đã hết hạn và muốn hỗ trợ relisting với điều kiện mới."
  3. Đính kèm thông tin cơ bản: "Danh sách: {{ $json.title }} | Loại: {{ $json.property_type }} | Giá: [Nếu có]."
  4. Kêu gọi hành động: "Hãy liên hệ với tôi qua email hoặc số điện thoại để relisting ngay!"
  5. Kết thúc bằng: "Trân trọng, [Tên bạn]."
  ```
- **Test Run**: Nhập một bản ghi mẫu vào **Google Sheets** và chạy **Test** để kiểm tra email được tạo ra có phù hợp không.

##### **🔹 Node 5: Gmail (Gửi Email)**
- **Credentials**: Chọn `gmailOAuth2`.
- **To**: Điền `{{ $json.email }}` (email chủ sở hữu).
- **Subject**: Điền `Relisting Opportunity: {{ $json.title }}`.
- **Body**: Chọn **HTML** và paste nội dung từ **OpenAI**.
- **Test Run**: Gửi email mẫu để kiểm tra có lỗi gì không.

---
#### **3. Kích Hoạt ⚡️**
- Sau khi cấu hình xong, nhấp **Active** để bật workflow.
- **Kiểm tra log**: Vào **Execution Logs** để theo dõi quá trình chạy.
- **Cập nhật Sheet**: Sau khi email được gửi, các sếp có thể thêm cột `follow_up_date` để ghi ngày gửi.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm **Slack Node** để thông báo khi email được gửi thành công.
   - **Prompt**: "Email đã được gửi cho {{ $json.owner_name }} về danh sách {{ $json.title }}."

2. **Lưu Log Tự Động**:
   - Thêm **Google Sheets Node** sau khi gửi email để ghi lại:
     - Ngày gửi.
     - Trạng thái (Gửi thành công/Thất bại).
     - Nội dung phản hồi (nếu có).

3. **Báo Cáo Định Kỳ**:
   - Sử dụng **Google Sheets Node** để tạo báo cáo hàng tuần:
     - Số lượng danh sách hết hạn.
     - Số lượng email đã gửi.
     - Tỷ lệ mở email (nếu tích hợp Google Analytics).

4. **Tối Ưu Prompt OpenAI**:
   - Nếu email không phù hợp, thử **Prompt mới**:
     ```plaintext
     Tôi là một chuyên gia marketing bất động sản. Viết email ngắn gọn (3-4 câu) để kích thích chủ sở hữu relisting, với:
     - Tôn trọng: "Chào {{ $json.owner_name }},"
     - Hấp dẫn: "Danh sách của bạn vẫn được lưu trữ và có thể relisting với điều kiện mới."
     - Hành động: "Hãy liên hệ với tôi qua số điện thoại [số của bạn] để thảo luận ngay!"
     ```

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp bất động sản, đồng thời **tăng cơ hội relisting** bằng cách tự động hóa quá trình theo dõi và gửi email cá nhân hóa. **Chỉ với 5 node đơn giản**, bạn đã có một **công cụ AI mạnh mẽ** để tối ưu hóa danh sách bất động sản.

**Hành động ngay**:
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với 1-2 danh sách mẫu** trước khi bật chạy toàn bộ.
3. **Theo dõi kết quả** và điều chỉnh prompt OpenAI nếu cần.

**🚀 Cùng tự động hóa ngay hôm nay!** Nếu có vấn đề, để lại comment bên dưới hoặc liên hệ với cộng đồng n8n tại [n8n.io/community](https://n8n.io/community).