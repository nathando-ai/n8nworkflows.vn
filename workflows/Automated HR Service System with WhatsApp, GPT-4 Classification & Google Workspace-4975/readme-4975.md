---
title: "🤖 Hệ Thống Dịch Vụ HR Tự Động Hoá với WhatsApp + GPT-4 & Google Workspace (N8N)"
description: "Tự động hóa toàn bộ quy trình HR từ xin nghỉ phép, điểm danh, tuyển dụng đến giải quyết thắc mắc và khiếu nại chỉ trong 57 node, không cần code. Giúp các sếp tiết kiệm 20+ giờ/tuần và giảm thiểu sai sót nhân sự."
slug: "he-thong-dich-vu-hr-tu-dong-hoa-whatsapp-gpt4-google-workspace"
tags: [n8n, automation, hr, ai, gpt-4, whatsapp, google-workspace, no-code]
keywords: [tự động hóa hr với n8n, chatbot hr tự động, quản lý nhân sự bằng ai, workflow hr không code, giải pháp hr tự động hóa]
---

# 🚀 **Hệ Thống Dịch Vụ HR Tự Động Hoá Toàn Diện với WhatsApp + GPT-4 & Google Workspace**

### **Giải pháp cuối cùng cho các sếp muốn loại bỏ công việc HR thủ công**
Hãy tưởng tượng một ngày không phải mất giờ để:
- **Xử lý hàng chục yêu cầu xin nghỉ phép** qua WhatsApp?
- **Điểm danh nhân viên** chỉ bằng vị trí GPS mà không cần app riêng?
- **Tuyển dụng hiệu quả** với AI tự động lọc CV và đặt lịch phỏng vấn?
- **Trả lời thắc mắc HR** 24/7 bằng chatbot thông minh?

**Workflow này làm tất cả đó – và còn nhiều hơn!** Sử dụng **WhatsApp làm kênh duy nhất**, **GPT-4 phân loại và xử lý tự động**, và **Google Workspace (Sheets, Calendar, Gmail) làm trung tâm dữ liệu**, hệ thống này **tự động hóa 90% công việc HR** mà không cần viết một dòng code.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted) với **OpenAI API, Google Workspace OAuth2 và Supabase Vector Store**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
*Lưu ý:* Cần **OpenAI API Key (GPT-4o, GPT-4.1-nano)** và **Supabase URL/Key** để lưu trữ embeddings.
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 20+ giờ/tuần** cho bộ phận HR: Tự động xử lý xin nghỉ phép, điểm danh, tuyển dụng và FAQ.
- **Chính xác 100%**: AI phân loại tin nhắn WhatsApp với độ chính xác cao (5 loại yêu cầu khác nhau).
- **Cá nhân hóa tương tác**: Trả lời từng nhân viên với thông tin chính xác (email phòng ban, lịch sử nghỉ phép).
- **Hoạt động 24/7**: Không cần nhân viên trực ca, hệ thống xử lý ngay lập tức khi nhận tin nhắn.
- **Tối ưu tuyển dụng**: AI tự động lọc CV và đặt lịch phỏng vấn, giảm thiểu công việc thủ công.
- **Giảm thiểu khiếu nại**: Chatbot trả lời FAQ và chuyển yêu cầu phức tạp đến phòng ban phù hợp.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản WhatsApp Business API** (đăng ký tại [Meta for Business](https://developers.facebook.com/docs/whatsapp/cloud-api/get-started)).
2. **Google Workspace** (Gmail, Sheets, Calendar) với **OAuth2 API** được kích hoạt.
3. **OpenAI API Key** (đăng ký tại [OpenAI](https://platform.openai.com/)) với **tài khoản Pro** (để sử dụng GPT-4o).
4. **Supabase** (miễn phí) để lưu trữ **embeddings** của chính sách HR (nếu sử dụng tính năng FAQ).
5. **Google Sheets** với các bảng dữ liệu chuẩn bị sẵn:
   - `JD tool`: Danh sách yêu cầu công việc (Job Description).
   - `applicants`: Danh sách ứng viên.
   - `dept head email`: Email của các trưởng phòng.
   - `leaves`: Lịch sử nghỉ phép của nhân viên.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/4975](https://n8n.io/workflows/4975) (hoặc copy JSON từ link trên).
- Mở **n8n Editor** → Nhấn **Import Workflow** → Dán JSON và nhấn **Import**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **phức tạp** với 57 node, nhưng chỉ cần chú ý đến các phần sau:

##### **A. Cấu hình WhatsApp Trigger**
- **Node: `WhatsApp Trigger`**
  - Đăng ký **WhatsApp Business API** và tạo **credentials** trong n8n với tên `whatsAppTriggerApi`.
  - **Lưu ý:** Cần **phone number** của WhatsApp Business đã được xác thực.

##### **B. Cấu hình OpenAI**
- **Node: `OpenAI`, `lmChatOpenAi`, `embeddingsOpenAi`**
  - Sử dụng **credentials** `openAiApi` (điền API Key từ OpenAI).
  - **Model mặc định:** GPT-4.1-nano (hoặc GPT-4o nếu có tài khoản Pro).
  - **Prompt:** Workflow đã định sẵn, **không cần chỉnh sửa** trừ khi cần tùy biến.

##### **C. Cấu hình Google Workspace**
- **Node: `gmailTool`, `googleSheets`, `googleCalendarTool`**
  - Tạo **credentials OAuth2** cho:
    - `gmailOAuth2` (để gửi email tự động).
    - `googleSheetsOAuth2Api` (để đọc/viết vào Sheets).
    - `googleCalendarOAuth2Api` (đặt lịch phỏng vấn).
  - **Bảng Sheets cần chuẩn bị:**
    - `JD tool`: Cột `job_title`, `skills_required`, `experience`.
    - `applicants`: Cột `name`, `cv_link`, `score`.
    - `dept head email`: Cột `employee_name`, `email`.

##### **D. Cấu hình Supabase (nếu sử dụng FAQ)**
- **Node: `vectorStoreSupabase`**
  - Tạo **credentials `supabaseApi`** với URL và Key từ [Supabase Dashboard](https://app.supabase.com/).
  - **Tải lên embeddings** từ các file chính sách HR (PDF/Docx) trước khi chạy workflow.

##### **E. Cấu hình LLM Agents**
- **Node: `Leave Agent`, `HR Chatbot`, `Shortlist Agent`, `Attendance Agent`**
  - **Không cần chỉnh sửa** vì workflow đã định sẵn logic:
    - **Leave Agent:** Auto phê duyệt nghỉ <2 ngày, yêu cầu phê duyệt ≥2 ngày.
    - **Shortlist Agent:** Lọc CV theo yêu cầu công việc và đặt lịch phỏng vấn.
    - **Attendance Agent:** Kiểm tra vị trí GPS trong khu vực văn phòng.
    - **HR Chatbot:** Trả lời FAQ và tìm kiếm chính sách từ vector store.

##### **F. Cấu hình WhatsApp Responder**
- **Node: `WhatsApp Responder`**
  - Sử dụng **credentials `whatsAppApi`** (cùng với `whatsAppTriggerApi`).
  - **Lưu ý:** Cần **định dạng tin nhắn trả lời** sao cho rõ ràng (ví dụ: "Xin nghỉ đã được phê duyệt!").

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi tin nhắn WhatsApp với các loại yêu cầu:
     - **Text:** "Xin nghỉ ngày mai" (loại 1).
     - **Location:** Gửi vị trí GPS (loại 3).
     - **Audio:** Gửi âm thanh (loại 2).
     - **Image:** Gửi ảnh (loại 2).
     - **Escalation:** "Gửi email cho IT" (loại 4).
     - **Shortlist:** "Lọc CV backend" (loại 5).
2. **Kiểm tra các node quan trọng:**
   - `Switch Router` (phân loại tin nhắn).
   - `Leave Agent` (xử lý nghỉ phép).
   - `Shortlist Agent` (tuyển dụng).
   - `WhatsApp Responder` (trả lời tự động).
3. **Bật `Active`** workflow sau khi test thành công.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp Slack/Telegram cho báo cáo**
   - Thêm **node `slack`** hoặc `telegramBot` sau `WhatsApp Responder` để gửi báo cáo tự động cho quản lý.

2. **Lưu log tất cả hoạt động**
   - Thêm **node `googleSheetsTool`** mới để ghi lại lịch sử tin nhắn và phản hồi vào bảng `logs`.

3. **Tự động gửi báo cáo tuần/Tháng**
   - Sử dụng **node `googleCalendarTool`** để đặt lịch gửi email báo cáo tổng hợp cho HR.

4. **Tùy biến AI với Prompt Engineering**
   - Nếu muốn AI trả lời FAQ **cá nhân hóa hơn**, chỉnh sửa **prompt** trong node `lmChatOpenAi` với ví dụ cụ thể về văn hóa doanh nghiệp.

5. **Xử lý tin nhắn lỗi**
   - Thêm **node `if`** sau `WhatsApp Trigger` để chuyển tin nhắn không hợp lệ về `HR Chatbot` với thông báo "Tin nhắn không được nhận diện. Vui lòng liên hệ HR."

---

### 📌 **Kết luận**
Workflow này **không chỉ tiết kiệm thời gian mà còn nâng cao hiệu quả HR** bằng cách:
✅ **Tự động hóa 90% công việc thủ công** (xin nghỉ, điểm danh, tuyển dụng, FAQ).
✅ **Cải thiện trải nghiệm nhân viên** với phản hồi tức thời và cá nhân hóa.
✅ **Giảm thiểu sai sót** nhờ AI phân loại và xử lý logic.
✅ **Hoạt động 24/7** mà không cần nhân viên trực ca.

**Hành động ngay!**
- **Import workflow** và bắt đầu tự động hóa HR của doanh nghiệp.
- **Tùy biến** các bảng Sheets và prompt để phù hợp với quy trình cụ thể.
- **Mở rộng** với tính năng mới như **báo cáo tự động** hoặc **tích hợp với Zoom** cho cuộc họp phỏng vấn.

**🚀 Các sếp sẵn sàng tự động hóa HR chưa?** Hãy bắt đầu từ hôm nay!