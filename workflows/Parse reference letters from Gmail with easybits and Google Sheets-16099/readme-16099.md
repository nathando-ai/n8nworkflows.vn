---
title: "📩 Tự Động Hóa Xử Lý Thư Mừng Tốt Nghiệp Từ Gmail Sang Google Sheets Với AI (Không Cần Code)"
description: "Giải pháp tự động hóa 100% không code để tự động phân tích, trích xuất và xếp hạng các thư mừng tốt nghiệp từ Gmail, lưu vào Google Sheets với cảm xúc và điểm số tự động. Tiết kiệm 10+ giờ công mỗi tháng cho bộ phận HR."
slug: "tieu-dong-hoa-xu-ly-thu-mung-tot-nghiep-gmail-sang-google-sheets"
tags: [n8n, automation, hr, ai-summarization, google-sheets, gmail, easybits]
keywords: [tự động hóa thư mừng tốt nghiệp, phân tích thư mừng bằng AI, google sheets tự động hóa, n8n workflow hr, trích xuất dữ liệu từ email, sentiment analysis]
---

# 🚀 **Tự Động Hóa Xử Lý Thư Mừng Tốt Nghiệp Từ Gmail Sang Google Sheets Với AI**

### **Nỗi Đau Của Các Sếp HR**
Các sếp HR thường phải mất **giờ đồng hồ** để:
- **Tìm kiếm và tải xuống** hàng chục thư mừng tốt nghiệp từ Gmail.
- **Đọc từng thư** để trích xuất thông tin như tên người viết, mối quan hệ, đánh giá về ứng viên, và cảm xúc chung.
- **So sánh và xếp hạng** các thư để đưa ra quyết định tuyển dụng.
- **Lưu trữ và quản lý** dữ liệu một cách rắc rối trên Google Sheets.

**Kết quả?** Thời gian và năng suất bị "chôn vùi" trong công việc thủ công, trong khi các quyết định quan trọng lại phụ thuộc vào cảm nhận chủ quan của cá nhân.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 10+ giờ/tháng** – Thư mừng tự động được phân tích và lưu vào Google Sheets.
✅ **Dữ liệu chính xác và nhất quán** – AI trích xuất 10 trường thông tin chính xác từ từng thư, không bị lệ thuộc vào cảm nhận cá nhân.
✅ **Xếp hạng tự động** – Hệ thống tính điểm cảm xúc (0-100) và phân loại thành **cao/middling/thấp** để sếp dễ dàng so sánh.
✅ **Quản lý dễ dàng** – Email đã xử lý được **xóa nhãn "References"** và thêm nhãn **"Reference processed"** để tránh xử lý lại.
✅ **Dữ liệu sẵn sàng** – Tất cả thông tin được lưu vào Google Sheets với **cấu trúc nhất quán**, sẵn sàng cho báo cáo và phân tích.

---
### **🔧 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
📌 **Tài Khoản & API Keys:**
- **Gmail OAuth2** (để đọc email và quản lý nhãn).
- **Google Sheets OAuth2** (để ghi dữ liệu vào bảng tính).
- **EasyBits Extractor API** (để trích xuất dữ liệu từ các thư mừng).

📌 **Cấu Hình Trước Khi Bắt Đầu:**
- **Tạo nhãn Gmail:**
  - Nhãn **"References"** (để email mới vào đây sẽ được tự động xử lý).
  - Nhãn **"Reference processed"** (để đánh dấu email đã xử lý).
- **Tạo bộ lọc Gmail tự động:**
  - Khi email có nhãn **"References"**, hệ thống sẽ tự động xử lý.
- **Chuẩn bị Google Sheet:**
  - Tạo một **tab mới** tên **"References"** với các cột sau:
    - `candidate_name` (tên ứng viên)
    - `referee_name` (người viết thư)
    - `referee_title_company` (chức vụ và công ty của người viết)
    - `relationship_type` (mối quan hệ: quản lý, đồng nghiệp, học viên,...)
    - `duration_known` (thời gian biết nhau)
    - `tone` (tính chất: tích cực, trung lập, thận trọng)
    - `would_rehire` (có tái tuyển không: có/không/chưa rõ)
    - `sentiment_score` (điểm cảm xúc từ 0-100)
    - `sentiment_tier` (tầng cảm xúc: cao/middling/thấp)
    - `strengths_text` (điểm mạnh)
    - `weaknesses_text` (điểm yếu)
    - `notable_quote` (một câu trích dẫn nổi bật)
    - `received_at` (ngày nhận thư)

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào n8n Editor:
- **Tải file JSON** từ [n8n.io/workflows/16099](https://n8n.io/workflows/16099) (hoặc sử dụng link này để tải trực tiếp).
- **Mở n8n Editor** → Nhấn **"Import"** → Chọn file JSON hoặc dán JSON vào ô nhập liệu.

#### **2. Các Lưu Ý Bắt Buộc Phải Chỉnh 📌**
Sau khi import, các sếp cần **cấu hình kỹ lưỡng** các node quan trọng sau:

##### **📧 Gmail Trigger (Gmail Trigger)**
- **Chọn credentials:** `gmailOAuth2` (đã cấu hình trước khi import).
- **Cấu hình:**
  - **Label:** Chọn nhãn **"References"** (để email mới vào đây sẽ được xử lý).
  - **Download Attachments:** **Bật** (để tải xuống các tệp đính kèm).
  - **Simplify:** **Tắt** (để giữ nguyên cấu trúc email, bao gồm đính kèm).

##### **🔍 Split Out: Attachments (Code Node)**
- **Mục đích:** Chia email có nhiều tệp đính kèm thành các mục riêng lẻ (mỗi tệp là một mục).
- **Lưu ý:**
  - Node này **tự động rename** các tệp đính kèm thành `data` để Extractor dễ dàng đọc.
  - **Không cần chỉnh sửa** nếu đã import từ file JSON.

##### **🛡️ Filter: Real Documents (Filter Node)**
- **Mục đích:** Lọc bỏ các tệp không phải là **PDF hoặc scan đầy trang** (loại bỏ logo, chữ ký, footer).
- **Cấu hình:**
  - **Guard:** Chọn **File Type** = `application/pdf` và **Filename** chứa từ khóa như `letter`, `reference`, `scan`.
  - **Lưu ý:** Nếu có tệp không phải PDF, node này sẽ **bỏ qua** nó.

##### **🤖 Extract Reference: Letter (EasyBits Extractor)**
- **Mục đích:** Trích xuất **10 trường dữ liệu** từ thư mừng bằng AI.
- **Cấu hình:**
  - **Credentials:** Chọn `easybitsExtractorApi` (đã cấu hình trước).
  - **Extractor Fields:** Đảm bảo các trường sau đã được **cấu hình trong EasyBits**:
    - `referee_name` (tên người viết)
    - `referee_title_company` (chức vụ và công ty)
    - `candidate_name` (tên ứng viên)
    - `relationship_type` (mối quan hệ)
    - `duration_known` (thời gian biết nhau)
    - `claimed_strengths` (điểm mạnh, dưới dạng mảng)
    - `claimed_weaknesses` (điểm yếu, dưới dạng mảng)
    - `would_rehire` (có tái tuyển không)
    - `tone` (tính chất: tích cực/trung lập/thận trọng)
    - `notable_quote` (một câu trích dẫn nổi bật)
  - **Lưu ý:** Nếu trường nào không được trích xuất được, nó sẽ trả về `null`.

##### **🧹 Normalize Reference: Fields (Code Node)**
- **Mục đích:** **Định dạng lại** dữ liệu trích xuất để nhất quán.
- **Lưu ý:**
  - Node này **chuyển đổi mảng thành chuỗi** (nếu cần).
  - **Đảm bảo các giá trị enum** (`tone`, `would_rehire`) được định dạng đúng (ví dụ: `positive`, `neutral`, `hedged`).
  - **Không cần chỉnh sửa** nếu đã import từ file JSON.

##### **📊 Score Reference: Sentiment (Code Node)**
- **Mục đích:** **Tính điểm cảm xúc** (0-100) dựa trên:
  - `tone` (tính chất của thư).
  - `would_rehire` (có tái tuyển không).
  - `sentiment_tier` (cao/middling/thấp).
- **Lưu ý:**
  - Điểm cao hơn **50** được coi là **tích cực**.
  - Điểm thấp hơn **30** được coi là **xấu**.
  - **Không cần chỉnh sửa** nếu đã import từ file JSON.

##### **📗 Append Row: References (Google Sheets Node)**
- **Mục đích:** **Ghi dữ liệu vào Google Sheet**.
- **Cấu hình:**
  - **Credentials:** Chọn `googleSheetsOAuth2Api`.
  - **Operation:** `append` (thêm hàng mới).
  - **Sheet Name:** `References` (phải trùng với tên tab trong Google Sheet).
  - **Headers:** Đảm bảo trùng với các cột đã định nghĩa trước.
  - **Lưu ý:** Nếu Sheet chưa tồn tại, node này sẽ **tạo mới**.

##### **🏷️ Remove Label: References & Add Label: Processed (Gmail Node)**
- **Mục đích:**
  - **Xóa nhãn "References"** để email không bị xử lý lại.
  - **Thêm nhãn "Reference processed"** để theo dõi lịch sử.
- **Cấu hình:**
  - **Credentials:** `gmailOAuth2`.
  - **Message ID:** Sử dụng giá trị từ **Gmail Trigger** (đã tự động truyền).
  - **Lưu ý:** Đảm bảo nhãn **"Reference processed"** đã được tạo trước.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Với Slack/Telegram**
   - Thêm một **node Webhook** để gửi thông báo khi có thư mới được xử lý.
   - Ví dụ: `"Thư mừng của [candidate_name] đã được xử lý với điểm cảm xúc: [sentiment_score]"`.
   - **Cách làm:**
     - Tạo một **Webhook** trong Slack/Telegram.
     - Thêm node **Webhook** vào workflow, chọn **HTTP Request** và gắn vào **Append Row** node.

2. **Lưu Log Xử Lý**
   - Thêm một **node Google Sheets** khác để ghi **lịch sử xử lý** (ngày giờ, email ID, điểm số).
   - **Cách làm:**
     - Tạo một **tab mới** trong Google Sheet tên **"Log"**.
     - Thêm node **Google Sheets** sau **Append Row**, với cấu trúc:
       - `email_id`, `processed_at`, `sentiment_score`, `status`.

3. **Báo Cáo Định Kỳ**
   - Sử dụng **node Google Sheets** để **tính tổng điểm trung bình** cho từng ứng viên.
   - **Cách làm:**
     - Thêm một **node Code** sau **Append Row** để tính toán.
     - Sau đó, sử dụng **node Google Sheets** để **ghi báo cáo** vào một tab mới.

4. **Tối Ưu Hóa EasyBits Extractor**
   - Nếu muốn **trích xuất thêm trường dữ liệu**, các sếp có thể:
     - Mở **EasyBits Dashboard** → **Settings** → **Add New Fields**.
     - Thêm trường mới và **cập nhật trong workflow**.

---
### **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp HR khỏi công việc thủ công, **tăng cường tính chính xác** trong phân tích thư mừng, và **cung cấp dữ liệu sẵn sàng** để ra quyết định tuyển dụng nhanh chóng.

**Hành động ngay:**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **Import workflow** và **cấu hình các credentials**.
3. **Label một thư mừng** để **test** và xem kết quả!

**Kết quả?** Một **bảng dữ liệu sạch sẽ, tự động hóa hoàn toàn**, giúp các sếp **tuyển dụng thông minh hơn, nhanh hơn!**

---
:::tip[Lời Khuyên Cuối Cùng]
Nếu gặp khó khăn trong quá trình cấu hình, các sếp có thể:
- **Xem video hướng dẫn** của EasyBits: [easybits.tech](https://easybits.tech).
- **Hỏi hỗ trợ** trên [n8n Community](https://community.n8n.io/).
- **Liên hệ với Felix** (tác giả workflow) qua email hoặc GitHub.
:::

---
**Chúc các sếp thành công với tự động hóa HR!** 🚀