---
title: "🔍 **Tự Động Hóa LinkedIn Job Hunter: Nhận Top 5 Vị Trí Tốt Nhất Mỗi Ngày qua Email (Không Cần Code!)**"
description: "Workflow tự động hóa 100% bằng n8n giúp các sếp tìm kiếm, lọc và nhận email hàng ngày với top 5 công việc phù hợp nhất trên LinkedIn, dựa trên CV của mình. Tiết kiệm thời gian lên tới 10 giờ/tuần và tăng cơ hội nhận được offer phù hợp."
slug: "tieu-dong-hoa-linkedin-job-hunter"
tags: [n8n, automation, no-code, ai, linkedin-job-search, google-gemini, email-automation]
keywords: [tự động hóa tìm việc linkedin, n8n workflow tìm việc, nhận email công việc phù hợp, ai chatbot tìm việc, google gemini n8n, tự động hóa marketing]
---

# 🚀 **Tự Động Hóa LinkedIn Job Hunter: Nhận Top 5 Vị Trí Tốt Nhất Mỗi Ngày qua Email**

### **💡 Bạn đã bao giờ mệt mỏi vì phải:**
- **Quét hàng trăm tin tuyển dụng** trên LinkedIn mỗi ngày?
- **Lọc thủ công** những công việc phù hợp với kinh nghiệm và kỹ năng của mình?
- **Đợi lâu** để nhận được offer từ nhà tuyển dụng?
- **Thất thời gian** vì phải copy-paste thông tin vào email?

**Workflow này giải quyết tất cả!** Dùng **n8n + AI Google Gemini**, nó sẽ:
✅ **Tự động tìm kiếm** công việc phù hợp với CV của bạn trên LinkedIn.
✅ **Lọc và xếp hạng** top 5 vị trí tốt nhất theo tiêu chí: lương, địa điểm, yêu cầu kỹ năng.
✅ **Gửi email tự động** với kết quả hàng ngày vào hộp thư của bạn.
✅ **Cập nhật liên tục** 24/7, không cần bạn làm gì!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần** so với cách tìm việc thủ công.
- **Nhận email hàng ngày** với top 5 công việc phù hợp nhất, **không bỏ lỡ cơ hội**.
- **Tối ưu hóa CV** bằng AI Google Gemini, giúp bạn **trông nổi bật hơn** trong ứng tuyển.
- **Hoạt động liên tục** 24/7, không phụ thuộc vào thời gian làm việc của bạn.
- **Tăng cơ hội nhận offer** với những công việc được lọc kỹ lưỡng.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản LinkedIn** (để scrape dữ liệu tuyển dụng).
✔ **Tài khoản Gmail** (để nhận email kết quả).
✔ **Tài khoản Google Drive** (để upload CV của bạn).
✔ **API Key Google Gemini** (miễn phí, đăng ký tại [Google AI Studio](https://makersuite.google.com/)).
✔ **Thời gian** để cấu hình workflow (khoảng 15-20 phút).

---
:::note[Lưu ý quan trọng]
- **LinkedIn có thể chặn scrape** nếu phát hiện hoạt động quá nhiều. Để tránh bị block, các sếp nên:
  - **Chỉ chạy workflow vào giờ rảnh** (ví dụ: 2-3 giờ sáng).
  - **Sử dụng proxy** (nếu cần, có thể thêm node `httpRequest` với proxy).
  - **Không scrape quá nhiều kết quả** trong một lần (đặt giới hạn ở 50-100 công việc/lần).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. **Tải file JSON** từ [n8n.io/workflows/3543](https://n8n.io/workflows/3543).
2. **Mở n8n Editor** → Nhấn **"Import"** → Chọn file JSON.
3. **Hoặc copy/paste** JSON vào ô **"Import Workflow"** và nhấn **"Import"**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **14 node**, các sếp cần chú ý cấu hình **các node quan trọng sau**:

##### **🔹 Node "Schedule Trigger" (Động cơ lịch)**
- **Cấu hình:**
  - **Frequency:** Chọn **"Daily"** (hoặc **"Every 24 hours"**).
  - **Time:** Đặt vào giờ rảnh (ví dụ: **2:00 AM**).
  - **Timezone:** Chọn **Việt Nam (Asia/Ho Chi Minh)**.

##### **🔹 Node "DownloadResume" (Tải CV từ Google Drive)**
- **Cấu hình:**
  - **Credentials:** Chọn tài khoản Google Drive đã kết nối.
  - **File ID:** Điền **ID file PDF của CV** (lấy từ liên kết Google Drive).
  - **Folder ID:** Nếu CV ở trong một thư mục, điền **ID thư mục**.
  - **File Name:** Đặt tên file (ví dụ: **"CV_Tien_Dat.pdf"**).

##### **🔹 Node "Extract Information from Resume PDF" (Trích xuất thông tin từ CV)**
- **Cấu hình:**
  - **File Type:** Chọn **"PDF"**.
  - **Extract:** Chọn **"All"** (hoặc chỉ trích xuất những thông tin cần thiết như **tên, kinh nghiệm, kỹ năng**).

##### **🔹 Node "ScrapeLinkedin" (Scrape LinkedIn)**
- **Cấu hình:**
  - **URL:** Điền **URL của trang LinkedIn** (ví dụ: `https://www.linkedin.com/jobs/search/?keywords=AI%20Engineer&location=Vietnam`).
  - **Headers:** Thêm header `User-Agent` để tránh bị block:
    ```json
    {
      "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"
    }
    ```
  - **Query:** Điền **từ khóa tìm việc** (ví dụ: `"AI Engineer"`, `"Data Scientist"`).
  - **Limit:** Đặt **số lượng kết quả scrape** (khuyến nghị **50-100** để tránh bị block).

##### **🔹 Node "AI Agent: Find Best-matched jobs" (AI Agent tìm công việc phù hợp)**
- **Cấu hình:**
  - **Prompt:** Sử dụng **prompt mặc định** (có thể tùy chỉnh để phù hợp với CV của bạn).
  - **Model:** Chọn **Google Gemini Pro** (hoặc **Gemini Flash** nếu muốn tiết kiệm chi phí).
  - **Input:** Điền **thông tin từ CV** (đã được trích xuất ở node trước).

##### **🔹 Node "Email the top job recommendations" (Gửi email kết quả)**
- **Cấu hình:**
  - **Credentials:** Chọn tài khoản Gmail đã kết nối.
  - **To:** Điền **email của bạn**.
  - **Subject:** Đặt tiêu đề email (ví dụ: **"Top 5 Job Matches for [Tên Bạn] - Ngày [Ngày Hiện Tại]"**).
  - **Body:** Sử dụng **template mặc định** (có thể chỉnh sửa để cá nhân hóa).

##### **🔹 Node "Google Gemini Chat Model" (AI Chatbot phân tích)**
- **Cấu hình:**
  - **Model:** Chọn **Google Gemini Pro**.
  - **Prompt:** Đặt câu hỏi để AI **phân tích và xếp hạng** công việc (ví dụ: `"Analyze these jobs and rank them from best to worst based on my resume"`).

---
#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **"Run Workflow"** để kiểm tra nếu tất cả node hoạt động bình thường.
   - Kiểm tra **email** đã nhận được kết quả chưa.
2. **Bật Active:**
   - Sau khi test thành công, nhấn **"Active"** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tối ưu hóa CV bằng AI:**
   - Sử dụng **Google Gemini** để **cải thiện CV** của bạn trước khi scrape.
   - **Prompt:** `"Rewrite my resume to match the job description of [Tên Công Việc] and make it more attractive to recruiters."`

2. **Gửi kết quả lên Slack/Telegram:**
   - Thêm node **Slack** hoặc **Telegram Bot** để nhận thông báo ngay khi có kết quả mới.

3. **Lưu log vào Google Sheets:**
   - Sử dụng node **Google Sheets** để **ghi lại lịch sử tìm việc**, giúp bạn theo dõi tiến độ.

4. **Tự động ứng tuyển:**
   - Nếu muốn, các sếp có thể thêm node **LinkedIn Apply** (nếu có API) để **ứng tuyển tự động** cho những công việc phù hợp.

5. **Chỉnh sửa từ khóa tìm việc:**
   - Thay đổi **từ khóa scrape** theo **ngành nghề** hoặc **kỹ năng** mới bạn muốn học.

---

### 📌 **Kết luận**
Workflow **Automated LinkedIn Job Hunter** là **giải pháp hoàn hảo** cho những người:
✔ **Bận rộn** và không có thời gian tìm việc thủ công.
✔ **Muốn tối ưu hóa CV** bằng AI.
✔ **Không muốn bỏ lỡ cơ hội** vì quên check LinkedIn.

**Hãy áp dụng ngay!** Tiết kiệm thời gian, tăng cơ hội nhận offer và **tự động hóa cuộc sống** của mình.

---
**🚀 Bắt đầu ngay:**
1. **Cài n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Nhận email hàng ngày** với top 5 công việc phù hợp nhất!

**Nếu có vấn đề, hãy để lại comment bên dưới!** 👇