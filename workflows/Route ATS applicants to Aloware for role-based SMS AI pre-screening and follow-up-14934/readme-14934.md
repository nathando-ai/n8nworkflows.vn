---
title: "🤖 Tự Động Hóa Xử Lý Ứng Viên (ATS) Với SMS AI Pre-Screening & Follow-up Cho Nhóm Nhiệm Vụ - Giảm 80% Công Việc Lặp Lại HR"
description: "Workflow này tự động nhận ứng viên từ hệ thống ATS, phân loại theo nhóm (Sales, Kỹ Thuật, Tổng Quát), gửi SMS AI pre-screening và theo dõi phản hồi tự động. Giúp HR tiết kiệm 80% thời gian xử lý ứng viên và cải thiện tỷ lệ phản hồi từ ứng viên."
slug: "tu-dong-hoa-ats-applicant-routing-ai-sms"
tags: [n8n, automation, hr, ai-chatbot, aloware, slack, no-code]
keywords: [n8n workflow ats, tự động hóa tuyển dụng, sms ai pre-screening, aloware n8n, giảm công việc hr, routing ứng viên theo nhóm]
---

# 🚀 **Tự Động Hóa Xử Lý Ứng Viên ATS Với SMS AI Pre-Screening & Follow-up Cho Nhóm Nhiệm Vụ**

### **Giải Pháp Cho Nỗi Đau Của Các Sếp HR**
Hàng ngày, các sếp HR phải mất **giờ đồng hồ** để:
- **Lọc và phân loại** ứng viên từ hệ thống ATS (Greenhouse, Lever, BambooHR...).
- **Gửi SMS/Email** giới thiệu công ty và yêu cầu phản hồi.
- **Theo dõi phản hồi** và chuyển tiếp ứng viên phù hợp cho bộ phận phù hợp.
- **Nhắc nhở lại** ứng viên chưa phản hồi sau 24h.

**Kết quả?** **90% thời gian** của HR bị "chôn vùi" trong công việc lặp lại, trong khi ứng viên tiềm năng có thể "trôi qua" vì không được theo dõi kịp thời.

**Workflow này giải quyết tất cả!**
- **Tự động nhận ứng viên** từ ATS qua webhook.
- **Phân loại và gửi SMS AI** theo nhóm (Sales, Kỹ Thuật, Tổng Quát).
- **Theo dõi phản hồi tự động** và gửi nhắc nhở nếu ứng viên không phản hồi.
- **Báo cáo Slack** cho bộ phận tuyển dụng khi ứng viên đã tương tác.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo an toàn và không bị giới hạn.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian** xử lý ứng viên thủ công.
✅ **Tăng tỷ lệ phản hồi** từ ứng viên (do SMS AI tự động và nhắc nhở).
✅ **Phân loại chính xác** ứng viên theo nhóm (Sales, Kỹ Thuật, Tổng Quát).
✅ **Báo cáo tự động** trên Slack cho bộ phận tuyển dụng.
✅ **Hoạt động liên tục** 24/7, không cần can thiệp của con người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Aloware** (để quản lý SMS và dây chuyền tự động).
2. **Tài khoản Slack** (để báo cáo kết quả).
3. **API Key của Aloware** và **URL Webhook của Slack**.
4. **Danh sách 3 dây chuyền (Sequence) trong Aloware**:
   - **Sales Pre-screening Sequence**
   - **Tech Pre-screening Sequence**
   - **General Pre-screening Sequence**
5. **Cấu hình biến (Variables) trong n8n**:
   - `ALOWARE_API_TOKEN`
   - `ALOWARE_LINE_PHONE`
   - `ALOWARE_SALES_SEQUENCE_ID`
   - `ALOWARE_TECH_SEQUENCE_ID`
   - `ALOWARE_OPS_SEQUENCE_ID`
   - `COMPANY_NAME`
   - `SLACK_WEBHOOK_URL`

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/14934](https://n8n.io/workflows/14934).
- **Mở n8n Editor** → Nhấn **Import** → Chọn file JSON.
- **Hoặc copy/paste** toàn bộ JSON vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **25 node**, nhưng các bước quan trọng nhất cần chú ý:

##### **A. Cấu Hình Webhook (ATS: New Application Received)**
- **Path:** `ats-new-application`
- **HTTP Method:** `POST`
- **Lưu ý:**
  - **Paste URL webhook** này vào **cài đặt của ATS** (Greenhouse, Lever, BambooHR...).
  - **Kiểm tra** để đảm bảo ATS gửi dữ liệu đúng định dạng JSON.

##### **B. Cấu Hình Aloware (HTTP Request)**
- **Thiết lập biến `ALOWARE_API_TOKEN`** trong **n8n Variables**.
- **Điền các ID Sequence** vào biến tương ứng:
  - `ALOWARE_SALES_SEQUENCE_ID`
  - `ALOWARE_TECH_SEQUENCE_ID`
  - `ALOWARE_OPS_SEQUENCE_ID`
- **Kiểm tra** các node `Aloware: Create or Update Contact` và `Aloware: Send Follow-up SMS` để đảm bảo **URL API** và **headers** đúng.

##### **C. Cấu Hình Slack (Slack: Notify Hiring Manager)**
- **Thiết lập credentials `slackApi`** trong n8n.
- **Điền `SLACK_WEBHOOK_URL`** vào biến tương ứng.
- **Kiểm tra nội dung thông báo** trong node Slack để đảm bảo thông tin được gửi chính xác.

##### **D. Điều Kiện IF (Phân Loại Nhóm)**
- Các node `Is Sales Role?`, `Is Engineering Role?` và `Is General Role?` **phải điều chỉnh tên nhóm** phù hợp với công ty.
  - Ví dụ: Nếu công ty không có nhóm "Sales" mà là "Revenue", **cần chỉnh lại** trong node `Is Sales Role?`.

##### **E. Thời Gian Chờ (Wait 24h)**
- Các node `Wait 24h (Sales)`, `Wait 24h (Tech)`, `Wait 24h (General)` **được thiết lập mặc định 24h**.
- **Không cần chỉnh** trừ khi công ty muốn thay đổi thời gian chờ.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run** với **dữ liệu mẫu** (ví dụ: một ứng viên giả mạo).
- **Kiểm tra** các bước:
  - Ứng viên có được **tạo contact** trong Aloware không?
  - SMS **được gửi** không?
  - **Phản hồi** được theo dõi đúng không?
- **Bật Active workflow** khi đã kiểm tra xong.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Google Sheets/Excel**
   - Thêm node **Google Sheets** để **lưu lịch sử ứng viên** và **báo cáo định kỳ**.
   - Ví dụ: Tạo một sheet mới mỗi tháng để theo dõi hiệu suất tuyển dụng.

2. **Gửi SMS Tùy Chỉnh Theo Nhóm**
   - Thay vì sử dụng **SMS mặc định**, các sếp có thể **tạo các template SMS riêng** cho mỗi nhóm (Sales, Kỹ Thuật, Tổng Quát) trong Aloware.

3. **Báo Cáo Hàng Tuần Cho Giám Đốc**
   - Thêm node **Email** (ví dụ: Gmail, Outlook) để **gửi báo cáo tuần** về số lượng ứng viên đã tương tác và tỷ lệ phản hồi.

4. **Sử Dụng AI Chatbot (LLM) Để Phân Loại Ứng Viên**
   - Thêm node **LLM (AI)** để **xác định nhóm phù hợp** dựa trên CV hoặc thông tin ứng viên.
   - Ví dụ: Nếu ứng viên nói về "mô hình machine learning", hệ thống tự động phân loại vào nhóm **Kỹ Thuật**.

5. **Tích Hợp với CRM (HubSpot, Salesforce)**
   - Sau khi ứng viên phản hồi, **tự động chuyển dữ liệu** vào CRM để bộ phận bán hàng theo dõi.

---

### 📌 **Kết Luận**
Workflow này **giải phóng HR khỏi công việc lặp lại**, giúp **tăng hiệu suất tuyển dụng** và **cải thiện trải nghiệm ứng viên** thông qua SMS AI tự động.

**Hành động ngay:**
1. **Cài đặt n8n trên VPS** (để đảm bảo an toàn và hoạt động 24/7).
2. **Import workflow** và **cấu hình biến** theo hướng dẫn.
3. **Test Run** với dữ liệu mẫu trước khi kích hoạt.
4. **Bắt đầu tự động hóa tuyển dụng** và **tiết kiệm thời gian** cho đội ngũ HR!

**🚀 CÓ THỂ CẦN GỌI TRỢ GIÚP KHI CẦN THIẾT!** Nếu có bất kỳ vấn đề nào trong quá trình setup, các sếp có thể liên hệ với **Maxim Dudnik** (tác giả workflow) hoặc cộng đồng **n8n.io** để hỗ trợ.

---
**Chúc các sếp thành công với việc tự động hóa tuyển dụng!** 💼🚀