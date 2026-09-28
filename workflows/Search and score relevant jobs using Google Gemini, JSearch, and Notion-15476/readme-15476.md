---
title: "🔍 Tự Động Hóa Tìm Và Đánh Giá Công Việc Phù Hợp Nhờ AI (Google Gemini + Notion) – Không Cần Code"
description: "Workflow tự động hóa tìm kiếm và đánh giá công việc phù hợp với hồ sơ ứng viên bằng AI Gemini, JSearch API và lưu kết quả vào Notion. Giúp các sếp tiết kiệm thời gian lên tới 80% trong quá trình tuyển dụng và phát triển nghề nghiệp."
slug: "tu-dong-hoa-tim-va-danh-gia-cong-viec-voi-ai-gemini-notion"
tags: [n8n, automation, ai-gemini, notion-integration, job-search, no-code]
keywords: [tự động hóa tìm việc bằng AI, n8n workflow tìm công việc, đánh giá phù hợp hồ sơ ứng viên, tự động hóa tuyển dụng, google gemini n8n, lưu kết quả vào notion]
---

# 🚀 **Tự Động Hóa Tìm Và Đánh Giá Công Việc Phù Hợp Nhờ AI – Không Cần Code**

### **Giải pháp cho ai?**
Các sếp, nhà tuyển dụng, hoặc ứng viên đang mệt mỏi với quá trình tìm kiếm công việc thủ công:
- **Tốn thời gian** phải tra cứu hàng trăm tin tuyển dụng trên nhiều trang web.
- **Khó đánh giá** xem công việc nào phù hợp với kỹ năng và kinh nghiệm của mình.
- **Lặp lại công việc** như nhập liệu vào Notion, đánh giá lại hồ sơ ứng viên.
- **Không cập nhật kịp thời** với những tin tuyển dụng mới nhất.

**Workflow này tự động hóa toàn bộ quá trình** bằng AI Gemini, API JSearch và Notion – giúp bạn **tìm ra công việc phù hợp chỉ trong vài giây** và lưu kết quả một cách chuyên nghiệp.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động tìm kiếm và đánh giá hàng trăm công việc trong vài phút thay vì nhiều giờ.
- **Đánh giá chính xác**: AI Gemini phân tích hồ sơ ứng viên và so sánh với yêu cầu công việc, cho ra **điểm phù hợp** và **tóm tắt chi tiết**.
- **Lưu trữ thông minh**: Kết quả được tự động lưu vào Notion với **cấu trúc chuyên nghiệp**, bao gồm:
  - Tiêu đề công việc, công ty, mô tả, loại việc làm (full-time/part-time/remote).
  - Điểm phù hợp, kỹ năng khớp, lương, thời gian ứng tuyển.
  - Trạng thái (chưa ứng tuyển/đã ứng tuyển).
- **Không trùng lặp**: Workflow tự động bỏ qua những công việc đã ứng tuyển trước đó.
- **Cập nhật liên tục**: Tự động lọc ra những tin tuyển dụng mới nhất.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Notion**:
   - Một **bảng dữ liệu "Job Database"** với các cột sau (đảm bảo đã tạo trước):
     - **Job ID** (ID duy nhất)
     - **Job Title** (Tiêu đề công việc)
     - **Company** (Công ty)
     - **Description** (Mô tả công việc)
     - **Employment Type** (Full-Time/Part-Time/N/A)
     - **Is Remote** (Yes/No/Hybrid)
     - **Language** (Nếu cần)
     - **Job Location** (Địa điểm)
     - **Salary** (Lương)
     - **Joining Timeline** (Thời gian bắt đầu)
     - **Relevance Score** (Điểm phù hợp)
     - **Skill Match** (Kỹ năng khớp)
     - **Summary** (Tóm tắt)
     - **Status** (Not Applied/Applied)
     - **URL** (Link tuyển dụng)
     - **Apply Options** (Lựa chọn ứng tuyển)
     - **Posted On** (Ngày đăng)
   - **Lấy Database ID**: Mở bảng Notion → URL sẽ có dạng `https://www.notion.so/.../.../...` → **Database ID** là phần sau `/.../` (ví dụ: `123456789abcdef`).

2. **API Key JSearch (RapidAPI)**:
   - Đăng ký tại [JSearch API](https://rapidapi.com/letscrape-6zs-6zs-default/api/jsearch) và lấy **API Key**.
   - **Lưu ý**: API này có giới hạn request, nên các sếp nên **cài đặt VPS** để workflow chạy 24/7 mà không bị giới hạn.

3. **Google Gemini API Key**:
   - Tạo tài khoản tại [Google AI Studio](https://makersuite.google.com/) và sinh **API Key**.
   - Chọn **Gemini Pro** (mô hình AI mạnh nhất hiện nay).

4. **Hồ sơ ứng viên (PDF)**:
   - Chuẩn bị **file PDF** của hồ sơ ứng viên (có thể là bản scan hoặc file Word chuyển đổi).
   - **Lưu file tại đường dẫn dễ truy cập** trên máy chủ VPS (ví dụ: `/home/user/resume.pdf`).

5. **n8n Self-hosted**:
   - Workflow này **không chạy được trên n8n Cloud** do giới hạn API và tài nguyên.
   - **👉 Cài đặt n8n trên VPS** để đảm bảo hoạt động 24/7:
     - [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
     - [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15476](https://n8n.io/workflows/15476) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import** → Dán JSON và nhấn **Import Workflow**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **15 node**, các sếp cần cấu hình **các node quan trọng** sau:

#### **A. Cấu hình Notion**
:::info[CẤU HÌNH NOTION]
- **Node**: `Add Record to Notion Database`, `Fetch Notion Database Info`, `Retrieve Existing Job Listings`.
- **Hành động**:
  1. Mở **Notion Credentials** trong n8n:
     - Tạo **new credential** với tên `notionApi`.
     - Điền **API Key** từ Notion (tạo tại [Notion API](https://www.notion.so/my-integrations)).
  2. Điền **Database ID** vào các node liên quan:
     - Mở node `Add Record to Notion Database` → Chọn `notionApi` → Điền **Database ID** (lấy từ bước chuẩn bị).
     - Lặp lại cho node `Fetch Notion Database Info` và `Retrieve Existing Job Listings`.
  3. **Kiểm tra cấu trúc bảng**: Đảm bảo các cột trong Notion khớp với yêu cầu trong workflow.
:::

#### **B. Cấu hình Google Gemini**
:::info[CẤU HÌNH GEMINI]
- **Node**: `Evaluate Job Relevance`, `Extract Current Job Title`.
- **Hành động**:
  1. Tạo **new credential** với tên `googlePalmApi`.
  2. Điền **API Key** từ Google AI Studio.
  3. **Không cần chỉnh sửa prompt** (workflow đã tối ưu sẵn), nhưng các sếp có thể **cập nhật yêu cầu đánh giá** nếu cần:
     - Ví dụ: Thêm yêu cầu về **ngôn ngữ** hoặc **kỹ năng cụ thể**.
:::

#### **C. Cấu hình JSearch API (RapidAPI)**
:::info[CẤU HÌNH RAPIDAPI]
- **Node**: `Search for Jobs via RapidAPI`.
- **Hành động**:
  1. Mở node → Chọn **Headers** → Điền:
     ```
     x-rapidapi-key: YOUR_API_KEY_HERE
     x-rapidapi-host: jsearch.p.rapidapi.com
     ```
  2. **Chỉnh sửa query tìm kiếm** (nếu cần):
     - Mặc định, workflow tìm kiếm theo **tên công việc** trong hồ sơ.
     - Các sếp có thể **cập nhật từ khóa** trong node `Search for Jobs via RapidAPI` để phù hợp với ngành nghề.
:::

#### **D. Cấu hình File Resume**
:::info[CẤU HÌNH FILE HO SƠ]
- **Node**: `Read Candidate Resume`.
- **Hành động**:
  1. Mở node → Chọn **File(s) Selector** → Điền **đường dẫn đầy đủ** đến file PDF:
     ```
     /home/user/resume.pdf
     ```
  2. **Lưu file trên VPS** để workflow có thể đọc được (không dùng đường dẫn local máy tính).
:::

#### **E. Cấu hình Rate Limit (Giới hạn API)**
:::info[GIỚI HẠN API]
- **Node**: `Rate Limit API Requests` (node `wait`).
- **Hành động**:
  - Workflow tự động **chờ 2 giây** giữa mỗi request API để tránh bị chặn.
  - Nếu API có giới hạn thấp, các sếp có thể **tăng thời gian chờ** trong node này (ví dụ: 5 giây).
:::

---
### **3. Kích hoạt ⚡️**
1. **Test run với dữ liệu mẫu**:
   - Nhấn **Run Workflow** và chọn **Manual Trigger**.
   - Kiểm tra **log** để đảm bảo không có lỗi.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển **Active** sang `ON`.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC TỐT NHẤT]
1. **Tự động gửi báo cáo hàng tuần**:
   - Sử dụng **n8n + Slack/Telegram** để gửi **tóm tắt công việc mới** và **điểm phù hợp cao nhất** vào cuối tuần.
   - **Cách làm**:
     - Thêm node **Slack/Telegram** sau node `Add Record to Notion Database`.
     - Sử dụng **n8n Schedule Node** để chạy workflow định kỳ (ví dụ: Chủ Nhật 8h sáng).

2. **Lưu log hoạt động**:
   - Thêm node **Google Sheets** hoặc **Notion Log** để ghi lại **lịch sử tìm kiếm** và **lỗi nếu có**.
   - **Ưu điểm**: Dễ dàng **theo dõi hiệu suất** và **sửa lỗi** sau này.

3. **Tích hợp với LinkedIn/Indeed**:
   - Nếu API JSearch không đủ, các sếp có thể **thêm node HTTP Request** để gọi API của **LinkedIn/Indeed** (nếu có API công khai).
   - **Lưu ý**: Nhiều API này yêu cầu **đăng ký và xác minh**, nên cần nghiên cứu kỹ.

4. **Cập nhật hồ sơ tự động**:
   - Nếu hồ sơ ứng viên thay đổi, **cập nhật file PDF** và chạy workflow lại.
   - Hoặc, **tích hợp với Google Drive/Dropbox** để tự động tải file mới nhất.

5. **Đánh giá lại công việc đã ứng tuyển**:
   - Thêm node **filter** để **bỏ qua công việc đã ứng tuyển** (trạng thái `Applied`).
   - **Cách làm**:
     - Sử dụng node `Filter` sau `Retrieve Existing Job Listings` với điều kiện:
       ```json
       { "Status": "Not Applied" }
       ```
:::

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa tìm kiếm và đánh giá công việc** một cách **chuyên nghiệp, tiết kiệm thời gian và không cần code**.

### **Bước tiếp theo**
1. **Cài đặt n8n trên VPS** (nếu chưa có).
2. **Chuẩn bị Notion Database** và các API Key.
3. **Import workflow** và **cấu hình** theo hướng dẫn.
4. **Kích hoạt** và **theo dõi kết quả**!

**🚀 Hãy thử ngay và tiết kiệm thời gian cho việc tìm kiếm công việc hiệu quả nhất!**

---
### **🔗 Tài liệu tham khảo**
- [n8n Workflow gốc](https://n8n.io/workflows/15476)
- [Google Gemini API](https://makersuite.google.com/)
- [JSearch API (RapidAPI)](https://rapidapi.com/letscrape-6zs-6zs-default/api/jsearch)
- [Notion API](https://www.notion.so/my-integrations)