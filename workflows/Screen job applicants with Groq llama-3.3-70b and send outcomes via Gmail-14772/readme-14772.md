---
title: "🤖 **Tự Động Học Viện & Lọc Ứng Viên Với Groq LLM + Gmail (N8n) – Giảm 90% Công Việc HR!**"
description: "Workflow tự động hóa toàn bộ quy trình tuyển dụng: nhận ứng viên qua webhook, đánh giá AI với Groq llama-3.3-70b, phân loại thành shortlist/waitlist/reject, gửi email tự động và thông báo Slack – **không cần viết code!**"
slug: "tu-dong-ho-va-loc-ung-vien-voi-groq-gmail-n8n"
tags: [n8n, automation, hr, ai-summarization, groq-llm, google-sheets, gmail, slack]
keywords: [tự động hóa tuyển dụng n8n, đánh giá ứng viên bằng AI, groq llama-3.3-70b, lọc ứng viên tự động, gửi email tự động từ n8n, workflow tuyển dụng no-code]
---

# **🚀 Tự Động Học Viện & Lọc Ứng Viên Với Groq LLM + Gmail (N8n) – Giải Pháp HR 24/7**

### **Nỗi Đau Của Các Sếp Trong Quy Trình Tuyển Dụng**
- **"Tôi phải đọc hàng trăm hồ sơ ứng viên mỗi ngày, mất thời gian và dễ bị mất tập trung."**
- **"Phân loại ứng viên theo tiêu chí khách quan là một thách thức – ai cũng có ưu điểm và nhược điểm."**
- **"Gửi email phản hồi cho từng ứng viên thủ công làm tôi mệt mỏi và dễ quên."**
- **"Không biết cách tối ưu hóa quy trình tuyển dụng để tiết kiệm chi phí và thời gian."**

**Workflow này giải quyết tất cả!** Với **AI Groq llama-3.3-70b**, n8n sẽ:
✅ **Nhận ứng viên tự động** qua webhook từ form ứng tuyển.
✅ **Đánh giá ứng viên** theo tiêu chí kỹ năng, kinh nghiệm, và phù hợp với vị trí.
✅ **Phân loại tự động** thành **Shortlist (top)**, **Waitlist (cần xem xét thêm)**, và **Reject (không phù hợp)**.
✅ **Gửi email phản hồi** (congratulations, waitlist, hoặc rejection) **tự động** qua Gmail.
✅ **Thông báo Slack** cho đội HR khi có ứng viên top.
✅ **Lưu tất cả dữ liệu** vào Google Sheets để theo dõi và phân tích.

---
## **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 90% thời gian** trong việc đọc và phân loại hồ sơ.
- **Đánh giá ứng viên khách quan** dựa trên AI Groq (llama-3.3-70b) – không bị chủ quan.
- **Gửi email phản hồi tự động** trong giây lát, không quên ứng viên.
- **Cập nhật Slack** khi có ứng viên top, giúp đội HR phản hồi nhanh chóng.
- **Lưu trữ dữ liệu** trong Google Sheets, dễ dàng theo dõi và báo cáo.
- **Hoạt động 24/7** – không cần người thủ công can thiệp.
:::

---
## **🔧 Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI LẮP ĐỘNG**]
Để workflow này hoạt động, các sếp cần chuẩn bị:
✔ **Tài khoản n8n Self-hosted** (khuyến nghị cài trên VPS để hoạt động 24/7).
✔ **API Key Groq** (để sử dụng Groq llama-3.3-70b).
✔ **Google Sheets** với:
   - **Bảng "Shortlist"** (để lưu ứng viên top).
   - **Bảng "Waitlist"** (để lưu ứng viên cần xem xét thêm).
   - **Bảng "Rejected"** (để lưu ứng viên không phù hợp).
✔ **Tài khoản Gmail** (để gửi email phản hồi tự động).
✔ **Slack API Token** (để thông báo đội HR khi có ứng viên top).
✔ **Webhook URL** từ hệ thống ATS (Applicant Tracking System) hoặc form ứng tuyển của bạn.
:::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/14772](https://n8n.io/workflows/14772) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/14772) và paste vào **Import Workflow** trong n8n.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **14 node**, mỗi node đều cần cấu hình chính xác. Dưới đây là hướng dẫn chi tiết:

#### **🔹 Node 1: Receive Application via Webhook**
- **Cấu hình:**
  - **Path:** `job-application` (không đổi).
  - **HTTP Method:** `POST`.
  - **Credentials:** Chọn **Webhook** (nếu chưa có, tạo mới).
  - **Lưu ý:** Cần **công khai URL webhook** này cho hệ thống ATS/form ứng tuyển của bạn.

#### **🔹 Node 2: Structure Job and Candidate Data**
- **Cấu hình:**
  - **Set JSON Path:** Đảm bảo dữ liệu ứng viên và vị trí được cấu trúc rõ ràng (ví dụ: `$.job`, `$.candidate`).
  - **Thêm timestamp:** Sử dụng `{{ $now }}` để thêm thời gian nhận ứng viên.

#### **🔹 Node 3 & 4: Check for Duplicate Application (Google Sheets + IF)**
- **Cấu hình Google Sheets:**
  - **Credentials:** Thêm OAuth2 của Google Sheets.
  - **Sheet ID & Range:** Điền ID bảng và tên sheet (ví dụ: `!A2:A` để kiểm tra ứng viên đã tồn tại).
  - **Lưu ý:** Nếu ứng viên đã tồn tại, **IF node sẽ dừng workflow** để tránh xử lý trùng lặp.

#### **🔹 Node 5: Score Candidate with AI (Groq LLM)**
- **Cấu hình Groq:**
  - **Credentials:** Thêm API Key Groq.
  - **Model:** Chọn `llama-3.3-70b-versatile`.
  - **Prompt:** Sử dụng template mặc định (có thể tùy chỉnh theo yêu cầu của công ty).
  - **Lưu ý:** Đảm bảo **dữ liệu đầu vào** (job description + candidate profile) được truyền đúng vào node này.

#### **🔹 Node 6: Parse Score, Reason, Strengths and Gaps (Code)**
- **Cấu hình JavaScript:**
  - **Mã code mặc định** đã phân tích output của Groq và trích xuất:
    - `score` (số điểm từ 0-100).
    - `reason` (lý do đánh giá).
    - `strengths` (điểm mạnh).
    - `gaps` (nhược điểm).
    - `band` (Strong/Moderate/Weak).
  - **Lưu ý:** Nếu cần thay đổi logic, chỉnh sửa mã ở đây.

#### **🔹 Node 7: Route by Score Band (Switch)**
- **Cấu hình:**
  - **Score Band:**
    - **Strong:** `>= 80` → Shortlist.
    - **Moderate:** `60-79` → Waitlist.
    - **Weak:** `< 60` → Reject.
  - **Lưu ý:** Có thể điều chỉnh ngưỡng điểm theo tiêu chí tuyển dụng của công ty.

#### **🔹 Node 8-13: Log & Send Emails (Google Sheets + Gmail)**
- **Cấu hình Google Sheets:**
  - **Operation:** `append` (thêm dữ liệu mới vào sheet).
  - **Range:** Điền tên sheet tương ứng (`Shortlist`, `Waitlist`, `Rejected`).
- **Cấu hình Gmail:**
  - **Credentials:** Thêm OAuth2 của Gmail.
  - **Email Template:** Tùy chỉnh nội dung email (congratulations, waitlist, rejection).
  - **Lưu ý:** Đảm bảo **địa chỉ email nhận** là chính xác.

#### **🔹 Node 14: Notify HR Team on Slack**
- **Cấu hình Slack:**
  - **Credentials:** Thêm API Token Slack.
  - **Channel ID:** Chọn channel HR (ví dụ: `#hr-notifications`).
  - **Message Template:** Tùy chỉnh thông báo (ví dụ: `🚀 New shortlist candidate: {{ $node["Structure Job and Candidate Data"].json["name"] }}`).

---
### **3. Kích Hoạt ⚡️**
- **Test Run:** Chạy thử với **dữ liệu mẫu** (ví dụ: một ứng viên giả).
- **Kiểm tra:**
  - AI có đánh giá đúng không?
  - Email có gửi được không?
  - Slack có thông báo không?
- **Bật Active:** Sau khi kiểm tra thành công, **bật workflow**.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[**CÁCH TIẾP CẬN THÊM**]
1. **Kết hợp với Zoom/Calendly:**
   - Sau khi shortlist, tự động **đặt lịch phỏng vấn** qua Zoom/Calendly.
2. **Lưu Log Dữ Liệu:**
   - Thêm node **Google Drive** hoặc **S3** để lưu toàn bộ lịch sử ứng viên.
3. **Báo Cáo Định Kỳ:**
   - Sử dụng **Google Sheets + Apps Script** để tự động tạo báo cáo hàng tuần/month.
4. **Tùy Chỉnh AI:**
   - Cập nhật **prompt** của Groq để phù hợp với tiêu chí tuyển dụng mới.
5. **Thông Báo Telegram:**
   - Thay Slack bằng **Telegram Bot** để nhận thông báo nhanh hơn.
:::

---
## **📌 Kết Luận**
Workflow này **giải phóng đội HR khỏi công việc thủ công**, giúp **tuyển dụng nhanh chóng, khách quan và tự động hóa hoàn toàn**. Với **Groq llama-3.3-70b**, ứng viên sẽ được đánh giá theo tiêu chí **cụ thể và khoa học**, trong khi **email phản hồi tự động** giúp tránh bỏ qua ứng viên.

**🚀 Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả tuyển dụng!**

---
### **🔗 Tài Liệu Tham Khảo**
- [Workflow gốc trên n8n.io](https://n8n.io/workflows/14772)
- [Hướng dẫn Groq API](https://console.groq.com/)
- [Cài đặt n8n Self-hosted](https://docs.n8n.io/hosting/installation/)

---
### **💡 Cần Hỗ Trợ?**
Nếu gặp vấn đề khi setup, **hãy liên hệ với iTechNotion** (tác giả của workflow) qua:
📧 [avkash@itechnotion.com](mailto:avkash@itechnotion.com)
🌐 [itechnotion.com](https://itechnotion.com)