---
title: "🤖 **Tự Động Hóa Phân Loại & Chuyển Động Lời Trả Lời Email Lạnh bằng Claude AI + Instantly.ai**"
description: "Giải pháp 100% tự động hóa phân loại và chuyển động lời trả lời email lạnh thông qua AI Claude, giúp các sếp tiết kiệm thời gian và tối ưu hóa quy trình bán hàng. Workflow này tự động nhận diện ý định của khách hàng (quan tâm, chưa sẵn sàng, hủy đăng ký, giới thiệu) và thực hiện hành động phù hợp: gửi thông báo Slack, email cá nhân hóa, hoặc loại bỏ khỏi danh sách theo dõi."
slug: "tieu-dong-hoa-phan-loai-email-lanh-claude-instantly"
tags: [n8n, automation, no-code, ai-chatbot, cold-email, instantly-ai, google-sheets, slack-integration]
keywords: [n8n workflow email lạnh, tự động hóa phân loại email, Claude AI n8n, Instantly.ai tự động hóa, quản lý leads AI, gửi email tự động]
---

# 🚀 **Tự Động Hóa Phân Loại & Chuyển Động Lời Trả Lời Email Lạnh bằng Claude AI + Instantly.ai**

## **💡 Giới Thiệu: Tiết Kiệm 10+ giờ/tuần cho bộ phận bán hàng**
Các sếp đã từng phải **quét hàng chục email lạnh hàng ngày**, phân loại từng lời trả lời, sau đó quyết định hành động tiếp theo? Đó là một công việc **mệt mỏi, dễ sai sót và tốn thời gian**—và nó **không hoạt động 24/7** như con người.

**Workflow này giải quyết tất cả:**
- **Tự động nhận và phân loại** mọi lời trả lời từ Instantly.ai.
- **Sử dụng AI Claude Haiku** để phân loại ý định khách hàng (quan tâm, chưa sẵn sàng, hủy đăng ký, giới thiệu) **với độ chính xác cao**.
- **Chuyển động tự động** dựa trên phân loại:
  - **Quan tâm?** → Gửi Slack alert + email link lịch hẹn.
  - **Chưa sẵn sàng?** → Đặt lại vào danh sách theo dõi sau 30 ngày.
  - **Hủy đăng ký?** → Loại bỏ khỏi tất cả chuỗi email.
  - **Giới thiệu?** → Gửi email yêu cầu giới thiệu.
- **Lưu tất cả dữ liệu** vào Google Sheets để theo dõi và phân tích.

**Kết quả?** Các sếp **tiết kiệm 10+ giờ/tuần**, **tăng cường phản hồi nhanh chóng** và **tối ưu hóa quy trình bán hàng** mà không cần viết một dòng code nào.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm thời gian:** Không phải thủ công phân loại email lạnh hàng ngày.
✅ **Chuyển động tự động:** AI phân loại và thực hiện hành động phù hợp **ngay lập tức**.
✅ **Tăng phản hồi nhanh:** Slack alert cho các lead hot giúp các sếp **đáp ứng kịp thời**.
✅ **Tối ưu hóa danh sách theo dõi:** Loại bỏ tự động khách hàng hủy đăng ký và tái kích hoạt sau 30 ngày.
✅ **Dữ liệu theo dõi toàn diện:** Tất cả lời trả lời được lưu vào Google Sheets với **thông tin chi tiết** (tên, email, công ty, nội dung, phân loại).
✅ **Cá nhân hóa email:** Gửi email link lịch hẹn hoặc yêu cầu giới thiệu **tự động** cho từng trường hợp.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Instantly.ai** (để nhận webhook và quản lý chuỗi email).
2. **API Key Claude AI** (trên [console.anthropic.com](https://console.anthropic.com/)).
3. **Tài khoản Google Sheets** (để lưu log tất cả lời trả lời).
4. **Tài khoản Gmail** (để gửi email link lịch hẹn và yêu cầu giới thiệu).
5. **Tài khoản Slack (tùy chọn)** (để nhận thông báo lead hot).
6. **API Key Instantly.ai** (để loại bỏ hoặc tái kích hoạt khách hàng).
7. **Link lịch hẹn (Calendly/Cal.com)** (để gửi cho lead quan tâm).
:::

---

## **🚀 Cách Import & Lưu ý khi "Lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow từ file JSON** hoặc **copy/paste JSON** vào n8n Editor:
- **Tải file JSON** từ [n8n.io/workflows/14622](https://n8n.io/workflows/14622).
- **Mở n8n Editor** → Nhấn **Import** → Chọn file JSON.
- **Hoặc copy toàn bộ JSON** vào **Import Workflow** trong n8n.

:::note[**LƯU Ý**]
- **Không kích hoạt workflow ngay lập tức**—cần cấu hình các node trước!
- **Kiểm tra lại URL webhook** của node *Receive Instantly Reply* sau khi import.
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Node 1: Receive Instantly Reply (Webhook)**
- **Cấu hình webhook** trong Instantly.ai:
  - Đi đến **Settings → Integrations → Webhooks**.
  - Thêm **một webhook mới** với:
    - **URL:** URL từ node *Receive Instantly Reply* (bắt đầu bằng `https://your-n8n-server/webhook/...`).
    - **Trigger:** Chọn *Reply Received*.
  - **Kích hoạt webhook** và lưu lại.

#### **🔹 Node 2: Claude Haiku (AI Phân Loại)**
- **Tạo credential Claude AI:**
  - Nhấn vào node *Claude Haiku* → Chọn **Add Credential**.
  - Điền **API Key** từ [console.anthropic.com](https://console.anthropic.com/).
  - **Model:** Đã mặc định là `claude-haiku-4-5-20251001` (không cần thay đổi).
- **Prompt mặc định:**
  ```plaintext
  You are a cold email reply classifier. Read the reply and return ONLY ONE WORD: INTERESTED, NOT_NOW, UNSUBSCRIBE, or REFERRAL.
  ```
  (Không cần chỉnh sửa, nhưng các sếp có thể tùy chỉnh nếu cần phân loại thêm).

#### **🔹 Node 3: Route by Intent (Switch Case)**
- Node này **chuyển động** dựa trên kết quả phân loại từ Claude.
- **Không cần cấu hình thêm**, chỉ cần đảm bảo **tất cả 4 branch** (Interested, Not Now, Unsubscribe, Referral) hoạt động.

#### **🔹 Node 4-7: Gửi Email & Slack (Gmail & Slack)**
- **Gmail:**
  - Nhấn vào node *Send Calendar Link* và *Send Referral Reply* → **Add Credential** → Đăng nhập tài khoản Gmail.
  - **Thay thế `YOUR_CALENDAR_LINK`** trong nội dung email bằng link thực tế (Calendly/Cal.com).
- **Slack (tùy chọn):**
  - Nhấn vào node *Notify Slack - Hot Lead* → **Add Credential** → Đăng nhập Slack.
  - Chọn **channel** (ví dụ: `#hot-leads`).
  - **Nếu không dùng Slack**, nhấn **Disable** node này.

#### **🔹 Node 8-11: Log to Google Sheets**
- **Tạo Google Sheet mới** với **cột đầu tiên** là:
  ```
  Timestamp | First Name | Last Name | Email | Company | Reply | Classification | Campaign
  ```
- **Cấu hình credential Google Sheets:**
  - Nhấn vào mỗi node *Log to Sheets* → **Add Credential** → Đăng nhập Google.
  - Chọn **Sheet** vừa tạo và **tab** tương ứng.
  - **Operation:** Đã mặc định là `append` (thêm mới).

#### **🔹 Node 12-13: Re-add/Remove from Instantly**
- **Tạo credential API Instantly:**
  - Nhấn vào node *Re-add to Instantly Sequence* và *Remove from Instantly Sequences* → **Add Credential**.
  - Điền **API Key** từ Instantly.ai.
- **Thay thế `YOUR_SEQUENCE_ID`** trong URL request bằng **ID chuỗi follow-up** (tìm trong URL chuỗi của bạn trên Instantly).

---

### **3. Kích hoạt ⚡️**
1. **Test run với dữ liệu mẫu:**
   - Gửi **một email mẫu** từ Instantly.ai (không phải thực tế).
   - Kiểm tra **tất cả branch** (Interested, Not Now, Unsubscribe, Referral) hoạt động như thế nào.
2. **Kích hoạt workflow:**
   - Nhấn **Active** trên canvas.
   - **Kiểm tra Google Sheets** và **Slack** (nếu dùng) để xác nhận dữ liệu được ghi và gửi đúng.

---

## **✍️ Mẹo & gợi ý nâng cao**

### **🔹 Tối ưu hóa AI phân loại**
- **Tùy chỉnh prompt** trong node *Claude Haiku* nếu muốn phân loại thêm trường hợp (ví dụ: `POTENTIAL_REFERRAL`).
- **Sử dụng temperature = 0** (đã mặc định) để đảm bảo **kết quả phân loại nhất quán**.

### **🔹 Kết hợp với Discord/Telegram**
- Thay thế node Slack bằng **Discord Webhook** hoặc **Telegram Bot** để nhận thông báo lead hot trên các nền tảng khác.

### **🔹 Tự động gửi báo cáo hàng tuần**
- **Thêm node Google Sheets** để **tính tổng số lead theo phân loại** và gửi báo cáo tự động qua email (sử dụng node **Gmail** hoặc **SendGrid**).

### **🔹 Lọc email spam**
- **Thêm node Filter** trước khi phân loại để loại bỏ email không liên quan (ví dụ: từ khóa "unsubscribe" hoặc "spam").

### **🔹 Tái kích hoạt sau thời gian khác**
- **Thay đổi thời gian chờ** trong node *Wait 30 Days* (ví dụ: 15 ngày hoặc 60 ngày) tùy vào chu kỳ bán hàng của doanh nghiệp.

---

## **📌 Kết luận: Tự động hóa bán hàng hiệu quả hơn 100%**

Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **quan trọng hơn**—giao tiếp với khách hàng và đóng giao dịch. **Không cần viết code, không cần chuyên gia IT**, chỉ cần **cấu hình theo hướng dẫn** và **bật workflow lên**.

**Bắt đầu ngay hôm nay!**
1. **Import workflow** từ [n8n.io/workflows/14622](https://n8n.io/workflows/14622).
2. **Cấu hình các node** theo hướng dẫn trên.
3. **Kích hoạt và test** với một email mẫu.
4. **Xem kết quả** trong Google Sheets và Slack!

**👉 [Đăng ký VPS TinoHost để self-host n8n 24/7](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N** - giảm tới 39%)**

---
**🚀 Hãy tự động hóa bán hàng của bạn ngay hôm nay!** 🚀