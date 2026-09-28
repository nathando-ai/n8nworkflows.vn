---
title: "🚀 Tự Động Hóa Briefing Sales AI Cho Cuộc Hẹn Calendly - Từ CRM Đến Slack & Email (N8N + OpenAI)"
description: "Workflow tự động hóa hoàn toàn không cần code giúp sales team nhận briefing chuẩn bị cuộc họp AI-personalized ngay khi khách hàng đặt lịch trên Calendly, tiết kiệm 8+ giờ/lần/người. Kết hợp HubSpot, Clearbit, OpenAI, Slack và Gmail để tạo ra những talking points độc quyền, tránh trùng lặp và tối ưu hóa quy trình bán hàng."
slug: "tieu-dong-hoa-briefing-sales-ai-calendly"
tags: [n8n, automation, sales, ai, hubspot, clearbit, openai, slack, gmail, no-code]
keywords: [tự động hóa briefing sales, n8n workflow calendly, ai tự động hóa sales, briefing cuộc họp tự động, tự động hóa hubspot, clearbit enrichment, openai talking points]
---

# 🚀 **Tự Động Hóa Briefing Sales AI: Từ Cuộc Hẹn Calendly Đến Briefing Chuyên Nghiệp Trên Slack & Email**

### **🔥 Nỗi Đau Của Sales Team**
Các sếp đã bao giờ phải:
- **Tìm kiếm thông tin khách hàng** trên HubSpot trong khi chờ họ đến cuộc họp?
- **Viết briefing từ đầu** mỗi lần khách hàng đặt lịch, mất 30-60 phút cho mỗi cuộc họp?
- **Đối mặt với khách hàng không chuẩn bị** vì thiếu thông tin chi tiết về công ty, lịch sử giao dịch?
- **Lặp lại công việc** vì không biết liệu briefing đã được gửi trước đó?

Workflow này **giải quyết tất cả** bằng cách tự động:
✅ **Lấy dữ liệu khách hàng** từ HubSpot và Clearbit trong giây lát.
✅ **Tạo talking points AI-personalized** cho mỗi cuộc họp.
✅ **Gửi briefing** đến sales rep qua Slack và email **ngay khi khách hàng đặt lịch**.
✅ **Tránh trùng lặp** bằng kiểm tra duplicate tự động.
✅ **Log tất cả hoạt động** lên Google Sheets để theo dõi.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. Với chi phí thấp nhưng hiệu suất cao:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 8+ giờ/lần/người**: Không phải tìm kiếm thông tin khách hàng hoặc viết briefing thủ công.
- **Cuộc họp chuyên nghiệp hơn**: Talking points AI-personalized giúp sales team **nắm bắt khách hàng nhanh chóng**.
- **Tránh trùng lặp**: Kiểm tra duplicate tự động **giảm thiểu công việc lặp lại**.
- **Hoạt động liên tục**: Workflow chạy **24/7** ngay cả khi team nghỉ ngơi.
- **Dữ liệu thống kê**: Log tất cả hoạt động lên Google Sheets để **theo dõi hiệu suất**.
- **Tối ưu hóa CRM**: Kết hợp HubSpot và Clearbit để **nâng cao chất lượng dữ liệu**.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Calendly** (để lấy webhook và signing secret).
✔ **API Key HubSpot** (để truy cập contact và deal).
✔ **API Key Clearbit** (để enrich company data).
✔ **API Key OpenAI** (để tạo talking points AI).
✔ **Credentials Slack** (để gửi thông báo).
✔ **Credentials Gmail** (để gửi email briefing).
✔ **Google Sheet** (để kiểm tra duplicate và log hoạt động).
✔ **Slack Channel ID** (để gửi briefing).

---
:::note[LƯU Ý]
- **Không cần code**: Workflow hoàn toàn **no-code**, chỉ cần cấu hình các node.
- **Tùy chỉnh dễ dàng**: Các sếp có thể **thay đổi prompt OpenAI** hoặc **cấu trúc email** theo nhu cầu.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào n8n Editor:
1. **Tải workflow** từ [n8n.io/workflows/16195](https://n8n.io/workflows/16195).
2. **Mở n8n Editor** và chọn **"Import"** → **"From JSON"**.
3. **Paste JSON** và nhấn **"Import"**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này có **16 node**, nhưng các node **quan trọng nhất** cần cấu hình kỹ lưỡng:

##### **🔹 Node 1: Calendly Webhook**
- **Cấu hình**:
  - **Path**: `calendly-meeting-booked`
  - **HTTP Method**: `POST`
  - **Signing Secret**: Điền **secret key** từ Calendly (tìm trong **Settings → Webhooks**).
  - **Test**: Gửi một cuộc họp mẫu từ Calendly để kiểm tra.

##### **🔹 Node 2: Validate Webhook Signature**
- **Mục đích**: Tránh **fake booking** hoặc lỗi security.
- **Lưu ý**:
  - **Không cần chỉnh sửa** nếu đã cấu hình Calendly đúng.

##### **🔹 Node 3: Check Duplicate in Sheet (Google Sheets)**
- **Cấu hình**:
  - **Sheet ID**: Điền **ID của Google Sheet** (tìm trong URL: `https://docs.google.com/spreadsheets/d/[ID]/edit`).
  - **Range**: `!A2:A` (giả sử cột A lưu ID cuộc họp).
  - **Test**: Nhập một ID mẫu để kiểm tra.

##### **🔹 Node 4: HubSpot - Get Contact & Get Open Deals**
- **Cấu hình**:
  - **API Token**: Điền **API Key HubSpot** (tìm trong **Settings → Integrations → API Keys**).
  - **Email Field**: Điền **cột email** trong HubSpot (thường là `email`).
  - **Test**: Nhập email mẫu để kiểm tra.

##### **🔹 Node 5: Clearbit - Enrich Company**
- **Cấu hình**:
  - **API Key**: Điền **API Key Clearbit** (tìm trong **Dashboard → API Keys**).
  - **URL**: `https://company.clearbit.com/v2/companies/enrich?domain={domain}`
  - **Test**: Nhập domain mẫu (ví dụ: `example.com`) để kiểm tra.

##### **🔹 Node 6: OpenAI - Generate Talking Points**
- **Cấu hình**:
  - **API Key**: Điền **API Key OpenAI**.
  - **Prompt**: Các sếp có thể **tùy chỉnh prompt** để phù hợp với phong cách sales:
    ```json
    "Tôi là một chuyên gia bán hàng. Viết 3 talking point cá nhân hóa cho cuộc họp với {prospect_name} từ {company_name}. Dữ liệu tham khảo:
    - Lịch sử giao dịch: {open_deals}
    - Thông tin công ty: {company_data}
    - Mục tiêu cuộc họp: {meeting_topic}
    Đảm bảo talking point ngắn gọn, chuyên nghiệp và có thể áp dụng ngay."
    ```
  - **Model**: Chọn `gpt-3.5-turbo` (mặc định).

##### **🔹 Node 7: Slack & Gmail - Send Prep Pack**
- **Cấu hình**:
  - **Slack**:
    - **Token**: Điền **Token Slack** (tìm trong **Settings → Apps → Your App → Basic Information → Signing Secret**).
    - **Channel ID**: Điền **ID của Slack Channel** (tìm trong URL: `https://slack.com/team/[ID]/channels/[CHANNEL_ID]`).
  - **Gmail**:
    - **Credentials**: Đăng nhập và **cho phép n8n truy cập Gmail**.
    - **Email Template**: Các sếp có thể **tùy chỉnh nội dung email** trong node **Code → Build Final Prep Pack**.

##### **🔹 Node 8: Log to Google Sheets**
- **Cấu hình**:
  - **Sheet ID**: Điền **ID của Google Sheet** (cùng với node **Check Duplicate**).
  - **Range**: `!B2:B` (giả sử cột B lưu log hoạt động).
  - **Test**: Nhập dữ liệu mẫu để kiểm tra.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn **node "Calendly Webhook"** và nhấn **"Run Workflow"**.
   - **Gửi một cuộc họp mẫu** từ Calendly để kiểm tra toàn bộ workflow.
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tùy Chỉnh Talking Points**:
   - Các sếp có thể **thêm/loại thông tin** trong prompt OpenAI để phù hợp với **phong cách sales** của team.
   - Ví dụ: Nếu team chuyên bán **SaaS**, có thể yêu cầu AI **nêu ra 3 lợi ích chính** của sản phẩm.

2. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **node `set`** để **lưu trữ dữ liệu** và sau đó **tạo báo cáo** bằng **Google Sheets** hoặc **PDF**.
   - Ví dụ: Tạo một **báo cáo tuần** về số lượng briefing được gửi và tỷ lệ thành công.

3. **Kết Nối Với CRM Khác**:
   - Nếu team sử dụng **Salesforce** hoặc **Pipedrive**, có thể **thay thế HubSpot** bằng các node tương ứng.

4. **Alert Lỗi Tự Động**:
   - Sử dụng **node `if`** để **kiểm tra lỗi** và gửi **thông báo Slack** khi workflow gặp vấn đề.

5. **Tích Hợp Với Zoom/Teams**:
   - Sau khi briefing được gửi, có thể **tự động tạo cuộc họp** trên Zoom/Teams bằng **node `httpRequest`**.

---

### 📌 **Kết Luận**
Workflow này **giải phóng sales team** khỏi công việc thủ công, giúp họ **nắm bắt khách hàng nhanh chóng** và **tăng tỷ lệ thành công** trong mỗi cuộc họp. Với **tự động hóa từ Calendly đến Slack & Email**, các sếp không chỉ **tiết kiệm thời gian** mà còn **nâng cao chất lượng briefing** bằng **AI-personalized talking points**.

**🚀 Hãy áp dụng ngay và xem sales team của bạn hoạt động như thế nào!**

---
:::tip[LƯU Ý CUỐI CUNG]
- **Backup workflow**: Trước khi bật **Active**, các sếp nên **backup JSON** để có thể **khôi phục** nếu cần.
- **Monitoring**: Sử dụng **n8n Dashboard** để theo dõi **status** của workflow.
- **Cập Nhật API Key**: Nếu **API Key** hết hạn, **cập nhật ngay** để workflow không bị ngắt.
:::

---
**💡 Cần hỗ trợ?** Liên hệ với **iTechNotion** (tác giả của workflow) qua [website](https://itechnotion.com) để **tùy chỉnh workflow** theo nhu cầu cụ thể!