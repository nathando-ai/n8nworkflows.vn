---
title: "🤖 **Tự Động Hóa Đánh Giá Bài Thi Học Sinh Với AI Gemini + Google Workspace (Không Cần Code!)**"
description: "Giải pháp tự động hóa đánh giá bài thi học sinh bằng AI Gemini, giúp giáo viên tiết kiệm thời gian đánh giá thủ công, giảm sai sót và tự động lưu kết quả vào Google Sheets. Phù hợp cho trường học, trung tâm đào tạo và các cơ sở giáo dục."
slug: "tieu-dong-hoa-danh-gia-bai-thi-hoc-sinh-ai-gemini"
tags: [n8n, automation, ai-gemini, google-workspace, no-code, giáo-duc, tự động hóa]
keywords: [n8n workflow giáo dục, tự động hóa đánh giá bài thi, AI Gemini đánh giá bài thi, Google Sheets tự động hóa, tự động hóa trường học]
---

# 🚀 **Tự Động Hóa Đánh Giá Bài Thi Học Sinh Với AI Gemini + Google Workspace**

### **Giải pháp cho giáo viên: Đánh giá bài thi chỉ trong vài giây thay vì mất nhiều giờ!**
Hãy tưởng tượng một ngày không còn phải ngồi trước hàng chục bài thi, so sánh từng câu trả lời, tính điểm và ghi chép kết quả vào bảng điểm. **Workflow này giúp giáo viên tự động hóa toàn bộ quá trình đánh giá bằng AI Gemini**, từ việc đọc bài thi quét ảnh đến tính điểm và lưu kết quả vào Google Sheets. Không cần viết một dòng code nào!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. Với chi phí thấp nhưng hiệu suất cao, các sếp có thể lựa chọn:
👉 **[VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao cho AI)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Đánh giá 100 bài thi trong **vài phút** thay vì mất **ngày đêm**.
✅ **Chính xác cao**: AI Gemini phân tích bài thi với độ chính xác gần như không sai sót.
✅ **Tự động hóa hoàn toàn**: Không cần nhập liệu thủ công vào bảng điểm.
✅ **Lưu trữ thông minh**: Kết quả được ghi vào **Google Sheets** với cấu trúc chi tiết (điểm số, câu trả lời sai/dúng).
✅ **Dễ dàng mở rộng**: Có thể kết nối với **Slack/Email** để thông báo kết quả cho học sinh/phụ huynh.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google Workspace** (để kết nối với Google Sheets và Google Docs).
✔ **API Key Google Gemini** (để AI Gemini hoạt động).
✔ **Bài thi mẫu** (đã quét ảnh hoặc chụp bằng máy tính).
✔ **Bài mẫu đáp án chính xác** (được lưu trong Google Docs).
✔ **Bảng điểm Google Sheets** (để lưu kết quả tự động).

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập vào tài khoản.
2. Nhấn **"Create Workflow"** → **"Import Workflow"**.
3. Chọn file JSON hoặc dán JSON từ [đây](https://n8n.io/workflows/10501) (hoặc tải từ link gốc).
4. Nhấn **"Import"** để workflow xuất hiện trên canvas.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **10 node** chính, các sếp cần **cấu hình kỹ lưỡng** các node sau:

#### **📌 Node 1: Answer Sheet Uploader (Form Trigger)**
- **Mục đích**: Giáo viên tải bài thi quét ảnh (PDF/JPG) và nhập tên học sinh.
- **Cấu hình**:
  - Thêm **fields** cho form:
    - `Teacher Name` (text)
    - `Student Name` (text)
    - `Answer Sheet` (file upload)
  - **Lưu ý**: Chọn **File Upload** để cho phép giáo viên tải ảnh bài thi.

#### **📌 Node 2 & 3: Analyze an image (Google Gemini) + AI Agent**
- **Mục đích**: AI Gemini **phân tích ảnh bài thi** và **so sánh với đáp án mẫu** để tính điểm.
- **Cấu hình**:
  - **Google Gemini API**:
    - Đăng nhập vào [Google Cloud Console](https://console.cloud.google.com/) → Tạo **API Key** cho **Vertex AI**.
    - Trong n8n, thêm **credentials** mới với tên `googlePalmApi` và dán **API Key**.
  - **AI Agent**:
    - Kết nối với **Google Docs** chứa:
      - **Question Paper 5Th Class** (câu hỏi thi)
      - **Answer Paper 5th Class** (đáp án mẫu)
    - **Lưu ý**: Đảm bảo **Google Docs** có **OAuth2 API** được kích hoạt.

#### **📌 Node 4: Google Gemini Chat Model**
- **Mục đích**: AI **tương tác với Gemini** để phân tích bài thi.
- **Cấu hình**:
  - Chọn **credentials** `googlePalmApi` (đã tạo ở trên).
  - **Prompt mẫu** (có thể tùy chỉnh):
    ```
    Analyze the student's answer sheet and compare it with the correct answer key.
    Return a structured JSON with:
    - Total Questions
    - Correct Count
    - Incorrect Count
    - Marks Obtained
    ```

#### **📌 Node 5 & 6: Google Docs Tool (Question Paper & Answer Paper)**
- **Mục đích**: AI **đọc câu hỏi thi và đáp án mẫu** từ Google Docs.
- **Cấu hình**:
  - Tạo **credentials OAuth2** cho Google Docs với tên `googleDocsOAuth2Api`.
  - Trong node:
    - **Operation**: `get`
    - **File ID**: Điền **ID của Google Docs** (tìm trong liên kết chia sẻ).

#### **📌 Node 7: Structured Output Parser**
- **Mục đích**: Chuyển **kết quả JSON** từ AI thành dạng **mã hóa** để dễ lưu vào Sheets.
- **Cấu hình**:
  - Chọn **schema** phù hợp với kết quả từ AI (ví dụ: `correctCount`, `incorrectCount`, `marksObtained`).

#### **📌 Node 8 & 9: Append Summary & Append Scorecard (Google Sheets)**
- **Mục đích**: **Lưu kết quả vào Google Sheets** với 2 dạng:
  1. **Tóm tắt**: Tên học sinh, số câu đúng/sai, điểm số.
  2. **Chi tiết**: Mỗi câu hỏi, đáp án đúng/sai của học sinh.
- **Cấu hình**:
  - Tạo **credentials OAuth2** cho Google Sheets với tên `googleSheetsOAuth2Api`.
  - Trong node:
    - **Operation**: `append`
    - **Sheet Name**: Chọn bảng cần ghi dữ liệu.
    - **Headers**: Điền tên cột (ví dụ: `Student Name`, `Correct Count`, `Marks Obtained`).

#### **📌 Node 10: Code (Merge JSON)**
- **Mục đích**: **Kết hợp tất cả câu hỏi** thành **1 JSON duy nhất** để lưu vào Sheets.
- **Lưu ý**: Các sếp **không cần chỉnh sửa code** này, nó đã được tối ưu sẵn.

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Tải một **bài thi mẫu** (quét ảnh) và nhập tên học sinh vào form.
   - Nhấn **"Execute Workflow"** để kiểm tra kết quả.
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Workflow Status** từ **"Inactive"** sang **"Active"**.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
🔹 **Gửi kết quả qua Email/Slack**:
   - Thêm **node Email** hoặc **Slack** sau khi lưu vào Sheets để thông báo kết quả cho học sinh/phụ huynh.
   - **Cấu hình**:
     - **Email**: Sử dụng node `n8n-nodes-base.email` với SMTP.
     - **Slack**: Sử dụng node `n8n-nodes-base.slack` và tạo **Webhook URL**.

🔹 **Lưu log hoạt động**:
   - Thêm **node `n8n-nodes-base.stickyNote`** để ghi lại lịch sử đánh giá (giáo viên có thể xem lại).

🔹 **Tích hợp với LMS**:
   - Nếu trường dùng **Google Classroom** hoặc **Moodle**, có thể **export kết quả** từ Sheets vào hệ thống này.

🔹 **Tùy chỉnh điểm số**:
   - Sửa **prompt AI** để phù hợp với **thang điểm** của trường (ví dụ: 10 điểm, 20 điểm).
   - Ví dụ:
     ```
     Calculate marks based on 20 points, where each correct answer is 1 point.
     ```

🔹 **Xử lý nhiều trang**:
   - Nếu bài thi có **nhiều trang**, sử dụng **node `n8n-nodes-base.ocr`** để quét ảnh và phân tích từng trang.
:::

---

## 📌 **Kết luận**
### **Giáo viên không còn phải lo lắng về việc đánh giá bài thi thủ công!**
Workflow này **giải phóng thời gian** cho giáo viên, giúp họ tập trung vào **giảng dạy và tương tác với học sinh** thay vì mất nhiều giờ vào việc chấm bài. Với **AI Gemini** và **Google Workspace**, quá trình đánh giá trở nên **nhanh chóng, chính xác và tự động hóa hoàn toàn**.

👉 **Hãy thử ngay!**
1. **Import workflow** từ [đây](https://n8n.io/workflows/10501).
2. **Cấu hình API và Google Docs** theo hướng dẫn.
3. **Bật workflow** và bắt đầu đánh giá bài thi **chỉ trong vài giây!**

**Nếu có vấn đề, hãy comment bên dưới hoặc liên hệ với tôi để được hỗ trợ!** 🚀