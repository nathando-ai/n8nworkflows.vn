---
title: "🛡️ **AI Security Firewall cho Agent: Bảo vệ Trực Tuyến với Guardrails AI trên n8n**"
description: "Workflow tự động hóa AI an toàn 100% không code, giúp các sếp kiểm soát, lọc và bảo mật nội dung từ AI trước khi xử lý, ngăn chặn nội dung nguy hại (PII, NSFW, URL độc hại, key bí mật) và đảm bảo tuân thủ chính sách nội bộ."
slug: "ai-security-firewall-guardrails-n8n"
tags: [n8n, automation, AI security, guardrails, LangChain, Google Gemini, no-code]
keywords: [n8n workflow an toàn AI, bảo mật agent AI, guardrails AI, lọc nội dung nguy hại, tự động hóa SecOps, Google Gemini n8n]
---

# 🛡️ **AI Security Firewall: Bảo vệ Agent AI của Các Sếp Trước Những Rủi Ro Ẩn Nghiêm Trọng**

## **🔍 Nỗi Đau Thực Tế: AI của Các Sếp Có An Toàn Không?**
Hiện nay, khi các sếp triển khai **AI Agent** (như chatbot, virtual assistant, hoặc hệ thống tự động hóa) để xử lý công việc hàng ngày, họ thường gặp phải những rủi ro an toàn nghiêm trọng mà không nhận thức được:
- **Nội dung nguy hại tự động sinh ra**: AI có thể trả lời chứa **thông tin cá nhân (PII)**, **từ ngữ không phù hợp (NSFW)**, hoặc **liên kết độc hại (malicious URLs)**.
- **Rò rỉ thông tin nhạy cảm**: AI có thể vô tình tiết lộ **API Keys**, **thông tin tài khoản**, hoặc **bí mật doanh nghiệp** trong quá trình xử lý.
- **Không kiểm soát chủ đề**: AI có thể trả lời **bất hợp pháp** hoặc **không phù hợp với chính sách nội bộ** của công ty.
- **Không có cơ chế kiểm duyệt tự động**: Các sếp phải **manually review** từng kết quả, tốn thời gian và dễ bỏ sót.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Lọc và loại bỏ** tất cả nội dung nguy hại **trước khi AI trả lời**.
✅ **Bảo mật thông tin cá nhân (PII)** và **API Keys** trong mọi trường hợp.
✅ **Kiểm soát chủ đề (Topical Alignment)** để AI chỉ trả lời những nội dung phù hợp với quy định.
✅ **Sử dụng Google Gemini** (AI mạnh nhất hiện nay) để xử lý **một cách an toàn và hiệu quả**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **An toàn tuyệt đối**: Không bao giờ có rủi ro từ AI sinh ra nội dung nguy hại.
- **Tiết kiệm thời gian**: Không cần manual review từng kết quả, AI tự động lọc và bảo mật.
- **Tuân thủ chính sách**: Đảm bảo AI chỉ trả lời những nội dung phù hợp với quy định nội bộ.
- **Hiệu suất cao**: Sử dụng **Google Gemini** để xử lý nhanh chóng và chính xác.
- **Dễ dàng mở rộng**: Có thể kết nối với **Slack, Email, hoặc Google Sheets** để báo cáo và log.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI LẮP ĐẶT**]
Để workflow này hoạt động **ổn định và an toàn**, các sếp cần chuẩn bị:
1. **Tài khoản Google Cloud** (để sử dụng **Google Gemini API**):
   - [Đăng ký Google Cloud](https://cloud.google.com/) và tạo **API Key**.
   - Cài đặt **Google Sheets** để lưu **dữ liệu test guardrails** (nếu cần).
2. **Credentials cho n8n**:
   - **Google Sheets API Key** (nếu sử dụng node `googleSheets`).
   - **API Key của Google Gemini** (để kết nối với `lmChatGoogleGemini`).
3. **N8n Enterprise** (để sử dụng **nodes LangChain** như `guardrails` và `lmChatGoogleGemini`).
   - Nếu chưa có, các sếp có thể **self-host n8n trên VPS** để tiết kiệm chi phí.
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow từ file JSON** hoặc **copy/paste JSON** vào **n8n Editor**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/11025) (nếu có).
- **Hoặc copy toàn bộ JSON** từ [đây](https://n8n.io/workflows/11025) và dán vào **n8n Editor** → **Create Workflow** → **Import from JSON**.

:::note[**Lưu ý quan trọng**]
- Workflow này **không hoạt động trên n8n Community** (miễn phí) vì sử dụng **nodes LangChain** (cần **n8n Enterprise**).
- Nếu các sếp muốn **self-host**, có thể cài **n8n Enterprise** trên **VPS** (gợi ý [TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N**).
:::

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **A. Cấu Hình Guardrails (Bảo vệ AI)**
Workflow này sử dụng **10 rule guardrails** để kiểm soát nội dung AI trả lời:
| **Rule**               | **Mô Tả**                                                                 | **Lưu Ý Cấu Hình**                                                                 |
|------------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------------|
| **Keywords**            | Chặn từ khóa nguy hại (ví dụ: "hack", "phishing").                       | Điền danh sách **keywords cấm** vào **Google Sheets** (nếu sử dụng).              |
| **Jailbreak**           | Ngăn chặn AI trốn qua kiểm soát bằng cách sử dụng từ khóa đặc biệt.      | **Không cần cấu hình**, guardrails tự động phát hiện.                           |
| **NSFW**                | Lọc nội dung không phù hợp (thô bạo, tình dục).                          | **Không cần cấu hình**, guardrails tự động kiểm tra.                            |
| **PII (Personal Data)** | Ngăn AI tiết lộ thông tin cá nhân (SDT, email, địa chỉ).                 | **Không cần cấu hình**, guardrails tự động loại bỏ.                              |
| **Secret Keys**         | Chặn API Keys, mật khẩu, token bí mật.                                    | **Không cần cấu hình**, guardrails tự động detect.                              |
| **Topical Alignment**   | Đảm bảo AI chỉ trả lời chủ đề được phép (ví dụ: không nói về chính trị). | Cấu hình **danh sách chủ đề cho phép** trong **Google Sheets** (nếu cần).       |
| **URLs**                | Ngăn AI trả lời liên kết độc hại hoặc không an toàn.                       | **Không cần cấu hình**, guardrails tự động kiểm tra.                            |
| **Sanitize PII/Keys/URLs** | Tự động **xóa hoặc thay thế** thông tin nguy hại.                     | **Không cần cấu hình**, guardrails tự động xử lý.                              |

#### **B. Cấu Hình Google Gemini Chat Model**
- **Node**: `Google Gemini Chat Model`
- **Cần thiết**:
  - **API Key Google Cloud** (điền vào **Credentials** của node).
  - **Model**: Chọn **`gemini-pro`** (mô hình mạnh nhất hiện nay).
  - **Prompt**: Có thể tùy chỉnh để phù hợp với công việc của các sếp.

#### **C. Cấu Hình Google Sheets (Nếu Sử Dụng)**
- **Node**: `Guadrails Test Data`
- **Cần thiết**:
  - **API Key Google Sheets** (để đọc/writing dữ liệu).
  - **Sheet Name**: Đặt tên cho **Google Sheet** chứa **dữ liệu test guardrails** (nếu có).

#### **D. Cấu Hình Manual Trigger**
- **Node**: `When clicking ‘Execute workflow’`
- **Lưu ý**:
  - Các sếp có thể **bỏ qua node này** và sử dụng **Webhook** hoặc **Schedule Trigger** để tự động chạy workflow.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với **dữ liệu mẫu**:
   - Gửi một **query test** (ví dụ: *"Hãy cho tôi một danh sách các API Key an toàn"*).
   - Kiểm tra **AI có bị chặn không** (nếu có, guardrails đang hoạt động).
2. **Bật Active**:
   - Chuyển **switch "Active"** thành **ON**.
   - **Kiểm tra log** để đảm bảo workflow chạy **ổn định**.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Kết Nối với Slack/Telegram để Báo Cáo**
- Sử dụng **node `slack`** hoặc **`telegram`** để **báo cáo ngay khi AI bị chặn** hoặc **trả lời không an toàn**.
- **Cách làm**:
  - Thêm **node `slack`** sau **node `Switch`**.
  - Cấu hình **webhook Slack** và gửi thông báo khi có **violation guardrails**.

### **2. Lưu Log vào Google Sheets/Database**
- Sử dụng **node `googleSheets`** hoặc **`database`** để **lưu lịch sử các query bị chặn**.
- **Ưu điểm**:
  - Các sếp có thể **analyze** xem AI bị chặn vì lý do gì.
  - **Dễ dàng báo cáo** cho quản lý.

### **3. Tự Động Chạy Workflow Theo Lịch**
- Sử dụng **node `schedule`** để **chạy workflow định kỳ** (ví dụ: **mỗi ngày 8h**).
- **Cách làm**:
  - Thêm **node `schedule`** vào đầu workflow.
  - Cấu hình **thời gian chạy** và **dữ liệu đầu vào** (nếu có).

### **4. Kết Nối với Email để Báo Cáo Violation**
- Sử dụng **node `email`** để **gửi báo cáo tự động** khi AI bị chặn.
- **Cách làm**:
  - Thêm **node `email`** sau **node `Switch`**.
  - Cấu hình **SMTP** và **địa chỉ email** của quản lý.

---

## **📌 Kết Luận: AI An Toàn Là Lựa Chọn Không Thể Tránh Khỏi**

Các sếp đã **xem xét rõ ràng** rằng **AI không phải là giải pháp hoàn hảo** nếu không có **mechanism kiểm soát**. Workflow này **giải quyết tất cả những rủi ro an toàn** bằng cách:
✔ **Lọc và loại bỏ** tất cả nội dung nguy hại **trước khi AI trả lời**.
✔ **Bảo mật thông tin cá nhân (PII)** và **API Keys** một cách tự động.
✔ **Kiểm soát chủ đề** để AI chỉ trả lời những nội dung phù hợp.
✔ **Sử dụng Google Gemini** (AI mạnh nhất) để xử lý **một cách an toàn và hiệu quả**.

**🚀 Hành động ngay hôm nay:**
1. **Self-host n8n Enterprise** trên **VPS** (gợi ý [TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N**).
2. **Import workflow** và **cấu hình guardrails**.
3. **Test run** và **bật Active** để **AI của các sếp trở nên an toàn hơn**.

**💡 Nếu các sếp cần hỗ trợ thêm**, có thể liên hệ với tác giả **Sandeep Patharkar** qua [FastTrackAiMastery](https://www.fasttrackaimastery.com/) để **cập nhật và tối ưu hóa workflow**!

---
**🔥 Chúc các sếp thành công với AI an toàn!** 🚀