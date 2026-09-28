---
title: "🚀 Tự Động Hóa Tìm Việc Làm Mới Nhất với Tavily + AI (Không Cần Code!)"
description: "Workflow tự động hóa tìm kiếm và tổng hợp tin tuyển dụng mới nhất từ web, xử lý bằng AI, gửi email tổng hợp hàng ngày cho các sếp. Giúp tiết kiệm 10+ giờ/tuần tìm việc thủ công."
slug: "tieu-dong-hoa-tim-viec-lam-voi-tavily"
tags: [n8n, automation, ai-summarization, job-hunting, tavily, openai]
keywords: [tự động hóa tìm việc, Tavily n8n, AI tổng hợp tin tuyển dụng, email tổng hợp việc làm, tự động hóa không code]
---

# 🚀 **Tự Động Hóa Tìm Việc Làm Mới Nhất với Tavily + AI (Không Cần Code!)**

### **💡 Nỗi Đau Của Các Sếp Khi Tìm Việc Làm Thủ Công**
- **Thời gian mất công**: Phải tra cứu hàng chục trang web tuyển dụng mỗi ngày, sao chép tin tuyển dụng vào Excel, và phân loại thông tin.
- **Thông tin rải rác**: Các tin tuyển dụng mới thường bị "chôn vùi" trong hàng trăm kết quả, khó theo dõi.
- **Không cá nhân hóa**: Không thể tự động lọc theo ngành nghề, mức lương mong muốn, hoặc địa điểm ưu tiên.
- **Rủi ro bỏ lỡ cơ hội**: Nhiều tin tuyển dụng mới chỉ tồn tại trong vòng vài giờ, nhưng các sếp không thể theo dõi 24/7.

**Workflow này giải quyết tất cả!** Sử dụng **Tavily** để tra cứu tin tuyển dụng mới nhất trên web, **AI (GPT-4)** để tổng hợp và xử lý thông tin, và **n8n** để tự động gửi email tổng hợp hàng ngày cho các sếp. **Không cần viết một dòng code nào!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần**: Không cần tra cứu thủ công trên các trang web tuyển dụng.
- **Tin tuyển dụng mới nhất**: Tra cứu từ hàng ngàn nguồn trên web (LinkedIn, Indeed, Glassdoor, và các trang nhỏ).
- **Tổng hợp tự động**: AI xử lý và định dạng tin tuyển dụng thành bảng thông tin rõ ràng (Tiêu đề, Mô tả, Yêu cầu, Công ty, Địa điểm).
- **Gửi email hàng ngày**: Nhận email tổng hợp tất cả tin tuyển dụng mới nhất vào email cá nhân.
- **Lọc theo yêu cầu**: Chỉ lấy tin tuyển dụng phù hợp với ngành nghề, mức lương, hoặc địa điểm mong muốn.
- **Hoạt động 24/7**: Workflow chạy tự động theo lịch trình (ngày hoặc tuần).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Tavily API**:
   - Đăng ký miễn phí tại [Tavily](https://tavily.com/) và lấy **API Key**.
   - Cài đặt **n8n Tavily Node** từ [n8n Tavily GitHub](https://github.com/tavily/n8n-nodes-tavily).
2. **Tài khoản OpenAI API**:
   - Đăng ký tại [OpenAI](https://platform.openai.com/) và lấy **API Key**.
   - Chọn model **gpt-4.1-mini** (miễn phí).
3. **Tài khoản Gmail**:
   - Các sếp cần một tài khoản Gmail để nhận email tổng hợp.
   - Cấu hình **OAuth 2.0** cho Gmail trong n8n (đăng nhập và cấp quyền).
4. **n8n Self-hosted**:
   - Workflow này **không chạy được trên n8n Cloud** do sử dụng Tavily API và Gmail OAuth.
   - Cài đặt n8n trên VPS (hướng dẫn [tại đây](https://docs.n8n.io/hosting/installation/)).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n Community](https://n8n.io/workflows/8616) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** (trang chủ của workflow self-hosted).
- Nhấn **Import** và dán JSON vào hoặc tải file JSON đã tải xuống.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này gồm **10 node**, nhưng các node quan trọng nhất cần cấu hình kỹ như sau:

##### **A. Cấu Hình Tavily Search**
- **Node**: *Search in Tavily*
  - **Query**: Điền **keyword tìm việc** (ví dụ: *"Chuyên viên Marketing Digital Vietnam 2024"*).
  - **Max Results**: Đặt số lượng kết quả (ví dụ: 20).
  - **Time Range**: Chọn *"Last 24 hours"* để lấy tin mới nhất.
  - **Trusted Domains**: Điền các trang web tin cậy (ví dụ: `linkedin.com`, `indeed.com`, `glassdoor.com`).
  - **API Key**: Điền **Tavily API Key** từ bước chuẩn bị.

##### **B. Cấu Hình OpenAI AI Agent**
- **Node**: *OpenAI Chat Model* và *Message a model*
  - **Model**: Chọn **gpt-4.1-mini** (miễn phí).
  - **API Key**: Điền **OpenAI API Key** từ bước chuẩn bị.
  - **Prompt**: Workflow đã cấu hình sẵn, nhưng các sếp có thể chỉnh sửa để yêu cầu AI:
    - Trích xuất **Tiêu đề, Mô tả, Yêu cầu, Công ty, Địa điểm**.
    - Định dạng tin tuyển dụng thành **JSON** hoặc **Markdown**.

##### **C. Cấu Hình Gmail**
- **Node**: *Send a message*
  - **Credentials**: Chọn **gmailOAuth2** (đã cấu hình trong bước chuẩn bị).
  - **To**: Điền email cá nhân của các sếp.
  - **Subject**: Đặt tiêu đề email (ví dụ: *"Tin tuyển dụng mới nhất - Ngày [DATE]"*).
  - **Body**: Workflow tự động điền nội dung từ AI.

##### **D. Cấu Hình Lịch Trình (Schedule Trigger)**
- **Node**: *Schedule Trigger*
  - Chọn **Daily** hoặc **Weekly**.
  - Thời gian chạy: Ví dụ, **8h sáng** (thời gian Việt Nam).

##### **E. Cấu Hình Memory (Lưu Trạng Thái)**
- **Node**: *Simple Memory*
  - Workflow sử dụng **Buffer Window** để lưu tin tuyển dụng cũ và so sánh với tin mới.
  - **Không cần chỉnh sửa**, nhưng các sếp có thể mở rộng để lưu thêm thông tin.

##### **F. Cấu Hình Aggregate (Tổng Hợp)**
- **Node**: *Aggregate*
  - Workflow tự động **ghép tất cả tin tuyển dụng** thành một mảng JSON duy nhất trước khi gửi email.

##### **G. Cấu Hình Code (Nếu Cần Chỉnh Sửa)**
- **Node**: *Code*
  - Nếu các sếp muốn **chỉnh sửa logic xử lý tin tuyển dụng**, mở node này và chỉnh sửa JavaScript.
  - Ví dụ: Lọc tin theo **ngành nghề cụ thể** hoặc **mức lương**.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và kiểm tra email đã nhận được không.
   - Nếu có lỗi, kiểm tra **log** trong tab **Execution**.
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Status** từ **Inactive** sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự Động Lọc Tin Tuyển Dụng**
   - Sử dụng **node Code** để thêm logic lọc tin theo:
     - **Ngành nghề** (ví dụ: chỉ lấy tin "Phần mềm", "Marketing").
     - **Mức lương** (ví dụ: > 20 triệu/tháng).
     - **Địa điểm** (ví dụ: chỉ Hà Nội hoặc TP.HCM).

2. **Gửi Email Định Kỳ Theo Ngày**
   - Thay vì gửi hàng ngày, các sếp có thể:
     - **Gửi vào thứ 2 và thứ 4** (ngày có nhiều tin tuyển dụng mới).
     - **Gửi vào buổi sáng** (8h-9h) để các sếp có thời gian xem.

3. **Lưu Log Tín Tuyển Dụng**
   - Sử dụng **n8n Database** hoặc **Google Sheets** để lưu tất cả tin tuyển dụng.
   - Hướng dẫn:
     - Thêm **node Google Sheets** sau *Aggregate*.
     - Lưu tin vào sheet mới với cột: **Tiêu đề, Mô tả, Yêu cầu, Công ty, Địa điểm, Ngày tìm thấy**.

4. **Kết Hợp với Slack/Telegram**
   - Thay vì email, các sếp có thể:
     - **Gửi tin tuyển dụng lên Slack** (sử dụng node **Slack Webhook**).
     - **Gửi tin lên Telegram** (sử dụng node **Telegram Bot**).

5. **Tự Động Xóa Tin Trùng Lặp**
   - Sử dụng **node Code** để so sánh tin tuyển dụng mới với tin cũ (đã lưu trong Memory).
   - Chỉ gửi tin **mới nhất** hoặc **cập nhật mới**.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa tìm việc làm** mà không cần viết code. Với **Tavily** tra cứu tin mới nhất, **AI** xử lý và định dạng, và **n8n** gửi email hàng ngày, các sếp sẽ **tiết kiệm thời gian, tránh bỏ lỡ cơ hội**, và **tìm việc hiệu quả hơn**.

**Hành động ngay!**
1. **Chuẩn bị tài khoản Tavily, OpenAI, và Gmail**.
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và bắt đầu nhận email tin tuyển dụng hàng ngày!

**🚀 Cảm ơn các sếp đã thử nghiệm!** Nếu có vấn đề, hãy để lại comment bên dưới hoặc liên hệ với cộng đồng n8n tại [n8n Community](https://community.n8n.io/).

---