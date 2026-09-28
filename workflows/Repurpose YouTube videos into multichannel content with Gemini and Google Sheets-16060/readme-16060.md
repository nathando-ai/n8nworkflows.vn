---
title: "🚀 Tự Động Hóa Chuyển Video YouTube Thành Nội Dung Multichannel Với Gemini AI & Google Sheets"
description: "Workflow tự động hóa chuyển video YouTube thành nội dung LinkedIn, blog, email hoặc bài viết xã hội khác chỉ với 1 form submit. Sử dụng Gemini AI để phân tích transcript, tự động đăng tải và theo dõi trạng thái - tiết kiệm 80% thời gian biên tập nội dung."
slug: "tieu-dong-hoa-chuyen-video-youtube-thanh-noi-dung-multichannel-voi-gemini"
tags: [n8n, automation, content-creation, ai-gemini, google-sheets, linkedin-automation, no-code]
keywords: [n8n workflow youtube, tự động hóa nội dung, gemini ai repurpose, google sheets automation, publish linkedin tự động, content repurposing]
---

# 🚀 **Tự Động Hóa Chuyển Video YouTube Thành Nội Dung Multichannel Với Gemini AI**

## **🔥 Nỗi Đau Của Các Sếp Trong Công Việc Tạo Nội Dung**
Bạn đã từng phải:
- **Tốn hàng giờ** để transcribe video YouTube và viết lại nội dung thành bài viết LinkedIn, blog hoặc email?
- **Bị mất tập trung** vì phải copy-paste và điều chỉnh lại nội dung cho từng kênh xã hội khác nhau?
- **Không biết cách tối ưu** transcript dài 1000 từ thành các đoạn ngắn, hấp dẫn cho LinkedIn?
- **Lo lắng về chất lượng** khi nội dung không phù hợp với mục đích của từng kênh?

**Workflow này giải quyết tất cả!** Chỉ với **1 form submit**, hệ thống sẽ tự động:
✅ **Lấy transcript** từ video YouTube
✅ **Tái tạo nội dung** phù hợp cho LinkedIn (hoặc blog/email) bằng **Gemini AI**
✅ **Đăng tải tự động** lên LinkedIn
✅ **Theo dõi trạng thái** và **log lỗi** trong Google Sheets
✅ **Tiết kiệm 80% thời gian** so với cách làm thủ công!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 8-10 giờ/tuần** so với cách làm thủ công.
- **Nội dung cá nhân hóa** cho từng kênh (LinkedIn, blog, email) chỉ với 1 nguồn gốc.
- **Chất lượng cao** nhờ Gemini AI phân tích ngữ cảnh và tạo ra nội dung hấp dẫn.
- **Theo dõi toàn bộ quá trình** trong Google Sheets (trạng thái, lỗi, log).
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Dễ dàng mở rộng** sang các kênh khác (Facebook, Twitter, Telegram).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Google** (để sử dụng **Google Sheets** và **Gemini API**).
✔ **Tài khoản LinkedIn** (để đăng tải nội dung tự động).
✔ **API Key YouTube Transcript** (có thể lấy miễn phí từ [RapidAPI](https://rapidapi.com/)).
✔ **Google Sheets** với **3 tab riêng biệt**:
   - `Content_Records` (lưu nội dung sinh ra)
   - `Status_Updates` (theo dõi trạng thái đăng tải)
   - `Error_Logs` (ghi lỗi nếu có)
✔ **N8n Self-Hosted** (không dùng phiên bản cloud để đảm bảo ổn định).

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/16060](https://n8n.io/workflows/16060).
2. **Mở n8n Editor** (trang chủ của n8n self-hosted).
3. **Nhấn "Import"** và chọn file JSON vừa tải.
4. **Chọn "Import"** để workflow xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Mở n8n Editor** → **Create New Workflow**.
2. **Nhấn "Import"** → **Paste JSON** và dán toàn bộ mã JSON từ [n8n.io/workflows/16060](https://n8n.io/workflows/16060).
3. **Chọn "Import"** để workflow được tạo.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **12 node** quan trọng, các sếp cần cấu hình kỹ lưỡng:

#### **🔹 Node 1: When Form Submitted (formTrigger)**
- **Thêm form** với **2 trường bắt buộc**:
  - `YouTube Video URL` (để lấy transcript).
  - `Target Platform` (chọn LinkedIn, Blog, Email...).
- **Lưu ý**:
  - Sử dụng **Google Forms** hoặc **Typeform** để tạo form.
  - **Không bỏ trống** trường `YouTube Video URL`.

#### **🔹 Node 2 & 3: Fetch Transcript & Process YouTube Transcript (httpRequest + code)**
- **Cấu hình API YouTube Transcript**:
  - **Host**: `https://youtube-transcript-api.p.rapidapi.com`
  - **Path**: `/getTranscript`
  - **Headers**:
    - `x-rapidapi-key`: [API Key của bạn](https://rapidapi.com/)
    - `x-rapidapi-host`: `youtube-transcript-api.p.rapidapi.com`
  - **Query Parameters**:
    - `videoUrl`: `$node["When Form Submitted"]["json"]["YouTube Video URL"]`
  - **Node Code (Process YouTube Transcript)**:
    - **Mục đích**: Lọc bỏ phần không cần thiết (chú thích, tiếng lóng) và chuẩn hóa transcript.
    - **Mẫu code**:
      ```javascript
      const transcript = $input.all();
      const cleanedTranscript = transcript.map(item => {
        return {
          text: item.text.replace(/[^\w\s]/g, '').trim(),
          timestamp: item.timestamp
        };
      }).filter(item => item.text.length > 10); // Lọc bỏ đoạn quá ngắn
      return cleanedTranscript;
      ```

#### **🔹 Node 4 & 5: Generate Content with LLM & AI Chat Model (chainLlm + lmChatGoogleGemini)**
- **Cấu hình Gemini API**:
  - **Credentials**: `googlePalmApi` (tạo trong **n8n Credentials**).
  - **Prompt mẫu** (có thể chỉnh sửa trong **chainLlm**):
    ```
    Tôi có một transcript video YouTube về chủ đề: {$input.all()[0].text}.
    Viết một bài viết LinkedIn ngắn gọn (tối đa 1000 ký tự) với:
    1. Một câu hook hấp dẫn.
    2. 3 điểm chính từ video.
    3. Kết luận và call-to-action.
    Đảm bảo nội dung phù hợp với mục đích của LinkedIn.
    ```
- **Lưu ý**:
  - **Kiểm tra API Key** của Google Gemini (nếu hết hạn, workflow sẽ lỗi).
  - **Test run** với 1 video mẫu trước khi chạy toàn bộ.

#### **🔹 Node 6: Parse Content Response (code)**
- **Mục đích**: Chuyển dữ liệu JSON từ Gemini thành **mảng có cấu trúc** để lưu vào Google Sheets.
- **Mẫu code**:
  ```javascript
  const response = $input.all()[0].json;
  return {
    content: response.content,
    platform: $input.all()[0].json["Target Platform"],
    videoUrl: $input.all()[0].json["YouTube Video URL"],
    timestamp: new Date().toISOString()
  };
  ```

#### **🔹 Node 7-10: Google Sheets (Append/Update)**
- **Cấu hình Google Sheets OAuth2**:
  - **Credentials**: `googleSheetsOAuth2Api` (tạo trong **n8n Credentials**).
  - **Spreadsheet ID**: ID của file Google Sheets (tìm trong URL: `https://docs.google.com/spreadsheets/d/[ID]/edit`).
  - **Sheet Name**:
    - `Content_Records`: Lưu nội dung sinh ra.
    - `Status_Updates`: Cập nhật trạng thái (Posted/Failed).
    - `Error_Logs`: Ghi lỗi nếu có.
  - **Column Mappings**:
    - `Content_Records`: `Content`, `Platform`, `Video URL`, `Timestamp`.
    - `Status_Updates`: `Content ID`, `Status`, `Timestamp`.
    - `Error_Logs`: `Error Type`, `Error Message`, `Timestamp`.

#### **🔹 Node 11: Post Content on LinkedIn (linkedIn)**
- **Cấu hình LinkedIn Credentials**:
  - **Tạo OAuth2** trong **n8n Credentials** với:
    - `Client ID` và `Client Secret` từ [LinkedIn Developer Portal](https://www.linkedin.com/developers/).
    - **Scope**: `r_liteprofile r_emailaddress w_member_social`.
  - **Lưu ý**:
    - LinkedIn có **hạn chế API**, nên **không đăng tải quá 10 bài/ngày**.
    - **Test run** với 1 bài viết mẫu trước khi chạy toàn bộ.

#### **🔹 Node 12: Handle Errors in Workflow (code)**
- **Mục đích**: Nếu workflow lỗi, nó sẽ **ghi log vào Google Sheets** thay vì dừng lại.
- **Mẫu code**:
  ```javascript
  const error = $inputError.all()[0];
  return {
    errorType: error.type,
    errorMessage: error.message,
    timestamp: new Date().toISOString()
  };
  ```

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với 1 video mẫu:
   - Nhập **YouTube URL** vào form.
   - Chọn **Target Platform** (LinkedIn).
   - **Run workflow** và kiểm tra:
     - **Google Sheets** có ghi nội dung không?
     - **LinkedIn** có đăng bài không?
     - **Error Logs** có lỗi nào không?
2. **Bật Active** nếu test thành công.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Mở Rộng Sang Các Kênh Xã Hội Khác**
- **Thay thế Node LinkedIn** bằng:
  - **Facebook API** (đăng bài tự động).
  - **Twitter API** (tweet ngắn).
  - **Telegram Bot** (gửi tin nhắn).
- **Cách làm**:
  - Thêm **node `httpRequest`** để gọi API của kênh mới.
  - Sử dụng **node `code`** để chuyển đổi format nội dung.

### **2. Tự Động Gửi Báo Cáo Hàng Tuần**
- **Sử dụng Node `Set` + `Schedule`** để:
  - **Lấy dữ liệu** từ `Status_Updates` trong Google Sheets.
  - **Tính toán** số bài đăng thành công/thất bại.
  - **Gửi email báo cáo** bằng **Gmail API** hoặc **SendGrid**.

### **3. Tối Ưu Hóa Prompt Gemini**
- **Chỉnh sửa prompt** trong **chainLlm** để:
  - **Tạo nội dung dài** cho blog (thay vì LinkedIn).
  - **Tạo email marketing** với CTA cụ thể.
  - **Tạo script podcast** từ transcript.

### **4. Lưu Log Lịch Sử Cho Dễ Theo Dõi**
- **Thêm 1 tab mới** trong Google Sheets: `Content_History`.
- **Sử dụng node `code`** để lưu:
  - `Content ID`, `Original Video`, `Generated Content`, `Platform`, `Date`.

### **5. Sử Dụng AI Chatbot Trả Lời Thắc Mắc**
- **Kết hợp với n8n + LangChain** để:
  - **Tạo chatbot** trả lời câu hỏi từ video (ví dụ: "Video nói gì về SEO?").
  - **Tích hợp vào website** bằng **n8n Webhook**.

---
## 📌 **Kết Luận**
Workflow này **giải phóng bạn khỏi công việc tẻ nhạt** của việc tạo nội dung từ video YouTube. Với **Gemini AI** và **Google Sheets**, bạn có thể:
✔ **Tự động hóa 80% công việc biên tập**.
✔ **Đăng tải nội dung trên nhiều kênh** chỉ với 1 nguồn gốc.
✔ **Theo dõi và tối Ưu hóa** hiệu quả của mỗi bài viết.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với 1 video mẫu**.
3. **Bật Active** và **nhận nội dung tự động** mỗi khi có video mới!

**🚀 CÓ THỂ LÀM ĐƯỢC HƠN NỮA!** Nếu cần hỗ trợ thêm về **cấu hình API**, **tối Ưu hóa prompt** hoặc **mở rộng sang các kênh khác**, hãy để lại comment bên dưới. Chúng tôi sẽ giúp bạn **tối Ưu hóa workflow** để phù hợp với nhu cầu cụ thể của doanh nghiệp!