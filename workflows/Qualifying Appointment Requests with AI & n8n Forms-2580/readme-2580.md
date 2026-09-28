---
title: "🤖 **Tự Động Hóa Xác Minh & Lên Lịch Hẹn AI với n8n Forms (Không Cần Code!)**"
description: "Workflow này tự động phân loại và xác minh yêu cầu lịch hẹn thông qua AI, giảm thiểu công việc thủ công cho bộ phận Sales/Marketing. Kết quả: Tiết kiệm 80% thời gian xử lý, giảm sai sót, và cải thiện trải nghiệm khách hàng với các form phân chia logic."
slug: "tieu-dong-hoa-xac-minh-lich-hen-ai-n8n-forms"
tags: [n8n, automation, no-code, ai-powered, sales, google-calendar, gmail, text-classifier]
keywords: [n8n workflow tự động hóa, AI phân loại yêu cầu lịch hẹn, n8n forms phân trang, tự động hóa Sales, xác minh AI, Google Calendar tự động, Gmail wait for approval]
---

# 🚀 **Tự Động Hóa Xác Minh & Lên Lịch Hẹn AI với n8n Forms (Không Cần Code!)**

### **Giải pháp cho bộ phận Sales/Marketing:**
Hàng ngày, các sếp phải xử lý **đống yêu cầu lịch hẹn** từ khách hàng, trong đó có rất nhiều yêu cầu không phù hợp hoặc không cần thiết. Điều này gây ra:
- **Tốn thời gian** để phân loại và xác minh từng yêu cầu thủ công.
- **Sai sót cao** do con người mệt mỏi hoặc thiếu tập trung.
- **Trải nghiệm khách hàng kém** khi phải chờ đợi lâu hoặc nhận phản hồi không chính xác.
- **Không tối ưu hóa lịch** của bộ phận vì không biết được yêu cầu nào thực sự cần thiết.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **AI tự động phân loại** yêu cầu lịch hẹn (thông qua **OpenAI Text Classifier**) để loại bỏ những yêu cầu không phù hợp.
✅ **Form phân trang** (multi-form) để tạo trải nghiệm người dùng **mượt mà và thân thiện**.
✅ **Xác minh tự động + thủ công** (Gmail "Wait for Approval") để đảm bảo chỉ những yêu cầu hợp lệ mới được lên lịch.
✅ **Tự động tạo sự kiện Google Calendar** khi được phê duyệt, tiết kiệm thời gian lên lịch thủ công.
✅ **Gửi thông báo tự động** cho khách hàng và quản lý, giảm thiểu việc nhắc nhở thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. Điều này đảm bảo:
- **Tốc độ cao** (không phụ thuộc vào n8n.io).
- **An toàn dữ liệu** (không chia sẻ API key với bên thứ ba).
- **Tích hợp hoàn toàn** với hệ thống nội bộ (Google Calendar, Gmail, API nội bộ...).

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo ổn định cho workflow AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** xử lý yêu cầu lịch hẹn (không cần phân loại thủ công).
- **Chỉ duyệt những yêu cầu thực sự cần thiết** (AI loại bỏ yêu cầu không phù hợp).
- **Trải nghiệm khách hàng chuyên nghiệp** (form phân trang + thông báo tự động).
- **Lịch được quản lý tự động** (Google Calendar cập nhật ngay khi được phê duyệt).
- **Giảm sai sót** (không phụ thuộc vào con người để xác minh).
- **Hoạt động liên tục** (không cần can thiệp thủ công).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản và API Key:**
   - **OpenAI API Key** (để sử dụng **Text Classifier** và **ChatGPT**).
   - **Gmail OAuth2** (để gửi email xác nhận, yêu cầu phê duyệt và thông báo kết quả).
   - **Google Calendar OAuth2 API** (để tạo sự kiện khi được phê duyệt).

2. **Dịch vụ cần tích hợp:**
   - **Google Calendar** (để tự động tạo sự kiện).
   - **Gmail** (để gửi email tự động và yêu cầu phê duyệt).
   - **n8n Forms** (để tạo form phân trang).

3. **Tài nguyên thêm (khuyến nghị):**
   - **Subworkflow** (để quản lý quá trình phê duyệt độc lập).
   - **Sticky Notes** (để ghi chú nội bộ trong workflow).

---
:::note[LƯU Ý QUAN TRỌNG]
- **Không cần kiến thức code** để sử dụng workflow này.
- **Workflow hoạt động trên n8n Community Edition** (miễn phí) hoặc **n8n Enterprise** (nếu cần tính năng nâng cao).
- **Không cần cài đặt thêm plugin** nào ngoài những node đã liệt kê.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:

**Cách 1: Import từ file JSON**
1. Tải file JSON từ [n8n.io/workflows/2580](https://n8n.io/workflows/2580).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

**Cách 2: Copy/Paste JSON**
1. Trên trang [n8n.io/workflows/2580](https://n8n.io/workflows/2580), nhấn **Export** → Chọn **JSON**.
2. Copy toàn bộ mã JSON.
3. Trên **n8n Editor**, nhấn **Import** → Chọn **Paste JSON** và dán mã vào.
4. Nhấn **Import**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **19 node** và **4 phần chính** cần cấu hình kỹ lưỡng:

##### **🔹 Phần 1: Cấu hình AI (Text Classifier & ChatGPT)**
- **Node "Enquiry Classifier" (Text Classifier):**
  - **Mô tả:** AI phân loại yêu cầu lịch hẹn để xác định xem yêu cầu đó **cần thiết** hay **không cần thiết**.
  - **Cấu hình:**
    - Chọn **OpenAI API Key** trong **Credentials**.
    - Điền **Prompt** để AI hiểu rõ yêu cầu (ví dụ: *"Nếu yêu cầu này không liên quan đến sản phẩm/dịch vụ của chúng tôi, hãy trả về 'Không phù hợp'. Ngược lại, trả về 'Phù hợp'."*).
    - **Model:** Chọn **gpt-3.5-turbo** (mặc định).

- **Node "Summarise Enquiry" (ChainLlm):**
  - **Mô tả:** AI tóm tắt yêu cầu của khách hàng để quản lý dễ dàng hơn.
  - **Cấu hình:**
    - Chọn **OpenAI API Key** trong **Credentials**.
    - Điền **Prompt** để AI tóm tắt ngắn gọn (ví dụ: *"Tóm tắt yêu cầu này trong 3 câu, bao gồm mục đích, thời gian mong muốn và thông tin liên hệ."*).

##### **🔹 Phần 2: Cấu hình Form (Multi-Form)**
Workflow sử dụng **3 form** để tạo trải nghiệm người dùng tốt:
1. **"n8n Form Trigger" (schedule_appointment):**
   - **Mô tả:** Form đầu tiên để khách hàng nhập **mục đích lịch hẹn**.
   - **Cấu hình:**
     - Thêm **1 trường text** với tiêu đề *"Mục đích của cuộc họp này là gì?"*.
     - Thêm **1 trường checkbox** với tiêu đề *"Tôi đồng ý với điều khoản và điều kiện"* (để xác minh người dùng đã đọc và chấp nhận).

2. **"Terms & Conditions" (Form):**
   - **Mô tả:** Hiển thị **điều khoản và điều kiện** trước khi người dùng tiếp tục.
   - **Cấu hình:**
     - Thêm **1 trường text** với nội dung điều khoản (có thể copy từ trang web của công ty).
     - Thêm **1 trường checkbox** yêu cầu người dùng **chấp nhận** trước khi tiếp tục.

3. **"Enter Date & Time" (Form):**
   - **Mô tả:** Form để khách hàng chọn **ngày giờ** thích hợp.
   - **Cấu hình:**
     - Thêm **1 trường date picker** với tiêu đề *"Chọn ngày"*.
     - Thêm **1 trường time picker** với tiêu đề *"Chọn giờ"*.
     - Thêm **1 trường text** với tiêu đề *"Thời gian ước tính cho cuộc họp (phút)"*.

##### **🔹 Phần 3: Cấu hình Email & Phê Duyệt (Gmail)**
- **Node "Send Receipt" (Gmail):**
  - **Mô tả:** Gửi **email xác nhận** cho khách hàng khi họ hoàn thành form.
  - **Cấu hình:**
    - Chọn **gmailOAuth2** trong **Credentials**.
    - **Subject:** *"Xác nhận yêu cầu lịch hẹn của bạn"*.
    - **Body:** Thêm nội dung email (có thể sử dụng **template** như sau):
      ```
      Xin chào [Tên khách hàng],

      Cảm ơn bạn đã gửi yêu cầu lịch hẹn! Chúng tôi đã nhận được thông tin và sẽ xử lý trong vòng 24 giờ.

      Nếu yêu cầu của bạn phù hợp, chúng tôi sẽ liên hệ để lên lịch. Nếu không, chúng tôi sẽ liên hệ để giải thích lý do.

      Trân trọng,
      Đội ngũ [Tên công ty]
      ```

- **Node "Wait for Approval" (Gmail):**
  - **Mô tả:** Gửi **email yêu cầu phê duyệt** cho quản lý, với **2 nút "Phê duyệt" và "Từ chối"**.
  - **Cấu hình:**
    - Chọn **gmailOAuth2** trong **Credentials**.
    - **Subject:** *"Yêu cầu phê duyệt lịch hẹn: [Tên khách hàng]"*.
    - **Body:** Thêm nội dung email (có thể sử dụng **template** như sau):
      ```
      Xin chào [Tên quản lý],

      Có một yêu cầu lịch hẹn mới từ [Tên khách hàng]. Dưới đây là thông tin chi tiết:

      - **Mục đích:** [Mô tả từ form]
      - **Ngày giờ:** [Ngày giờ từ form]
      - **Tóm tắt:** [Tóm tắt từ AI]

      Vui lòng **phê duyệt** hoặc **từ chối** yêu cầu này bằng cách nhấn nút tương ứng dưới đây.

      Trân trọng,
      Hệ thống tự động
      ```
    - **Thêm 2 nút:**
      - **Nút 1:** *"Phê duyệt"* → Liên kết đến **Node "Create Appointment"** (tạo sự kiện Google Calendar).
      - **Nút 2:** *"Từ chối"* → Liên kết đến **Node "Send Rejection"** (gửi email từ chối).

- **Node "Send Rejection" (Gmail):**
  - **Mô tả:** Gửi **email từ chối** cho khách hàng nếu yêu cầu không được phê duyệt.
  - **Cấu hình:**
    - Chọn **gmailOAuth2** trong **Credentials**.
    - **Subject:** *"Yêu cầu lịch hẹn của bạn đã bị từ chối"*.
    - **Body:** Thêm nội dung email (có thể sử dụng **template** như sau):
      ```
      Xin chào [Tên khách hàng],

      Sau khi xem xét yêu cầu lịch hẹn của bạn, chúng tôi xin thông báo rằng yêu cầu này đã bị từ chối với lý do: [Lý do từ AI/quản lý].

      Nếu bạn có bất kỳ câu hỏi nào, vui lòng liên hệ với chúng tôi.

      Trân trọng,
      Đội ngũ [Tên công ty]
      ```

##### **🔹 Phần 4: Cấu hình Google Calendar**
- **Node "Create Appointment" (Google Calendar):**
  - **Mô tả:** Tạo **sự kiện Google Calendar** khi yêu cầu được phê duyệt.
  - **Cấu hình:**
    - Chọn **googleCalendarOAuth2Api** trong **Credentials**.
    - **Title:** *"Lịch hẹn với [Tên khách hàng]"*.
    - **Description:** *"Lịch hẹn đã được phê duyệt. Thời gian: [Ngày giờ từ form]."*.
    - **Start Time:** *[Ngày giờ từ form]*.
    - **End Time:** *[Ngày giờ + thời gian ước tính từ form]*.
    - **Location:** *"Online"* (hoặc địa điểm cụ thể nếu cần).

##### **🔹 Phần 5: Cấu hình Subworkflow (Trigger Approval Process)**
- **Node "Trigger Approval Process" (ExecuteWorkflow):**
  - **Mô tả:** Gọi **subworkflow** để quản lý quá trình phê duyệt.
  - **Cấu hình:**
    - Chọn **subworkflow** đã tạo (nếu chưa có, tạo mới với tên *"Approval Process"*).
    - **Input:** Điền các dữ liệu cần truyền (ví dụ: `{{ $json["email"] }}`, `{{ $json["name"] }}`, `{{ $json["purpose"] }}`).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run (Đi thử):**
   - Nhấn **Run Workflow** và nhập **dữ liệu mẫu** vào form để kiểm tra:
     - AI có phân loại đúng không?
     - Email xác nhận có được gửi không?
     - Quá trình phê duyệt có hoạt động không?
     - Sự kiện Google Calendar có được tạo không?

2. **Bật Active:**
   - Sau khi kiểm tra thành công, nhấn **Active** để workflow **chạy tự động** khi có yêu cầu mới.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH TIẾP CẬN THÊM]
1. **Kết hợp với Slack/Telegram:**
   - Thêm **node Slack** hoặc **Telegram** để gửi thông báo khi có yêu cầu mới hoặc khi được phê duyệt/từ chối.
   - **Cách làm:**
     - Thêm **node Slack** sau **Node "Send Receipt"** và **Node "Send Rejection"**.
     - Cấu hình **webhook Slack** trong **Credentials**.

2