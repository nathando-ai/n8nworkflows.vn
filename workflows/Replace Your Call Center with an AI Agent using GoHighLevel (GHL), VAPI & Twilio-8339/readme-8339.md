---
title: "🤖 Thay Thế Trung Tâm Điện Thoại Bằng AI Agent Tự Động Hóa Với GoHighLevel, VAPI & Twilio (N8N)"
description: "Tự động hóa cuộc gọi bán hàng 24/7 bằng AI Agent thông minh, giảm 90% công việc thủ công cho call center. Giúp doanh nghiệp tiết kiệm thời gian, tăng tỷ lệ chuyển đổi và tối ưu chi phí."
slug: "thay-the-trung-tam-dien-thoai-bang-ai-agent-ghl-va-twilio"
tags: [n8n, automation, no-code, gohighlevel, twilio, ai-chatbot, lead-nurturing, call-center-automation]
keywords: [tự động hóa call center n8n, ai agent bán hàng, gohighlevel automation, twilio api tự động gọi điện, lead nurturing tự động, giảm chi phí call center]
---

# 🚀 **Thay Thế Trung Tâm Điện Thoại Bằng AI Agent Tự Động Hóa (GoHighLevel + Twilio + N8N)**

### **🔥 Nỗi Đau Của Các Sếp: Call Center Chậm, Tốn Kém, Và Không Hiệu Quả**
Hàng ngày, các sếp phải đối mặt với:
- **Chi phí cao** vì phải thuê nhân viên call center, trả lương, và quản lý thời gian làm việc.
- **Tỷ lệ chuyển đổi thấp** vì cuộc gọi tự động hoặc nhân viên không thể cá nhân hóa trải nghiệm khách hàng.
- **Khách hàng không đáp ứng** khi gọi vào giờ không phù hợp, dẫn đến mất cơ hội bán hàng.
- **Công việc thủ công** như theo dõi trạng thái cuộc gọi, cập nhật thông tin khách hàng, và phân loại leads – mất nhiều thời gian mà không mang lại giá trị cao.

**Giải pháp?** **AI Agent tự động hóa call center** với GoHighLevel (GHL), Twilio, và N8N – một hệ thống **24/7**, **tự động gọi điện**, **lắng nghe phản hồi**, và **cập nhật thông tin khách hàng** mà không cần nhân viên.

---

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
✅ **Tiết kiệm 90% chi phí call center** – Không cần thuê nhân viên, chỉ trả phí API và hosting N8N.
✅ **Tăng tỷ lệ chuyển đổi lên 3-5x** – AI Agent cá nhân hóa cuộc gọi, lắng nghe phản hồi, và chuyển tiếp cho nhân viên khi cần.
✅ **Hoạt động 24/7** – Khách hàng được gọi vào thời gian phù hợp (ví dụ: 9h sáng EST), tăng cơ hội đáp ứng.
✅ **Tự động cập nhật CRM** – Thông tin khách hàng (trạng thái cuộc gọi, phản hồi, lead score) được ghi lại tự động trên GoHighLevel.
✅ **Tối ưu thời gian** – Không cần theo dõi thủ công, hệ thống tự động retry cuộc gọi cho leads chưa đáp ứng.
:::

---

### **🔧 Yêu Cầu Cần Thiết**
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản GoHighLevel (GHL)** – Để quản lý leads và cập nhật thông tin khách hàng.
   - **API Key** của GHL (tìm trong **Settings > API Keys**).
   - **ID của Campaign** hoặc **Contact List** chứa leads.
   - **Credentials** để cập nhật tags và thông tin contact.

2. **Tài khoản Twilio** – Để thực hiện cuộc gọi và xử lý âm thanh.
   - **Account SID** và **Auth Token** (tìm trong **Twilio Console > Project > API Keys**).
   - **Twilio Phone Number** (số điện thoại được cấp bởi Twilio).

3. **Tài khoản VAPI (Voice API)** – Để phân tích âm thanh cuộc gọi (nếu muốn thêm tính năng OCR hoặc nhận dạng giọng nói).
   - **API Key** và **Secret Key** của VAPI.

4. **n8n Self-Hosted** – Để workflow chạy 24/7 ổn định.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

5. **Dữ liệu leads** – Danh sách khách hàng (số điện thoại, email, thông tin liên hệ) trong GoHighLevel.

---

### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/8339](https://n8n.io/workflows/8339) hoặc copy toàn bộ JSON từ link trên.
- Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON hoặc paste JSON vào ô **Import Workflow**.
- **Lưu workflow** với tên **"AI Agent Call Center"** (hoặc tên phù hợp).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **22 node**, chia thành **3 phần chính**:
- **Phần 1: Chuẩn bị và gọi điện** (Step 1-6).
- **Phần 2: Xử lý phản hồi và logic retry** (Step 7-14).
- **Phần 3: Cập nhật CRM và lịch trình** (Step 15-22).

##### **🔹 Cấu Hình Cần Thiết Cho Mỗi Node**
| **Node** | **Loại Node** | **Cần Chỉnh Gì?** | **Hướng Dẫn** |
|----------|--------------|------------------|---------------|
| **Step 1 - Create Customer** | `httpRequest` | **Headers** và **Body** | - **Method:** `POST` <br> - **URL:** `https://api.gohighlevel.com/v1/contacts` <br> - **Headers:** `Authorization: Bearer {GHL_API_KEY}` <br> - **Body (JSON):** `{ "first_name": "${{ $json["first_name"] }}", "last_name": "${{ $json["last_name"] }}", "phone": "${{ $json["phone"] }}", "email": "${{ $json["email"] }}", "campaign_id": "{CAMPAIGN_ID}" }` |
| **Step 2 - Initiate Call** | `httpRequest` | **Twilio API** | - **Method:** `POST` <br> - **URL:** `https://api.twilio.com/2010-04-01/Accounts/{TWILIO_ACCOUNT_SID}/Calls.json` <br> - **Headers:** `Authorization: Basic ${{ base64Encode(${"${TWILIO_ACCOUNT_SID}}:${TWILIO_AUTH_TOKEN}") }}` <br> - **Body (JSON):** `{ "To": "${{ $json["phone"] }}", "From": "{TWILIO_PHONE_NUMBER}", "Url": "https://your-vapi-endpoint.com/process-call" }` |
| **Step 3 - Get Call Data** | `httpRequest` | **Twilio Call Status** | - **Method:** `GET` <br> - **URL:** `https://api.twilio.com/2010-04-01/Accounts/{TWILIO_ACCOUNT_SID}/Calls/{CALL_SID}.json` <br> - **Headers:** `Authorization: Basic ${{ base64Encode(${"${TWILIO_ACCOUNT_SID}}:${TWILIO_AUTH_TOKEN}") }}` |
| **Step 4 - Set (Parse Call Result)** | `set` | **Trích xuất dữ liệu** | - **Expression:** `${{ $json }}` (để lưu trữ dữ liệu cuộc gọi). |
| **Step 5 - If (Call Answered?)** | `if` | **Điều kiện** | - **Condition:** `${{ $json.status === "completed" || $json.status === "answered" }}` |
| **Set Attempt Count + Init Status** | `code` | **Cập nhật biến** | - **JavaScript:** ```javascript { "json": { "attempt_count": ${{ $node["Set Attempt Count + Init Status"].json["attempt_count"] || 0 }} + 1, "status": "pending", "last_attempt": ${{ new Date().toISOString() }} } } ``` |
| **GHL Paginated Request** | `httpRequest` | **Lấy leads từ GHL** | - **Method:** `GET` <br> - **URL:** `https://api.gohighlevel.com/v1/contacts?campaign_id={CAMPAIGN_ID}&limit=100` <br> - **Headers:** `Authorization: Bearer {GHL_API_KEY}` |
| **Start Calls - 9AM EST** | `scheduleTrigger` | **Thời gian chạy** | - **Cron Expression:** `0 9 * * ?` (chạy hàng ngày lúc 9h EST). |

##### **🔹 Node Quan Trọng Khác**
- **Add Call Status Tag** (`highLevel`): Cập nhật tags cho contact trong GHL.
  - **Headers:** `Authorization: Bearer {GHL_API_KEY}`.
  - **Body:** `{ "contact_id": "${{ $json.id }}", "tags": ["called", "status_${{ $json.status }}"] }`.
- **Update Contact - Call Summary** (`highLevel`): Ghi lại tổng kết cuộc gọi.
  - **Body:** `{ "contact_id": "${{ $json.id }}", "custom_fields": { "call_summary": "${{ $json.summary }}", "last_call_date": "${{ new Date().toISOString() }}", "lead_score": ${{ $json.lead_score || 0 }} } }`.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với 1-2 leads mẫu:
   - Chạy workflow với **manual trigger** (nút **Run Workflow**).
   - Kiểm tra:
     - Cuộc gọi có được khởi động không?
     - Trạng thái cuộc gọi được cập nhật trên GHL không?
     - Logic retry hoạt động không?
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Status** từ **Inactive** sang **Active**.
   - Đảm bảo **scheduleTrigger** (`Start Calls - 9AM EST`) được kích hoạt.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để báo cáo kết quả cuộc gọi (ví dụ: "Lead ABC đã đáp ứng, lead score: 90").
   - **Node cần thêm**: `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram`.

2. **Lưu Log Cuộc Gọi**:
   - Sử dụng node **Google Sheets** hoặc **Airtable** để lưu trữ lịch sử cuộc gọi chi tiết.
   - **Node cần thêm**: `n8n-nodes-base.googleSheets`.

3. **Gửi Báo Cáo Định Kỳ**:
   - Tạo một workflow riêng để tổng hợp dữ liệu cuộc gọi hàng tháng và gửi báo cáo qua email.
   - **Node cần thêm**: `n8n-nodes-base.email` + `n8n-nodes-base.set` (tính toán thống kê).

4. **Cá Nhân Hóa Giọng Nói**:
   - Nếu sử dụng **VAPI**, có thể thêm tính năng **giọng nói tự động** (ví dụ: "Xin chào, tôi là AI Agent của [Tên Công Ty], có thể giúp gì cho bạn?").
   - **Node cần thêm**: `n8n-nodes-base.httpRequest` (gọi API VAPI để phát âm thanh).

5. **Optimize Logic Retry**:
   - Thay đổi thời gian chờ (`Wait Before Retry`) từ 1 giờ sang 24 giờ cho leads có lead score thấp.
   - **Node cần chỉnh**: `n8n-nodes-base.wait` → Thay đổi `duration` trong **Options**.

---

### **📌 Kết Luận**
Workflow này **thay thế hoàn toàn call center truyền thống** bằng một **AI Agent tự động hóa**, tiết kiệm chi phí, tăng hiệu quả, và hoạt động 24/7. **Không cần code**, chỉ cần cấu hình n8n và kết nối với GoHighLevel, Twilio, và VAPI.

**🚀 Hành động ngay:**
1. **Đăng ký VPS** để self-host n8n (để workflow chạy 24/7).
2. **Import workflow** và cấu hình các API key.
3. **Test với 1-2 leads** trước khi bật chế độ tự động.
4. **Mở rộng** bằng cách kết nối Slack, Google Sheets, hoặc email báo cáo.

**💡 Nếu cần hỗ trợ:**
- **Tác giả workflow**: [Dragos Țugui](https://n8n.io/workflows/8339) (có thể liên hệ qua LinkedIn hoặc email trong profile).
- **Cộng đồng n8n Việt Nam**: [Facebook Group](https://www.facebook.com/groups/n8nvietnam/) hoặc [Discord](https://discord.gg/n8n).

**🎯 Kết quả cuối cùng?** **Một call center tự động hóa, hiệu quả gấp 10 lần, chi phí thấp hơn 90%.** Hãy thử ngay! 🚀