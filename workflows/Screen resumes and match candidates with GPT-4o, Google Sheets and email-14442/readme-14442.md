---
title: "🤖 Tự Động Học Viên & Phân Tích CV Tiếng Việt: AI GPT-4o + Google Sheets + Email (N8n)"
description: "Workflow tự động hóa tuyển dụng siêu thông minh: Phân tích CV, đánh giá kỹ năng, trải nghiệm và phù hợp văn hóa bằng GPT-4o, lưu kết quả vào Google Sheets và gửi báo cáo email tự động. Giúp các sếp tiết kiệm 80% thời gian phỏng vấn sơ bộ."
slug: "tuyen-dung-ai-gpt4o-google-sheets-email"
tags: [n8n, automation, ai-summarization, hr-automation, gpt-4o, google-sheets, email-automation]
keywords: [n8n workflow tuyển dụng, tự động hóa phân tích CV, AI GPT-4o tuyển dụng, lưu kết quả Google Sheets, gửi báo cáo email tự động]
---

# 🚀 **Tự Động Học Viên & Phân Tích CV: AI GPT-4o + Google Sheets + Email (N8n)**

### **Giải pháp AI tự động hóa tuyển dụng cho các sếp: Phân tích CV, đánh giá kỹ năng, trải nghiệm và phù hợp văn hóa chỉ trong vài giây!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo bảo mật và hiệu suất tối ưu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian phỏng vấn sơ bộ**: AI tự động phân tích CV và đánh giá phù hợp với yêu cầu công việc.
- **Đánh giá toàn diện**: Kỹ năng, kinh nghiệm, và phù hợp văn hóa được đánh giá song song bởi 4 AI chuyên biệt.
- **Lưu trữ tự động**: Kết quả phân tích được lưu vào **Google Sheets** với định dạng chuyên nghiệp.
- **Gửi báo cáo email tự động**: Các ứng viên có độ tin cậy cao được gửi báo cáo ngay, còn những trường hợp cần xem xét thêm được nhắc nhở qua email.
- **Cải thiện chất lượng tuyển dụng**: Giảm thiểu rủi ro tuyển dụng sai người nhờ hệ thống đánh giá AI.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **API Key OpenAI** (hoặc mô hình LLM tương thích khác) để sử dụng GPT-4o.
2. **Google Sheets** với các tab đã chuẩn bị:
   - `Analysis Results` (lưu kết quả phân tích có độ tin cậy cao).
   - `Low Confidence Cases` (lưu trường hợp cần xem xét thêm).
3. **Tài khoản email** (SMTP hoặc Gmail OAuth) để gửi báo cáo tự động.
4. **Webhook URL** để nhận dữ liệu CV và thông tin công việc từ hệ thống tuyển dụng.
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/14442](https://n8n.io/workflows/14442) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/14442) và dán vào **Import Workflow** trong n8n Editor.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **A. Cấu hình Webhook (Nhận dữ liệu CV)**
- Node: **"Receive Resume & Job Data"**
  - Đảm bảo **path** là `recruitment-analysis` và **HTTP Method** là `POST`.
  - **Lưu ý**: Cần cung cấp URL webhook này cho hệ thống tuyển dụng của bạn để gửi dữ liệu CV và thông tin công việc.

#### **B. Cấu hình AI GPT-4o**
- **Tất cả các node sử dụng GPT-4o** (Matching Agent, Resume Parser, Skill Analysis, Experience Assessment, Cultural Fit) đều cần:
  - **Credentials**: Chọn `openAiApi` (đã cấu hình trước trong n8n).
  - **Model**: Đảm bảo chọn `gpt-4o` (hoặc mô hình tương thích khác nếu sử dụng API khác).
  - **API Key**: Đã được thêm trong **Credentials** của n8n (nếu chưa, tham khảo [hướng dẫn OpenAI](https://platform.openai.com/account/api-keys)).

#### **C. Cấu hình Google Sheets**
- Node: **"Store Analysis Results"** và **"Store Low Confidence Cases"**
  - **Credentials**: Thêm tài khoản Google Sheets vào n8n (nếu chưa, tham khảo [hướng dẫn kết nối](https://docs.n8n.io/integrations/built-in/nodes/n8n-nodes-base.googleSheets/)).
  - **Sheet ID**: Điền ID của các tab `Analysis Results` và `Low Confidence Cases` (có thể lấy từ liên kết Google Sheets).
  - **Range**: Điền tên tab tương ứng (ví dụ: `Analysis Results!A1`).

#### **D. Cấu hình Email**
- Node: **"Send High Confidence Report"** và **"Send Review Required Alert"**
  - **Credentials**: Chọn tài khoản email đã cấu hình (SMTP hoặc Gmail OAuth).
  - **From Email**: Điền địa chỉ email gửi.
  - **To Email**: Điền địa chỉ email nhận (có thể sử dụng biến `{{ $json["email"] }}` để tự động lấy từ dữ liệu CV).
  - **Subject & Body**: Sử dụng **template email** đã định sẵn, có thể tùy chỉnh theo nhu cầu.

#### **E. Cấu hình Logic Confidence Level**
- Node: **"Check Confidence Level"**
  - **Threshold**: Đặt ngưỡng độ tin cậy (ví dụ: `0.7` cho cao, `0.4` cho thấp). Các giá trị này quyết định ứng viên sẽ được gửi báo cáo tự động hay cần xem xét thêm.

---

### **3. Kích hoạt ⚡️**
1. **Test Run**: Chạy thử với một mẫu dữ liệu CV (JSON) để kiểm tra workflow.
   ```json
   {
     "resume": "Tôi có kinh nghiệm 5 năm trong lĩnh vực phát triển phần mềm...",
     "job_description": "Cần nhà phát triển Fullstack với kinh nghiệm Node.js và React...",
     "email": "candidate@example.com"
   }
   ```
2. **Active Workflow**: Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động khi nhận dữ liệu.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh mô hình AI**:
   - Thêm **domain-specific scoring rubrics** (bảng điểm chuyên ngành) vào các AI chuyên biệt (Skill Analysis, Experience Assessment) để phù hợp với ngành nghề cụ thể (ví dụ: kỹ thuật, marketing, quản lý).

2. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo kết quả phân tích ngay khi có ứng viên mới.

3. **Lưu log và báo cáo định kỳ**:
   - Sử dụng node **Google Drive** hoặc **Google Sheets** để lưu lịch sử phân tích và tạo báo cáo hàng tuần/month cho ban lãnh đạo.

4. **Tích hợp với ATS (Applicant Tracking System)**:
   - Nếu sử dụng hệ thống quản lý ứng viên (ví dụ: Greenhouse, Lever), có thể kết nối webhook để tự động cập nhật trạng thái ứng viên trong hệ thống.

5. **Optimize Performance**:
   - Nếu workflow chạy chậm, có thể **limit concurrency** của các node AI (ví dụ: `parallel: 2` cho các agent song song).

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quy trình tuyển dụng, giảm thiểu công việc thủ công và tăng chất lượng tuyển dụng. Với **AI GPT-4o**, **Google Sheets** và **email tự động**, bạn có thể:
✅ **Phân tích CV trong giây lát**.
✅ **Đánh giá ứng viên toàn diện** (kỹ năng, kinh nghiệm, phù hợp văn hóa).
✅ **Lưu trữ và báo cáo tự động**.
✅ **Tiết kiệm thời gian và chi phí**.

**Hãy áp dụng ngay và bắt đầu tự động hóa tuyển dụng của bạn!** 🚀

---
**Liên hệ với tác giả (Dr. Cheng Siong CHIN)** để tùy chỉnh workflow cho nhu cầu riêng:
📩 [Email](mailto:chengsiong.chin@gmail.com) | 🌐 [Website](https://www.chengsiong.chin)