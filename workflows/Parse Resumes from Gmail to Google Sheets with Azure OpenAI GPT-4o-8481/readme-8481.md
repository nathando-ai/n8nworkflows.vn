---
title: "🚀 Tự Động Hóa Xử Lý CV từ Gmail sang Google Sheets Với AI Tóm Tắt GPT-4o (Không Cần Code)"
description: "Workflow tự động hóa nhận, tóm tắt và lưu trữ CV từ email vào Google Sheets với AI Azure OpenAI GPT-4o, tiết kiệm thời gian cho bộ phận HR lên tới 80%. Giúp các sếp loại bỏ công việc thủ công, giảm sai sót và tối ưu quy trình tuyển dụng."
slug: "tieu-dong-hoa-xu-ly-cv-tu-gmail-sang-google-sheets-voi-gpt-4o"
tags: [n8n, automation, hr, ai-summarization, azure-openai, google-sheets, no-code]
keywords: [tự động hóa cv, n8n workflow cv, ai tóm tắt cv, google sheets tự động, gpt-4o tự động hóa]
---

# 🚀 **Tự Động Hóa Xử Lý CV từ Gmail sang Google Sheets Với AI Tóm Tắt GPT-4o**

### **Giải pháp cho bộ phận HR: Từ "đọc hàng trăm CV" sang "tóm tắt và lưu trữ tự động" chỉ trong vài giây!**

Hiện nay, bộ phận HR thường phải dành **giờ đồng hồ** để đọc, tóm tắt và lưu trữ hàng trăm CV từ email vào Google Sheets. Đây là công việc **mòn mỏi, dễ sai sót** và **tốn thời gian** mà lại không mang lại giá trị cao. **Workflow này sẽ tự động hóa toàn bộ quy trình đó bằng AI GPT-4o**, giúp các sếp:
✅ **Tiết kiệm 80% thời gian** trong việc xử lý CV.
✅ **Tóm tắt nội dung chính** của CV một cách chính xác và cá nhân hóa.
✅ **Lưu trữ tự động** vào Google Sheets với định dạng sạch sẽ.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định và an toàn**, các sếp nên **self-host n8n** trên VPS để tránh phụ thuộc vào phiên bản cloud có giới hạn.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (phù hợp cho n8n + AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động nhận CV từ Gmail** (không cần copy-paste).
- **AI GPT-4o tóm tắt CV** thành 3-5 điểm chính (ngôn ngữ tự nhiên, không mất thời gian đọc).
- **Lưu trữ vào Google Sheets** với cấu trúc sạch sẽ (tên ứng viên, email, tóm tắt, file CV).
- **Hoạt động liên tục** (không cần phải check email liên tục).
- **Giảm sai sót** (AI không bị mệt mỏi như con người).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Gmail** (cần quyền truy cập vào thư mục Inbox).
✔ **Tài khoản Google Drive & Google Sheets** (để lưu trữ CV và tóm tắt).
✔ **API Key Azure OpenAI** (để sử dụng GPT-4o).
✔ **Credentials cho các node**:
   - **Gmail**: OAuth 2.0 (cần cấp quyền cho n8n truy cập email).
   - **Google Drive/Sheets**: OAuth 2.0 (cấp quyền chỉnh sửa).
   - **Azure OpenAI**: API Key + Endpoint (đăng ký tại [Azure Portal](https://azure.microsoft.com/)).

---
:::note[LƯU Ý QUAN TRỌNG]
- **Không sử dụng email cá nhân** (nên tạo một email chuyên dụng cho bộ phận HR).
- **Kiểm tra quyền truy cập** của OAuth 2.0 để workflow không bị lỗi.
- **Nếu sử dụng GPT-4o**, đảm bảo tài khoản Azure OpenAI có đủ credit.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [n8n.io/workflows/8481](https://n8n.io/workflows/8481).
- **Nhấn "Import"** trong n8n Editor và chọn file.
- **Hoặc copy toàn bộ JSON** và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **9 node** quan trọng, các sếp cần cấu hình kỹ lưỡng:

| **Node**               | **Lưu ý cấu hình**                                                                 | **Tham số cần điền**                          |
|------------------------|-------------------------------------------------------------------------------------|-----------------------------------------------|
| **Gmail Trigger**      | Chọn **Inbox** hoặc thư mục chuyên dụng để nhận CV.                                | -                                            |
| **Get the attachment** | Chọn **file đính kèm** (CV) từ email.                                             | -                                            |
| **Download file**      | Lưu CV vào Google Drive trước khi xử lý.                                           | -                                            |
| **Extract from File**  | Chọn loại file (PDF/Docx) và cấu hình nếu cần.                                     | File Type: PDF/Word                          |
| **Azure OpenAI Chat**  | **Cấu hình API Key** và **Endpoint** từ Azure.                                     | API Key, Endpoint, Model: gpt-4o             |
| **AI Agent**           | **Prompt tóm tắt CV** (các sếp có thể chỉnh sửa để phù hợp).                     | Prompt: *"Tóm tắt CV này thành 3-5 điểm chính, bao gồm kinh nghiệm, kỹ năng và yêu cầu ứng viên."* |
| **Google Sheets Append**| Chọn **Sheet** và **Sheet Name** để lưu trữ dữ liệu.                              | Sheet Name: "CV_Processed"                   |
| **Code (nếu cần)**    | Nếu muốn thêm logic xử lý đặc biệt (ví dụ: loại bỏ CV không phù hợp).              | JavaScript (nếu cần)                        |

:::warning[CẢNH BÁO]
- **Không để trống Prompt** trong AI Agent, nếu không AI sẽ trả về kết quả không chính xác.
- **Kiểm tra quyền Google Drive** để file CV được tải xuống thành công.
- **Nếu CV quá dài**, AI có thể không tóm tắt đầy đủ → các sếp nên **cắt ngắn Prompt** hoặc **tăng token limit** trong Azure OpenAI.
:::

#### **3. Kích hoạt ⚡️**
- **Test Run** với một email mẫu (đính kèm CV) để kiểm tra workflow hoạt động.
- **Bật Active** khi đã kiểm tra thành công.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÂNG CAO]
1. **Gửi thông báo Slack/Telegram** khi có CV mới:
   - Thêm **node Slack/Telegram Webhook** sau **Google Sheets Append** để báo cáo tự động.
2. **Lưu log vào Google Sheets** để theo dõi lịch sử:
   - Thêm **node Code** để ghi thời gian xử lý và trạng thái.
3. **Loại bỏ CV không phù hợp** bằng AI:
   - Chỉnh sửa **Prompt** trong AI Agent để loại bỏ ứng viên không đáp ứng yêu cầu.
4. **Tích hợp với CRM** (như HubSpot, Salesforce):
   - Sau khi tóm tắt, tự động chuyển dữ liệu vào CRM để theo dõi ứng viên.
5. **Sử dụng AI để đánh giá CV** (ví dụ: điểm số phù hợp với vị trí):
   - Chỉnh sửa **Prompt** để AI đánh giá và xếp hạng ứng viên.
:::

---

### 📌 **Kết luận**
Workflow này **giải phóng bộ phận HR khỏi công việc mòn mỏi** và **tăng hiệu suất tuyển dụng lên gấp 5 lần**. Với **AI GPT-4o**, các sếp không chỉ tiết kiệm thời gian mà còn **nhận được tóm tắt chính xác và cá nhân hóa** cho mỗi CV.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với email mẫu** để đảm bảo hoạt động.
3. **Bật Active** và **nhận CV tự động** từ bây giờ!

👉 **[Tải workflow nguyên bản](https://n8n.io/workflows/8481)** và bắt đầu tự động hóa ngay!

---
**Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để self-host và tránh giới hạn phiên bản cloud! 🚀