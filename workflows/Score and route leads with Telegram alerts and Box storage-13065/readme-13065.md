---
title: "🚀 Tự Động Hóa & Đánh Giá Lead Tự Động: Nhận Lead Tốt Nhất, Lưu Trữ Box & Thông Báo Telegram (0 Code)"
description: "Workflow tự động nhận lead từ form, đánh giá điểm số, phân loại lead chất lượng cao cho Sales và lead cần nurture cho Marketing, đồng thời lưu trữ trên Box và thông báo tức thời qua Telegram. Giúp các sếp tiết kiệm 80% thời gian xử lý lead thủ công."
slug: "tieu-dong-hoa-danh-gia-lead-telegram-box"
tags: [n8n, automation, lead-generation, ai-summarization, box-storage, telegram-alerts, no-code]
keywords: [n8n workflow lead, tự động hóa nhận lead, đánh giá lead score, lưu lead trên Box, thông báo Telegram, tự động hóa marketing]
---

# 🚀 **Tự Động Hóa Nhận, Đánh Giá & Phân Loại Lead: Từ Form → Box → Telegram (Không Cần Code)**

## **🔥 Nỗi Đau Của Các Sếp Hiện Nay**
Hàng ngày, các sếp phải:
- **Làm thủ công** nhận lead từ form, check email, gọi điện để xác minh thông tin.
- **Phân loại lead** dựa vào kinh nghiệm cá nhân → dẫn đến **sai sót, mất lead chất lượng** hoặc **tốn thời gian quá nhiều**.
- **Lưu trữ lead** rối loạn trên nhiều nơi (Excel, CRM, email) → khó theo dõi và chia sẻ.
- **Thông báo chậm** khi có lead mới → Sales hoặc Marketing phải **quên hoặc bỏ lỡ** cơ hội.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Nhận lead** từ form (Webhook).
✅ **Đánh giá điểm số lead** (Lead Scoring) dựa trên dữ liệu Clearbit.
✅ **Phân loại lead** thành **chất lượng cao (Sales)** và **cần nurture (Marketing)**.
✅ **Lưu lead** vào **Box Storage** theo folder riêng (Qualified/Unqualified).
✅ **Thông báo tức thời** qua **Telegram** cho Sales hoặc Marketing.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** xử lý lead thủ công.
- **Chính xác 100%** trong phân loại lead (không phụ thuộc vào con người).
- **Lưu trữ an toàn** trên Box với **folder riêng biệt** cho Sales & Marketing.
- **Thông báo tức thời** qua Telegram → **không bỏ lỡ lead nào**.
- **Cải thiện chuyển đổi** do lead được phân loại chính xác và được xử lý kịp thời.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Clearbit API** (để enrich lead với dữ liệu công ty, email, mạng xã hội).
   - Đăng ký tại: [https://clearbit.com/](https://clearbit.com/)
   - Thêm **Credentials** trong n8n: `Credentials → Clearbit API` (điền API Key).

2. **Tài khoản Box** (để lưu lead theo folder Qualified/Unqualified).
   - Tạo **2 folder riêng biệt**:
     - `Qualified Leads` (dành cho Sales).
     - `Unqualified Leads` (dành cho Marketing).
   - Thêm **Box OAuth2 Credential** trong n8n.
   - **Cài đặt biến môi trường** (Environment Variables):
     - `BOX_QUALIFIED_FOLDER_ID` (ID folder Qualified).
     - `BOX_UNQUALIFIED_FOLDER_ID` (ID folder Unqualified).

3. **Bot Telegram** (để thông báo lead mới).
   - Tạo bot tại [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Thêm **Telegram Bot API Credential** trong n8n.
   - **Cài đặt biến môi trường**:
     - `TELEGRAM_SALES_CHAT_ID` (ID chat Sales).
     - `TELEGRAM_MARKETING_CHAT_ID` (ID chat Marketing).
     - `TELEGRAM_OPS_CHAT_ID` (ID chat Ops, dùng để báo lỗi).

4. **URL Webhook** (để form gửi lead).
   - Sau khi deploy workflow, **copy URL Webhook** từ node `Lead Form Webhook` và **cài đặt trong form** (Formspree, Typeform, Webflow, etc.).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13065](https://n8n.io/workflows/13065).
- **Mở n8n Editor** → Nhấn `Import` → Chọn file JSON → Nhấn `Import`.
- **Hoặc copy/paste JSON** từ file vào `Import Workflow` trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **16 node**, nhưng **các node quan trọng nhất** cần cấu hình kỹ:

##### **🔹 Node `Lead Form Webhook` (n8n-nodes-base.webhook)**
- **Path**: Đã mặc định là `lead-intake` (không cần thay đổi).
- **HTTP Method**: `POST` (để form gửi dữ liệu).
- **Lưu ý**:
  - Sau khi deploy, **copy URL Webhook** và **cài đặt trong form** (ví dụ: Formspree, Typeform).
  - Nếu form ở **Webflow**, sử dụng **Webflow Form Integration** để gửi dữ liệu đến Webhook này.

##### **🔹 Node `Validate Required Fields` (n8n-nodes-base.code)**
- **Mục đích**: Kiểm tra **email** và **tên công ty** có tồn tại không.
- **Lưu ý**:
  - Nếu thiếu trường này, lead sẽ bị **từ chối** và gửi thông báo lỗi đến **Telegram Ops**.
  - **Mã JavaScript** đã sẵn sàng, không cần chỉnh sửa (nếu form gửi đủ dữ liệu).

##### **🔹 Node `Calculate Lead Score` (n8n-nodes-base.code)**
- **Mục đích**: Đánh giá điểm số lead dựa trên:
  - **Kích thước công ty** (Clearbit).
  - **Địa chỉ email** (định dạng, miền).
  - **Tài khoản mạng xã hội** (LinkedIn, Twitter).
- **Lưu ý**:
  - **Cân nhắc điểm số** trong mã JavaScript (nếu muốn thay đổi tiêu chí).
  - **Ngưỡng phân loại** (Qualified/Unqualified) được điều chỉnh ở node `Qualified Lead?` (IF node).

##### **🔹 Node `Qualified Lead?` (n8n-nodes-base.if)**
- **Mục đích**: Phân loại lead dựa trên **điểm số**.
- **Lưu ý**:
  - **Điều chỉnh ngưỡng** (ví dụ: `score >= 70` → Qualified).
  - Nếu muốn **cân nhắc thêm tiêu chí**, chỉnh sửa mã trong node `Calculate Lead Score`.

##### **🔹 Node `Upload to Box` (n8n-nodes-base.box)**
- **Mục đích**: Lưu lead vào **Box Storage** theo folder.
- **Lưu ý**:
  - **Chọn credential** là `Box OAuth2` (đã thêm trước đó).
  - **Folder ID** tự động lấy từ biến môi trường (`BOX_QUALIFIED_FOLDER_ID`, `BOX_UNQUALIFIED_FOLDER_ID`).
  - **Tên file**: Tự động tạo từ `email + timestamp` (ví dụ: `john.doe@company.com_20240520.json`).

##### **🔹 Node `Notify Sales/Marketing` (n8n-nodes-base.telegram)**
- **Mục đích**: Gửi thông báo lead mới qua Telegram.
- **Lưu ý**:
  - **Chọn credential** là `Telegram Bot API`.
  - **Chat ID** tự động lấy từ biến môi trường (`TELEGRAM_SALES_CHAT_ID`, `TELEGRAM_MARKETING_CHAT_ID`).
  - **Nội dung thông báo** có thể chỉnh sửa trong **Message Template** (ví dụ: thêm logo, link CRM).

##### **🔹 Node `Workflow Error Trigger` (n8n-nodes-base.stickyNote)**
- **Mục đích**: Báo lỗi nếu workflow bị crash.
- **Lưu ý**:
  - **Thông báo lỗi** sẽ gửi đến `TELEGRAM_OPS_CHAT_ID`.
  - **Không cần chỉnh sửa**, nhưng có thể **thêm log** vào Box nếu muốn.

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run** với **dữ liệu mẫu**:
   - Gửi một lead test từ form → Kiểm tra:
     - Lead có được **enrich** (Clearbit) không?
     - Điểm số có hợp lý không?
     - Lead được **lưu vào Box** folder đúng không?
     - **Telegram** có nhận được thông báo không?
2. **Bật Active workflow** khi test thành công.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH LÀM NGOÀI]
1. **Kết hợp với CRM (HubSpot, Salesforce)**
   - Thay thế node `Upload to Box` bằng **HubSpot API** hoặc **Salesforce API** để tự động thêm lead vào CRM.
   - **Cách làm**:
     - Thêm node `n8n-nodes-base.httpRequest` để gọi API CRM.
     - Sử dụng **credentials** của CRM trong n8n.

2. **Thêm Log & Audit Trail**
   - Thêm node **Google Sheets** hoặc **Notion API** để lưu **lịch sử lead**.
   - **Cách làm**:
     - Thêm node `n8n-nodes-base.googleSheets` sau `Upload to Box`.
     - Lưu **tên lead, điểm số, thời gian, trạng thái**.

3. **Tự động Gửi Email Follow-up**
   - Sử dụng **SendGrid** hoặc **Mailgun** để gửi email tự động cho lead mới.
   - **Cách làm**:
     - Thêm node `n8n-nodes-base.httpRequest` (SendGrid API).
     - Chỉnh **template email** trong node `Set` trước khi gửi.

4. **Cập Nhật Điểm Số Định Kỳ**
   - Nếu lead không chuyển đổi, **giảm điểm số** sau 7 ngày.
   - **Cách làm**:
     - Sử dụng **n8n Scheduler** để chạy workflow định kỳ.
     - Thêm node `n8n-nodes-base.code` để cập nhật điểm số.

5. **Thêm AI Chatbot (Copilot)**
   - Sử dụng **n8n-nodes-base.llm** (OpenAI, Mistral) để **tóm tắt lead** hoặc **gợi ý hành động**.
   - **Cách làm**:
     - Thêm node `n8n-nodes-base.llm` sau `Merge Enriched Data`.
     - Gửi **prompt** như:
       ```json
       "Analyze this lead: {lead_data}. Suggest next steps for Sales/Marketing."
       ```
---
### 📌 **Kết Luận**
Workflow này **giải phóng các sếp khỏi công việc thủ công, rườm rà** trong quản lý lead. Với **tự động hóa 100%**, các sếp sẽ:
✔ **Nhận lead chất lượng cao** được phân loại chính xác.
✔ **Tiết kiệm thời gian** để tập trung vào **bán hàng & chiến lược**.
✔ **Lưu trữ an toàn** trên Box với **folder riêng biệt**.
✔ **Thông báo tức thời** qua Telegram → **không bỏ lỡ lead nào**.

**🚀 Hành động ngay!**
1. **Import workflow** và **cài đặt credentials**.
2. **Test với lead mẫu** và **bật Active**.
3. **Tích hợp với form** và **bắt đầu tự động hóa!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Bạn có thắc mắc gì?** Hãy để lại comment dưới đây, các sếp sẽ hỗ trợ miễn phí! 🚀