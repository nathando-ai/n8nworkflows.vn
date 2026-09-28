---
title: "🤖 Tự Động Xếp Hạng Ứng Viên Với Gemini AI: Từ Jotform → Hệ Thống Tuyển Dụng Notion (N8n)"
description: "Workflow tự động hóa tuyển dụng 100% không code, sử dụng Gemini AI để phân tích CV, đánh giá phù hợp với vị trí và tự động cập nhật vào Notion. Giúp doanh nghiệp tiết kiệm 80% thời gian sàng lọc ứng viên thủ công."
slug: "tuyen-dung-ai-gemini-jotform-notion"
tags: [n8n, automation, hr, ai-summarization, gemini-ai, jotform, notion, self-hosted]
keywords: [tự động hóa tuyển dụng n8n, gemini ai phân tích cv, jotform notion workflow, sàng lọc ứng viên tự động, ai trong tuyển dụng]
---

# 🚀 **Tự Động Xếp Hạng Ứng Viên Với Gemini AI: Từ Jotform → Hệ Thống Tuyển Dụng Notion**

### **Giải pháp nào giúp các sếp:**
- **Tiết kiệm 80% thời gian sàng lọc ứng viên** bằng AI Gemini phân tích CV, cover letter và phù hợp với vị trí.
- **Cập nhật tự động vào Notion** với thông tin ứng viên, điểm số phù hợp và đánh giá chi tiết.
- **Gửi thông báo Slack/Gmail** cho team tuyển dụng ngay khi có ứng viên phù hợp (điểm > 40).
- **Loại bỏ ứng viên không phù hợp** tự động, không cần can thiệp thủ công.

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: AI tự động phân tích CV và cover letter trong vài giây thay vì mất giờ của team HR.
✅ **Đánh giá khách quan**: Điểm phù hợp (fit score) từ AI giúp team tuyển dụng quyết định nhanh chóng.
✅ **Hệ thống hóa dữ liệu**: Tất cả ứng viên được lưu vào Notion với thông tin chi tiết, dễ theo dõi và báo cáo.
✅ **Hoạt động 24/7**: Workflow chạy tự động ngay khi ứng viên nộp đơn, không cần can thiệp thủ công.
✅ **Cá nhân hóa thông báo**: Gửi email xác nhận và thông báo Slack cho team khi có ứng viên tiềm năng.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Jotform** (đăng ký [tại đây](https://www.jotform.com/?partner=atakhalighi)) với **form tuyển dụng** có cấu trúc như sau:
   - **Full Name** (tên ứng viên)
   - **Email** (để gửi email xác nhận)
   - **Phone Number** (tùy chọn)
   - **File Upload** (chỉ chấp nhận **PDF**)
   - **Dropdown** (vị trí ứng tuyển) → **Phải trùng khớp với tên trang trong Notion Open Positions**
   - **Long Text** (cover letter) → **Bắt buộc**, nội dung sẽ được AI phân tích.

2. **Tài khoản Notion** với **database "Open Positions"** (danh sách vị trí tuyển dụng).
3. **API Keys & Credentials**:
   - **Jotform API Key** (để tải CV từ URL)
   - **Google Gemini API** (để phân tích AI)
   - **Gmail OAuth2** (gửi email xác nhận)
   - **Slack API** (thông báo team tuyển dụng)
   - **Notion API** (cập nhật dữ liệu ứng viên)

4. **n8n Self-hosted** (để workflow chạy 24/7 ổn định).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/9955) hoặc copy toàn bộ JSON từ trang này.
- Vào **n8n Editor** → Nhấn **Import Workflow** → Dán JSON và nhấn **Import**.

### **2. Các lưu ý BẮT BUỘC phải chỉnh 📌**
Workflow này **không hoạt động được** nếu không cấu hình chính xác các node sau:

#### **🔹 Node 1: JotForm Trigger**
- **Yêu cầu form Jotform** phải có **các trường bắt buộc** như mô tả ở trên.
- **Cách lấy Question IDs**:
  1. **Nộp form test** (sử dụng email cá nhân).
  2. **Xem output** của node này → Lấy **Question IDs** (ví dụ: `q3_fullName`, `q7_positionApplying`).
  3. **Cập nhật vào các node downstream**:
     - `Download Resume PDF` → Thay đổi URL file upload (ví dụ: từ `uploadYour` thành `uploadYour_QID`).
     - `Find Job in Notion` → Thay đổi `q7_positionApplying` thành `QID` của dropdown vị trí.
     - `AI Candidate Analysis` → Thay đổi `q8_typeA8` thành `QID` của cover letter.

#### **🔹 Node 2: Google Gemini Chat Model**
- **Kết nối Google AI credentials**:
  1. Vào **Credentials** → Thêm **Google Palm API**.
  2. **Cập nhật Prompt**:
     - Tìm phần `...json.q8_typeA8` → Thay thế `q8_typeA8` bằng **Question ID của cover letter** từ node JotForm Trigger.
     - Ví dụ:
       ```json
       "prompt": "Analyze the candidate's resume, cover letter ({{ $json.q12_coverLetter }}), and job description ({{ $json.jobDescription }}) to determine if they are a good fit. Return a structured JSON with: {summary, fitScore, keySkills}"
       ```

#### **🔹 Node 3: Download Resume PDF**
- **Cấu hình URL**:
  - Thay đổi từ `https://form.jotform.com/.../uploadYour` thành:
    ```
    https://form.jotform.com/.../uploadYour{{ $json.q10_resume }}
    ```
  - **Lấy `q10_resume` từ output của JotForm Trigger**.

#### **🔹 Node 4: Find Job in Notion**
- **Chọn Database**:
  - Vào **Database ID** → Chọn **"Open Positions"** của bạn.
- **Cập nhật Filter**:
  - Thay đổi `{{ $('Jotform Trigger').item.json.q7_positionApplying }}` thành **Question ID của dropdown vị trí** (ví dụ: `q5_position`).

#### **🔹 Node 5: Score > 40? (If Condition)**
- **Không cần chỉnh sửa**, workflow sẽ tự động phân loại ứng viên:
  - **Điểm > 40** → Tạo bản ghi Notion + thông báo Slack.
  - **Điểm ≤ 40** → Bỏ qua (node `Ignore`).

#### **🔹 Node 6: Create Candidate in Notion**
- **Kiểm tra cấu trúc dữ liệu**:
  - Workflow sẽ tự động tạo **bản ghi ứng viên** với:
    - Tên, email, phone, vị trí, điểm phù hợp, đánh giá AI.
  - **Không cần chỉnh sửa** nếu cấu trúc Notion phù hợp.

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nộp **form test** (sử dụng email cá nhân).
   - Kiểm tra **output** của mỗi node để đảm bảo dữ liệu truyền đúng.
2. **Bật Active**:
   - Nhấn **Active** trên workflow.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC TỐT NHẤT KHI SỬ DỤNG]
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram** để thông báo ứng viên phù hợp ngay khi nộp đơn.
   - Ví dụ:
     ```json
     "text": "🚀 New candidate alert! 🚀\nName: {{ $json.fullName }}\nPosition: {{ $json.positionApplying }}\nFit Score: {{ $json.fitScore }}"
     ```

2. **Lưu log hoạt động**:
   - Thêm node **StickyNote** để ghi lại lịch sử phân tích (ví dụ: ngày, điểm số, AI comment).

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n Schedule Node** để gửi email báo cáo tổng hợp ứng viên hàng tuần.

4. **Cập nhật Notion tự động**:
   - Nếu Notion có **trang "Rejected Candidates"**, thêm node Notion để lưu ứng viên bị loại.

5. **Tối ưu Prompt AI**:
   - Nếu muốn AI đánh giá **ngôn ngữ kỹ thuật**, cập nhật Prompt:
     ```json
     "prompt": "Analyze the candidate's technical skills in {{ $json.positionApplying }} job description and resume. Return a structured JSON with: {technicalSkills, missingSkills, overallFit}"
     ```
:::

---

## 📌 **Kết luận**
Workflow này **giải phóng team HR khỏi công việc sàng lọc CV thủ công**, thay vào đó sử dụng **Gemini AI** để tự động phân tích và xếp hạng ứng viên. Kết quả:
✅ **Tiết kiệm 80% thời gian**.
✅ **Đánh giá khách quan** với điểm số AI.
✅ **Hệ thống hóa dữ liệu** trên Notion.
✅ **Hoạt động 24/7** mà không cần can thiệp.

**Hành động ngay!**
1. **Chuẩn bị form Jotform** và **Notion Open Positions**.
2. **Import workflow** và **cập nhật Question IDs**.
3. **Test run** với form test.
4. **Bật Active** và **nhận ứng viên phù hợp tự động**!

👉 **Bạn có thắc mắc?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để workflow chạy ổn định 24/7! 🚀