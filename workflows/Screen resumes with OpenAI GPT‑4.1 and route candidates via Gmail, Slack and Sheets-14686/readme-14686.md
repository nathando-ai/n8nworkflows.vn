---
title: "🤖 **Tự Động Xếp Hạng & Lọc Sơ Lọc CV Bằng AI GPT-4.1 + Gmail/Slack/Sheets - Giúp HR Tiết Kiệm 100h/Năm**"
description: "Workflow tự động hóa lọc CV bằng AI GPT-4.1, tự động phân loại ứng viên thành 'Chấp nhận', 'Từ chối' hoặc 'Xét lại' và gửi thông báo tự động qua Gmail, Slack và Google Sheets. Giúp HR tiết kiệm thời gian, giảm sai sót và tối ưu quy trình tuyển dụng."
slug: "tieu-dong-hoa-loc-cv-bang-ai-gpt-4-1"
tags: [n8n, automation, hr, ai-summarization, openai, gmail, slack, google-sheets, no-code]
keywords: [tự động hóa tuyển dụng, lọc cv bằng ai, gpt-4.1 n8n, workflow hr, tự động hóa slack gmail, ai tuyển dụng, n8n openai]
---

# 🚀 **Tự Động Xếp Hạng & Lọc Sơ Lọc CV Bằng AI GPT-4.1 + Gmail/Slack/Sheets**

### **Giải pháp AI tự động hóa tuyển dụng: Từ "Chấp nhận" đến "Từ chối" chỉ trong vài giây!**
Hiện nay, việc thủ công đánh giá hàng trăm CV mỗi ngày khiến HR cảm thấy **mệt mỏi, mất thời gian và dễ bị sai sót**. Workflow này giúp tự động hóa **tất cả quy trình lọc CV** bằng AI GPT-4.1, phân loại ứng viên và gửi thông báo tự động qua **Gmail, Slack và Google Sheets** – giúp bạn **tiết kiệm 100+ giờ/năm** và nâng cao chất lượng tuyển dụng.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo bảo mật và hiệu suất tối ưu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: AI tự động đánh giá CV trong **vài giây**, thay vì mất **30-60 phút/người**.
✅ **Chính xác & khách quan**: GPT-4.1 phân tích kỹ năng, kinh nghiệm và phù hợp với vị trí, giảm sai sót của con người.
✅ **Tự động hóa toàn bộ quy trình**: Từ nhận CV đến gửi thông báo kết quả (chấp nhận/từ chối/xét lại).
✅ **Theo dõi dễ dàng**: Tất cả kết quả được **ghi chép tự động vào Google Sheets** và thông báo trên **Slack/Gmail**.
✅ **Tối ưu nguồn nhân lực**: Giúp HR tập trung vào **phỏng vấn và tuyển dụng chất lượng** thay vì làm việc thủ công.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
- **Tài khoản OpenAI** (API Key) để sử dụng GPT-4.1.
- **Tài khoản Gmail** (đã cấu hình OAuth 2.0) để gửi email chấp nhận/từ chối.
- **Tài khoản Slack** (Webhook URL) để thông báo ứng viên có điểm "xét lại".
- **Google Sheets** (một bảng mới để lưu log kết quả).
- **Webhook URL** (để ứng viên upload CV).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/14686](https://n8n.io/workflows/14686) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/14686) và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này bao gồm **15 node**, nhưng các bước sau đây là **quan trọng nhất** cần điều chỉnh:

##### **A. Cấu hình Webhook (Resume Upload)**
- Node: **"Resume Upload Webhook"**
  - Đảm bảo **path = `resume-upload`** và **HTTP Method = POST**.
  - **Lưu ý**: Cần cung cấp **URL webhook** cho ứng viên upload CV (ví dụ: `https://tên-domain-n8n.com/webhook/resume-upload`).

##### **B. Cấu hình AI Scoring (GPT-4.1)**
- Node: **"OpenAI Chat Model"**
  - **Model**: Chọn `gpt-4.1-mini` (hoặc `gpt-4` nếu có budget).
  - **API Key**: Điền **OpenAI API Key** vào **Credentials** của node này.
  - **Prompt**: Workflow đã định sẵn, nhưng các sếp có thể **cập nhật yêu cầu đánh giá** (ví dụ: yêu cầu kỹ năng cụ thể cho vị trí).

##### **C. Cấu hình Email (Gmail)**
- Node: **"Send Acceptance Email"** và **"Send Rejection Email"**
  - **Credentials**: Chọn tài khoản Gmail đã cấu hình OAuth 2.0.
  - **Template Email**: Cần **cập nhật nội dung email** để phù hợp với doanh nghiệp (ví dụ: tên công ty, thông tin liên hệ).

##### **D. Cấu hình Slack (Notify HR)**
- Node: **"Notify HR - Borderline"**
  - **Webhook URL**: Điền **Webhook URL của Slack** (tạo từ **Apps > Incoming Webhooks**).
  - **Channel**: Chọn **#hr-notifications** hoặc channel phù hợp.

##### **E. Cấu hình Google Sheets (Logging)**
- Node: **"Log to Google Sheets - Accept"**, **"Log to Google Sheets - Reject"**, **"Log to Google Sheets - Borderline"**
  - **Credentials**: Chọn tài khoản Google đã kết nối với Sheets.
  - **Sheet Name**: Điền **tên bảng** (ví dụ: `CV_Screening_Log`).
  - **Range**: Điền **tên sheet** (ví dụ: `Sheet1`).
  - **Headers**: Đảm bảo **cột đầu tiên** là `Name, Email, Score, Status, Notes`.

##### **F. Cấu hình Threshold (Điểm chấp nhận/từ chối)**
- Node: **"Check Score - Accept"** và **"Check Score - Borderline"**
  - **Điểm chấp nhận**: Cần **cập nhật ngưỡng điểm** (ví dụ: `>= 80`).
  - **Điểm xét lại**: Cần **cập nhật ngưỡng điểm** (ví dụ: `>= 60 và < 80`).

#### **3. Kích hoạt ⚡️**
- **Test Run**: Chọn **Run Workflow** và upload một **CV mẫu** (PDF/DOCX) để kiểm tra.
- **Active Workflow**: Sau khi kiểm tra thành công, **bật Active** để workflow hoạt động 24/7.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động hóa thêm Slack/Telegram**:
   - Thêm node **Slack/Telegram Bot** để thông báo kết quả cho ứng viên (ví dụ: `Tôi đã được chấp nhận!`).

2. **Lưu log chi tiết hơn**:
   - Thêm **Google Drive** để lưu CV gốc của ứng viên (node `n8n-nodes-base.googleDrive`).

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n + Google Sheets + Email** để tự động gửi **báo cáo hàng tuần** về số lượng CV được chấp nhận/từ chối.

4. **Cập nhật AI Prompt**:
   - Nếu muốn **chỉnh sửa cách AI đánh giá**, hãy cập nhật **Prompt** trong node `lmChatOpenAi` (ví dụ: yêu cầu AI chú trọng kinh nghiệm trong ngành cụ thể).

5. **Sử dụng AI Agent cho phỏng vấn**:
   - Kết hợp với **n8n + Zoom/Calendly** để tự động lịch phỏng vấn cho ứng viên được chấp nhận.

---

### 📌 **Kết luận**
Workflow này **giải phóng HR khỏi công việc lặp lại**, giúp **tự động hóa 100% quy trình lọc CV** bằng AI GPT-4.1. **Chỉ cần upload CV, AI sẽ tự đánh giá và gửi kết quả** – tiết kiệm **thời gian, giảm sai sót và nâng cao hiệu quả tuyển dụng**.

**🚀 Hãy áp dụng ngay và bắt đầu tự động hóa tuyển dụng của bạn!**
Nếu có vấn đề, hãy **đăng ký VPS n8n** và liên hệ hỗ trợ để **cài đặt và cấu hình** workflow này một cách dễ dàng.

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/14686)**
**📌 [Hướng dẫn cài n8n trên VPS](https://docs.n8n.io/hosting/installation/self-hosted)**